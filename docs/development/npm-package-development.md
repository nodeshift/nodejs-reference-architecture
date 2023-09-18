# Npm Package Development

## Recommended Components

N/A

## Guidance

### Package Creation

When starting the creation of a new package, it is recommended to use the `npm init` command instead of hand coding, to quickly and accurately create a new package.json.  The results of accepting all the defaults, which can be done easily with this command `npm init -y`, is below:

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

It should be noted that users and organizations can modify how `npm init` works, tailoring the resulting package.json to their needs.  For more information on this, check out the [official docs](https://docs.npmjs.com/cli/v9/commands/npm-init)

#### package.json

While **name** and **version** are the only fields that are required to publish a package, the team recommends a few others that provide more information to the user.  Recommended package.json fields are below:

* **name** - This is a required field.  While the package name can be anything, it is recommended that the name be something related to the package being created.

  If an organization will be creating multiple packages, it can be a good idea to use the scoping syntax for those packages.  For example, a scoped package in the Nodeshift organization might look like this: `@nodeshift/package1`

* **version** - This is a required field.  It is recommended that any package that is publish adhere to [semantic versioning](https://semver.org/).

  It is recommended that when an older Node.js version is removed and no longer supported, the package should release a new major version.

  For more information and tools that can help with this, checkout our [Module Version](./npm-publishing.md#module-versions) section of the [npm publishing section](./npm-publishing.md).

* **description** - This is a string that will help users discover the package, especially if it is published to the public npm registry

* **keywords** - This is an array of strings that will help users discover the package, especially if it is published
to the public npm registry

* **homepage** - A url to the project homepage,  most likely to point at a github repo.

* **bugs** - The url to your project's issue tracker and / or the email address to which issues should be reported. These are helpful for people who encounter issues with your package.  Formatting should look like this:

  ```
    {
      "url" : "https://github.com/owner/project/issues",
      "email" : "project@hostname.com"
    }
  ```

* **author** - An Author is one person or company who maintains the package.  This field usually consists of an object with a name, and optionally an email and url.

* **contributors** - Contributors is an array of people who maintain the package

* **license** - You should specify a license for your package so that people know how they are permitted to use it, and any restrictions you're placing on it.  The team has the most experience with using both the MIT and Apache-2 licenses, but if you are publishing a package on behalf of a company, it is recommended to consult your organization on what licenses they prefer.

  If a package is going to be unlicensed, it is recommended to set the **private** field to `true`

  More information on licenses and how they relate to the package.json can be [found here](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#license)

* **files** - The list of files that you want published with your package.  This field is very handy when using a bundler to transpile code and you only want to include that transpiled code.  The team recommends not to include tests, which should reduce the package size, but to include docs.  For a listing of the files that are automatically included, check out the [npm docs here](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#files)

* **main** - This is the primary entry point to your package.  This should be a module relative to the root of your package folder.  Most times this will be `index.js`, which is the default if this field is not set.

* **bin** - If your package is intended to be used as a CLI tool, this field should be added and is a map of the command name to the local file name.

  ```
    {
      "bin": {
        "myapp": "./cli.js"
      }
    }
  ```

* **repository** - Specify the place where your code lives. If your package is public, this is helpful for people who want to contribute.

* **scripts** - This property is an array containing script commands that are run at various times in the lifecycle of your package. The key is the lifecycle event, and the value is the command to run at that point.  The team recommends creating scripts that handle calling the tests, linters and any build steps that might need to occur.  The team does recommend to not use a postInstall script if possible, as this could be a security risk.

* **engines** - This is recommended to show which versions of Node.js your package supports.  If this is a public module, it is recommended to try and support the latest LTS versions.  If this is a private package, then this value could be determined by your company.

* **private** - This field is only recommended and should be set to `yes` if your package will not be published to npm.

* **support** - This field is to help package maintainers communicate with and set expectations for their users about the level of support they are willing to provide on a package.  The team has worked closely with the [Node.js Package Maintenance Team](https://github.com/nodejs/package-maintenance) on their recommendations on what this support field should look like.  For one of your modules, [opossum](https://github.com/nodeshift/opossum), we [set this field](https://github.com/nodeshift/opossum/blob/main/package.json#L75) to `true` and supplied our support information in a separate [package-support.json file](https://github.com/nodeshift/opossum/blob/main/package-support.json).

  For more information on the support field, check out what the [Package Maintenance Team says](https://github.com/nodejs/package-maintenance/blob/main/docs/PACKAGE-SUPPORT.md)

* **type** - This field defines the module format that Node.js will use.  For ES Modules(ESM), use `module` and for Common JS(CJS) modules, use `commonjs`.  For more information on how Node.js determines the difference between ESM and CJS modules take a [look at the Node.js official docs here](https://nodejs.org/dist/latest-v18.x/docs/api/packages.html#determining-module-system)

* **types/typings** - For those packages that would like to provide Typescript typings, the types/typings field can be used.  For more information on developing with Typescript, check out our section on [Typescript](./typescript.md)

#### Development Dependencies

While there is no list of development dependencies that the team recommends, we do find that it is helpful to agree on the same list across a team of developers.  This is especially important for linting and testing libraries.  Having a similar set can help with ramp up time if a developer moves teams.

#### Dependencies

For the teams guidance on choosing dependencies, check out the [Choosing and vetting dependencies](./dependencies.md).

During development of a package, it is helpful to add the package-lock.json to source control, so all developers working on the package will be able to install the same versions of dependencies.

It is also recommended to know what semver range you are specifying for any dependency you wish to install.  For example:

The `^` will give you all the minor and patch releases when they become available.

The `~` will include everything greater than a particular version in the same minor range.

This [semver calculator](https://semver.npmjs.com/) is a great resource to make this determination


### Workspaces

npm Workspaces supports managing multiple projects within a singular top-level, root package.  To learn more about using Workspaces, check out the [Mono-Repository (monorepo) Tooling and Guidance](./mono-repository.md) section


### Bundlers and Transpilers

Bundlers are helpful if your package needs to be used by both Node.js and the browser.  The same codebase can be packaged for multiple platforms with a trivial amount of work by using a bundler.  [Webpack](https://webpack.js.org/) is one such bundler that the team has some familiarity with.

For those packages being written in Typescript, you will need to use a transpiler since Node.js does not support running TypeScript natively, so it must first be transpiled to JavaScript. We recommend the `tsc` transpiler that is shipped with [typescript](https://www.npmjs.com/package/typescript). This supports both type checking and transpilation to JavaScript.

For more information on developing with Typescript, check out our section on [Typescript](./typescript.md)

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

* https://docs.npmjs.com/cli/v9/commands/npm-init
* https://docs.npmjs.com/cli/v8/configuring-npm/package-json
* https://docs.npmjs.com/cli/v8/using-npm/scripts
* https://nodejs.org/dist/latest-v18.x/docs/api/packages.html#determining-module-system
* https://semver.npmjs.com/
* https://docs.npmjs.com/cli/v9/commands/npm-dist-tag
* https://docs.npmjs.com/cli/v9/commands/npm-deprecate

* [Introduction to the Node.js reference architecture: Node Module Development](https://developers.redhat.com/articles/2023/02/22/installing-nodejs-modules-using-npm-registry)
