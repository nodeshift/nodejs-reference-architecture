---
sidebar_position: 4
---

# Npm Publishing Guidelines

## Guidance

When publishing modules to npm, it is recommended to enable 2 factor authentication. How to set that up can be found here https://docs.npmjs.com/configuring-two-factor-authentication. It is also a good practice to require the use of two-factor authentication or automation tokens for each module that is published.

If the module will be maintained by a group of people, it is better to create an organization for your team/project on npm to make it easier for multiple maintainers to manage and publish the package.

It is also a good practice to have a "prepublish" npm script in the package.json that runs linting and tests before publishing happens. If your code needs to be transpiled first, having a "prepublish" script will make sure this is also done before publishing.

The use of scoped packages is a good practice if you are creating many related packages.

When creating modules that will be published to an internal registry that is not upstream npm, it is a good practice to scope those modules to the name of your organization. It is also important that you or your company are the owners of the scoped organization on upstream npm. This is important if a public module which depends on a private module is accidentally published to upstream npm, which can lead to the "Dependency Confusion" hack that is outlined [in this post](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)

## Publishing Modules

### Preparing Code

#### `.npmignore` or `files`

[npm] has default ignore rules and loads from `.gitignore` but it also offer two methods for you to keep your published packages tidy.

- specifying ignore files in `.npmignore`
- specifying files you only want to publish with `files` in your `package.json`.

Which one to go with is solely up to you and your preference.

#### Tests and Docs

For your tests and any extra documentation, like API reference docs, that goes beyond the packages README, you can choose to publish them or not. For modules that the team publishes we:

- include docs
- exclude tests

Not including these files can decrease the size of the package that is being installed. If the source code for the package is hosted on github, it is a common practice to use github pages to host any API reference docs and provide a link to those in the README and the package.json.

#### Transpiling Sources

A package written in another language like TypeScript should be published with transpiled JavaScript as the primary executable.

Generally the original sources should not be required to use your published package, but it's your preference whether to publish them or not. Similar to the guidance on tests, the modules that the team publishes that are transpiled only contain the generated code.

If your module requires build steps, it is recommended to run those before you publish and not when the user installs the package. This is where you would use the `prePublish` script as mentioned above.

It is important if you are using Typescript or are generating type definitions for your package, that you make sure to add a reference to the generated type file in your package.json and ensure that the file is included when publishing. For Example:

```
  "name": "some_module",
  "description": "A module that does something",
  "main": "./bin/index.js",
  "module": "index.js",
  "types": "types/index.d.ts"
```

#### Module Versions

It is recommended to use [Semantic Versioning](https://semver.org/) when possible. This will make it easier for a user to determine if a new version of a module will potentially break their code.

There are some automation tools that can help with bumping your module to the correct version.

- [release-please](https://github.com/googleapis/release-please)
- [standard-version](https://github.com/conventional-changelog/standard-version)

Both of those tools will base the version bump on commit messages that follow the [conventional commit standard](https://www.conventionalcommits.org/en/v1.0.0/)

The npm cli also provides a [`version` command](https://docs.npmjs.com/cli/v7/commands/npm-version) that can be used to increase the version of package.

#### Publish Internal Modules

When publishing to an internal registry, like Artifactory or Nexus, it is recommended to scope your package. This adds extra protection if this module is accidentally published to a public registry and avoids the dependency confusion hack mentioned above.

How to publish to an internal registry is up to you, but the team recommends the usage of a `.npmrc` file.

A `.npmrc` file can also be used either per project or globally to change the registry that your package is published to. The contents of this file might look something like this:

```
registry=http://my-internal-registry.local
```

If you are using the global `.npmrc` file, you can use the [npmrc module](https://www.npmjs.com/package/npmrc) to easily switch between multiple `.npmrc` configurations, although it is not necessary for publishing to an internal registry.

## Further Reading

* [Introduction to the Node.js reference architecture: Node Module Development](https://developers.redhat.com/articles/2023/02/22/installing-nodejs-modules-using-npm-registry)

* https://github.blog/changelog/2020-10-02-npm-automation-tokens/

* https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610
