---
sidebar_position: 3
---

# Npm Proxy / Internal Registry

The npm registry is a key part of the node(and Javascript) ecosystem. It allows users to install third-party easily with just a few commands. But what happens when you are part of an organization that limits internet access, or you are worried that a module you use might disappear from the public registry. This is where having a layer between your organization and the public npm registry can help. This is commonly referred to as a npm mirror/npm proxy

## Recommended Components

The _team_ has familiarity with using both Artifactory and Sonatype Nexus. Both have free and enterprise grade tiers available.

## Guidance

It is recommended to use a Proxy/Mirror when possible. There are a few different reasons why you might consider this.

- You need to limit the installation of modules to only a specific set.

- If you have limited network access

- Using a proxy/mirror can provide a centralized point for scanning for security vulnerabilities

- A mirror can reduce the dependency on the public registry.

- You need to maintain a copy of a module incase it is removed from the public registry.

- Being a good npm citizen. The public registry is a free service and npm allows for [update to 5 million requests per month](https://blog.npmjs.org/post/187698412060/acceptible-use), which can be used up quickly with CI builds.

Using a npm mirror/proxy is fairly easy. You can set the _registry_ that the npm cli uses by running `npm set registry URL`.

Since these registry are not Node.js specific and can be used by other languages, organizations might already have something running where npm support can be turned on.

## Further Reading

* [Introduction to the Node.js reference architecture: Node Module Development](https://developers.redhat.com/articles/2023/02/22/installing-nodejs-modules-using-npm-registry)

* https://jfrog.com/artifactory/

* https://guides.sonatype.com/repo3/quick-start-guides/proxying-maven-and-npm/

* https://www.sonatype.com/products/repository-oss-vs-pro-features
