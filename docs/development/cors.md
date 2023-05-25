# Cross origin resource sharing (CORS)

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell the browser to let a web application running at one origin(domain) have permission to access selected resources from a server at a different origin. A web application makes a cross-origin HTTP request when it requests a resource that has a different origin (domain, protocol, and port) than its own origin.

In other words, CORS is a browser security feature that restricts cross-origin HTTP requests with other servers and specifies which domains access your resources.

CORS works by adding new HTTP headers that let servers describe which origins are permitted to read that information from a web browser.  For HTTP requests other than GET and POST, the CORS specification mandates that browers "preflight" the request with an HTTP OPTIONS method to check which methods are supported by the server.  Upon "approval" from the server, the request can be made.

## Simple Requests

Requests that don't trigger a CORS preflight are know as simple requests.  A simple request can be either a GET or a POST.

Given this example:

```js
const xhr = new XMLHttpRequest();
const url = "https://bar.other/resources/public-data/";

xhr.open("GET", url);
xhr.onreadystatechange = someHandler;
xhr.send();
```

This performs a simple exchange between the client and server, using CORS headers to handle the privileges.

The browser might send something that looks like this:

```
GET /resources/public-data/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:71.0) Gecko/20100101 Firefox/71.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Connection: keep-alive
Origin: https://foo.example
```

The request header of note is Origin, which shows that the invocation is coming from https://foo.example.

The server might respond like this:

```
HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2
Access-Control-Allow-Origin: *
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Transfer-Encoding: chunked
Content-Type: application/xml

[…XML Data…]
```

In response, the server returns an **Access-Control-Allow-Origin** header with `Access-Control-Allow-Origin: *` , which means that the resource can be accessed by any origin.

This pattern of the **Origin** and **Access-Control-Allow-Origin** headers is the simplest use of the access control protocol.  If the resource owners at https://bar.other wished to restrict access to the resource to requests only from https://foo.example, they could send `Access-Control-Allow-Origin: https://foo.example`



## Preflighted requests

Unlike simple requests, for "preflighted" requests the browser first sends an HTTP request using the OPTIONS method to the resource on the other origin, in order to determine if the actual request is safe to send. Such cross-origin requests are preflighted since they may have implications for user data.


## Recommended Components

[cors](https://www.npmjs.com/package/cors) is a node.js package for providing a Connect/Express middleware that can be used to enable CORS with various options.

## Guidance

### Reasons to enable CORS

By default, browers assume that your backend server doesn't want to share its resources with a front-end that it doesn't know about.  However, there are certain situations where your backend might want to be accessible to a front-end application, like a website, CORS should be enabled.  List below are some situations, where you might want to make sure CORS is enabled

#### External APIs

For those backends that will be accessible to the outside world, whether they are public or not, should have CORS enabled.


#### Access to Multiple Environments

As part of the development and testing process of a front-end application, you might want to test against multiple environments, like staging and pre-productions, before pushing to production.  If CORS is not enabled on each of these backends, the front-end application will fail to communicate with them.

### Enabling CORS

For backend applications that are written using Express.js, the [cors](https://www.npmjs.com/package/cors) module is an easy way to enable CORS.

Below is an example that enables CORS for all requests received by the backend application:

```
const express = require('express');
const cors = require('cors');

const app = express();

app.use(cors());
```

CORS can also be enabled for just a single route:

```
const express = require('express');
const cors = require('cors');

const app = express();

app.get('/greeting', cors(), (req, res) => {
  ....
});
```

The cors module allows for an options object to be passed in to specify the origin:

```
const express = require('express');
const cors = require('cors');

const app = express();

const corsOptions = {
  origin: 'http://example.com'
}

app.use(cors(corsOptions));
```

### Complex Requests

Certain CORS requests are considered 'complex' and require an initial OPTIONS request (called the "pre-flight request"). An example of a 'complex' CORS request is one that uses an HTTP verb other than GET/HEAD/POST (such as DELETE) or that uses custom headers

Similar to the above example, CORS can be enabled for these "pre-flight" requests per route or for all routes:


```
...
app.options('*', cors()) // include before other routes
...
```

```
...
app.options('/items/:id', cors());
app.del('/items/:id', cors(), (req, res) => {
  ....
});
...
```

Most web frameworks, like express.js, have [similar modules](https://www.npmjs.com/search?q=cors) to help easily enable and manage CORS requests

## Further Reading

* [cors](https://www.npmjs.com/package/cors)

* [CORS module search on npm](https://www.npmjs.com/search?q=cors)

* [CORS on mdn](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)




------------------------------------------

recoomend componts - mention that they all use the same underlying module

pair down the intro section, and then attribute

disambiquate the intro paragraph

access to multiple
- env variable for different environments

guidance
 - proxy server is one way?
  - do we want to do that? it circumvents the browser model
  - if we do have recommnedations on this, needs caveats and related things
- additional htpp layer before the node server,
- separate proxy section, possibly look at API section, even auth section

subsection related to patterns
- token related things


Rename - cross domain communication


reason to enbable:
  - have to require instead of nice to add
  - limit to just domains,  if possible.  public not so much, could whitelist with tokens
  - teams have seen specific origins for things like auth providers,  open for more public things
    - only setting the clients domains for certain projects - david from IBM
curl doesn't care about cors

API section - securing your backend
