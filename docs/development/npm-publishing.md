# Npm Publishing Guidelines


## Guidance

When publishing modules to npm, it is recommened to enable 2 factor authenticaton.  How to set that up can be found here https://docs.npmjs.com/configuring-two-factor-authentication.  It is also a good practice to require the use of two-factor authentication or automation tokens for each module that is published.

If the module will be maintained by a group of people, it is better to create an organization for your team/project on npm to make it easier for multiple maintainers to manage and publish the package.

It is also a good practice to have a "prepublish" npm script in the package.json that runs linting and tests before publishing happens.  If your code needs to be transpiled first, having a "prepublish" script will make sure this is also done before publishing.

The use of scoped pacakges is a good practice if you are creating many related packages.

When creating modules that will be published to an internal registry that is not upstream npm, it is a good practice to scope those modules to the name of your organization.  It is also important that you or your company are the owners of the scoped orginization on upstream npm.  This is important if a public module which depends on a private module is accidently published to upstream npm


### Automating Releases

*Not sure if this section makes sense in this doc or not*

* Release-please?
* Link to the ci token article




## Learning Resources

* https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610



