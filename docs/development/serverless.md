# Serverless

Serverless is a powerful and popular paradigm where you don’t have to worry about managing and maintaining your application infrastructure. In the serverless context, a function is a single-purpose piece of code created by the developer but run and monitored by the managed infrastructure. A serverless function’s value is its simplicity and swiftness, which can entice even those who don’t consider themselves developers.


## Recommended Components

N/A

## Guidance

While the team doesn't have to much experience in the serverless realm at the moment, there is still some guidance that can be recommended.

### Functions

One of the main recommendations that we can give related to Functions and Serverless in general, is to keep things as stateless as possible.  When a request comes in, the function will scale up and become available for a set period of time before it scales back down and the current context is destroyed.

### Serverless Platforms

#### Openshift Serverless

OpenShift Serverless is based on the open source Knative project, which provides portability and consistency across hybrid and multi-cloud environments by enabling an enterprise-grade serverless platform.

Developers on OpenShift Serverless can use the provided Kubernetes native APIs, as well as familiar languages and frameworks, to deploy applications and container workloads.

OpenShift Serverless on OpenShift Container Platform enables stateless serverless workloads to all run on a single multi-cloud container platform with automated operations. Developers can use a single platform for hosting their microservices, legacy, and serverless applications.



## Further Reading

[Node.js Circuit Breakers for Serverless Functions](https://developers.redhat.com/articles/2021/09/15/nodejs-circuit-breakers-serverless-functions)

[Create your first serverless function with Red Hat OpenShift Serverless Functions](https://developers.redhat.com/blog/2021/01/04/create-your-first-serverless-function-with-red-hat-openshift-serverless-functions#)

[Node.js serverless functions on Red Hat OpenShift, Part 1: Logging](https://developers.redhat.com/articles/2021/07/01/nodejs-serverless-functions-red-hat-openshift-part-1-logging)

[Node.js serverless functions on Red Hat OpenShift, Part 2: Debugging locally](hhttps://developers.redhat.com/articles/2021/07/13/nodejs-serverless-functions-red-hat-openshift-part-2-debugging-locally)

[Node.js serverless functions on Red Hat OpenShift, Part 3: Debugging on a cluster](https://developers.redhat.com/articles/2021/12/08/nodejs-serverless-functions-red-hat-openshift-part-3-debugging-cluster)

