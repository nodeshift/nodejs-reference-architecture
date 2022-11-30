---
sidebar_position: 13
---

# Transaction Handling

Transactions are a common requirement for applcations. They
are needed when you want a set of updates either to all
succeed for fail as a group. For a nice intro to some of
the concepts check out
[Transactions](https://cs.uwaterloo.ca/~tozsu/courses/CS338/lectures/15.%20Transactions.pdf).


## Recommended packages

None

### General Guidance

Unlike like Java ecosystem, there are no well established application
servers that support transactions and no JavaScript specific standards
for transactions.

However, this does not mean that you cannot use transactions with
Node.js. Many of the databases and the recommended clients covered
in the [databases](./databases.md) section support transactions.
This makes it relatively easy to update multiple elements
with the database within a transaction. Typically
the clients provide a simple API to start, commit and rollback
transactions or the equivalent can be done by submitting queries
through the same APIs used to query and update data. Since
these APIs vary by database, consult the documentation for the
client and database for examples of how to use transactions.

Node.js applications are often structured to use microservices
instead of a monolith which may limit the ability to leverage
the transaction support in databases as not all elements
being updated are updated through the same database
connection. The related challenges are not specific to
Node.js and there are common techniques that are used
including:
  * 2 phase commit
  * Saga pattern

If you want to read more in depth about these techniques
and which one you might want to use, 
[Saga: The new era of transactions in a microservices architecture](https://www.redhat.com/files/summit/session-assets/2019/T42224.pdf)
covers them in more depth.

To implement 2 phase commit and saga techniques you may also
need some form of messaging queing as covered
in the [message queuing](message-queuing.md) section.

Some databases offer support to help with implementing
2 phase commit so read through the documentation for the
database you are using if you are planning to that technique.
