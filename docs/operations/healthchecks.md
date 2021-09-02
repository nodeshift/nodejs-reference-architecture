# Health Checks

## Recommended Components

We don't recommend the use of a module to add health checks to your application. It's
best to stick with a minimal implementation for most cases. The tradeoff between the amount
of code you need to add to your application for a minimal implementation versus
the costs of adding a new dependency leads us to recommend adding the code directly.
Examples of how to add this code to your application are provided in the Guidance section.

## Guidance

Kubernetes includes built in liveness and readiness monitoring and document
requirements for these endpoints. We recommended following the
kubernetes requirements as they are well defined, broadly used, and make
your application ready for Kubernetes deployment even if you initially use
something else.

[Kubernetes liveness and readiness probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) offer three different options: Probe type, port and response as described in the
sections which follow.

### Probe type

We recommend using an HTTP probe type (`httpGet`). It demonstrates that the HTTP
server is up and responding to requests and is the most commonly used probe
type for services that expose HTTP as part of their function.

When using a Service Mesh (Istio), there are are potential
issues that you need to address. If you have mutual TLS enabled,
using `httpGet` probes with Istio requires some specific configuration. Check the Istio
[guide](https://istio.io/docs/ops/configuration/mesh/app-health-check/) to see
the options available when using HTTP request. If this configuration is
not practical for your deployment then TCP probes provide less coverage but
are simpler to support.

### Port

We recommend responding to probes from the same port as the application server.
Its simple, common, and demonstrates that the HTTP server is up and responding
to requests.

By listening on the same port, it makes it easy to be certain that the container
does not start responding to probes until it is ready to respond with
application traffic.

### Response

The response does not need to return any data, but status must be `200/OK`. For
humans, it may be useful to return a minimal response body, such as `ok`.

It may be tempting (particularly based on
tutorials available on the web) to do additional internal state checks
or checks on the availability of dependencies.

For liveness probes in particular
this can often do more harm than good as the end result is the container
being restarted. For example, if a database used by the application is
down, restarting the container in which the Node.js application using that
database runs, is unlikely to help and can hurt but adding the additional
load of continuously restarting containers.

For readiness probes, there are advanced use cases where it makes sense
for the service to modify its probe states to
participate in container orchestration. For example, stopping responding on
/readyz and allowing active connections to drain on the main port. When these
requirements exist it makes sense to implement a more complete readiness
endpoint. In other cases it is better to stick to the
simple implementation. For example, in the case of a database that is
down, it is better to respond indicating there is a problem with the database
versus failing the readiness check as that results in the loss of the
ability to provided 5xx responses to requests so that the client
knows what's wrong.

### Endpoints

We recommend that you use consistent naming for your endpoints across micro-services.  `/readyz` and `/livez` are common choices for the endpoints for the readiness and
liveness probes, respectively.

Any route name can work if it agrees with the probe configuration, but in the
absence of some requirement by the tooling, best to use names that have a
clear relationship to their purpose. `/healthz` is not clear as to whether it is
liveness or readiness.  Because
[the differences between them are important](https://developers.redhat.com/blog/2020/11/10/you-probably-need-liveness-and-readiness-probes),
it's best to clarify.

The "z" at the end of `/readyz` and `/livez` are a pattern called "z pages" that
is a pattern used by [internal Kubernetes services](https://kubernetes.io/docs/reference/using-api/health-checks/) and has also been adopted by some other projects like [OpenCensus](https://opencensus.io/zpages/).

### Frequency of checking

Since probe states shouldn't change once the application is serving traffic,
there is no need for aggressive probe periods. The initial delay for the liveness
probe should be ample enough for application startup. If its too short,
Kubernetes will keep terminating the container before it serves traffic. Since
the only typical reason to not respond to a readiness probe once the application
is up is that the application is exiting on container termination, Kubernetes
will already know that the container is terminating. Excessively frequent
checking here can also be counter productive.

We recommend that you don't specify specific values for your application and
use the cluster defaults unless your application needs more time to
startup (readiness) or to respond to liveness checks when under load.

### Example code and configuration

It is easy to add simple endpoints with with pure Express.js,
or your framework of choice. For example with Express:

```javascript
const app = require("express")();

// Note that when collecting metrics, the management endpoints should be
// implemented before the instrumentation that collects metrics, so that
// these endpoints are not counted in the metrics.
app.get("/readyz", (req, res) => res.status(200).json({ status: "ok" }));
app.get("/livez", (req, res) => res.status(200).json({ status: "ok" }));

// ... rest of app...

app.listen();
```

The kubernetes endpoints exposed by the application have to agree with the probe configuration:

```yaml
readinessProbe:
  httpGet:
    path: /readyz
    port: 3000
livenessProbe:
  httpGet:
    path: /livez
    port: 3000
```
