---
sidebar_position: 1
---

# Distributed Tracing

## Recommended Components

Distributed tracing typically requires a mechanism for collecting traces (instrumentation)
and a separate mechanism for reporting and visualizing those traces.

- [OpenTelemetry](https://opentelemetry.io/) provides instrumentation in multiple languages
  including Node. OpenTelemetry is not yet released as a final stable version and is in Beta.
  OpenTelemetry replaces both OpenTracing and OpenCensus, neither of which are actively being
  developed (security fixes only).

For adding instrumentation to Node applications and services:

- [@opentelemetry/sdk-trace-base](https://www.npmjs.com/package/@opentelemetry/sdk-trace-base)
- [@opentelemetry/sdk-trace-node](https://www.npmjs.com/package/@opentelemetry/sdk-trace-node) - See the
  [Getting Started Guide](https://opentelemetry.io/docs/instrumentation/js/getting-started/)

Reasons for choosing OpenTelemetry:

- the open source tracing library that's replacing both OpenCensus and OpenTracing
- handles basic use cases really well, includes good default configuration for most use cases
- includes support for newer efficient Node implementation for correlating outbound traffic
  to incoming requests
- supports multiple languages for tracing (not just Node) with a consistent API.

## Guidance

There is significant value in collecting distributed tracing as it:

- allows easy identification of performance critical services and code
- allows quick navigation to failing calls that are "buried" deep in the system
- allows a clearer understanding of the interdependencies of complicated systems

These benefits come at a cost in:

- adding instrumentation to each application and the related negligible application overhead
- significant additional network and storage utilization
- additional services, and the related administration (Jaeger/ElasticSearch, etc.)

For non-trivial systems the benefits are typically worth the costs, especially when investigating
problems.

OpenTelemetry allows the ability to sample a subset of traces to reduce the storage and network
utilization of the tracing data. The guidance here is that, where possible, sampling should be disabled
such that all traces are recorded. If sampling is enabled, it is inevitable that the trace data is
missing when trying to investigate some critical failure.

Be aware that:

- some error conditions that do not trigger network traffic are not traced (e.g. DNS lookup
  failures, etc.)
- existing instrumentation libraries are not customizable (no hooks, or extension points -
  not able to extend instrumentation to add additional data without reimplementing them)
- you are not able to post process traces from instrumentation prior to exporting them
- you are not able to easily change configuration options dynamically (enabling/disabling tracing)

### Infrastructure

- [Jaeger](https://www.jaegertracing.io/) provides visualization of distributed traces.
- [ElasticSearch & Kibana](https://www.elastic.co/elastic-stack) provides storage for persisting
  the data behind Jaeger as well as alternate mechanisms in Kibana to search, visualize, and manage
  that data.
- An alternate for Jaeger is [Zipkin](https://zipkin.io/) which is also directly supported by
  OpenTelemetry for visualizing distributed traces. The instrumentation in Node is not impacted
  by the selection of the visualization tool. Both Jaeger and Zipkin can be used concurrently if
  storage space is available. If using Zipkin, [Cassandra](https://cassandra.apache.org/) may be used
  instead of ElasticSearch.

### Integration suggestions

Data management becomes a critical aspect of distributed tracing. Consider:

- expiring data as it ages out and is no longer relevant
- volumes and network traffic can become excessive
- storage costs can be large.

OpenTelemetry by default installs instrumentation patches for many communication protocols
(HTTP, HTTPS, GPRC, etc.). Configure OpenTelemetry to install just those patches for protocols that are
actively used in your applications.

OpenTelemetry can be installed in container-based systems like Kubernetes. When used in conjunction with
Istio care needs to be taken to ensure that either:

- Istio distributed tracing is disabled
- Istio distributed tracing is enabled and also exports all trace data to the same systems as OpenTelemetry.
  Additionally, since Istio is typically the entry point for new connections, it is what sets the
  sampling conditions for traces, and not OpenTelemetry. Ensure sampling in Istio is correctly configured.
  If Istio distributed tracing is enabled, but not exported to the same systems as OpenTelemetry, it
  will cause gaps and orphans in the tracing hierarchies.
