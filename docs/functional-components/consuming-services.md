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

## Recommened Packages

Two packages that the team has had success with are:

- [axios](https://www.npmjs.com/package/axios) for Node.js
  Axios is a promise based HTTP client for the browser and node.js.
  Axios is a client that is full featured and has
  significant ecosystem usage.

- [node-fetch](https://github.com/node-fetch/node-fetch) for standard
  `fetch` API compatibility A light-weight module that brings
  [window.fetch](https://fetch.spec.whatwg.org/) to Node.js.
  Using the fetch API provides fewer features, however it has the
  advantage of being almost what is provided in the browser. Node.js has an
  [experimental version of fetch](https://nodejs.org/docs/latest/api/globals.html#fetch)
  which may be a good alternate choice in the future.

## General Guidance

While [request](https://www.npmjs.com/package/request) is a widely used
package, it has been deprecated and will not be getting updates.
For new applications we recommend you
do not use it and start with one of the above.  (TODO I remember
a mentioned of a maintained fork of request and that it
would be useful to mention here).

The tools outlined in [REST APIs Development](./rest-api-development.md) may
generate clients in addition to stubs for the API itself. If those
tools generate clients for you, feel comfortable using the http packages
they depend on even if they are not those recommended above.

The API provided by [node-fetch](https://github.com/node-fetch/node-fetch)
and the
[experimental version of fetch](https://nodejs.org/docs/latest/api/globals.html#fetch)
in Node.js are not the same. This is because although the fetch API was
designed for the browser, and it cannot be implemented completely and
without extensions in the back end. For this reason moving from
node-fetch to the built in version of fetch in Node.js will not be seamless.






