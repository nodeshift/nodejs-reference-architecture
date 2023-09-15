# Secure Development Process

It is important to build security into your software development process. Some of the key elements to address in the development process for Node.js modules and applications include:

* Managing dependencies
* Managing access and content of public and private data stores
  such as npm and github 
* Writing defensive code
* Limiting required execution privileges
* Supporting logging and monitoring
* Externalizing secrets
* Maintaining a secure and up to date foundation for deployed
 applications
* Maintaining individual modules

Many modern applications are deployed through containers so that is the focus of this section. However, most of the guidance should apply to other packaging/deployment methods with the requirement to maintain secure base container images replaced with the requirement to keep the bare metal machines used for deployments secure and up to date.

## Recommended Components

N/A

## Guidance

### Managing dependencies

Dependencies are a common vector for security vulnerabilities
and it is important to manage dependencies carefully. This
is covered in the
[choosing and vetting dependencies](./dependencies.md) section of the reference architecture.

### Managing access and content of public and private data stores

Modern development flows often use public and private data stores
including npm and GitHub. We recommend the following:

* Enable Two-Factor Authentication (2FA)
* Ensure projects use a `.npmignore`, `.gitignore`, etc. to avoid 
  accidentally publishing secrets.

2FA is important to ensure the integrity of the committed code and published assets.

A `.npmrc` file is often needed to do npm installs, particularly
if you have private modules. Avoid leaking information in the `.npmrc`
file when building containers through one of these options:
* Use 2 stages builds and avoiding copying the `.npmrc` to the final image
* Avoid adding the secrets to any image in the build process by mounting
  secrets into containers during the build process. Buildah has some functionality
  build in to make this easier. The
  [sneak secreats into your containers](https://projectatomic.io/blog/2018/06/sneak-secrets-into-containers)
  article provides some info on how to do this.
* Delete the `.npmrc` file from the final image AND compressing images
  to flatten layers (least preferred).

### Writing defensive code

Defensive code should:
* Avoid global state.
* Set NODE_ENV to production.
* Use `strict` mode 
* Include good exception handling
* Avoid complex regexes
* Limit the attack surface
* Harden external endpoints
* Take precautions against brute force and denial of service 
  attacks
* Avoid leaking info through errors
* Limit data sent back to front ends
* Discard sensitive data after use
* Validate input and output

**Avoid global state**

Avoid global state. It's an easy way to accidentally leak
information between requests.


**Set NODE_ENV to production**

Some packages use this to decide if they need to
lock things down/share less information.

**Use strict mode**

For files which are not part of ES6 modules enable strict mode by adding `use strict;` to the start of each file. This is not required for ES6 modules as strict mode is enabled by default.

**Include good exception handling**


Handle uncaught exceptions, listen to errors when using EventEmitters and check for errors passed into asynchronous calls.

Have a default handler for express (and other web frameworks) to avoid returning exceptions with the stack trace to the end user.


**Avoid complex regexes**

Complex regexes can lead to potential denial of service attacks. This article provides a good overview of the risks: [Regular_expression_Denial_of_Service_-_ReDoS](https://owasp.org/www-community/attacks/Regular_expression_Denial_of_Service_-_ReDoS)

**Limit the attack surface**

Limit the available attack surface by:
* Only exposing APIs that are needed to support the intended
  functionality. For example, when using express remove any unnecessary routes.
* Group all external endpoints under a prefix (for example /api). This
  makes it easier to only expose APIs which are intended to
  be external in the ingress configuration. Don’t path rewrite to /.
* Limiting access based on authentication. When possible integrate
  an organizational Identity and access control provider instead of
  implementing your own.

**Harden external HTTP endpoints**

Harden external http endpoints by:
* Adding defensive HTTP headers using packages like [Helmet](https://www.npmjs.com/package/helmet).
* Taking precautions against brute force and denial of service 
  attacks. These can come in different types. Most often the team uses
  the following to address each type:
  * Denial of service -> Content delivery network (CDN) and rate limit login
  * One customer using too much -> External API manager (for example Red Hat 3scale API management)
  * Over sized requests -> Enforcing request size limits
* If you are not using a Web Application Firewall (as part of your CDN or stand-alone), ensure you:
  * Prevent HTTP parameter pollution with packages like
    [hpp](https://www.npmjs.com/package/hpp)
  * Protect against Cross site scripting (XSS). For example by using a package like [xss]
    (https://www.npmjs.com/package/xss).
  * Protect against cross site forgery requests
 Use Anti-CSRF tokens. Note that [csurf](https://www.npmjs.com/package/csurf) is deprecated
      and not recommended for use.

**Avoid leaking info through errors**

Do not expose sensitive or internal information in errors returned to the end user. Instead return a unique ID that can be tied back to more specific error information that is written to internals logs.

**Limit data sent back to front ends**

Only send the required data to the front end. For example if a database query returns 4 fields but the front end will only display 3, make sure to remove the fourth field before sending the data on to the front end.

**Discard sensitive data after use**

Do not retain sensitive information beyond where it is needed. Overwrite fields/variables that contain sensitive data once it is not longer needed.

**Validate input**

Unvalidated input can result in:
* command injection
* sql injection
* data corruption
* denial of service

Always validate user input before using it within your application code. Make sure you do this even if you do validation in the client side (browser, mobile application, etc.) as an attacker could send requests directly to the APIs without using the client.

Do not pass unsanitized user input to the Node.js [child_process](https://nodejs.org/api/child_process.html) functions as this can result in command injection where an attacker can run a command on the server on which Node.js is running. This is a good article that goes into more details: 
[avoiding-arbitrary-code-execution-vulnerabilities-when-using-nodejs-child-process-apis](https://developer.ibm.com/articles/avoiding-arbitrary-code-execution-vulnerabilities-when-using-nodejs-child-process-apis/).

Avoid using the [eval](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) function. If you must use it, ensure that you have validate/sanitized all inputs that may be added to the string passed to eval.

When passing user input to database clients always validate the inputs and use prepared statements instead of dynamically building requests (for example an SQL request string).

Unvalidated json input if written directly to a database or accessed by your application can result in data corruption or denial of service when your application fails because it cannot access the fields it expects. Always validate JSON input with a package like [ajv](https://www.npmjs.com/package/ajv).

**Use static analysis**

As part of PR process, incorporate static analysis. A number of the teams members have had success with `Sonarqube` and `checkmarx` to complete these scans.

### Limiting required execution privileges

Design your application to run with the least privileges required. Ensure your application can run as a non-root user, especially when being deployed within containers. See [building-good-containers](./building-good-containers.md) for container recommendations.


### Support logging and monitoring

Design your application to log sensitive/interesting actions and to make it easy for monitoring tools to collect and analyze these logs to identify suspicious patterns. See the section on [logging](../operations/logging.md) for package recommendations.

### Externalize secrets

Secrets should be externalized and made available to the application at runtime through secure means. Make sure you don't commit secrets in code repositories and that you don't build them into container images.

This article provides a good overview and references to additional articles covering the techniques and components used to manage externalized secrets - [GitOps secret management](https://cloud.redhat.com/blog/gitops-secret-management).

More specific to Node.js deployments, [dotenv](https://www.npmjs.com/package/dotenv) is a package that has been used by the team's members and we are also contributing to [kube-service-bindings](https://www.npmjs.com/package/kube-service-bindings) in order to support the use of [kubernetes service bindings](https://github.com/servicebinding/spec).

[node-vault](https://www.npmjs.com/package/node-vault) was mentioned in our discussions as a client for one of the leading products for managing externalized secrets. Similarly, team members involved in deployments with the IBM cloud mentioned [@ibm-cloud/secrets-manager](https://www.npmjs.com/package/@ibm-cloud/secrets-manager).

### Maintaining a secure and up to date foundation for deployed applications

A Node.js application is built on top of a number of foundation components. Throughout its lifetime it is important that you keep this foundation secure and up to date, even if no code changes within your application.

The key elements include:
* Secure and up to date base container images
* Secure and up to date version of the Node.js runtime
* Secure and up to date dependencies

Based on the teams experience we recommend:

* Leverage containers that come with Node.js already bundled in.
Typically there will be an updated container when there are CVE's reported against the Node.js runtime or any of the other components within the container. This is one of the reasons the teams members often use the ubi/nodejs container images(For example: [ubi8/nodejs-14](https://catalog.redhat.com/software/containers/ubi8/nodejs-14/5ed7887dd70cc50e69c2fabb)).
* If you build Node.js binaries into a base image yourself, make sure to subscribe to the [nodejs-sec](https://groups.google.com/g/nodejs-sec) mailing list. This low volume mailing list is used to provide advance notice of security releases and will give you the earliest warning that you may need to update your Node.js version.
* On a regular basis, check for new versions of the base container that you use and plan your CI/CD pipeline so that you can rebase your application or dependency image on a new version of the container when updates are available.
* If you use common dependencies across a number of projects
create a dependency image. While is this good for build times as outlined in [dependency image](https://github.com/nodeshift/nodejs-reference-architecture/blob/main/docs/development/building-good-containers.md#dependency-image), it will also help to reduce the total work required for dependency updates when shared across a number of projects.
* On each update to the dependency image and on a regular basis scan the dependencies in the dependency image for vulnerabilities. A number of the teams members have had success in using `snyk` to complete these scans. Plan your dependency image CI/CD pipeline so that you can update to new versions of dependencies and publish a new version of the dependency image when necessary. Plan your application CI/CD pipelines so that you can rebase your applications on a new version of the dependency image when necessary.
* On each deployment, change to an application's dependencies, and on regular basis scan the dependencies which are deployed for each application. A number of the teams members have had success in using `snyk` to complete these scans. Plan your application CI/CD pipelines so that you can update to new versions of dependencies and redeploy your application when necessary.

### Resolving nested dependencies

Tools like snyk or Mend (aka WhiteSource) will identify npm packages dependencies with versions that have known security vulnerabilities (typically tracked with CVE's).  While often such vulnerabilities are 
not actually exposed in the app using them, like the case of prototype pollution vulnerabilities in an app that does strong input checking, its very hard to prove and maintain/track the lack of exposure to a 
given vulnerable dependency version.  Therefore, security teams will require your app have the updated dependency versions for simplicity.  Ideally, in the case where a nested npm module is pulled in is 
vulnerable, the parent module using it will have a newer version that references a fixed version in its dependencies.  However, that is not always the case and there are tools to manage the cases where
a nested vulnerable dependency version is pulled in by a different npm library that has not yet adjusted it dependencies to the fixed versions. 

If you are using npm the best approach is to use npm version 8.3 or higher and using the [overrides](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#overrides) section. It supports the same single 
version override mechanism as "resolutions" but also supports specifying different dependency versions based on the parent module.  This way, if a single older library can not use the latest dependency due to 
breaking changes, while other dependencies require the latest breaking changes, one can specify a default version and different version for the specific older library. 

For older versions of npm, [npm-force-resolutions](https://www.npmjs.com/package/npm-force-resolutions) library, which reads a "resolutions" section in the package.json to force all instances of a given 
npm module to be set to that version in the package-lock.json. This tool is then run in a "preinstall" script phase so that the actual "npm install" follows the versions it configures in the package-lock.json.

If you are using the `yarn` package-management tool it honors the
[resolutions](https://yarnpkg.com/configuration/manifest#resolutions) 
section without any needing an additional package.

### Maintaining individual modules

Based on the teams experience we recommend:

* For modules maintained in GitHub, enable the `snyk` integration 
  and review/land the PRs generated.
* Test and ensure that the module runs/passes tests on the
  latest LTS versions. This will reduce risk when updates are required for Node.js security releases.

## Further Reading

[Introduction to the Node.js reference architecture: 8 elements of securing Node.js applications](https://developers.redhat.com/articles/2022/08/09/8-elements-securing-nodejs-applications)
