---
sidebar_position: 6
---

# Message Queuing

## Recommended packages

| Server   | Recommended client |
| -------- | ------------------ |
| Kafka    | [node-rdkafka][]   |
| Kafka    | [KafkaJS][]        |
| ActiveMQ | [rhea][]           |
| Redis    | [ioredis][]        |

## Kafka

It's currently difficult to make a single recommendation for a Node.js
Kafka client. 

The team currently has the most real-world experience with 
[node-rdkafka][]. In the past it has been widely used and
recommended by the messaging groups within the `teams`
organizations for performance, features, and protocol compatibility.
One of it's strengths is that is based on the same
[librdkafka](https://github.com/edenhill/librdkafka), maintained
by the Kafka project and used by most language clients. **However**
it is in the midst of a maintenance challenge that it does not
seem to be pulling out of (for example at the time this was written
node-rdkafka does not build on Node.js version 16).

[KafkaJS][] is a newer Node.js 
Kafka client which is more actively maintained and is growing in
popularity. It's pure JavaScript implementation makes it
easier to install and use.  While we don't have past history of real-world
experience with the KafkaJS client, we have reviewed the features
and usage versus node-rdkafka and it compares favorably. The one
potential caveat is with respect to performance where node-rdkafka, likely
due to its use of [librdkafka](https://github.com/edenhill/librdkafka),
comes out ahead. While the difference a simple benchmark is quite
significant, whether that matters for a real-world application will
depend on the application.

At this point our recommendation is: 
* if you need the highest possible performance or longest track record of production use and are
using an older version of Node.js (14.x or earlier) and can tolerate
the risk on the maintenance side [node-rdkafka][] may still be
your best choice.
* otherwise you should consider [KafkaJS][]. If your application
has high performance requirements you should plan to validate
that you can meet those requirements with KafkaJS early on in your
development lifecycle.

### Guidance

Reuse connections. Do not write apps that connect/send/disconnect
repeatedly in a loop. This will result in poor performance, not only for the
individual application, but will also impact the Kafka cluster for other users.

Architect applications so that they connect and keep
an open connection on which events are processed when they arrive.

## ActiveMQ

Recommendation is to use [rhea][] which supports AMQP1.0
(one of the protocols supported by ActiveQ). This module is maintained by Red Hat and has
higher weekly downloads than the competing module for ActiveMQ which supports the STOMP
protocol (the native ActiveMQ protocol).

### Guidance

## Redis

Recommendation is to use [ioredis][].
There are 2 good options with no clear technical winner, but IBM has experience
in production with [ioredis][] so that is why it is recommended over [redis][].

### Guidance

If you are already using redis for messaging this can provide a low cost option
but does not support more advanced features like High Availability. For more
sophisticated uses cases you should consider a more complete option like Kafka.

[@stomp/stompjs]: https://www.npmjs.com/package/@stomp/stompjs
[amqplib]: https://www.npmjs.com/package/amqplib
[ioredis]: https://www.npmjs.com/package/ioredis
[node-rdkafka]: https://www.npmjs.com/package/node-rdkafka
[redis]: https://www.npmjs.com/package/redis
[ioredis]: https://www.npmjs.com/package/ioredis
[rhea]: https://www.npmjs.com/package/rhea
[KafkaJS]: https://github.com/tulios/kafkajs
