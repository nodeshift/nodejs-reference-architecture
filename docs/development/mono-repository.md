---
sidebar_position: 7
---

# Mono-Repository (monorepo) Tooling and Guidance

Working across multiple repositories for the same project and/or team is cumbersome and slows down developer velocity. A way to improve developer velocity for teams and projects is to leverage a mono-repository (monorepo). With a monorepo, teams will be able to maintain multiple packages in a singular repository without having to switch to different repositories to maintain other packages. A monorepo may not be only JavaScript, and can be a mixture of languages. For example, a monorepo can contain JavaScript, TypeScript, Golang, Python, etc. A monorepo could also be scoped per team or project, meaning any project could belong in a monorepo, or a monorepo could be exclusively scoped for a particular project. As an example, [babel][babel] is a monorepo for babel, whereas Google has an entire monorepo for the company.

## Recommended Packages

To enable a mono-repository, we recommend leveraging [yarn workspaces][yarn-workspaces] or [npm workspaces][npm-workspaces].

### Setup with Yarn Example

#### Modify package.json in the workspace root

```
{
  "private": true,
  // this is an array containing glob paths to each workspace
  "workspaces": ["workspace-a", "packages/*"]
}
```

#### Create subfolders and package.json for each package in the monorepo

```
// /workspace-a/package.json
{
  "name": "workspace-a",
  "version": "1.0.0",
  "dependencies": {
    "foo": "0.0.1"
  }
}

// /packages/foo/package.json
{
  "name": "foo",
  "version": "1.0.0"
}
```

#### Run `yarn install` in the workspace root


Given the above, we should expect the following folder structure
```
/package.json
/yarn.lock
/workspace-a/package.json
/packages/foo/package.json
/node_modules
/node_modules/workspace-a -> /workspace-a
```

## Guidance

There are a handful of benefits and challenges to monorepos.

With a monorepo, it is recommended to leverage a common set of tooling for [linting][linting] and [testing][testing] across all packages in the repository. See our [code-consistency][code-consistency] section for further guidance. Having a common set of tooling is a benefit for monorepos since each package managed in the repo does not need its set of tooling or versioning. On the other hand, teams can also control scripts individually per artifact or package if necessary. See `Advanced Tips / Tricks` section for more details.

While there are a benefits, there are challenges to overcome.

* Detecting what to build. Build times can be long due to overbuilding the entire repository
* Long build times. Because of having to build the entire repository, this will cause build times to increase because tooling no longer is just building one artifact/package, but many different ones.
* Not just JavaScript. A monorepo may not just be JavaScript, and can impact organization, tooling, and how to approach building different artifacts or packages in different languages.
* Git repositories can grow larger in size.  Since we are building and maintaining different packages in a singular repository, we can exponentially grow the size of the git repository.
* Commit messages can be harder to interpret due to multiple artifacts, packages, or teams.


### Building

When building npm packages (or any type of package) (the build) in the monorepo, we have had success using:

* [bazel][bazel]
* Custom scripts

Using appropriate build tools help overcome challenges state previously. With build tools, we are able to detect file changes and build the appropriate artifact/packages necessary without building the entire repository. This helps reduce long build times. Having a good build tool like [bazel][bazel] also allows for potential to build out other project artifact/packages in different languages.

When committing messages, teams can utilize [conventionalcommits][conventionalcommits] to reduce confusion when working on a monorepo.

#### Bazel

We use the Bazel to support multiple programming languages and to determine what components have to be compiled and tested based on source code changes.

#### Custom Scripts

For custom scripts, we leverage Shell Scripts, Makefiles, JS, and Golang tooling to detect changes and build packages and services.

### Publishing

If you are working with a set of packages that need to be published, you can leverage:

* [changesets][changesets]

About [lerna][lerna]: Lerna was previously used but because of [yarn workspaces][yarn-workspaces] and [npm workspaces][npm-workspaces], teams have no longer found a need for [lerna][lerna]

#### Package Releasing

We recommend following semantic versioning across all packages. If a change does not impact all packages, then bump the appropriate minor/patch version as necessary.

For example, if a Package A needs security remediation, and Package B does not, simply increment patch version for Package A.

If you are making a breaking change that is across all packages, apply major version to all packages.

#### Service Releasing

Service releasing is treated differently than publishing since services are released not for package consumption but as a service.

Dependent upon deployment strategy, releases could be tagged differently per change or as an entire set (version of the repository).

[yarn-workspaces]: https://classic.yarnpkg.com/lang/en/docs/workspaces/
[npm-workspaces]: https://docs.npmjs.com/cli/v7/using-npm/workspaces
[lerna]: https://github.com/lerna/lerna
[babel]: https://github.com/babel/babel
[code-consistency]: ./code-consistency.md#guidance
[changesets]: https://github.com/atlassian/changesets
[semantic-release]: https://github.com/semantic-release/semantic-release
[bazel]: https://bazel.build/
[linting]: ./code-consistency.md
[testing]: ./testing.md
[conventionalcommits]: https://www.conventionalcommits.org/en/v1.0.0/
