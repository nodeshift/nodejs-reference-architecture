---
sidebar_position: 6
---

# API First REST backends with OpenAPI Specification 

## Guidance (change guidance

This reference describes what it means to use the API-first design approach with Node.js backends and JavaScript client applications. Reference is going to use OpenAPI standard along with supporting packages and tools we recomend to implement API first applications.

> NOTE: This guide focused on the OpenAPI Specification for building RESTfull services. 
For GraphQL please refer to the dedicated [GraphQL Guide][]

### What "API-first" mean?

With the API-first approach, designing the API is the first priority before writing any code. Design of the API involves thorough thinking and planning through collaboration with different teams (both client and backend side). This result in high-level documentation describing the intent of the API and ability to build client without waiting for server to be finished.

This API contract acts as a central draft keeping all your team members aligned on what your API’s objectives are and how your API’s resources are exposed. The finalization of the contract allows the team to build the interface of the application.

After this, the cross-functional teams rely on this interface to build the rest of the application independent of each other. In practice teams can generate backends stubs and fully functional client libraries to avoid deviation from specification set in the OpenAPI spec file.

### When to use OpenAPI first and when to avoid

TODO

## Code First vs API first

TODO

### Rest API- Define the API using OpenAPI 3.0

You can write OpenAPI definitions in YAML or JSON formats. 
OpenAPI spec provides an complete and minimalistic [PetStore](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml) example.
This example follows all the best practices and patterns for building API.
Alternatively you can an automatically generate parts of the API from database or entities 
with tools like [apicurio]

### Good patterns for building API First Fullstack Node.JS solutions

1. Preffer generating code from OpenAPI file for both client and server. Generating code based on the specification will ensure that the same types, formats are used. This will enable your team to iterate on the specification without worry of getting out of sync.

2. When making changes in the OpenAPI file change it's [version](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml#L3). Changed version will help others to detect what kind of changes were made.

3. When introducing breaking changes consider adding them as new endpoints by introducing another v2 prefix in the API path. 
 
4. Every path should have `operationId` field specified. This field is used by generator to generate method names for clients etc.

5. When building response objects preffer referencing predefined Objects and Enums in [Schemas](https://swagger.io/docs/specification/data-models/)

6. If API return specific [error object](https://github.com/OAI/OpenAPI-Specification/blob/main/examples/v3.0/petstore-expanded.yaml#L148-L158) it should be defined in Schemas.

7. Declare servers and security scheme to enable users to call API from OpenAPI Editor and other tools. 

8. Use [tags](https://swagger.io/docs/specification/grouping-operations-with-tags/) to define namespaces for your API. Grouping operations with tags that will be used to organize your generated source code into folder structure.

// TODO move this to the top

## Recommended Packages

List bellow provides comprehensive set of libraries that can be used for end to end full stack application written in Node.JS, Express.js and client side application.

### Code Generation Tools

#### @openapitools/openapi-generator-cli - <https://openapi-generator.tech>

CLI provides support for generating source code based on the OpenAPI spec. CLI supports wide range of languages and frameworks:

https://openapi-generator.tech/docs/generators

CLI has widespread usage across industry including many community projects at Red Hat.

Project is maintained by OpenAPI Generator Community

### Node.js backend generator

#### nodejs-express-server - <https://openapi-generator.tech/docs/generators/nodejs-express-server>

This generator generates Express.js based stub implementation based on your OpenAPI file. 
Generation can be done by using openapi-generator cli:

```bash
openapi-generator generate -g nodejs-express-server -i yourapi.json -o ./yourproject
```

### Client Side generator

#### typescript-node - <https://openapi-generator.tech/docs/generators/typescript-node>

This generator generates client for Node.js backend that allows us to perform requests against another backend
against a

```bash
openapi-generator generate -g typescript-node -i yourapi.json -o ./yourproject
```

### API mocking

#### openapi-backend - <https://www.npmjs.com/package/openapi-backend>


### Express validator

#### express-openapi-validator

https://www.npmjs.com/package/express-openapi-validator

### Building OpenAPI

https://www.npmjs.com/package/swagger-editor

https://www.npmjs.com/package/openapi-editor

https://github.com/42Crunch/vscode-openapi

https://www.apicur.io/studio/


[GraphQL Guide]: https://nodeshift.dev/nodejs-reference-architecture/functional-components/graphql