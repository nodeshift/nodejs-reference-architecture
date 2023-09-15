# Consuming Services

Consuming services over HTTPs is a common pattern in Node.js applications.
Most often these are [REST](https://www.ibm.com/cloud/learn/rest-apis)
apis.

Node.js has a built in HTTP/HTTPs client, however, the experience of the
team is that real deployments need more capabilities than provided by that
built in client.

This section is the compliment to
[REST APIs Development](./rest-api-development.md) sharing our experience
with the packages used to comsumes services instead of building
them.

## Recommended Packages

Two packages that the team has had success with are:

- [axios](https://www.npmjs.com/package/axios) is a promise based
  HTTP client for the browser and node.js.
  Axios is a client that is full featured and has
  significant ecosystem usage.

- [node-fetch](https://github.com/node-fetch/node-fetch) is a light-weight module that brings
  [window.fetch](https://fetch.spec.whatwg.org/) to Node.js.
  Using the fetch API provides fewer features, however it has the
  advantage of being almost what is provided in the browser. While node-fetch version 3 is
  ESM only, the project has indicated that they
  [continue to maintain version 2](https://github.com/node-fetch/node-fetch#commonjs). Node.js has an
  [experimental version of fetch](https://nodejs.org/docs/latest/api/globals.html#fetch)
  which may be a good alternate choice in the future.

## General Guidance

Plan to use a more complete HTTP client from the start of your development.
The experience of the team is that real deployments need more capabilities
than provided by the Node.js HTTP client. Some of the areas where team
commonly find additional functionality is required include:

* Automatic Retries limited to a specified time period
* Caching based on response cache headers to reduce pulling same content repeatedly
* Error handling based on error code to retry or fail quickly

If both the front and backend are written in JavaScript, using the same library
across both front end and backend is good practice. This may favor node-fetch
as it avoids having to pull in an additional library in the browser.

The tools outlined in [REST APIs Development](./rest-api-development.md) may
generate clients in addition to stubs for the API itself. If those
tools generate clients for you, feel comfortable using the http packages
they depend on even if they are not those recommended above. 

Many cloud SDKS provide a higher level API and should be preferred
versus using the HTTP clients recommended above even if they use
a different HTTP client under the covers.

When using node-fetch all HTTP codes are treated as successful, even the 4XX and
5XX. In order to get the behaviour expected with most other clients you will
need to add something like 

```JavaScript
if (res.ok) {return res.json()} else {throw new Error(...) }
```
The fetch API was designed for the browser and cannot be fully
implemented in the back end. In addition, it does cover all aspects
required for a back-end implementation. The API 
provided by [node-fetch](https://github.com/node-fetch/node-fetch)
and the
[experimental version of fetch](https://nodejs.org/docs/latest/api/globals.html#fetch)
in Node.js are not the same as difference choices were made on how
to handle the gaps. For this reason moving from
node-fetch to the built in version of fetch in Node.js will not be seamless.

While [request](https://www.npmjs.com/package/request) is a widely used
package, it has been deprecated and will not be getting updates.
For new applications we recommend you
do not use it and start with one of the above.  (TODO I remember
a mentioned of a maintained fork of request and that it
would be useful to mention here).
