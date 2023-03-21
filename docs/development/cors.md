# Cross origin resource sharing (CORS)

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell the browser to let a web application running at one origin(domain) have permission to access selected resources from a server at a different origin. A web application makes a cross-origin HTTP request when it requests a resource that has a different origin (domain, protocol, and port) than its own origin.

In other words, CORS is a browser security feature that restricts cross-origin HTTP requests with other servers and specifies which domains access your resources.


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
