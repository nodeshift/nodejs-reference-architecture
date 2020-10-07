## Static assets

For serving static resources we recomend using `express.static` middleware.
Using express.static() method, you can server static resources directly by specifying the folder name where you have stored your static resources.
Documentation for the middleware can be found in:

https://expressjs.com/en/starter/static-files.html

## Caching

The static middleware does no server-side caching. 
It lets you do two methods of client-side caching: ETag and Max-Age
If you configured your static middleware to use client side caching please make sure that 
every modification in your code is represented as different file name. 

When using bundlers you will explicitly need to generate different file names every time content changes.
Example for webpack (most popular bundler) can be found here:

https://webpack.js.org/guides/caching