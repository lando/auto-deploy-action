# Autodeploy Action

This is a GitHub action that allows you to automatically deploy new packages from a source repo to various dependent repos.

A concrete example would be you have 30 [VitePress](https://vitepress.dev/) sites that rely on a [custom theme](https://vitepress-theme-default-plus.lando.dev/). When that custom theme pushes a new stable release to `npm` it also automatically opens a pull request on all 30 sites with the updated `npm` pacakge.

In this way it is _sorta_ like `dependapot` except that the source repo **pushes** updates to its dependents as opposed to the dependent periodically looking for upstream updates.

It currently comes with the following caveats:

#### Caveats

* Only works with `bun`, `npm` and `yarn` as package managers (would love to add support for `composer`, `pip` etc)
* Only works with `npm`, `yarn` and `github` as "upstream" registries
* Only works `GitHub` repo to `GitHub` repo
* User is responsible for installing any underlying deps (eg `node` and `yarn`) required by this action

## Required Inputs

These keys must be set correctly for the action to work.

| Name | Description | Example Value |
|---|---|---|
| `slug` | The GitHub repo slug you want to deploy the update package to.  | `lando/php` |

## Optional Inputs

These keys are set to sane defaults but can be modified as needed.

| Name | Description | Default | Example |
|---|---|---|---|
| `args` | Extra options to pass into the manager update command. | "" | `--dev` |
| `branch` | The branch to deploy the updated package to. | Automatically created. If `pr` is `false` then the Default branch for `slug`. | `master` |
| `dirs` | The dirs containing a package.json to update. | `./` | `./,./subdir1,./subdir2` |
| `manager` | The package manager to use for updating. | `auto` | `bun` \| `yarn` \| `npm` |
| `package` | The name of the package to update. | Set based on `registry` | `@lando/php` |
| `pr` | Open a pull request with the change. | `true` | `false` |
| `pr-base` | The base branch to open the PR against. | `main` | `master` |
| `registry` | The place we should get the updated package from. | `npm` | `yarn` \| `npm` \| `github` |
| `separator` | The character that separates the `package` and `version` in the package manager update command  | Set based on `registry` | `@` |
| `token` | [GitHub Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) with permission to `read/write` to target `slug` | `${{ github.token }}`. | `MYTOKEN` |
| `version` | The version of the package to update to. | Set based on `registry` | `1.3.2` |

> [!NOTE]
> The `manager` setting defaults to `auto`, using the first lockfile it finds. To avoid ambiguity, don’t mix lockfiles (e.g., package-lock.json and yarn.lock). If you must keep multiple lockfiles, set `manager` explicitly.

## Testing Inputs

These keys are usually not needed but can be useful for testing.

| Name | Description | Default | Example |
|---|---|---|---|
| `deploy` | Toggle to disable deployment. Will `--dry-run` the `git push`. | `true` | `false` |
| `update` | Toggle to disable updating. | `true` | `false` |

## Outputs

These outputs are mostly used internally but are nonetheless available.

```yaml
outputs:
  branch:
    description: "The branch to deploy to."
    value: ${{ steps.auto-deploy-action.outputs.branch }}
  package:
    description: "The package name from user or manifest file to auto deploy."
    value: ${{ steps.auto-deploy-action.outputs.package }}
  version:
    description: "The package version from user or manifest file to auto deploy."
    value: ${{ steps.auto-deploy-action.outputs.version }}
  separator:
    description: "The separator between package and version"
    value: ${{ steps.auto-deploy-action.outputs.separator }}
```

## Changelog

We try to log all changes big and small in both [THE CHANGELOG](https://github.com/lando/auto-deploy-action/blob/main/CHANGELOG.md) and the [release notes](https://github.com/lando/auto-deploy-action/releases).

## Releasing

Create a release and publish to [GitHub Actions Marketplace](https://docs.github.com/en/enterprise-cloud@latest/actions/creating-actions/publishing-actions-in-github-marketplace). Note that the release tag must be a [semantic version](https://semver.org/).

## Maintainers

* [@pirog](https://github.com/pirog)
* [@reynoldsalec](https://github.com/reynoldsalec)

## Contributors

<a href="https://github.com/lando/auto-deploy-action/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=lando/auto-deploy-action" />
</a>

Made with [contrib.rocks](https://contrib.rocks).

## Other Resources

* [Important advice](https://www.youtube.com/watch?v=WA4iX5D9Z64)
