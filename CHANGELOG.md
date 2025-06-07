## {{ UNRELEASED_VERSION }} - [{{ UNRELEASED_DATE }}]({{ UNRELEASED_LINK }})

* Added support for `bun` package manager
* Added `auto` detection of `manager` and set as the default

## v3.0.0 - [February 8, 2024](https://github.com/lando/auto-deploy-action/releases/tag/v3.0.0)

* Rebased on `npm` as the default `manager`

## v2.0.5 - [June 17, 2023](https://github.com/lando/auto-deploy-action/releases/tag/v2.0.5)

* Switched release flow over to [@lando/prepare-release-action](https://github.com/lando/prepare-release-action)

## v2.0.4 - [June 17, 2023](https://github.com/lando/auto-deploy-action/releases/tag/v2.0.4)

* Switched release flow over to [@lando/prepare-release-action](https://github.com/lando/prepare-release-action)

## v2.0.3 - [April 27, 2023](https://github.com/lando/auto-deploy-action/releases/tag/v2.0.3)

* Updated core actions to `v3`

## v2.0.2 - [April 27, 2023](https://github.com/lando/auto-deploy-action/releases/tag/v2.0.2)

* Switched `set-output` and `save-state` to new `$GITHUB_OUTPUT` and `$GITHUB_STATE`. See [this](https://github.blog/changelog/2022-10-11-github-actions-deprecating-save-state-and-set-output-commands/)

## v2.0.1 - [December 6, 2022](https://github.com/lando/auto-deploy-action/releases/tag/v2.0.1)

* Added a `dirs` key for monorepo projects that need to update multiple dirs

## v2.0.0

* Added `pr` key to automatically open a Pull Request against the target repo. Set this as the default.

## v1.0.1

* First release
