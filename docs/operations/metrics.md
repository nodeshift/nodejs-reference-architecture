# Metrics

## Recommended packages

- [prom-client](https://www.npmjs.com/package/prom-client). With >300k weekly downloads
  prom-client is both the most used and most flexible prometheus client. It also has
  a shallow dependency tree.

- [express-prom-bundle](https://www.npmjs.com/package/express-prom-bundle), version 5
  or later. It is based on prom-client and if you are using the Express web
  framework this is a good way to export prometheus metrics. It's more succinct
  to use to get started, but also more opinionated. Its a reasonable option
  until/unless more control or custom metrics are needed.

## Guidance

- Export prometheus endpoints for containers running Node.js applications. Without
  these end points it can be difficult monitor your applications. Prometheus is
  the defacto standard for exposing metrics in Cloud Native applications. Further
  Cloud Native infrastructure (Kubernetes distributions) make it easily to collect
  prometheus metrics and it is also easy to collect and graph even if you need
  to install the infrastructure components.

- Collect and monitor "RED" metrics. Details are available in

  - https://medium.com/faun/how-to-monitor-the-sre-golden-signals-1391cadc7524
  - https://www.weave.works/blog/the-red-method-key-metrics-for-microservices-architecture/

- For HTTP expose the `RED` metrics as:

  - request rate - requests which are handled ok (status code==2xx). Expose this as the total
    count.
  - error rate - requests which are not handled ok ( status code!=2xx). Expose this metric
    as a percentage of the total rate.
  - request latency - duration of requests which are handled ok, grouped into ranges/buckets and
    exposed through a prometheus histogram.

- [prometheus-nodejs-tutorial](https://github.com/csantanapr/prometheus-nodejs-tutorial) provides
  examples of using prom-client and express-prom-bundle to collect metrics. Lab 3 and 6
  show how to generate the http_request_duration_seconds_bucket metric.

  Configure prometheus middleware as the first middleware to start the timer as soon as possible.
  When setting up the middleware define your expose route for metrics `/metrics` before activating the middleware
  to avoid calls to `/metrics` to be counted as part of the metrics, you can do the same for
  liveness and readiness checks to define them before prometheus middleware if you want to discard them from your
  http metrics calculations.

  For success rate the prometheus query would be
  `sum(rate(http_request_duration_seconds_count{code="2xx", app="myapp"}[5m]))`.
  The sum over all instances, the rate of change of the request count for app
  my app with status_code 2xx over a 5m window

  For error rate, but the status_code is usually 4xx or 5xx expressed as [45]xx. The
  prometheus query would be `sum(rate(http_request_duration_seconds_count{code="[45]xx", app="myapp"}[5m]))`.

  For duration, or latency the metric is a histogram so you will graph and
  monitor percentiles instead of a summary. For example, the prometheus query would be
  to get the 95 percentile over all instances over 5m window would be
  `histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket{code="2xx", app="myapp"}[5m]))`

- Export additional custom metrics to provide key attributes about the operation of
  your application which are not part of the standard metrics.

- Be aware that the prometheus client instance needs to be a singleton within your app.  For example, if your
  application imports separate packages that utilize the "prom-client" package, like customized RabbitMQ &
  Redis drivers that write metrics to prom-client, you need to make sure they use the same prom-client instance.
  A common way to do that is to make the prom-client instance as an optional parameter in the constructor for
  those drivers, and then your app can pass in the same prom-client instance into both.
