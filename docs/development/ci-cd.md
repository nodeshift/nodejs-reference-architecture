---
sidebar_position: 14
---

# CI/CD

Based on common developer workflows as documented in the section titled
[Typical Development Workflows](./docs/development/dev-flows.md#typical-development-workflows)
the end target/deployment artifact is often a container. Most of our
advice/recommendations are therefore in the context of building/testing
one or more containers.

In the context of a Node.js component the version of the component and
the version of Node.js used to run that component are managed through
tools like [helm](https://helm.sh/) or [flux](https://fluxcd.io/) to
configure the version of the component and the base container to be
used in a deployment. The base container may be an existing Node.js
container (for example)
[ubi8/nodejs-16](https://catalog.redhat.com/software/containers/ubi8/nodejs-16/615aee9fc739c0a4123a87e1)
container or a [dependency image](./docs/development/building-good-containers.md#dependency-image).

While a Node.js developer may not need to setup the CI/CD pipleline a
good understanding of their organizations pipeline is often valuable
in order to understand what's needed to externalize configuration in
the code they write as well as being able to investigate problems that
may occur during different environments in the pipeline.

## Recommended Packages

N/A

## Guidance

The team's experiece is that there are most often two different ci/cd flows
which are used at the same time:

* Testing on code check-in
* Container pipeline - a pipeline to build and test containers as they
  are promoted from development through to production.

While tools like [Source to image](https://github.com/openshift/source-to-image),
[docker](https://www.docker.com/) or [podman](https://podman.io/) maybe used by
the developer to test locally as documented in
[Fully local development, container based](./docs/development/dev-flows.md#fully-local-development-container-based),
the developer does not push the container to source control. Instead,
the containers used for deployment are build as part of the container pipeline.

## Testing on code check-in

When updates are checked into a source code repository (most often
some form of git these days) initial testing is automatically kicked off
using services like [Travis CI](https://www.travis-ci.com/) or
[GitHub actions](https://github.com/features/actions). This level of testing
is generally `unit` and `code quality` testing and the teams recommendations
for this kind of testing for Node.js components are captured in the
[Code Consistency](./docs/development/code-consistency.md),
[Testing](./docs/development/testing.md), and
[Code Coverage](./docs/development/code-coverage.md) sections.

When an update lands in the source code repository after passing
those checks, the pipeline for building and testing containers may be triggered
automatically or it may be triggered separately at some interval.

Check-in testing if often configured to run on a number of Node.js
versions in parallel and the team recommends that you test at least on the
LTS version of Node.js that you currently deploy with along with
later LTS versions in order to enable future upgrades.

While the check-in testing may not run on the container that flows
through the container pipeline, the team tries to ensure
that testing is on the same environment/architecture as used
by the container pipeline. In addition, the team also recommends
that the same is true for local testing done by developers.

## Container Pipeline

Once updates have passed the initial check-in testing, the container
pipeline is kicked off. In the teams experience the pipeline may
support a number of stages/environments including:

* Development
  * This environment often mirros the main branch of each component
    and may sometimes not be working due to mistmatches in APIs/use of APIs.
  * Once tests pass in development, PRs may be automatically opened to
    update Staging to the new component levels.
* Staging
  * Staging uses tagged versions of each component which are know to
    work together.
  * They may be multiple staging environments. One which
    mirrors production in terms of non-application components
    (versions of istio, kubernetes, etc.) and additional
    environments which reflect future target configurations
    for these components.
  * PRs may be automatically created to update components version in
    production once test pass in Staging but there is most often a
    formal sign off (by QA or other teams) for these to be accepted
    into production.
* Pre-Production (optional)
  * pre-production may be used to allow customer testing/sign
    off before push to production.
* Production
  * Environment that hosts the customer facing service.

In addition to these environments, the team has also found that supporting
the ability to spin up ephemeral environments to do specific testing when
needed is advantageous.

The version of the component and the version of Node.js (through the base
container image used) is fixed in the Development stage of the pipeline
where the container is built for the component. That container is typically
pushed to an internal registry and later steps in the pipeline use a tagged
version of that container from the registry. 

As the container for the Node.js component is built once and promoted
through the pipeline stages, it is important that all configuration
related to the environment is externalized so that environment specific
values can be provided in each environment. This includes for example
configuration for how to connect to databases and other services, the
Node.js run configuration (production/development) and any other configuration
information.

[Jekins](https://www.jenkins.io/) and
[Tekton Pipelines](https://tekton.dev/) are common tools that have been
used by the team to implement the container pipeline.

The team has found that it is advisable to use a separate git repository/branch
to configure the versions of the components to be tested in each environment
within the container pipeline. One commmon pattern the team has seen is using
helm charts within this repo to configure the versions of the components used
along with the configuration required for a given environment.

The team has found is useful to have shared helm charts for common application
categories, deploying them helm parameters. In addition the team has also found
it useful to separate configuration of the component versions from other
configuration which does not change as often. This helps to isolate other
changes from the more common component version changes.

## Security scans

Security checks are an important part of CI/CD pipelines. Typically the team
deploys checks in both the check-in tests as well as the container pipeline.

Tools like [mend](https://www.mend.io/), [Synk](https://snyk.io/) and those
built into GitHub have been used for scanning in the check-in phase.

Additional container based scans are then employed in the piplelines phases.











