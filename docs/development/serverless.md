# Serverless

Serverless is a powerful and popular development model where you don’t have to worry about managing and maintaining your application infrastructure. There are two main paradigms when it comes to Serverless.  The first is the operations paradigm which is responsible for the orchestration of containers, scaling them up from and down to zero running instances.

The second paradigm is the functions programming model.  In the serverless context, a function is a single-purpose piece of code created by the developer but run and monitored by the managed infrastructure. A serverless function’s value is its simplicity and swiftness, which can entice even those who don’t consider themselves developers.


## Recommended Components

N/A

## Guidance

While the team doesn't have to much experience in the serverless realm at the moment, there is still some guidance that can be recommended.

### Functions

One of the main recommendations that we can give related to Functions and Serverless in general, is to keep things as stateless as possible.  When a request comes in, the function will scale up and become available for a set period of time before it scales back down and the current context is destroyed.

Node.js is one of the top recommended languages for Functions due to Node's small memory foot print, quick startup time and asynchronous nature.

#### Challenges

There are some challenges when deciding to use functions.  The first is that there is no standard.  How a function should be created and what data and types are available in the function signature, is based on the vendor that the function is being created for.  While not a standard for how functions should be created, the [CloudEvents specification](https://github.com/cloudevents/spec) standardizes on many platforms, such as Knative Serverless and Google Cloud Functions, the payload that is sent.

Second is the local development and remote debugging experience.  This can be challenging for a couple of reasons.  First, when developing locally, if the function needs to interact with other remote services, this can be challenging to setup.  Second, once the function is running on its respective serverless platform, debugging the remote function can be challenging, since it is no small feat to connect a debugger to a remote service.

There are tools that exist to help with this experience, such as the [faas-js-runtime](https://www.npmjs.com/package/faas-js-runtime), but again, this is based on a specific vendor.

### Serverless Platforms

#### Openshift Serverless

OpenShift Serverless is based on the open source Knative project, which provides portability and consistency across hybrid and multi-cloud environments by enabling an enterprise-grade serverless platform.

Developers on OpenShift Serverless can use the provided Kubernetes native APIs, as well as familiar languages and frameworks, to deploy applications and container workloads.

OpenShift Serverless on OpenShift Container Platform enables stateless serverless workloads to all run on a single multi-cloud container platform with automated operations. Developers can use a single platform for hosting their microservices, legacy, and serverless applications.

<!--
#### Apache OpenWhisk

TODO

#### AWS Lambda

TODO

#### Akamai EdgeWorkers

TODO

#### Cloudflare Workers

TODO

#### Fastly Compute@Edge

TODO

-->

## Further Reading

[Node.js Circuit Breakers for Serverless Functions](https://developers.redhat.com/articles/2021/09/15/nodejs-circuit-breakers-serverless-functions)

[Create your first serverless function with Red Hat OpenShift Serverless Functions](https://developers.redhat.com/blog/2021/01/04/create-your-first-serverless-function-with-red-hat-openshift-serverless-functions#)

[Node.js serverless functions on Red Hat OpenShift, Part 1: Logging](https://developers.redhat.com/articles/2021/07/01/nodejs-serverless-functions-red-hat-openshift-part-1-logging)

[Node.js serverless functions on Red Hat OpenShift, Part 2: Debugging locally](https://developers.redhat.com/articles/2021/07/13/nodejs-serverless-functions-red-hat-openshift-part-2-debugging-locally)

[Node.js serverless functions on Red Hat OpenShift, Part 3: Debugging on a cluster](https://developers.redhat.com/articles/2021/12/08/nodejs-serverless-functions-red-hat-openshift-part-3-debugging-cluster)

