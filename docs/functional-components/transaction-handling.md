---
sidebar_position: 13
---

# Transaction Handling

Transactions are a common requirement for applications. They
are needed when you want a set of updates either to all
succeed or fail as a group. For a nice intro to some of
the concepts check out
[Transactions](https://cs.uwaterloo.ca/~tozsu/courses/CS338/lectures/15.%20Transactions.pdf).


## Recommended packages

None

### General Guidance

Unlike in the Java ecosystem, there are no well-established application
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
database you are using. As an example this 
[section in the Node.js pg client documentation](https://node-postgres.com/features/transactions)
shows how to handle rollback when using transactions. 

In the team's experience transactions work best with async/await versus
generators and it is good to have a try/catch around the
rollback sections in addition to those which do the commit.

Node.js applications are often structured to use microservices
instead of a monolith which may limit the ability to leverage
the transaction support in databases as not all elements
being updated are updated through the same database
connection. The related challenges are not specific to
Node.js and there are common techniques that are used
including:
  * [2 phase commit](https://www.educative.io/answers/what-is-the-two-phase-commit-protocol)
  * [Saga pattern](https://medium.com/trendyol-tech/saga-pattern-briefly-5b6cf22dfabc)
  
In the teams experience Node.js applications will most often use the
Saga pattern as opposed to 2 phase commit. When 2 phase commit is
used it will have to depend on external support from an underlying
data store. Some databases offer support to help with implementing
the 2 phase commit technique, so read through the documentation for the
database you are using if you are planning to use that technique.

If you want to read more in depth about these techniques
and which one you might want to use, 
[Saga: The new era of transactions in a microservices architecture](https://www.redhat.com/files/summit/session-assets/2019/T42224.pdf)
covers them in more depth.

Some databases offer support to help with implementing
the 2 phase commit technique, so read through the documentation for the
database you are using if you are planning to use that technique.

## Further Reading

* [Introduction to the Node.js reference architecture: Testing](https://developers.redhat.com/articles/2023/07/31/how-handle-transactions-nodejs-reference-architecture)
