# Npm Package Development

* intro

* npm init?
  * custom init files - maybe only if we have experience with it?
  * custom create- ?

* package.json things
  * main prop
  * bin - if cli
  * setting the node version / engines?
  * name and description?
  * using npm scripts
    * Do we care to comment on not using the post-publish as advertising? - no
    * maybe not use postInstall scripts - additional security risk
  * structure?
    * mention that if a company has many modules,  it is good to have common development deps(linting, testing)
    * link to recommended testing libs
  * including files

  * Dependecies
    * looking at vetting deps for this one
  * Dev Dependecies
  * Peer Dependecies
    * bad practice to include peer deps unless as a dev dep?
  * See vetted deps for a guide on ...

* ESM / CJS - What do we have familiarty with?
  * Not a guide on how to setup bundlers or dual esm/cjs

* bundlers
  * mention you can use these for creating both node and browser
  * TS
  * transpile

## Recommended Components

N/A

## Guidance

### Package Creation

When starting the creation of a new package, it is recommended to use the `npm init` command instead of hand coding, to quickly and accuretly create a new package.json.  The results of accepting all the defaults, which can be done easily with this command `npm init -y`, is below:

```
{
  "name": "package_name",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

//TODO: talk about changing the licnese
* propritory stuff, put unlicensed?
* the team most often uses apache2 / MIT

//TODO: add a small mention that you can override the `init` command?  Does any of our teams do this?  if we don't then do we mention this?

-- CREATE JIRA to create thing

-type - which is for cjs/esm
import/export

#### package.json

While name and version are the only fields that are required to publish a package, the team recommends a few others that provide more information to the user.


**Current List of fields(delete this heading once we get the full list)**

* Added the private field?

* description - Yea
* main or bin or both
  * entry point for the package, usually index.js
  * use bin when you are creating a cli
    * recommended to name the executable file the same as the package name?
    * show example?
* scripts
  * mention testing / linting / building?
  * mention the pre/post things
  * mention composable
* keywords // probably a good idea
* author // Be the company name? or indivual user? depends on what?
* license - what license you use is up to you - link out to ref arch recommendation?
* repository - if this is a public module
* files
  * add the files that you want to publish
  * something about compiling and pointing to the dist instead of src?
    * briefly mention the src vs. dist but not go into it,  thats not really what this doc is
  * mention that some things are included by default
  * recommendation on what those files should be. don't usually include tests, but docs sometimes
  * https://docs.npmjs.com/cli/v8/configuring-npm/package-json#files
* bugs?
  * if a public package and code is on github, then usually point to those issues
  * company one, point to theirs,  or nothing
* homepage?
  * usually points to GH repo(if one)
* maintainers?
  * public package, could to show the maintainers?
* engines - should have these
  * what engines you support are up to you,  and if for a company, could be dictated there.  if a public module, should look to support the lts versions
* support - need to go into this a little
  * mention working closely with the package maintence team?

* type`
  * "commonjs" or "module"

  https://nodejs.org/dist/latest-v18.x/docs/api/packages.html#determining-module-system

https://nodejs.org/api/packages.html#exports


#### Development Dependecies

While there is no list of development dependecies that the team recommends, we do find that it is helpful to agree on the same list across a company/organization/division/some_other_name.  This is especially important for linting and testing libraries.  Having a similar set can help with ramp up time if a developer moves teams.

* say something about how we on the nodeshift team used a tool to make sure all the modules are using a certain list.

#### Peer Dependecies

//TODO: need more info here
// bad practice to include peer deps unless as a dev dep?

#### Dependencies

See the vetted section [link]
* add something about best practice with semver things

package-lock/not package lock
shrinkwrap.json

section on trade-off with versions of other modules

TS Typing version?

### CJS / ESM ?

Is there anything to mention in the package.json or name of the file if using esm and not CJS?

* post to node.js/javascript chat

* look at module list and see what they support

### Bundlers

* mention browser / node combo
* tree-shaking?
* for typescript modules?
  * don't want to be a typescript module creation tutorial



### Publish

  For the teams publishing recommendations, see the [Npm Publishing Guidelines](./npm-publishing.md) section

#### tags

There are times when we want to publish an early-release or need to have multiple development streams for a package.  The team recommends the usage of the `tag` flag.

By default, the `latest` tag is used when a package is published.  The `latest` tag is also used when doing a `npm install <package>` when no version is specified.

Here is an example of a package being published as a beta release:

```
npm publish exampleModule --tag beta
```

We can also add tags to previously published packages using the `dist-tag` command:

```
npm dist-tag add exampleModule@0.1.0 beta
```

To see the current list of tags available for a package, use the `npm dist-tag ls` command.

### Deprecate

There might come a time when a package needs to be deprecated.  The general guidance that the team follows is to first update any readme that is associated with the package with details on the deprecation, then do a release.  The next step is to run the `npm deprecate` command to update the npm registry for a package, providing a deprecation warning to all that attempt to install it.

## Further Reading

* https://docs.npmjs.com/cli/v8/configuring-npm/package-json
* https://docs.npmjs.com/cli/v9/commands/npm-dist-tag
* https://docs.npmjs.com/cli/v9/commands/npm-deprecate
