## Static assets

## Recommended packages

* [express-static](https://expressjs.com/en/starter/static-files.html). 
Express static is part of the express.js package that allows evelopers to expose static middlewares.

## Guidance

For serving static resources we recomend using `express.static` middleware as it has been widely used and tested in production.
When using express.static() method, we can server static resources directly by specifying the folder name where we have stored our static resources.

Documentation for the middleware can be found in:
https://expressjs.com/en/starter/static-files.html

### Caching

The static middleware does server-side caching. 
It lets you do two methods of client-side caching: ETag and Max-Age
If you configured your static middleware to use client side caching please make sure that 
every modification in your code will be creating resources with different file name. 

When using bundlers you will explicitly need to generate different file names every time content changes.
Example for webpack (most popular bundler) can be found here:

https://webpack.js.org/guides/caching