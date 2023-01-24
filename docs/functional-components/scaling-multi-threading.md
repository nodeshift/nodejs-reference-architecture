---
sidebar_position: 9
---

# Load balancing, Scaling and Multi-threading

Node.js is said to be `single-threaded`. While not quite true, it reflects that
most work is done on a single thread running the event loop. The asynchronous
nature of JavaScript means that Node.js can handle a larger number of
concurrent requests on that single thread.

At the same time that does not mean that Node.js applications/solutions are
`single-threaded`. Today's computers provide multiple concurrent threads of
execution (either with multiple cores and/or cores that can support
multiple concurrent threads of execution) and Node.js applications have
long exploited those additional threads by running multiple Node.js instances.

Mutiple threads within a single machine can typically either be exploited within
a single process or by starting multiple processes. There are advantages
and dis-advantages to each.

Processes provide better isolation but also lower
opportunities to share resources and makes communication between threads
more costly. While using multiple threads within a process may be able to
scale more efficiently within a single process it has the hard limit
of only being able to scale to the resources provided by a single machine.

With container based deployments the number of threads available may
also be limited, with the assumption that when additional cpu resources
are needed, additional containers will be created and the load
spread across those containers.

Today's cloud native deployments generally have a goal to be able to
scale to a level that that cannot be met through by the
resources/availability that can be achieved on a single machine. This
naturally favors scaling by adding additional copies of a container,
each of which, is typically running a single process.

The small footprint and fast startup of Node.js, along with the
ability to handle many concurrent requests without needing multiple
threads of execution and synchornization between those threads makes
it a good fit for todays approach to scaling using containers.

## Recommended Components

We don't recommened any specific components at this time.

## Guidance

- when possible applications should be decomposed so that a
  request to a single container will need no more than single
  thread of execution in order to complete in a reasonable time.
  When necessary to achieve this, consider further decomposing
  the application. If this is not reasonable,
  [WorkerThreads](https://nodejs.org/api/worker_threads.html)
  are recommended versus multiple processes in the same container.

- delegate management of the containers supporting
  the application and the load balancing/routing of requests
  to those containers to the highest layer possible. For
  example, if the application is deployed to kubernetes,
  do not use tools like the
  [Cluster API](https://nodejs.org/api/cluster.html) to manage
  requests within a container, instead rely on the facilities
  provided by kubernetes. In our experience this has been
  just as efficient in terms of machine resources and allows
  better scaling.

  - Avoid blocking the event loop for a prolonged period
    of time. If you have a mix of request types where some are long
    running, consider moving the long running requests so that they
    execute in their own set of containers in order to enable better
    scaling. However, even once moved it often makes sense to use
    [WorkerThreads](https://nodejs.org/api/worker_threads.html) to
    run the long running request in order to
    avoid blocking the main event loop. This is to prevent
    long running requests on the main event loop from stalling
    requests to health monitoring, metrics and similar endpoints
    that need to be supported by a containter.

- When using [WorkerThreads](https://nodejs.org/api/worker_threads.html)
  make sure you pool worker threads (for example
  by using something like [piscina](https://www.npmjs.com/package/piscina)
  and ensure you preserve ascync context for requests with
  [AsyncResource](https://nodejs.org/api/async_hooks.html#async_hooks_class_asyncresource)
  if you don't use an existing pooling library like piscina which
  does this for you.

- [WorkerThreads](https://nodejs.org/api/worker_threads.html)
  may also be appropriate if your application
  must run as a single process (for example a desktop application). In these
  cases it is known that you cannot scale beyond the resources of the single
  machine and it is often preferrable to have the application show up
  as a single processes versus many individual processes.
