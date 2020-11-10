# Clients for REST/HTTP APIs

Node.js applications and frameworks often need to call existing REST/HTTP APIs
as clients.

## Recommended packages

- [axios](https://github.com/axios/axios) for Node.js

  Axios is a promise based HTTP client for the browser and node.js

- [node-fetch](https://github.com/node-fetch/node-fetch) for standard `fetch` API compatibility

  A light-weight module that brings [window.fetch](https://fetch.spec.whatwg.org/) to Node.js

## Guidance

The Node.js core provides low level APIs for HTTP clients, which are not friendly
for application developers. It's often desirable to use a npm package thats offer high
level APIs for ease of use.

There are many modules available for HTTP clients. The popular
[request package](https://github.com/request/request) has been
[deprecated](https://github.com/request/request/issues/3142) and some alternatives
are listed on https://github.com/request/request/issues/3143. A good comparison
is also available on https://github.com/sindresorhus/got#comparison.

A few key perspectives are used to evaluate such packages:

1. Features

- Errors with metadata
- JSON mode
- Browser support
- Promise API
- Stream API
- TypeScript support
- Hooks

- RFC compliant caching
- Cookies (out-of-box)
- Follows redirects
- Advanced timeouts
- Handles gzip/deflate
- Custom defaults
- Install size
- Dependents

- HTTP/2 support
- Pagination API
- Request cancellation
- Retries on failure
- Progress events
- Timings

2. Health of the project

- Issues open
- Issues closed
- Coverage
- Build
- Bugs
- Last commit

3. Popularity

- Downloads
- GitHub stars
