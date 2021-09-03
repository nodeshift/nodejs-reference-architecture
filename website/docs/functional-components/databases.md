---
sidebar_position: 3
---


# Databases

We'll not recommend which database to use but instead share
our experience with the Node.js clients used to connect
to whichever database your project/organization has chosen. 

In most cases there is only a single client with widespread
usage, often provided by the project or organizations which
builds the database itself.

## Recommended packages

Members of the team have had success using the following
clients:

| Server        | Recommended client           |
| ------------- | ---------------------------- |
| Cloudant      | [@ibm-cloud/cloudant][]      |
| CouchDB       | [nano][]                     |
| Elasticsearch | [@elastic/elasticsearch][]   |
| Generic SQL   | [odbc][]                     |
| IBM Db2       | [ibm_db][], [odbc][]         |
| Mongo         | [mongodb][]                  |
| Postgress     | [pg][]                       |
| Redis         | [ioredis][]                  |

There are popular databases for which there are
no recommendations. However, if the team did not
have some experience with the Node.js client we've not
included it in the list.

### General Guidance

* Many clients support connection pooling. When available use
  pooling to avoid creating a new connection for each request.

* By default many clients will return all results for a query
  unless you take steps to limit the result size. Unless you are
  sure the result set will always be a manageable size use
  avaliable options to return only a subset of results at a time.

* Some of the the clients require a native database binding
  to be installed. This may limit the platforms on which
  you can run the client. Some may also support both
  pure JavaScript and native bindings. In those cases
  pure JavaScript will be easier to install but the
  native binding may provide better performance.

## Postgress

Recommendation is to use [pg][] as the most
widely used (if not only) client.

## Mongo

Recommendation is to use [mongodb][] which is the
official MongoDB driver provided by the Mongo 
project.

## Redis

Recommendation is to use [ioredis][].
There are 2 good options with no clear technical winner, but IBM has experience
in production with [ioredis][] so that is why it is recommended over [redis][].

### Guidance

If you are already using redis for messaging this can provide a low cost option
but does not support more advanced features like High Availability.

## Cloudant

Current versions of cloundant require a cloudant specific client
which is [cloudant-node-sdk][]. While it is version 0.0.16 as when
this section was last updated, it is a fork of the [nano][] CouchDB
client which has a long history. This client can also be used
to access CouchDB instances if you are using both Cloudant and
CouchDB.

If you are using classic Cloudant instances then you can use the clients
recommended for CouchDB

## IBM Db2

On databases except for Db2 for i the recommendation is to
use [ibm_db][] which is the official driver provided by IBM.

For the Db2 for i database the primary recommendation is to
use [odbc][] which is maintained by IBM and allows you to
do local development and then deploy your application
to the IBM i platform. If you are doing both development and
depolyment on IBM i then using [idb-connector][], [idb-pconnector][]
are good alternatives which require no configuration
or additional installation.

### Guidance

* On IBM i clients can inherit authentication based on the Operating
  system user. In these cases ensure you run the Node.js program
  using the client as non-admin user.

## Elasticsearch

Recommendation is to use [@elastic/elasticsearch][] which is the
official driver provided by Elastic. Note that this client is replacing
the original client provided by Elastic which is being deprecated.

## CouchDB

The primary recommendation is to use [nano][] which
is the official Apache CouchDB client.

A secondary recommendation is [pouchdb][] which makes it easy to
have a local copy which is kept in sync and is great for unit testing.

## Generic SQL

If there is no database specific client or you want your code to be database
agnostic the [odbc][] client is a good choice. It's currently maintained by
IBM team and is the recommended client for access to the IBM i database.

This client should work for any database for which there is an
[odbc](https://github.com/microsoft/ODBC-Specification/blob/master/ODBC%204.0.md)
compliant driver.

### Guidance

Use the built in odbc connection pooling support to avoid creating/destroying
a connecttion for each request.

Use the odbc built in functions for:
* isolation/commit
* transaction support

instead of the SQL equivalents.

[ioredis]: https://www.npmjs.com/package/ioredis
[redis]: https://www.npmjs.com/package/redis
[pg]: https://www.npmjs.com/package/pg
[mongodb]: https://www.npmjs.com/package/mongodb
[oracledb]: https://www.npmjs.com/package/oracledb
[mysql]: https://www.npmjs.com/package/mysql
[mysql2]: https://www.npmjs.com/package/mysql2
[@elastic/elasticsearch]: https://www.npmjs.com/package/@elastic/elasticsearch
[odbc]: https://www.npmjs.com/package/odbc
[cassandra-driver]: https://www.npmjs.com/package/cassandra-driver
[idb-connector]: https://www.npmjs.com/package/idb-connector
[idb-pconnector]: https://www.npmjs.com/package/idb-pconnector
[ibm_db]: https://www.npmjs.com/package/ibm_db
[mssql]: https://npmjs.com/package/mssql
[@ibm-cloud/cloudant]: https://www.npm.js.com/package/@ibm-cloud/cloudant
[nano]: https://www.npmjs.com/package/nano
[pouchdb]: https://www.npmjs.com/package/pouchdb
