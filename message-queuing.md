# Message Queuing

## Recommended packages

| Server       |  Recommended client        |
|--------------|----------------------------|
|Kafka         |  [node-rdkafka][]          |
|ActiveMQ      |  [rhea][]                  |
|Redis         |  [ioredis][]               |

## Kafka

Recommendation is to use [node-rdkafka][], because it is:
- Widely used and recommended by IBM and RedHat messaging teams,
  for performance, features, and protocol compatiblity.
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

### IBM and Red Hat use

* Included in the Cloud Event service samples:
  - https://github.com/ibm-messaging/event-streams-samples/blob/master/docs/librdkafka.md
  - https://github.com/ibm-messaging/event-streams-samples/tree/master/kafka-nodejs-console-sample

* Used as part of the Quality Engineering testing for AMQ Streams(Red Hat Kafka product
  at Red Hat (from Simon Woodman swoodman@redhat.com>). In Red Hat backlog to `productize`
  librdkafka which package is based on.
  
* Andrew Schofield(Chief Architect Event streams, Hybrid Cloud) indicated that node-rdkafka is
  the library that most people have had success with.

### Support capability:

* Lead contact: ?

The first place to try and get help if we need to field questions is by posting to the
`#eventstreams-onprem` slack channel. If that does not work out Dale Lane <dale.lane@uk.ibm.com>
from the Cloud messaging team has agreed to help out.

## ActiveMQ

Recommendation is to use [rhea][] which supports AMQP1.0 
(one of the protocols supported by ActiveQ). This module is maintained by Red Hat and has
higher weekly downloads than the competing module for ActiveMQ which supports the STOMP 
protocol (the native ActiveMQ protocol).

### Guidance

### IBM and Red Hat use

- [rhea][] was written by and is maintained by Red Hat. Lead maintainer is jross@redhat.com.
- Included in the Red Hat nodeshift starters [nodejs-messaging-work-queue](https://github.com/nodeshift-starters/nodejs-messaging-work-queue/blob/master/frontend)

### Support capability:

* Lead contact: jross@redhat.com

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
