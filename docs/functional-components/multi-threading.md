# Multi-threading

Node.js is said to be `single-threaded`. While not quite true, it reflects that
most work is done on a single thread running the event loop. The asynchronous
nature of JavaScript means that Node.js can handle a larger number of
concurrent requests on that single thread. 

At the same time that does not mean that Node.js applications/solutions are
`single-threaded`. Today's computers provide multipe concurrent threads of
executaiton and Node.js applications have long exploited those additional
threads by running multiple Node.js instances.

Mutiple threads within a machine can typically either be exploited within
a single process or by starting multiple processes. There are advantages
and dis-advantages to each.

Processes provide better isolation but also lower
opportunities to share resources and makes communication between threads
more costly. While using multiple threads within a process may be able to
scale more efficiently within a single process it has the hard limit
of only being able to scale to the resources provided by a single machine.

Today's cloud native deployments generally have a goal to be able to
scale to a level that that cannot be met through by the 
resources/availability that can be achieved on a single machine. This
naturally favors scaling through multiple processes.

The small footprint and fast startup of Node.js, along with the
ability to handle many concurrent requests without needing multiple
threads of execution and synchornization between those threads makes
it a good fit for todays approach to scaling using processes.

## Recommended Components

We don't recommened any specific components at this time.

## Guidance

The trend for managing scaling an application across processes is to
externalize the management from the application and to delegate
as much as possible to the infrastructure in which the applications
runs. 

* applications should be decomposed so that a request to a single
  process will need no more than single thread of execution to
  complete in a reasonable time. If not, consider further
  decomposition.

* delegate management for of the processes supporting
  the application and the routing of requests to those processes
  to the highest layer possible. For example, if the application
  is deployed to kubernetes, do not use tools like the
  [Cluster API](https://nodejs.org/api/cluster.html) to manage
  requests within a machine, instead rely on the facilities
  provided by kubernetes. In our experience this has been
  just as efficient in terms of machine resources and allows
  better scaling.

* For the exceptional cases where a single thread of execution
  cannot complete a request in a reasonable time, and a large
  amount of data must be shared across multiple threads to complete
  the request efficiently
  [WorkerThreads](https://nodejs.org/api/worker_threads.html)
  is an option along with using language features like
  [SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer).
  In this case make sure you pool worker threads (for example
  by using something like [piscina](https://www.npmjs.com/package/piscina)
  and ensure you preserve ascync context for requests with
  [AsyncResource](https://nodejs.org/api/async_hooks.html#async_hooks_class_asyncresource)
  if you don't use an existing pooling library which does this
  for you.

* [WorkerThreads](https://nodejs.org/api/worker_threads.html) can also
  help if a process serves different transaction types and some may
  run for a significant amount of time. In those cases WorkerThreads
  can be used to avoid blocking the event loop, however, it is often
  better to move those transactions so that the longer ones
  execute in their own set of processes in order to enable better
  scaling.

* [WorkerThreads](https://nodejs.org/api/worker_threads.html)
  may also be appropriate if your application
  must run as a single process (for example a desktop application). In these
  cases it is known that you cannot scale beyond the resources of the single
  machine and it is often preferrable to have the application show up
  as a single processes versus many individual processes.

