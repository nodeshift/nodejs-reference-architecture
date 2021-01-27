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
  option to ensure sensitive data is not logged. Simiarly, if you're using the
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
with every log line, a cleaner technique is to utilize
[asyncLocalStorage](https://nodejs.org/api/async_hooks.html#async_hooks_class_asynclocalstorage)
to store those values in express middleware, and fetch them back out inside a log formatter.
If you have to use an older nodejs that doesn't support asyncLocalStorage, the [cls-hooked](https://www.npmjs.com/package/cls-hooked)
library can provide similar function.

1. Define a log [formatter](https://getpino.io/#/docs/api?id=formatters-object)
   that adds the desired entries into the log:

```
// to be passed into Pino logger construction
const emptyLocalStorage = new Map();
const formatters = {
  log (obj) {
    const als = asyncLocalStorage.getStore() || emptyLocalStorage;
    const orgId: string = als.get('OID');
    const userId: string = als.get('UID');
    const transactionId: string = als.get('TraceId');
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

2. Define an express middleware layer to be loaded before authentication
   middleware that binds the asyncLocalStorage to the REST request,
   and adds in the trace-id.

```
import { v4 as uuid } from 'uuid';
import { RequestHandler, Request, Response, NextFunction } from 'express';
const traceabilityMiddleware: RequestHandler =
  session.bind(
    async (req: Request, res: Response, next: NextFunction) => {
      const passedTraceId = req.get('X-Trace-Id');
      const traceId = passedTraceId ? passedTraceId : uuid();

      const als = new Map(['TraceId', traceId]);
      // Always return the trace-id as header so we can debug/trace calls
      // that don't return an error but didn't work right
      res.set('X-Trace-Id', traceId);

      // By invoking next in here, the cls_hooked context remains
      // active for the following express middlware layers to access
      asyncLocalStorage.enterWith(als);
      return next();
    },
    session.createContext()
  );
```

3. Update your authentication express middleware layer to write the OID and UID
   into the asyncLocalStorage, example from a JWT-token based authentication scheme:

```
const session = getOrCreateNamespace('logging');

...
< inside the authentication middlware >
    const token = opts.tokenFrom(req);
    if (token) {
      // Token validation
      const authentication = await opts.verifier.verifyAndDecode(token);

      // Set things for logger down the line
      const als = asyncLocalStorage.getStore();
      if (als && authentication.uid) {
        als.set('UID', authentication.uid);
      }
      if (als && authentication.oid) {
        als.set('OID', authentication.oid);
      }
...
```
