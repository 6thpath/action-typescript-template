[![Build & Test](https://github.com/6thpath/action-typescript-template/actions/workflows/build-test.yml/badge.svg)](https://github.com/6thpath/action-typescript-template/actions/workflows/build-test.yml)
[![CodeQL Analysis](https://github.com/6thpath/action-typescript-template/actions/workflows/codeql-analysis.yml/badge.svg)](https://github.com/6thpath/action-typescript-template/actions/workflows/codeql-analysis.yml)

# Create a Github Action using TypeScript

Use this template to bootstrap the creation of a TypeScript action. :rocket:

This template includes compilation support, tests, a validation workflow, publishing, and versioning guidance.

If you are new, there's also a simpler introduction.  See the [Hello World JavaScript Action](https://github.com/actions/hello-world-javascript-action)

## Create an action from this template

Click the `Use this Template` and provide the new repo details for your action

## Development

### Requisite

- [NodeJS](https://nodejs.org/) version **16 or later**
- [Yarn Berry](https://yarnpkg.com/)

### Setup

- Install the dependencies

  ```bash
  yarn install
  ```

- Build the typescript and package it for distribution

  ```bash
  yarn package
  ```

- Run the tests :heavy_check_mark:

  ```bash
  $ yarn test

  PASS  tests/main.test.ts
  ✓ throws invalid number (3 ms)
  ✓ wait 500 ms (502 ms)
  ✓ test runs (622 ms)

  ...
  ```

### Change action.yml

The action.yml defines the inputs and output for your action.

Update the action.yml with your name, description, inputs and outputs for your action.

See the [documentation](https://help.github.com/en/articles/metadata-syntax-for-github-actions)

### Change the Code

Most toolkit and CI/CD operations involve async operations so the action is run in an async function.

```typescript
import * as core from '@actions/core';
...

async function run() {
  try {
    // ...
  } catch (error) {
    core.setFailed(error.message);
  }
}

run()
```

See the [toolkit documentation](https://github.com/actions/toolkit/blob/master/README.md#packages) for the various packages.

## Publish to a distribution branch

Actions are run from GitHub repos so we will checkin the packed dist folder.

Then run [ncc](https://github.com/vercel/ncc) and push the results:

```bash
yarn package
git add dist
git commit -a -m "prod dependencies"
git push origin releases/v1
```

Note: We recommend using the `--license` option for ncc, which will create a license file for all of the production node modules used in your project.

Your action is now published! :rocket:

See the [versioning documentation](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md)

### Validate

You can now validate the action by referencing `./` in a workflow in your repo (see [test.yml](.github/workflows/test.yml))

```yaml
uses: ./
with:
  milliseconds: 1000
```

See the [actions tab](https://github.com/6thpath/action-typescript-template/actions) for runs of this action! :rocket:

### Usage

After testing you can [create a v1 tag](https://github.com/actions/toolkit/blob/master/docs/action-versioning.md) to reference the stable and latest V1 action
