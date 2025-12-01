## Introduction

Node runtime CI checks.

## Usage

```yaml
name: CI Checks

on: [push, pull_request]

jobs:
  format:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./.github/actions/node-checks
        with:
          check-type: format

  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./.github/actions/node-checks
        with:
          check-type: lint

  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./.github/actions/node-checks
        with:
          check-type: test

  types:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: ./.github/actions/node-checks
        with:
          check-type: types
```

## Inputs

| Name | Description | Default | Required |
|------|-------------|---------|----------|
`check-type`  |  Type of check to run.  |  Options: `format`, `lint`, `test`, `types`  |  Yes  |  N/A

## Check Types

### format

Runs Prettier formatting check.

- **Command**: `npm run format:check`
- **Expected script**: `"format:check": "prettier --check ."`

### lint

Runs ESLint linting.

- **Command**: `npm run lint`
- **Expected script**: `"lint": "eslint ."`

### test

Runs unit tests.

- **Command**: `npm run test`
- **Expected script**: `"test": "vitest run"` (or your test runner)

### types

Runs TypeScript/Svelte type checking.

- **Command**: `npm run check`
- **Expected script**: `"check": "svelte-kit sync && svelte-check --tsconfig ./tsconfig.json"` (or `tsc --noEmit` for non-Svelte projects)
