# Spark Docker Publish Action

## Version `5.0.0-beta.1`

## Description

A GitHub Action to publish Spark Docker containers to a Docker registry.

## Required Inputs

These keys must be set correctly for the action to work.

| Name | Description | Recommended Value |
|---|---|---|
| `package-token` | A [GitHub personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) with `read:packages` permissions. Used for downloading private `npm` packages. | `${{ secrets.CPENY_GH_PACKAGE_READ_TOKEN }}` |
| `publish-token` | A [GitHub personal access token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) with `write:packages` permissions. Used to publish containers to the package registry. | `${{ secrets.CPENY_MACHINE_USER_WRITE_PACKAGES_TOKEN }}` |
| `ssh-key` | An SSH private key with pull access to the repository. | `${{ secrets.CPENY_GH_SSH_PRIVATE_KEY }}` |
| `business-unit` | The full name of the business unit. | `foxsports \| foxnews \| foxbusiness` |
| `component` | The spark stack component we're building for. | `api \| cms \| frontend \| layout-manager \| styles \| scripts`

## Optional Inputs

These keys are set to sane defaults but can be modified as needed.

| Name | Description | Default Value |
|---|---|---|
| `build` | A toggle to prevent a build from happening. Setting this to `false` will also set `push` to `false`.  | `true` |
| `push` | A toggle to prevent the image from being published. | `true` |
| `registry` | The URL of the container registry to publish to.  | `ghcr.io` |
| `ref` | The commit hash, branch or tag to be checked out.  | `${{ github.event.release.target_commitish }}` |
| `slug` | The GitHub repo slug containing the source for the image.  | `${{ github.repository }}` |
| `tag` | The tag version for the image being published. | `${{ github.ref_type == 'branch' && github.sha \|\| github.ref_name }}` |

## Deprecated Inputs

* **`businessUnit`** - **DEPRECATED** in favor of `business-unit`.
* **`publishToken`** - **DEPRECATED** in favor of `publish-token`.
* **`readToken`** - **DEPRECATED** in favor of `package-token`.
* **`sshKey`** - **DEPRECATED** in favor of `ssh-key`.
* **`sourceBranch`** - **DEPRECATED** in favor of `ref`.
* **`version`** - **DEPRECATED** in favor of `tag`.

Note that at some point these will be removed so please switch your action's config to the favored keys.

## Outputs



## Usage Example

```yml
name: Publish Spark Docker Container
on:
  release:
    types: [published, edited]
jobs:
  publish_docker_container:
    runs-on: ubuntu-latest
      - name: Publish Spark Docker Container
        id: publish_spark_docker_container
        uses: foxcorp/spark-docker-publish-action/@v5
        with:
          package-token: ${{ secrets.CPENY_MACHINE_USER_READ_PACKAGES_TOKEN }}
          publish-token: ${{ secrets.CPENY_MACHINE_USER_WRITE_PACKAGES_TOKEN }}
          ssh-key: ${{ secrets.CPENY_GH_SSH_PRIVATE_KEY }}
          business-unit: usfl
          component: api
```
