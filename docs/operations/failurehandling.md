---
sidebar_position: 2
---

# Fault Tolerance

## Recommended Components

We recommend that you first investigate if your environment supports a service mesh like [Istio](https://istio.io/).
In that case it's recommended to leverage the capabilities of the mesh in order to handle fault tolerance.

If your environment does not support a service mesh then we recommend the [Opossum](https://www.npmjs.com/package/opossum) module. It is the most widely used fault tolerance Node.js module, has no dependencies and has good community support. Opossum is a Node.js circuit breaker that executes asynchronous functions and monitors their execution status. When things start failing, opossum plays dead and fails fast. In addition you can provide a fallback function to be executed when in the failure state.

The metrics that opossum collects can easily be fed into the companion [Prometheus](https://www.npmjs.com/package/opossum-prometheus) module in order to feed data in the [recommended metrics collection framework](https://github.com/rh-ibm-synergy/Nodejs-reference-architecture/blob/add-circuit-breaker/metrics.md).

## Guidance

Many applications and services make calls to external services. Due to the asynchronous nature of Node.js, in most cases when an external call fails the best way to handle the failure is to propagate the failure back up the call chain, often resulting in an error being returned to the user of your application or caller of your service. This is true for Node.js as an asynchronous call which is blocked waiting for a response does not prevent other requests from being handled as would be the case for other runtimes which consume a thread for each active request.

In specific cases, however, it is better to either:

- retry the failed call
- avoid repeating the call for some period of time and return an error up the call stack
- avoid repeating the call for some period of time and use cached data to provide potentially degraded service

The technique for implementing the last two is often called a `circuit breaker`. The basic idea behind the circuit breaker is that you wrap a protected function call in a circuit breaker object, which monitors for failures. Once the failures reach a certain threshold, the circuit breaker trips and enters the `open` state, and all further calls to the circuit breaker return with an error, without the protected call being made at all.

Circuit breakers are recommended in the following situations:

- repeated calls to the external service will worsen the situation, making it take longer for the external service to
  resume normal operation. If callers can cope with cached data then return that, otherwise simply return an error up
  the call chain while in the `open` state.
- the application can cope by using cached data, and it is known that the external service takes time to ramp up capacity
  in the face of increasing numbers of requests.
- There is a persistent occasional intermittent failure in the external service and a retry is the only way to avoid
  returning intermittent errors. In this case it is important to use a circuit breaker to limit the number of retries.
- It is more important to return a response within a fixed maximum upper bound (even if that response is an error or a
  previously cached result) than it is to return live data.

Examples of how to configure opossum circuit breakers are available in the main opossum [repo](https://github.com/nodeshift/opossum#usage).

More detailed examples are available in the following starters:

- https://github.com/nodeshift-starters/nodejs-circuit-breaker
- https://github.com/nodeshift-starters/opossum-examples
