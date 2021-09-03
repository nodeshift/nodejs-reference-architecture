---
sidebar_position: 1
slug: /
---

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

