# Node.js Reference Architecture

## Overview

The goal of the Node.js reference architecture is to present
IBM and Red Hat's 'opinion' on what components our customers
and internal teams should use when building Node.js applications
and guidance for how to be successful in production with those components.

Traditionally there has been reluctance to recommend a subset
of the modules the JavaScript ecosystem but our customers are increasingly
looking to Red Hat and IBM for an opinion of where to start.

The components in this architecture are what we recommend to help internal 
IBM and Red Hat teams, as well as external customers, get started based on
our opinion. Other components may be equally
good, but these are the ones we know best and have the most experience with.
* Where possible the opinion is based on what we've used internally and in our customer engagements.
* The components specified will be our first priority for our contributions to open source projects in the JavaScript ecosystem.
* Due to the above these are the components we are best positioned to help you with in Node.js deployments. However, 
  we do not include formal support for these components in any of our support offerings unless specifically identified
  in those offerings.
* These may also shift overtime as technologies and approaches change. The goal is to keep this up to date as a
  central document of record.

### Scope

The goal is for the reference architecture to reflect an opinion that can be supported by groups across IBM and Red Hat, including:

* IBM App Platform
* IBM Cloud Garage
* IBM Node.js Runtimes
* IBM DEG
* IBM Public cloud Node.js Templates
* IBM i Open Source
* RedHat Node.js Runtimes
* RHEL Collections team
* Major IBM Node.js deployments including
  - IBM Cloud UI
  - [Weather Company](https://developer.ibm.com/articles/nodejs-weather-company-success-story/)

### Key tenets

* Whenever possible components should have been validated at scale within our internal
  Node.js deployments (for example Cloud UI or Weather Company) or in engagements with our customers.
* We should identify primary contacts for each of the components so that if we get questions
  or need to support our customers we know who to loop into the conversation first.
* We need to consider licensing and other due diligence when selection components.
* We are going to start with a focus on the back-end, a similar effort for front-end
  components will make sense as a follow on.

## Components

The reference architecture covers the following components:

* Functional Components
  * [Web Framework](./webframework.md)
  * [Message Queuing](./message-queuing.md)
  * [Internationalization](./internationalization.md)
  * Accessibility
  * API Definition
  * Databases
  * [Authentication and Authorization](./auth.md)
  * Caching
  * Multithreading
  * Consuming Services
  * Node versions/images
  * Transactions_handling

* Development
  * Static Assets
  * Testing
  * Keeping up to date
  * Code Quality
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
  * Loadbalancing
  * [Failure Handling](./failurehandling.md)


