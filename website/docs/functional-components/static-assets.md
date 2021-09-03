---
sidebar_position: 9
---

# Static assets

## Strategies

There are different strategies when dealing with assets/resources in a Node.js application:

### Static only content

If your application has only client JavaScript, like a Single Page Application (SPA), look no further. You most likely do not need to use Node.js to host the static content. You can use web servers or object storage like `nginx`, `Apache`, `COS`, `S3`, etc, and front that system with caching (CDN).

### Application with dynamically growing content (user generated content)

If your application has primarily server logic, but with growing content, consider using Node.js in combination with an external storage system like `COS` or `S3`. For example, if you have a Node.js application for uploading images, instead of saving images to the file system, consider saving images to object storage. This is a more scalable approach compared to saving images on the file system, which can grow beyond the infrastructure. 

### Application with frontend

If your application has client and server logic, then you should consider using Node.js web server (express) with static middleware. It is a best practice to couple your frontend and backend together as a single, deployable artifact. Doing so addresses concerns such as:

* Syncing assets to external environments (CDNs, object storage, etc)
* Deploying artifact to different environments (because the assets are self contained, no issues with syncing)
* Able to use same domain for HTTP2

Read futher for additional guidance on using cache-control headers for static assets.

## Recommended packages

* [express.static][]: `express.static` is part of the Express.js package that allows developers to expose static middlewares.

## Guidance

For serving static resources on the application, we recommend using [express.static][] middleware as it has been widely used and tested in production.

When using `express.static()` method, we can serve static resources directly by specifying the folder name where we have stored our static resources.

Documentation for the middleware can be found [here][express.static]

### Caching

The static middleware allows caching of static resources via exposed [caching-headers][].

Origin servers communicate caching instructions via the header `Cache-Control`. The values of `Cache-Control` are called directives. Example directives include: `max-age`, `no-store, no-cache, must-revalidate`, `public, private`, etc.

Freshness control of the resource happens in cache and is based on time. The validation that happens on origin server is based on time and identifiers (ETags). It is important to have ETag header on all HTTP resources (better/stronger than time based header).

#### Common Directive Use Cases

Note: Upstream systems can be picky about interpreting directives for caching. You may have to read documentation for the particular system (Akamai, Fastly, Google CDN, Cloudflare, nginx, varnish) to verify valid directives.

##### Caching static assets for a year

Cache static assets for a year if the filename and contents are uniquely generated

```
Cache-Control: public, max-age=31536000

```

If `Cache-Control` does not have max-age, it will respect Expires header

```
Cache-Control: public
Expires: Sat, 13 Feb 2022 07:00:00 GMT
```

##### Caching HTTP resources only on browser

In some cases, we want to force cache only for the browser and not for CDN or other upstream caches.

```
Cache-Control: private
```

##### No caching allowed

Force upstream to not cache at all. Useful if you need to ensure that an HTTP resource always goes to origin (for example, if the HTTP resource varies due to a cookie and the endpoint is common to all users)

```
Cache-Control: no-store, no-cache, must-revalidate
```

#### Advanced Caching Guidance

For more advanced use cases, caching can be controlled independently of the `Cache-Control` headers. Depending on upstream caching system, you can configure `Cache-Control` header from origin to the CDN, and configure a separate set of caching rules for downstream (the browsers).

Say for example your application contains pages/resources that change depending on a user's logged in state. It is important that `Cache-Control` is not cached on the browser, however we can still cache at the edge and control the "cache key" based on unique identifiers (such as a userId).

This ensures less hits to origin, takes advantage of caching at the edge, and removes the potential for bad user experiences due to aggressively cached pages.

If the application contains uniquely different pages/resources from a non-logged in user, you could keep `Cache-Control` with `private, max-age=300` (or max-age as appropriate based on content and session expiration). 

### Naming Static Assets

If you configured your static middleware to use client side caching please make sure that 
every modification in your code will be creating resources with different filename. 

When using bundlers you will explicitly need to generate different filenames every time content changes. If hash is used in filename, caching directives can be set as long as a year.

Example for webpack (most popular bundler) can be found [here][webpack-caching]. 

[caching-headers]: https://www.freecodecamp.org/news/an-in-depth-introduction-to-http-caching-cache-control-vary/
[express.static]: https://expressjs.com/en/4x/api.html#express.static
[webpack-caching]: https://webpack.js.org/guides/caching
