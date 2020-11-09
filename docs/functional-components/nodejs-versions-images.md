# Node.js Versions and Container Images

## Recommended Components

| Distribution type                 | Recommended source                                            |
|-----------------------------------|---------------------------------------------------------------|
| Raw binaries                      | [Node.js Download site](https://nodejs.org/en/download/)      |
| Windows, Mac Installers           | [Node.js Download site](https://nodejs.org/en/download/)      |
| Version manager                   | [nvm](https://github.com/nvm-sh/nvm#installation-and-update)  |
| Commercially Supported Binaries   | OS Packages from OS vendor                                    |
| Binaries with FIPs support        | OS Packages from OS vendor                                    |
| Containers                        | Official Docker images excluding Alpine                       |
| Commercially Supported Containers | Images from distros (for example rhel or ubi images)          |
| Containers with FIPs support      | Images from distros (for example rhel or ubi images)          |

We recommend that you use only [LTS](https://github.com/nodejs/release#release-phases)
versions for production use, and in addition test on the latest `Current` in order
to prepare for future upgrades. A new LTS version is available every October from the
project and past LTS versions go EOL in April 30 months after they were released.
You should 

### Raw binaries

The Node.js projects provides binaries for the 
supported platforms on the [download](https://nodejs.org/en/download/) page.

These are the most up to date packages available and new releases show
up on this page first.

### Windws and Mac installers

The Node.js projects provides installers for Windows and Mac
on the [download](https://nodejs.org/en/download/) page.

These are the most up to date installers available and new releases show
up on this page first.

### Node.js version managers

Node.js version managers provide an easier way to get Node.js
versions from the Node.js download site and switch between them.
The the teams organizations have the most experience with
[nvm](https://github.com/nvm-sh/nvm#installation-and-update)
with the caveat that it does not support windows and that
it should only be used for development as opposed to production
deployments.

### Commercially Supported Binaries

Most often the easiest way to get support is from an operating system
vendor. This generally requires using the binaries which are 
installed using the native package managers for that OS.

**Note:** It is quite common for the version of Node.js which
is installed in this way to be tied to the OS version.
for example if you simply install `apt-get install nodejs` on
Ubuntu 18.04 you get Node.js v8.10.0 which is already end of life (EOL). 

Therefore, it is generally not recommeneded that you use the default
Node.js version provided by an OS package manager. Instructions
on this [page](https://nodejs.org/en/download/package-manager/) may
help in configuring so that you get an up to date version.

For Red Hat and IBM deployments that need commercial support
we recommend the binaries which come with RHEL.

### Binaries with FIPs support  

The community is an awkward period where the only suppored versions
of OpenSSL do not have a FIPs certication. The community binaries
and containers are, therefore, not suitable for deployments that
need FIPs compliance.  

Several Operating system vendors have worked to include Node.js in
the certification of their Operating systems and those are the
recommended way to get a Node.js binaries for use where FIPs is
a requirement.

For Red Hat and IBM deployments that need FIPs support
we recommend the binaries which come with RHEL.

### Container images 

Container images are docker images which have the Node.js binaries already
bundled into the container.

The Node.js [docker](https://github.com/nodejs/docker-node) team works with docker hub
to maintain as set of `official` nodejs docker images on hub.docker.com - 
https://hub.docker.com/_/node

Images are provided for:
  * debian
  * debian-minimal
  * alpine

There are two image flavors based on debian so that you can achieve smaller container
sizes using [multi-stage docker builds](https://docs.docker.com/develop/develop-images/multistage-build/).
The larger images has all of the tools need to build the application while
the minimal image has only the base components needed to run Node.js. In both cases
these images bundle in the binaries which are available on the Node.js download
site and support multiple ptatforms (x64, PPC and s390)

Images are also provided for Alpine which can allow you to achieve even smaller
images sizes. **However**, if you check the
[BUILDING.md](https://github.com/nodejs/node/blob/master/BUILDING.md)
file for the Node.js project you'll see that support for Alpine is `experimental`.
This also means that there is no binary which can be bundled and instead
the creation of the Alpine containers includes building the binaries
themselves. For there reasons we don't recommend using the Alpine images
unless the smaller size is an absolute requirement.

### Commercially Supported Containers

Most often the easiest way to get support is from an operating system
vendor. This generally requires using a host running an operating
system from the vendor as well as containers from that vendor which
include the Node.js binaries.

For example.  if you want to take advantage of the support for
Node.js that comes with RHEL or RedHat Runtimes you will need to use
the rhel or ubi images available from the
[Red Hat container catalog](https://catalog.redhat.com/)

### Containers with FIPs support  

The community is an awkward period where the only suppored versions
of OpenSSL do not have a FIPs certication. The community binaries
and containers are, therefore, not suitable for deployments that
need FIPs compliance.  

Several Operating system vendors have worked to include Node.js in
the certification of their Operating systems and those are the
recommended way to get a Node.js containers for use where FIPs is
a requirement.

For Red Hat and IBM deployments that need FIPs support
we recommend the rhel and ubi Node.js containers.

## Guidance

When possible deploy using containers versus managing the Operating system
and Node.js binaries yourself. This will simplify upgrades and security
response handling.

Always cache the binaries, containers or OS packages tha you use in
production and in build/test pipelines. For example, do not depend
on the Node.js download site being available 24/7.

Subscribe to the nodejs-sec mailing list. This low volumne
mailing list is used to provide advance notice of security releases
and will give you the earliest warning that you may need
to update your Node.js version.

For new applications alwasys start with the latest LTS version.

For existing applications plan to do advance testing on your next
target LTS version when it is released in April each year (it will be the
`Current` for 6 months before being promoted to LTS at the end of
October) and then put it into production in January the following year.  
This will ensure you can ensure that any issues specific to your
deployment can be reported/addressed by the project before it
becomes LTS and ensure you have enough time before the existing LTS
version you are using goes EOL in April.



