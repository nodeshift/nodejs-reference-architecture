# Building Good Containers

There are a number of recommendations based on our experience building
Node.js applications in containers for deployments:

* build non-root containers
* avoid using trusted ports
* use multi-stage builds
* add key tools for problem determination
* use a process manager 
* setting memory limits

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

* Avoid using trusted ports

Ports below 1024 are considered `trusted` and a process must have
additional priviledges to be able to bind to them.

If you respect the recommendation to build your containers as
`non-root` then your process will not be able to bind to the
trusted ports.

Further, although there are ways to set capabilities on the
container to allow non root users to bind to these ports, at
the time of this writing doing so may cause other problems such
as not being able use the `NODE_EXTRA_CA_CERTS` environment
variable. You can read more about the issue
[here](https://github.com/nodejs/node/pull/37727).

Typical work arounds which include using firewall functionality to
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

[multistage-build](https://docs.docker.com/develop/develop-images/multistage-build/)
[Modern web applications on OpenShift: Part 2 -- Using chained builds](https://developers.redhat.com/blog/2018/10/23/modern-web-applications-on-openshift-part-2-using-chained-builds)

It is recommended that you use multi-stage builds to minimize
container size.


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
special expetations for the process run as PID 1 including
reaping zombies and not meeting these expectations can lead
to problems. You can read about the issue in:
[docker-and-the-pid-1-zombie-reaping-problem](https://blog.phusion.nl/2015/01/20/docker-and-the-pid-1-zombie-reaping-problem/) 

[Tini](https://github.com/krallin/tini) is a process manager some of our teams have
used successefully.

## Manage scaling outside of the container

Avoid using the cluster module and processes managers inside of the
container.

From our experience it as efficient or more efficient to handle
scaling outside of the container and ensures the layer with the
best information can scale your application when needed.

##
