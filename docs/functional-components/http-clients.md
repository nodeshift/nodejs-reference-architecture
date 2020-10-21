# Clients for REST/HTTP APIs

- [ ] Agreement in reference architecture team
- [ ] Validated at scale through IBM use
- [ ] Consistent with guidance in templates/starters
- [ ] IBM Capability to support

Node.js applications and frameworks often need to call existing REST/HTTP APIs
as clients.

## Client libraries for REST/HTTP APIs

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

- For best browser and Node.js compatibility, [node-fetch](https://github.com/node-fetch/node-fetch)
  is recommended as it is mostly compatible with
  [browser fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API).

- For Node.js, [axios](https://github.com/axios/axios) is recommended.
