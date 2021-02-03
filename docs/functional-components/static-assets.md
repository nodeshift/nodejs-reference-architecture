## Static assets

## Recommended packages

* [express.static][]: `express.static` is part of the Express.js package that allows developers to expose static middlewares.

## Guidance

For serving static resources on the application, we recommend using [express.static][] middleware as it has been widely used and tested in production.

When using `express.static()` method, we can serve static resources directly by specifying the folder name where we have stored our static resources.

Documentation for the middleware can be found [here][express.static]

### Caching

The static middleware allows caching of static resources via exposed [caching-headers][].

Origin servers communicate caching instructions via the header `Cache-Control`. The values of `Cache-Control` are called directives. Example directives include: `max-age`, `no-store, no-cache, must-revalidate`, `public, private`, etc.

Freshness control of the resource happens in cache and is based on time. The validation that happens on origin server is based on time and identifiers (ETags).

#### Common Directive Use Cases

Note: Upstream systems can be picky about interpreting directives for caching.

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

### Naming Static Assets

If you configured your static middleware to use client side caching please make sure that 
every modification in your code will be creating resources with different filename. 

When using bundlers you will explicitly need to generate different filenames every time content changes. If hash is used in filename, caching directives can be set as long as a year.

Example for webpack (most popular bundler) can be found [here][webpack-caching]. 

[caching-headers]: https://www.freecodecamp.org/news/an-in-depth-introduction-to-http-caching-cache-control-vary/
[express.static]: https://expressjs.com/en/4x/api.html#express.static
[webpack-caching]: https://webpack.js.org/guides/caching
