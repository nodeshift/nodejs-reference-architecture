# GraphQL Development

GraphQL developement requires number of tools and packages that can be used on both client and server. Our target will be to provide comprehensive set of the tools to add graphql support for both client 
and server side applications

## Recommended Packages for Node.js Server development

* `express-graphql` - https://graphql.org/graphql-js/express-graphql
Exposes GraphQL schema using Express.js

* `GraphQL Tools` - https://github.com/ardatan/graphql-tools
Builds GraphQL schema using resolvers

* `DataLoader` - https://github.com/graphql/dataloader
Prevents from overfetching data when querying relationships

## Recomended packages for Client side development

* `GraphQL-Tag` - https://github.com/apollographql/graphql-tag
Compiles graphql schema on the client (provides browserify plugin)

* `URQL` - https://formidable.com/open-source/urql
GraphQL Client with caching and offline support

* `Apollo-Client` - https://github.com/apollographql/apollo-client/
Alternative GraphQL Client with caching and offline support

* `GraphQL-Code-Generator` - https://graphql-code-generator.com
Generates TypeScript source code for client and server

## Recommended Tools for visualizing GraphQL Schema and Queries

* `graphiql` - https://github.com/graphql/graphiql
Graphiql is web application that allows you to build and execute GraphQL queries against your schema

* `GraphQL-CLI` https://github.com/Urigo/graphql-cli
Suite of tools and commands for performing various operations on GraphQL schema. 

## Recomended practices for GraphQL Schema development

* `GraphQL Rules` - https://graphql-rules.com/
Set of recomendations for building proper schema

* `GraphQL CRUD` - https://graphqlcrud.org
Set of rules and generators to automate building GraphQL schema

## Guidance

When building GraphQL API from scratch we recomend using reference GraphQL-js reference implementation which was 
proven to be the most performant and have continous support from community. Entire development is currently backed by Linux foundation.

### GraphQL Server

For GraphQL Server we recomend using GraphQL-Express for exposing GraphQL APIs over the network and GraphQL-Tools to build GraphQL Schema:

https://github.com/ardatan/graphql-tools#example

Developers can use top level database query languages. 
We recomend using Knex(http://knexjs.org/) for performing queries from GraphQL to relational databases.

If your GraphQL model have relationships please consider using DataLoader to prevent from overfetching problem:

https://github.com/graphql/dataloader

### GraphQL Client

For GraphQL client we recomend URQL (https://formidable.com/open-source/urql/) that can work with React and any other JS based library. 
When using bundler we strongly recomend to compile your graphql queries using GraphQL-Tag:

https://github.com/apollographql/graphql-tag

### Typescript support

If you use typescript in your project we recomend GraphQL-Code-Generator to generate typings for both client and server:

https://graphql-code-generator.com

### Persisted queries

Persisted queries are mechanism to improve performance by utilizing already cached and well known queries.
Those queries can be also later hosted on the CDN.

For persisted queries we can use approaches that are:

- Dynamic (no need to compile queries on client as server caches them)
- Static (requires client side compilation)

For static persited queries we recomend
https://github.com/valu-digital/graphql-codegen-persisted-query-ids

For dynamic persisted queries we recomend 

2. [Apollo APQs](https://www.apollographql.com/docs/apollo-server/performance/apq/) which needs [Apollo server](https://www.apollographql.com/docs/apollo-server/)


