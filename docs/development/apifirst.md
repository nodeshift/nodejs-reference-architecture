---
sidebar_position: 6
---

# REST APIs

Building [RESTFull](https://www.redhat.com/en/topics/api/what-is-a-rest-api) APIs is a typical use
case for Node.js. There are two typical approaches:

* API First - define the API, use tools to help scaffold and then fill in the implementation.
* Code First - implement the APIs and then generate documentation based on exposed API

The team's experience is that the API first approach based on [OpenAPI](https://swagger.io/specification/)
provides benefits in both initial implementation and maintenance and our recommended packages and
guidance is based on that approach, particularly if one or more of the following are true:

- New project without existing API
- Client side and backend are developed by different teams that need way to communicate API changes
- Development on clients and backends starts around the same time giving developers ability to mock API based on OpenAPI spec

> NOTE: This section of the reference arcahitecture focusses on building RESTfull APIs. 
For GraphQL please refer to the [GraphQL Guide][] section.

## "API-first" approach

With the API-first approach, designing the API is the first priority before writing any code. Design of the API involves thorough thinking and planning through collaboration with different teams (both client and backend side). This results in high-level documentation describing the intent of the API and ability to build client without waiting for server to be finished.

This API contract acts as a central draft keeping all your team members aligned on what your API’s objectives are and how your API’s resources are exposed. The finalization of the contract allows the team to build the interface of the application.

After this, the cross-functional teams rely on this interface to build the rest of the application independent of each other. In practice, teams can generate backends stubs and fully functional client libraries to avoid deviation from specification set in the OpenAPI spec file.

## Code First vs API first

Code first approach provides libraries that understand server side backend structure and generate respective OpenAPI files. 
In this approach full control over API lies within server side team - generated OpenAPI file is read only and cannot be effectively
used to negotiate API between client and server.

API first approach uses OpenAPI file as source of truth. Both client and server side generate code based on the OpenAPI file.

## Recommended Packages

List bellow provides comprehensive set of libraries that can be used for an end to end full stack application written in Node.js, 
Express.js as well as client side applications.

### Code Generation Tools

[openapitools/openapi-generator-cli](https://www.npmjs.com/package/@openapitools/openapi-generator-cli)
This CLI provides support for generating source code based on the OpenAPI spec. The project that
provides this cli for JavaScript also provides generators for a number of other
languages as well. This CLI has widespread usage across industry including many community projects at Red Hat.
The project is maintained by OpenAPI Generator Community and you can read the documentation
here:- <https://openapi-generator.tech>. It can be used as both a backend and client generator as follows:

**backend generator**

The nodejs-express-server option  can be used to generate Express.js based stub
implementations based on your OpenAPI file. 
```bash
npx openapi-generator-cli generate -g nodejs-express-server -i yourapi.json -o ./yourproject
```

**Client generator**

The typescript-node option can be used to generate a client for Node.js applications
that allows us to perform requests against another backend

```bash
openapi-generator generate -g typescript-node -i yourapi.json -o ./yourproject
```

### API mocking

[openapi-backend](https://www.npmjs.com/package/openapi-backend) allows you to mock based
on an OpenAPI definition by returning predefined strings. The library provides way not only
return predefined stubs but also perform validation or handle different use cases depending on request 

[@stoplightio/prism](https://www.npmjs.com/package/@stoplight/prism-http) allows you to
automatically mock API using OpenAPI spec definitions. This package is recommended if you
need is an out of the box way to mock API without any development involved.

### API validation middleware

[express-openapi-validator](https://www.npmjs.com/package/express-openapi-validator) is a validator
for express middleware that some of the build have used successfully.

### Creating/editing OpenAPI Specifications

[swagger-editor](https://www.npmjs.com/package/swagger-editor) is the most popular editor
which can be embedded into an existing server or run standalone. If you want to edit your
specifications in YAML, you can use the
[openapi-editor](https://www.npmjs.com/package/openapi-editor) wrapper.

[vscode-openapi](https://github.com/42Crunch/vscode-openapi) is a VScode plugin for
building and validation of OpenAPI files that members of the team using vscode
have used successfully.

## Guidance

Based on the teams experience we recommend the following:

1. Define the API using OpenAPI 3.0, you can write the OpenAPI definitions in YAML or JSON formats, the team does not have a preference for one over the other.
2. Prefer generating code from OpenAPI file for both client and server. Generating code based on the specification will ensure that the same types, formats are used. This will enable your team to iterate on the specification without worry of getting out of sync.
3. When making changes in the OpenAPI file change it's [version](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml#L3). Changed version will help others to detect what kind of changes were made.
4. When introducing breaking changes consider adding them as new endpoints by introducing another v2 prefix in the API path. 
5. Every path should have `operationId` field specified. This field is used by generator to generate method names for clients etc.
6. When building response objects prefer referencing predefined Objects and Enums in [Schemas](https://swagger.io/docs/specification/data-models/)
7. If an API returns a specific [error object](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml#L148-L158) it should be defined in the Schemas.
8. Declare servers and security scheme to enable users to call API from OpenAPI Editor and other tools. 
9. Use [tags](https://swagger.io/docs/specification/grouping-operations-with-tags/) to define namespaces for your API. Grouping operations with tags that will be used to organize your generated source code into folder structure.

### A good example

OpenAPI spec provides an complete and minimalistic [PetStore](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml) example. This example follows all the best practices and patterns for building API.


[GraphQL Guide]: https://nodeshift.dev/nodejs-reference-architecture/functional-components/graphql
