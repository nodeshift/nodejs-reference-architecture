## Static assets

## Recommended packages

* [express-static][]: `express-static` is part of the Express.js package that allows developers to expose static middlewares.

## Guidance

For serving static resources on the application, we recommend using [express-static][] middleware as it has been widely used and tested in production.

When using express.static() method, we can serve static resources directly by specifying the folder name where we have stored our static resources.

Documentation for the middleware can be found [here][express-static]

## Caching

The static middleware allows caching of static resources via exposed [caching-headers][].

Origin servers communicate caching instructions via the header `Cache-Control`. The values of `Cache-Control` are called directives. Example directives include: `max-age`, `no-store, no-cache, must-revalidate`, `public, private`, etc.

Freshness control of the resource happens in cache and is based on time. The validation happens on origin server is based on time and identifiers (ETags).

### Naming Static Assets

If you configured your static middleware to use client side caching please make sure that 
every modification in your code will be creating resources with different filename. 

When using bundlers you will explicitly need to generate different filenames every time content changes. If hash is used in filename, caching directives can be set as long as a year.

Example for webpack (most popular bundler) can be found [here][webpack-caching]. 

[caching-headers]: https://www.freecodecamp.org/news/an-in-depth-introduction-to-http-caching-cache-control-vary/
[express-static]: https://expressjs.com/en/starter/static-files.html
[webpack-caching]: https://webpack.js.org/guides/caching
