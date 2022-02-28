---
sidebar_position: ?
---

# Problem Determination

It is important to be able to investigate problems that occur in production.
Team members have typically used one of these implementations:
* existing Application Performance Management offering
* custom solution leveraging avialable platform tools (for example,
  those provided by a Cloud provider or OpenShift)

Irrespective of the implementation, the experience of the team is that it is important
to plan for problem determination up front and use metrics to identify when problems
occur and need to be investigated. You can read more about the suggested approach
for capturing metrics in the
[metrics](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/metrics.md)
section.

Once your metrics have identified that there is a problem, it will often fall into
one of the common categories.

The teams recommendations/guidance is based on the implementation and typical categories
of problems that we have seen.

## Recommended Components

## Guidance

### Common problems

#### Memory Leak

* Symptoms
  * metrics report that application is slowly becoming less responsive 
  * metrics report heap size is continuously growing despite stable load on the application
  * metrics report increasing time spent running the garbage collector

* Approach
  * generate a sequence of [heap dumps](https://nodejs.org/dist/latest-v17.x/docs/api/cli.html#--heapsnapshot-signalsignal)
    at 1 minute intervals, compare using chrome dev tools to see what is growing
  * enable the [heap profiler](https://nodejs.org/dist/latest-v17.x/docs/api/cli.html#--heap-prof)
    and look at where allocations are taking place

Generating heap dumps will have a performance impact on the process both in terms of memory
and execution when the dump is being generated. Some of the team's suggestions for limiting the impact:
* only enable heap dumps for one process/instance of the application, leaving the others to better server customers
* try to minimize the size of the heap dumps. For example, if you increased the memory allocated to the application
  as part of trying to investigate the issue, revert that change. If possible limit the instance of the application
  to using less memory than you normally would.
* Make sure you have enough additional memory available on the machine running the process. The dump may need double
  the size of heap while it is being generated

#### Hangs or slow performance

* Symptoms
  * process health checks fail
  * metrics report longer than expected request times
  * metrics report higher than expected CPU usage

* Approach
  * generate a [Diagnostic report](https://nodejs.org/api/report.html) and look for ref flags
  * generate a [flame graph](https://nodejs.org/en/docs/guides/diagnostics-flamegraph/). The team
    has had success with [0x](https://www.npmjs.com/package/0x) and [bubbleprof(https://clinicjs.org/bubbleprof/)
    and [Flame](https://clinicjs.org/flame/)

It may be difficult to investigate performance issues in the production system. Once you have identified
that there is a problem, being able to recreate in another environment make it much easier. The team has
had success using [goreplay](https://github.com/buger/goreplay) as well as
[Autocannon](https://www.npmjs.com/package/autocannon) to generate load in test environments in order to
reproduce issue seen in production.

If you must investigate in production, you may have to disable or extend the health check period so that
you can generate diagnostic reports and/or flame graphs. Ensure that you don't allow more than one
process to be in the hung/slow state while investigating in order to limit impact on end users.

#### Application failures

* Symtoms
  * metrics report failure reponses

* Approach
  * Review application logs, turn on additional levels of logging if necessary
  * Review [transaction traces](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/distributed-tracing.md)


#### Unhandled promise rejections or exceptions

* Symtoms
  * process terminatese reporting an unhandled rejection or exception
  
* Approach
  * review log to find stack strace, review code indicated in stack trace
    to look for cause.

#### Resource Leaks

* Symptoms
  * process fails reporting lack of resources (for example sockets)

* Approach
  * generate a sequence of [Diagnostic report](https://nodejs.org/api/report.html)s.
  * compare resources reported between reports using
    [report-toolkit](https://developer.ibm.com/articles/introducing-report-toolkit-for-nodejs-diagnostic-reports/)


#### Network Issues

* Symtoms
  * external health checks fail, while internal metrics look ok

* Approach
  * use curl to check connectivity/responsiveness from different parts of network
  * if using [istio](https://istio.io/) check logs

#### Native crashes

* Symptoms
  * Unexpected process crash/restart, logs indicates native crash (SIGSEV or equivalent)

* Approach
  * Enable core dump collection
  * Analyze core dump with [llnode](https://developer.ibm.com/articles/explore-nodejs-core-dumps-using-the-llnode-plugin-for-lldb/)

### Implementation

#### Application Performance Management Solutions

If you are operating a service where you own all deployments an existing Application
Performance Management (APM) solution can make sense if budget is not an issue.
(they can become expensive for large deployments). They offer the advantage
or requiring less up front investment and leveraging a solution designed to help
investigate problems. The team has had success with using
[Dynatrace](https://www.dynatrace.com/),
[Instana](https://www.ibm.com/cloud/instana),
and [NewRelic](https://newrelic.com/)

If you develop applications that will be operated by customers, adding a dependency
on a specifc APM for problem determination is not recommended. The cost may be an issue
for some customers, while others may already have standardized on a specific APM. Larger
organizations in particular are likely to want to leverage their APM of choice across
applications. It is recommended that whenever possible you leverage standard clients
that will be able to feed data to different APMs and/or customer solutions.

Typically APMs will be able to help you generate and consume
[logs](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/logging.md),
[metrics](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/metrics.md)
and [traces](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/distributed-tracing.md)
as well as generate HeapDumps in order to support problem determination for the common problems
outlined above.

If you rely on an APM, It is important to ensure you have enough licences so
that you can use the APM for local development/debugging in addition to production deployments.

#### Custom solution leveraging platform tools

Platform tools will provide some support for generating key metrics as well as storing 
[logs](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/logging.md),
and [metrics](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/metrics.md).

The level of support available will depend on the platform with cloud platforms and kubernetes based platforms
(for example OpenShift) providing more built in capabilities than an operating system. The team
has had success in using [Prometheus](https://prometheus.io/) and
[Grafana](https://grafana.com/) to store, graph and analyse metrics and
logs on platforms that do not have integrated support.

You will need to plan for how you instrument the application in order to capture 
[logs](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/logging.md),
[metrics](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/metrics.md).
and [traces](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/operations/distributed-tracing.md)
with our recommendations outlined in those sections.

You will also need to plan for how to:
* generate and extract heap snapshots
* generate and extract core dumps
* dynamically change log levels

Cloud platforms also often provide templates for these activities so if you are on a specific cloud
platform look for the corresponding templates.

A key consideration is how to make the additional components required for problem determination available.
[Ephemeral containers](https://opensource.googleblog.com/2022/01/Introducing%20Ephemeral%20Containers.html)
 may help in the future, but today you most likely need to include the components
in your deployment or pre-plan/approve the process to add them to the production environment when needed.

*Generating and extracting heap snapshots*

The team has used a few approaches to generate and extract heap snapshots:

* Approach 1
1. Use the `--heapsnapshot-signal=SIGUSR2` command line option to enable heap dump generation on `SIGUSR2` 
1. Add heap-dump script in the applications package.json to trigger SIGUSR2 with kill
1. use `kubectl exec` to run the heap-dump script and then `kubectl cp` to copy out
   the dump (or equivalent in non kubernetes environments)

* Approach 2
1. adding  a hidden rest call to the application to trigger a heap dump (only accessible internally)
1. when the rest call is invoked generate heap dump into shared mount 
 
*Generating and extracting core dumps*

The team has succesfully used [core-dump-handler](https://github.com/IBM/core-dump-handler) for generating
and extracting core dumps in kubernetes environments.

*Dynamically change log levels*

The team has used a hidden rest call in the application which allows changing the log level.
See [Node.js Reference Architecture, Part 2: Logging in Node.js](https://developer.ibm.com/blogs/nodejs-reference-architectire-pino-for-logging/)
for more details.












