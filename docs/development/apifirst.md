---
sidebar_position: 6
---

# API First

## Guidance

This article describes what it means to use the API-first design approach. It also walks through an example of using this approach with the OpenAPI Specification and with oas-tools as the Node.js back-end application, which enables you to care only about the business logic. All the validation of incoming requests are done by the oas-tools library (based on the OpenAPI Specification file provided).

## What does "API-first approach" mean?

With the API-first approach, designing the API is the first priority before writing any code. Design of the API involves thorough thinking and planning through collaboration with different stakeholders. This result in high-level documentation describing the intent of the API.

This API contract acts as a central draft keeping all your team members aligned on what your API’s objectives are and how your API’s resources are exposed. The finalization of the contract allows the team to build the interface of the application.

After this, the cross-functional teams rely on this interface to build the rest of the application independent of each other. For example, the back-end developer starts building out the implementation logic behind the API,  the front-end developer starts working on different front-end applications, and quality testers start writing tests for the exposed interface.

## Choose an API specification
The first step is to choose an API specification. API specification is a term that is often used interchangeably with API definition. While these terms have many similarities, they are different entities.

An API specification provides a broad understanding of how an API behaves and how the API links with other APIs. It explains how the API functions and the results to expect when using the API.

There are several API specification options:

OpenAPI Specification
GraphQL