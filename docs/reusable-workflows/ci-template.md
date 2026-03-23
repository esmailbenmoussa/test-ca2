# CI Template

This is a reusable workflow that runs linting. It can be called from other workflows using `workflow_call`.

## Trigger

This workflow uses `workflow_call`, which means it can only be triggered by another workflow.

## Jobs

| Job | Description |
|-----|-------------|
| `lint` | Runs linting checks on the codebase |

## Usage

Call this workflow from another workflow:

```yaml
jobs:
  ci:
    uses: ./.github/workflows/ci-template.yml
```

## Usage from external repository

```yaml
jobs:
  lint:
    uses: esmailbenmoussa/test-composite-actions/.github/workflows/ci-template.yml@main
```

## Workflow definition

```yaml
name: CI Template

on:
  workflow_call:

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Running linter..."
      - run: echo "Lint passed"
```

> **Source of** `.github/workflows/ci-template.yml@main`
