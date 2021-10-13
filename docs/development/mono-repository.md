---
sidebar_position: 7
---

# Mono-Repository (monorepo) Tooling and Guidance

Working across multiple repositories for the same project and/or team is cumbersome and slows down developer velocity. A way to improve developer velocity for teams and projects is to leverage a mono-repository (monorepo). With a monorepo, teams will be able to maintain multiple packages in a singular repository without having to switch to different repositories to maintain other packages.

## Tooling

To enable a mono-repository, we recommend leveraging [yarn workspaces](yarn-workspaces) or [npm workspaces](npm-workspaces).

### Setup with Yarn Example

#### Modify package.json in the workspace root

```json
{
  "private": true,
  // this is an array containing glob paths to each workspace
  "workspaces": ["workspace-a", "packages/*"]
}
```

#### Create subfolders and package.json for each package in the monorepo

```json
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

#### Maintaining

With a monorepo, teams can now leverage a common set of tooling for [linting](linting) and [testing](testing) across all packages in the repository. 

Simply modify the `package.json` `scripts` section with linting and testing commands.

##### Building

When building package artifacts in the monorepo, we recommend:

* [bazel](bazel)
* Custom scripts

##### Publishing

If you are working with a set of packages that need to be published, you can leverage:

* [changesets](changesets)
* [semantic-release](semantic-release)

We recommend following semantic versioning across all packages. If a change does not impact all packages, then bump the appropriate minor/patch version as necessary.

For example, if a Package A needs security remediation, and Package B does not, simply increment patch version for Package A.

If you are making a breaking change that is across all packages, apply major version to all packages.


[yarn-workspaces]: https://classic.yarnpkg.com/lang/en/docs/workspaces/
[npm-workspaces]: https://docs.npmjs.com/cli/v7/using-npm/workspaces
[changesets]: https://github.com/atlassian/changesets
[semantic-release]: https://github.com/semantic-release/semantic-release
[bazel]: https://bazel.build/
[linting]: ./linting.md
[testing]: ./testing.md
