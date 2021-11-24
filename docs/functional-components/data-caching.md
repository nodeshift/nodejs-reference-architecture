---
sidebar_position: 3
---

# Data Caching

There are two main types of caching used within Node.js applications. These include:

- in-process
- cluster wide

## Recommended packages

| Caching type | Recommended client |
| ------------ | ------------------ |
| in process   | [lru-cache][]      |
| cluster wide | [ioredis][]        |

### In process

Recommendation is to use [lru-cache][] which is broadly used within the
the `teams` organizations and in the JavaScript ecosystem with > 28 million weekly
downloads.

### Cluster wide

For cluster wide caching with Redis, the recommendation is to use [ioredis][].
There are 2 good options with no clear technical winner for redis, but the `teams`
organizations have experience in production with [ioredis][] so
that is why it is recommended over [redis][]. Depending on the server you are
using there may be features which are only available in a server specific client and
if you need those features then using the specific client makes sense insteda of ioredis.

## Guidance

- Consider your call behaviour to ensure you need to cache a specific piece of data at all
- For cluster wide caching, include a version prefix as part of keys from the start, otherwise you
  will encouter problems when you try to update the caching schema

[ioredis]: https://www.npmjs.com/package/ioredis
[lru-cache]: https://www.npmjs.com/package/lru-cache
[redis]: https://www.npmjs.com/package/redis
