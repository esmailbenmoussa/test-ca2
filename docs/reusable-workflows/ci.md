# CI

This workflow runs the full CI/CD pipeline including build, test, lint, and deploy stages.

## Triggers

| Trigger | Description |
|---------|-------------|
| `push` | Runs on push to `main` branch |
| `workflow_dispatch` | Manual trigger with environment selection |

## Manual Trigger Inputs

| Input | Description | Options | Default |
|-------|-------------|---------|---------|
| `environment` | Target environment | dev, staging, prod | `dev` |

## Jobs

The workflow consists of 4 sequential jobs:

```
build → test → ci (lint) → cd (deploy)
```

| Job | Description | Dependencies |
|-----|-------------|--------------|
| `build` | Builds the project | None |
| `test` | Runs tests | `build` |
| `ci` | Runs linting via reusable workflow | `test` |
| `cd` | Deploys using composite action | `ci` |

## Usage

### Automatic (on push)

```yaml
on:
  push:
    branches: [main]
```

### Manual dispatch

Trigger manually from the GitHub Actions UI with environment selection.

## Workflow structure

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: echo "Building..."

  test:
    needs: build
    # ...

  ci:
    needs: test
    uses: ./.github/workflows/ci-template.yml

  cd:
    needs: ci
    steps:
      - uses: ./.github/actions/deploy
        with:
          environment: ${{ inputs.environment || 'dev' }}
```

> **Source of** `.github/workflows/ci.yml@main`
