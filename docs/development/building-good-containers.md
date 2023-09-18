---
sidebar_position: 1
---

# Building Good Containers

There are a number of recommendations based on our experience building
Node.js applications in containers for deployments:

- build non-root containers
- avoid reserved/privileged ports (i.e. 1-1023)
- use multi-stage builds
- add key tools for problem determination
- use a process manager
- setting memory limits
- avoiding using `npm` to start application
- tooling for building containers

This section relies of you having already chosen the base images to
start with. For recommendations on base images check out
[Node.js Versions and Container Images - Container images](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/functional-components/nodejs-versions-images.md#container-images)
and [Node.js Versions and Container Images - Commercially Supported Containers](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/functional-components/nodejs-versions-images.md#commercially-supported-containers).

## Build non-root containers

Running processes as root, even in containers can be a security risk,
particularly if external resources are mapped into the container.
The following is a good article which explains why:
[Processes In Containers Should Not Run As Root](https://medium.com/@mccode/processes-in-containers-should-not-run-as-root-2feae3f0df3b#:~:text=Containers%20are%20not%20trust%20boundaries,a%20container%20on%20your%20server)

There are also systems which support running containers as `rootless`.
In order to ensure that your containers can run on these system you
want to avoid running process as root as they may end up depending
on capabilities that are not available when they are run `rootless`.

When using docker/podman you can change the user with the `USER` command.
Well designed base containers will have already done this, but you should
always check what user will be used by default.

```shell
USER 1001
COPY --chown=1001:0 . .
```

It is recommended that you run processes as `non-root` inside your containers.

## Avoid using trusted ports

Ports below 1024 are considered `trusted` and a process must have
additional privileges to be able to bind to them.

If you respect the recommendation to build your containers as
`non-root` then your process will not be able to bind to the
trusted ports.

Further, although there are ways to set capabilities on the
container to allow non root users to bind to these ports, at
the time of this writing doing so may cause other problems such
as not being able use the `NODE_EXTRA_CA_CERTS` environment
variable. You can read more about the issue
[here](https://github.com/nodejs/node/pull/37727).

Typical workarounds which include using firewall functionality to
proxy ports most often don't work in containers as the firewall
capability is often not included in container distributions.

It is recommended that you build your containers so that internally
only ports 1024 and above are used.

## Use multi-stage builds

While layering can reduce the size of the layer that contains
your Node.js application, the total size of all of the layers
for a container still ends up being a concern. This is
particularly true in Kubernetes environments where Pods and
Nodes may come/go frequently and the case were all layers
need to be installed is more common than might be expected.

Best practice is to use a two stage build where a larger
build image is used to build an application and then the
resulting artifacts are copied to a run image. The build
image includes all of the tools needed to build the application
(compilers etc.) while the run image only includes what's
needed for the application to run. The size difference
between the build and run images can often be significant.

There are different ways to build containers but most
will support using a build and run image. You read more
about a few examples in these references:

- [multistage-build](https://docs.docker.com/develop/develop-images/multistage-build/)
- [Modern web applications on OpenShift: Part 2 -- Using chained builds](https://developers.redhat.com/blog/2018/10/23/modern-web-applications-on-openshift-part-2-using-chained-builds)

It is recommended that you use multi-stage builds to minimize
container size.

When using multi-stage builds there are two additional
techniques which can make your build/development process
more efficient:

- using `.dockerignore`
- image layering

### using `.dockerignore`

You might wonder why `.dockerignore` would be useful if
you have a multistage build and only `COPY` the required
artifacts into the deployment image. In this case it is
not about keeping the final image size small, but instead
avoiding slowing down copies into the initial build
image.

As an example, it's common to run npm install locally
to validate the package.json or test locally. If you do
that a COPY command which would normally copy over only
the files required to build (ex `COPY --chown=1001:0 . .`)
will end up copying the `node_modules` directory, and
taking a lot longer.

It's recommended that you use a `.dockerignore` file
which at a minium includes:

```shell
node_modules
.git
.cache
```

### dependency image

The dependencies for your application likely change
less often than the code for your application. This
means that if you build/install your dependencies and
application in the same step you'll end up building/installing
the dependencies even when they have not changed. Couple
that will the fact that it often takes much longer
to build/install the dependencies than the application
and the result is that your build will likely take
longer than needed.

In order to optimize your build times it is often useful
to build a dependency image. The creation of the
dependency image builds/installs the application dependencies
to create a new image (often this is just npm install). Each
time you change your application you then build on top of
that dependency image which can often just be a `COPY`
of JavaScript and other static files into the
dependency image.

## Add key tools for problem determination

It can be difficult to add tooling/packages after the fact when
issues are identified in production. Plan how you will
investigate problems reported in production and include tooling
in your containers in order to support problem determination
workflows.

This may increase the size of your containers but is worth
the increase in size based on our experience.

## Use a process manager

The Node.js and npm processes do not expect to run as PID 1
which is the case when run in a container. There are
special expectations for the process run as PID 1 including
reaping zombies and not meeting these expectations can lead
to problems. You can read about the issue in:
[docker-and-the-pid-1-zombie-reaping-problem](https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/)

[Tini](https://github.com/krallin/tini) is a process manager some of our teams have
used successfully.

## Manage scaling outside of the container

Avoid using the cluster module and processes managers inside of the
container.

From our experience it as efficient or more efficient to handle
scaling outside of the container and ensures the layer with the
best information can scale your application when needed.

## setting memory limits

The Node.js runtime sets default memory limits for the heap which may not
match what you want to use in production.

Use an environment variable in your start scripts so that you can
tell the Node.js runtime in the container to use a limit which matches
the amount of memory you will provide to the container when it is run.

The following is an example of doing so in the start script within
`package.json`:

```shell
"start": "if [ -z \"$MAX_NODE_MEMORY\" ]; then export MAX_NODE_MEMORY=2048; fi; node --max-old-space-size=$MAX_NODE_MEMORY bin/app.js",

```

This will then allow you to configure the `max-old-space-size` to
align with what you define in your kubernetes deployment files or
set withe the --memory option in docker run commands.

## avoiding using `npm` to start application

While you will often see `CMD ["npm", "start"]` in docker files
used to build Node.js applications there are a number
of good reasons to avoid this:

- One less component. You generally don't need `npm` to start
  your application. If you avoid using it in the container
  then you will not be exposed to any security vulnerabilities
  that might exist in that component or its dependencies.
- One less process. Instead of running 2 process (npm and node)
  you will only run 1.
- There can be issues with signals and child processes. You
  can read more about that in the Node.js docker best practices
  [CMD](https://github.com/nodejs/docker-node/blob/main/docs/BestPractices.md#cmd).

Instead use a command like `CMD ["node","index.js"]`,

## tooling for building containers

When containers were first introduced the only way to build
and run them was with `docker`. Depending on the operating
system you are running on, there may be other options which
provide advantages and are worth considering. You can
read more about some of these in
[Podman and Buildah for Docker users](https://developers.redhat.com/blog/2019/02/21/podman-and-buildah-for-docker-users#what_is_buildah_and_why_would_i_use_it_-h2).


## Further Reading

[Introduction to the Node.js reference architecture: Building Good Containers](https://developers.redhat.com/articles/2021/08/26/introduction-nodejs-reference-architecture-part-5-building-good-containers)
