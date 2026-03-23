# Deploy

This composite action performs a deployment to the specified environment and returns deployment information.

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `environment` | Target environment (dev, staging, prod) | Yes | `dev` |

## Outputs

| Output | Description |
|--------|-------------|
| `deploy-url` | The deployment URL |
| `status` | Deployment status |
| `timestamp` | Deployment timestamp (ISO 8601 format) |

## Usage

```yaml
- name: Deploy to environment
  id: deploy
  uses: ./.github/actions/deploy
  with:
    environment: dev

- name: Show deployment info
  run: |
    echo "Deployed to: ${{ steps.deploy.outputs.deploy-url }}"
    echo "Status: ${{ steps.deploy.outputs.status }}"
    echo "Timestamp: ${{ steps.deploy.outputs.timestamp }}"
```

## Deploy to production

```yaml
- name: Deploy to production
  uses: ./.github/actions/deploy
  with:
    environment: prod
```

> **Source of** `.github/actions/deploy/action.yml@main`
