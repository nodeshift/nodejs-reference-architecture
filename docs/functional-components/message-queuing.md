# Message Queuing

## Recommended packages

| Server       |  Recommended client        |
|--------------|----------------------------|
|Kafka         |  [node-rdkafka][]          |
|ActiveMQ      |  [rhea][]                  |
|Redis         |  [ioredis][]               |

## Kafka

Recommendation is to use [node-rdkafka][], because it is:
- Widely used and recommended by the messaging groups within the `teams`
  organizations for performance, features, and protocol compatibility.
- Based on the same [librdkafka](https://github.com/edenhill/librdkafka),
  maintained by the Kafka project and used by most language clients.

This is not without risks:
- In the midst of a maintenance challenge that it may or may not be
  [pulling out of](https://github.com/Blizzard/node-rdkafka/issues/628).
- It is written in C++, which can be problematic in some environments.

We are keeping an eye on the situation and may update the recommendation
based on what happens going forward.

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
