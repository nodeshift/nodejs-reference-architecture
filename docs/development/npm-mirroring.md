# Npm Proxy / Internal Registry

The npm registry is a key part of the node(and Javascript) ecosystem.  It allows users to install third-party easily with just a few commands.  But what happens when you are part of an organization that limits internet access, or you are worried that a module you use might disappear from the public registry.  This is where having a layer between your organization and the public npm registry can help.  This is commonly refered to as a npm mirror/npm proxy


## Recommended Components

The *team* has familiarity with using both Artifactory and Sonatype Nexus.


## Guidance

There are a few different reasons why you might consider mirroring the public npm registry.

* You need to limit the installation of modules to only a specific set.

* If you have limited network access

* You need to maintain a copy of a module incase it is removed from the public registry.

Using a npm mirror/proxy is fairly easy.  You can set the *registry* that the npm cli uses by running `npm set registry URL`.  You can also use the `HTTP_PROXY` and `HTTPS_PROXY` environment variables to set the mirrored registry.


## Learning Resources

https://jfrog.com/artifactory/

https://guides.sonatype.com/repo3/quick-start-guides/proxying-maven-and-npm/

https://verdaccio.org/
