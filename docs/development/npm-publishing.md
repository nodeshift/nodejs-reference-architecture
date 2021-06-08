# Npm Publishing Guidelines


## Guidance

When publishing modules to npm, it is recommened to enable 2 factor authenticaton.  How to set that up can be found here https://docs.npmjs.com/configuring-two-factor-authentication.  It is also a good practice to require the use of two-factor authentication or automation tokens for each module that is published.

If the module will be maintained by a group of people, it is better to create an organization for your team/project on npm to make it easier for multiple maintainers to manage and publish the package.

It is also a good practice to have a "prepublish" npm script in the package.json that runs linting and tests before publishing happens.  If your code needs to be transpiled first, having a "prepublish" script will make sure this is also done before publishing.

The use of scoped pacakges is a good practice if you are creating many related packages.

When creating modules that will be published to an internal registry that is not upstream npm, it is a good practice to scope those modules to the name of your organization.  It is also important that you or your company are the owners of the scoped orginization on upstream npm.  This is important if a public module which depends on a private module is accidently published to upstream npm

## Publishing Modules

### Preparing Code

#### `.npmignore` or `files`

[npm] has default ignore rules and loads from `.gitignore` but it also offer two methods for you to keep your published packages tidy.

- specifying ignore files in `.npmignore`
- specifying files you only want to publish with `files` in your `package.json`.

Which one to go with is solely up to you and your preference.

#### Tests and Docs

For your tests and any extra documentation, like API reference docs, that goes beyond the packages README, it's your preference on whether to publish them or not.  If the source code for the package is hosted on github, it is a common practice to use github pages to host any API reference docs and provide a link to those in the README.


#### Transpiling Sources

A package written in another language like TypeScript should be published with transpiled JavaScript as the primary executable.

Generally the original sources should not be required to use your published package, but it's your preference whether to publish them or not.

If your module does require any build steps, it is recommended to run those before you publish and not when the user installs the package.  This is where you would use the `prePublish` script as mentioned above.

#### Module Versions

It is recommened to use [Semantic Versioning](https://semver.org/) when possible.  This will make it easier for a user to determine if a new version of a module will potentianlly break their code.

There are some automation tools that can help with bumping your module to the correct version.

* [release-please](https://github.com/googleapis/release-please)
* [standard-version](https://github.com/conventional-changelog/standard-version)

Both of those tools will base the version bump on commit messages that follow the [coventional commit standard](https://www.conventionalcommits.org/en/v1.0.0/)

The npm cli also provides a [`version` command](https://docs.npmjs.com/cli/v7/commands/npm-version) that can be used to increase the version of package.


#### Publish Internal Modules

// TODO: need input from the other folks



## Learning Resources

* https://github.blog/changelog/2020-10-02-npm-automation-tokens/

* https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610



