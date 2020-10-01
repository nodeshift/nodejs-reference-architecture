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
* Where possible the opinion is based on what we've used internally and in our customer engagements.
* The components specified will be our first priority for our contributions to open source projects in the JavaScript ecosystem.
* Due to the above these are the components the `team` is best positioned when working with internal and external customers.
  However, we do not include formal support for these components in any of our support offerings unless specifically identified
  in those offerings.
* The recommended components may change over time as technologies and approaches change.

### The team

The `team` consists of engineers from across groups within IBM and Red Hat who:

* are actively engaged in the JavaScript/Node.js community
* have large Javascript/Node.js deployments
* provide consulting advice and/or development related to JavaScript/Node.js for customers
* develop/deliver JavaScript or Node.js components

### Key tenets

* Whenever possible components should have been validated at scale within the `team's`
  JavaScript/Node.js deployments or in engagements with our customers.
* We need to consider licensing and other due diligence when selecting components.
* We are going to start with a focus on the back-end, a similar effort for front-end
  components will make sense as a follow on.

## Components

The reference architecture covers the following components (currently a work in progress
with only a subset of sections having recommendations):

* Functional Components
  * [Web Framework](./webframework.md)
  * [Template Engines](./template-engines.md)
  * [Message Queuing](./message-queuing.md)
  * [Internationalization](./internationalization.md)
  * Accessibility
  * API Definition
  * Databases
  * [Authentication and Authorization](./auth.md)
  * Caching
  * Multi-threading
  * Consuming Services
  * Node versions/images
  * Transactions_handling

* Development
  * Static Assets
  * Keeping up to date
  * Code Quality
    * [Code Consistency](./code-consistency.md)
    * Testing
  * References to CI/CD
  * Npm Mirroring
  * Secure Development Process

* Operations
  * [Health Checks](./healthchecks.md)
  * Monitoring/Metrics
    * Monitoring
    * [Metrics Collection](./metrics.md)
    * Distributed Tracing
  * Problem Determination
  * [Logging](./logging.md)
  * Rollout
  * Deployment
    * Containers
    * Serverless
  * Load-balancing
  * [Failure Handling](./failurehandling.md)

## Contributing

To Contribute to this project, please see the [Contributing Guide](./CONTRIBUTING.md).
