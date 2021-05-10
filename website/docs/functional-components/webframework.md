---
sidebar_position: 9
---


# Web Framework

## Recommended Components

- Express - https://expressjs.com/
  With 10 million downloads a month, Express is the most popular backend Node.js web framework.
  By comparison all of the competitors together have 500k-1m downloads and many of those use Express under the covers.
  It provides a fast, opinionated, minimalist web framework on top of Node.js

## Guidance

Express - https://expressjs.com/ is the recommended general web framework for Node.js based on it's broad use, shallow dependency tree and the available resources for getting started.

When deploying Express we have the following additional recommendations:

- Use the latest version of the 4.x release line. This version is currently the most suitable for production use.
  We recommend using ~4.x.y (where x.y reflects the version you start at) in your package.json so that you get patch
  version updates as you update your application in development. We recommend planned periodic reviews
  to decide when to update to new minor versions.

- Use different ports for different concerns when possible.
  An application can provide additional endpoints for metrics collection or other concerns. It is recommended that
  the main port (for example 3000 or 8080) be reserved for business logic and an admin
  port be used for supporting endpoints. This helps to separate out requests to business logic and makes it easier to collect
  data specific to requests to the business logic.

- Use an environment variable to define the port for the business logic and for the admin port.
  We recommend you use `PORT` and `ADMIN_PORT` as the names. We also recommend that the default ports be `8080` (business) and `9080` (admin).

- Include a liveness and readiness endpoint even if not deploying initially to kubernetes. These endpoints are useful in environments
  other than kubernetes for problem determination and monitoring. See the section on "Health Checks" for more information.

- Define global middleware before routes. Not doing so is a common mistake that can result in middleware not running when expected.

- Use Helmet (https://www.npmjs.com/package/helmet) to set HTTP headers for a basic level of protection from some common attacks.

- Make testable for application testable by:

  - Breaking out logic into smaller components and routes
  - Define a "test" entry in the "scripts" section of the package.json for your applications which runs the units tests.

- See the sections on Logging and Authentication for further recommendations
