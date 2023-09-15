# Typical Development Workflows

Development flows within the team's developer and the customers the team works
with need to accommodate the following:

* the end target/deployment artifact is most often a container
* for some platforms, deployment remains a server or virtual machine
* applications are made of multiple components some of which may be being developed
  by other teams.

The typical development flows encountered by the team include:

* Fully local development
* Fully local development, container based
* Local development of team's component, remote services in a common development environment
* Fully remote development, container based.
* Zero install development environment

Regardless of the development flow, developers typically develop on Windows or MacOS with Linux being
distant third. When running on Windows the trend is towards the use of the Windows Subsystem for Linux.

With developers developing on Windows/MacOS and the deployment target most often being Linux in
a container, the team's experience is that it is important for the developer to do some level of
testing in a container as part of their workflow.

In the past the most common approach for building/running containers on Windows and MacOS
was docker desktop. Now that docker desktop is no longer free, development teams are exploring other

options which include:
* Virtualbox with a linux VM (the disadvantage is that this requires developers to become more
  familiar with Linux). Docker client is still free and it can connect to a remove virtual
  machine.
* podman and podman desktop which provides similar functionality to docker desktop but is
  open source and free.

## Fully local development, native platform

Developers build/test in the local environment (Windows/MacOS) using npm start and once
ready push to CI where the target container or server deployment bundle is built. Testing
with other components is limited to test/integration environments. Any local testing
uses mocks for other components.

This is a common starting point when teams are building a simple application, with a limited
number of components that can be easily moc'd or run locally.

Advantages:
* Easy to set up

Disadvantages:
* native testing means problems due to difference between operation on development
  platform (Windows/MacOS) and deployment platform (Linux/container) are not
  discovered until later in the integration test environment.
* problems related to interaction with other components is not discovered until later
  in the integration test environment

## Fully local development, container based

Developers build/test/integrate in containers and run other components in containers
locally. Kubernetes is often used to run containers along with Helm to spin up other
components needed for testing. Docker compose is another approach that the team 
sees being used to run other components in containers within the local environment.

In both cases a mounted file system is often used to allow live
changes to a running container with strategies like nodemon style watching and
kubectl copy.

Advantages:
* problems related to differences in development(Windows/MacOS) and deployment 
  target (Linux container) are found earlier in the development process.
* Problem related to interaction with other components are discovered earlier
  in the development process.
* No need for network access in order while developing/testing 
* Easier to manage and test against different application dependency versions
  as they are managed locally instead of a shared environment and often have easy to
  use docker image tags.

Disadvantages:
* more complex to setup and manage for each developer
* significant developer machine requirements to run kubernetes and other components
* harder to manage configuration drift between development environment and
  deployment environment because the container infrastructure used on the developers
  workstation often different than that used for production deployment.

## Local development of team's component, remote services in a common development environment

Developers build/test/integrate in containers and access other components for
testing in a shared development/test environment. 

Advantages:
* More limited resource requirement for developer machines
* Less management/complexity for developers

Disadvantages:
* Network connectivity is required to develop
* Harder to explore/test out changes needed in other components to support
  the component you are working on
* Concurrent use of of shared development/test environment running other
  services can add need for co-ordination with other developers/teams. 
* There may be more limited access to containers when running in the
  shared environment, making it harder to debug.

## Fully remote development, container based

Developers build/test/integrate in containers by pushing changes which are built and
tested in a kubernetes environment which is also running the other required components.
Developers often run some limited test with npm start but bulk of testing is done
on remote system.

Advantages:
* Limited resource requirements for developer machines
* Less management/complexity for developer
* Easier to keep development and deployment environments in sync

Disadvantages:
* Network connectivity is required to develop
* Time to push changes can affect iteration time
* Each developer requires sandbox in common kubernetes, adding to management
  complexity and resource requirements.
* Cleanup of non-used resources can be a challenge
  
## Zero install development environment

Developers use a virtualized remote environment and use their local laptop
only as a thin client.

This model is typically an extension to one of the other
development models listed, with the difference being where the code being
developed resides/is created by the developer. For example, as an extension
to the fully local development workflow the developer may use a
remote virtual machine instead of developing directly on their laptop.
As another example, as an extension to the fully remote development workflow a
shared development environment may provide UI's to edit code, build
containers and deploy to a shared kubernetes environment.

The most extreme case of this model is to limit access to a Cloud based IDE
which restricts the functionality available to the developer.

As a baseline this approach inherits the advantages/disadvantages of
the underlying model that it extends.

Additional Advantages:
* Easier setup
* Better control for an organization over the development environment
  and code being developed
* Supports organizations that use a perimeter security model

Additional Disadvantages:
* Additional resources are required
* Cleanup of non-used resources can be a challenge
* High dependency on network connection
* Cloud IDEs tend to be more locked down, giving developers less
  flexibility over development workflow and tools

## Further Reading

[Introduction to the Node.js reference architecture: Typical development workflows](https://developers.redhat.com/articles/2022/12/21/typical-development-workflows)
