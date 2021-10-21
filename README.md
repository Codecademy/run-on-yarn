# run-on-yarn

Composite GitHub Action to run a command with Yarn. ✨

## Usage

This action will:

1. Use `actions/checkout` and `actions/setup-node` to set up a yarn environment
2. Use `actions/cache` to restore a cache based on the `yarn.lock`
3. `yarn install --frozen-lockfile` if the folder didn't exist in the cache
4. Run `yarn ${{ inputs.command }}`

### Inputs

* `command`: Command to run. Required.

## Example

Assuming the `compile`, `format:verify`, and `test` scripts exist in your `package.json`, this setup will run those commands in parallel as your Push CI job:

```yml
# .github/workflows/push.yml
name: Push CI

jobs:
  ci:
    runs-on: ubuntu-latest
    steps:
      - uses: Codecademy/run-on-yarn@v1
        with:
          command: ${{ matrix.command }}

    strategy:
      fail-fast: false
      matrix:
        command: ['compile', 'format:verify', 'test']

on: push
```

### Contribution Guidelines

We'd love to have you contribute!
Check the [issue tracker](https://github.com/Codecademy/run-on-yarn/issues) for issues labeled [Accepting PRs](https://github.com/Codecademy/run-on-yarn/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3A%22Accepting+PRs%22) to find bug fixes and feature requests the community can work on.
If this is your first time working with this code, the [Good First issue](https://github.com/Codecademy/guidelines/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3A%22Good+First+Issue%22+) label indicates good introductory issues.

Please note that this project is released with a [Contributor Covenant](https://www.contributor-covenant.org).
By participating in this project you agree to abide by its terms.
See [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md).
