# Logging

## Recommended Components

- Pino - http://getpino.io/#/

Pino provides an easily consumed API, structured logging and good performance
which makes it well suited to cloud native deployments were more complicated
APIs/features are not required as log output is simply written to standard out
It has a respective level of weekly npm downloads (495k as of Nov 2019)
and is growing. It was inspired by Bunyan which no longer seems to be maintained
and is a good migration option.

# Guidance

Pino http://getpino.io/#/ is the recommended log framework for Node.js due
to its easily consumed API, structured json logging by default
and good performance.

When deploying Pino we have the following additional recommendations:

- send logs to standard out and use log aggregation tools to collect
  logs across processes, containers and applications. All log processing
  should be done in a separate process.
- Plan for a final resting place for log data. After 7 days migrate
  log data to a lower cost storage (manual retrieval is likely ok).
- Add code to your application in order to allow logger.level
  to be set through an Environment variable so that can be easily
  changed in container environments.
- Use the [redaction](https://github.com/pinojs/pino/blob/HEAD/docs/redaction.md)
  option to ensure sensitive data is not logged.  Simiarly, if you're using the
  [convict](https://www.npmjs.com/package/convict) library to manage application
  configuration data (like database credentials), marking appropriate fields as
  sensitive will redact them when logging the config structures at startup.
- Limit the use of warn, error, and fatal levels to information
  which must always be logged.
- Limit the use of info level to important information which can
  always be logged without introducing significant overhead.
- Don't throw and catch multiple errors, throw once and catch/log at the
  highest level.
- Every source file should utilize Pino's child method off of the common logger
  instance, passing in { file: module } to make the source file path is part of 
  the log.

# Generating user and trace filterable logs

If your application is going to be utilized by a large number of users, your 
support team will likely require the ability to be able filter logs to actions 
from a specific user or organization (details of such are specific to your 
authentication nodel), or to be able to see all the logs corresponding to a 
specific REST call. Rather than force the developers to pass and log those values 
with every log line, a cleaner technique is to utilize async-hooks to store those 
values in express middleware, and utilize log formatters to print those stored 
values.  In the example below we used 
[cls-hooked](https://www.npmjs.com/package/cls-hooked) package to reference 
async_hooks.

1) Define a local cls-hooked library (./cls_hooked.ts in this case) like:
```
import * as cls_hooked from 'cls-hooked';
/**
 * Wraps cls_hooked getNamespace or createNamespace.
 * There should only be one createNamespace per namespace. Otherwise a new
 * session is created in a different context and loaded into cls.
 *
 * @param namespace name of namespace
 * @return {cls_hooked.Namespace} existing or new namespace
 */
function getOrCreateNamespace(namespace: string): cls_hooked.Namespace {
  const ns = cls_hooked.getNamespace(namespace);
  return ns ? ns : cls_hooked.createNamespace(namespace);
}
export { getOrCreateNamespace };
```

2) Define a log [formatter](https://getpino.io/#/docs/api?id=formatters-object)
that adds the desired entries into the log:
```
import { getOrCreateNamespace } from './cls_hooked';
const session = getOrCreateNamespace('logging');

// to be passed into Pino logger construction
const formatters = {
  log (obj) {
    const orgId: string = session.get('OID');
    const userId: string = session.get('UID');
    const transactionId: string = session.get('TraceId');
    if (orgId) {
      obj['OID'] = orgId;
    }
    if (userId) {
      obj['UID'] = userId;
    }
    if (transactionId) {
      obj['TraceId'] = transactionId;
    }
    return obj;
  }
}
```

3) Define an express middleware layer to be loaded before authentication
middleware that binds the cls-hooked namepsace to the request, 
and adds in the trace-id.
```
import { getOrCreateNamespace } from './cls_hooked';
import { v4 as uuid } from 'uuid';
import { RequestHandler, Request, Response, NextFunction } from 'express';
const session = getOrCreateNamespace('logging');
const traceabilityMiddleware: RequestHandler =
  session.bind(
    async (req: Request, res: Response, next: NextFunction) => {
      if (req instanceof EventEmitter) {
        session.bindEmitter(req);
      }
      if (res instanceof EventEmitter) {
        session.bindEmitter(res);
      }

      const passedTraceId = req.get('X-Trace-Id');
      const traceId = passedTraceId ? passedTraceId : uuid();

      // Assuming your authentication layer wrote the OID/UID into the Request
      // similar to this
      //since the context forked, it contains stale values needs explicit reset
      session.set('OID', undefined);
      session.set('UID', undefined);
      session.set('TraceId', traceId);
      // Always return the trace-id as header so we can debug/trace calls
      // that don't return an error but didn't work right
      res.set(Headers.TraceId, traceId);
      return next();
    },
    session.createContext()
  );
```

4) Update your authentication express middleware layer to write the OID and UID
into the cls-hooked session, example from a JWT-token based authentication scheme:
```
const session = getOrCreateNamespace('logging');

...
< inside the authentication middlware >
    const token = opts.tokenFrom(req);
    if (token) {
      // Token validation
      const authentication = await opts.verifier.verifyAndDecode(token);

      // Set things for logger down the line
      if (authentication.uid) {
        session.set('UID', authentication.uid);
      }
      if (authentication.oid) {
        session.set('OID', authentication.oid);
      }
...
```
