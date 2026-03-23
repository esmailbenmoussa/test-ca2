# Test Composite Actions

This repository contains reusable GitHub Actions components for CI/CD pipelines.

## Overview

This project demonstrates how to create and use:

- **Composite Actions** - Reusable action steps that can be shared across workflows
- **Reusable Workflows** - Complete workflow templates that can be called from other workflows

## Repository Structure

```
.github/
├── actions/
│   └── deploy/              # Composite action for deployments
│       └── action.yml
└── workflows/
    ├── ci.yml               # Main CI workflow
    ├── ci-template.yml      # Reusable workflow template
    └── deploy-docs.yml      # Documentation deployment
```

## Quick Start

### Using the Deploy Action

```yaml
- name: Deploy
  uses: ./.github/actions/deploy
  with:
    environment: dev
```

### Calling the CI Template Workflow

```yaml
jobs:
  ci:
    uses: ./.github/workflows/ci-template.yml
```

## Components

| Component | Type | Description |
|-----------|------|-------------|
| [Deploy](composite-actions/deploy.md) | Composite Action | Deploys to target environment |
| [CI](reusable-workflows/ci.md) | Workflow | Full CI pipeline with build, test, lint, deploy |
| [CI Template](reusable-workflows/ci-template.md) | Reusable Workflow | Lint job that can be called by other workflows |
