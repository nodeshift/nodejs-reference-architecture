# Typical Development Workflows

Developement flows within the team's developer and the customers the team works
with need to accomodate the following:

* the end target/deployment artifact is most often a container
* applications are made of multiple components some of which may be being developed
  by other teams.

The typical development flows encountered by the team include:

* Fully local development
* Fully local development, container based
* Local development of team's component, remote services in a common development environment
* Fully remote development, container based.

Regardless of the development flow, developers typically develop on Windows or MacOS with Linux being
distant third. When running on Windows the trend is towards the use of the Windows Subsystem for Linux.

With developers developing on Windows/MacOS and the deployment target most often being Linux in
a container, the team's experience is that it is important for the developer to do some level of
testing in a container as part of their workflow.

In the past the most common approach for building/running containers on Windows and MacOS
was docker desktop. Now that docker desktop is longer free, development teams are exploring other
options which include:
* Virtualbox with a linux VM (the disadvantage is that this requires developers to become more
  familiar with Linux). Docker client is still free and it can connect to a remove virtual
  machine.
* podman and podman desktop which provides similar functionality to docker desktop but is
  open source and free.

## Fully local development, native platform

Developers build/test in the local environment (Windows/MacOS) using npm start and once
ready push to CI where the target container is built. Testing with other components
is limited to test/integration environments. Any local testing uses mocs for other components.
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

Disadvantages:
* more complex to setup and manage for each developer
* significant developer machine requirements to run kubernetes and other components

## Local component development, remove services

Developer build/test/integrate in containers and access other components for
testing in a shared development/test environment. 

Advantages:
* More limited resource requirement for developer machines
* Less management/complexity for developer

Disadvantages:
* Network connectivity is required to develop
* Concurent use of of shared development/test environment running other
  services can add need for co-ordination with other developers/teams. 

## Fully remote development, container based

Developers build/test/integrate in containers by pushing changes which are built and
tested in kubernetes environment which is also running the other required components.
Developers often run some limited test with npm start but bulk of testing is done
on remote system.

Advantages:
* Limited resource requirement for developer machines
* Less management/complexity for developer

Disadvantages:
* Network connectivity is required to develop
* Time to push changes can affect interation time.
