# Node.js Reference Architecture

## Overview

The goal of the Node.js reference architecture is to present
the `teams` 'opinion' on what components our customers
and internal teams should use when building Node.js applications
and guidance for how to be successful in production with those components.

Traditionally there has been reluctance to recommend a subset
of the packages the JavaScript ecosystem but our customers are increasingly
looking to the `team` for an opinion of where to start.

The components in this architecture are what we recommend to help internal
and external customers get started based on our experience. Other components may be equally
good, but these are the ones we know best and have the most experience with.

- Where possible the opinion is based on what we've used internally and in our customer engagements.
- The components specified will be our first priority for our contributions to open source projects in the JavaScript ecosystem.
- Due to the above these are the components the `team` is best positioned when working with internal and external customers.
  However, we do not include formal support for these components in any of our support offerings unless specifically identified
  in those offerings.
- The recommended components may change over time as technologies and approaches change.

If you want to learn more about some of the discussions that went into the Node.js reference architecture you can check out the [Introduction to the Node.js reference architecture](https://developers.redhat.com/blog/2021/03/08/introduction-to-the-node-js-reference-architecture-part-1-overview) blog post series.

### The team

The `team` consists of engineers from across groups within IBM and Red Hat who:

- are actively engaged in the JavaScript/Node.js community
- have large Javascript/Node.js deployments
- provide consulting advice and/or development related to JavaScript/Node.js for customers
- develop/deliver JavaScript or Node.js components

### Key tenets

- Whenever possible components should have been validated at scale within the `team's`
  JavaScript/Node.js deployments or in engagements with our customers.
- We need to consider licensing and other due diligence when selecting components.
- We are going to start with a focus on the back-end, a similar effort for front-end
  components will make sense as a follow on.

## Components

The reference architecture covers the following components (currently a work in progress
with only a subset of sections having recommendations):

- Functional Components

  - [Web Framework](./docs/functional-components/webframework.md)
  - [Template Engines](./docs/functional-components/template-engines.md)
  - [Message Queuing](./docs/functional-components/message-queuing.md)
  - [Internationalization](./docs/functional-components/internationalization.md)
  - [GraphQL](./docs/functional-components/graphql.md)
  - [Databases](./docs/functional-components/databases.md)
  - [Authentication and Authorization](./docs/functional-components/auth.md)
  - [Data Caching](./docs/functional-components/data-caching.md)
  - [REST API Development](./docs/functional-components/rest-api-development.md)
  - [Scaling and Multi-threading](./docs/functional-components/scaling-multi-threading.md)
  - Consuming Services
  - [Node versions/images](./docs/functional-components/nodejs-versions-images.md)
  - Transactions_handling

- Development

  - [Choosing and vetting dependencies](./docs/development/dependencies.md)
  - [Building good containers](./docs/development/building-good-containers.md)
  - [Static Assets](./docs/functional-components/static-assets.md)
  - [Protecting Code](./docs/development/protecting-code.md)
  - Code Quality
    - [Code Consistency](./docs/development/code-consistency.md)
    - [Testing](./docs/development/testing.md)
    - [Code Coverage](./docs/development/code-coverage.md)
    - [TypeScript](./docs/development/typescript.md)
  - [Accessibility](./docs/development/accessibility.md)
  - References to CI/CD
  - Npm
    - [Npm Proxy / Internal Registries](./docs/development/npm-proxy.md)
    - [Npm Publishing](./docs/development/npm-publishing.md)
    - Package Development
  - [Secure Development Process](./docs/development/secure-development-process.md)

- Operations
  - [Health Checks](./docs/operations/healthchecks.md)
  - Monitoring/Metrics
    - Monitoring
    - [Metrics Collection](./docs/operations/metrics.md)
    - [Distributed Tracing](./docs/operations/distributed-tracing.md)
  - [Problem Determination](./docs/operations/problem-determination.md)
  - [Logging](./docs/operations/logging.md)
  - Rollout
  - Deployment
    - Containers
    - Serverless
  - Load-balancing
  - [Failure Handling](./docs/operations/failurehandling.md)

## Module Diligence

As a minimum, any modules recommended as part of this reference architecture should meet the following criteria:

- The module is not deprecated.
- The module has an appropriate license.
  - Generally leaning towards permissive licenses such as MIT - others should be reviewed on case by case basis.
- The module runs on LTS versions of Node.js.
- The module has appropriate testing.
- The module is appropriately maintained:
  - Regular releases (where appropriate).
  - Critical bugs reports are acknowledged and addressed.
  - Reported security vulnerabilities are patched and released.

## Contributing

To Contribute to this project, please see the [Contributing Guide](./CONTRIBUTING.md).

## Contributors

- Anthony Whalley - Technology Partner Architect - IBM
- Bethany Griggs - Sr. Software Engineer - Red Hat
- Carlos Santana - Senior Technical Staff Member - IBM
- Dominic Harries - Dev Lead at IBM Garage for Cloud
- Jim Lindeman - Sr. Software Engineer - IBM
- Joe Sepi - Open Tech Program Director - IBM
- Lucas Holmquist - Sr. Software Engineer - Red Hat
- Michael Dawson - Node.js lead for Red Hat and IBM
- Noel Madali - Web Architect - The Weather Company at IBM 
- Tony Erwin - Senior Technical Staff Member - IBM
- Wojciech Trocki - Software Engineer - Red Hat
