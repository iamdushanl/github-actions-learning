# Secrets and Environment Variables

## Environment Variables

Environment variables store configuration data as key-value pairs.

### Scope Levels

#### 1. Runner/Global Level
Available to all steps:

```yaml
env:
  DEPLOY_ENV: production
  LOG_LEVEL: debug

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo $DEPLOY_ENV
```

#### 2. Job Level
Available to all steps in a job:

```yaml
jobs:
  deploy:
    env:
      NODE_ENV: production
    runs-on: ubuntu-latest
    steps:
      - run: echo $NODE_ENV
```

#### 3. Step Level
Available only to that step:

```yaml
steps:
  - run: npm build
    env:
      NODE_ENV: production
```

### Using Environment Variables

```yaml
- run: echo "Environment: ${{ env.NODE_ENV }}"
```

## Secrets

**Secrets** are encrypted environment variables. Use them for sensitive data like API keys, tokens, and credentials.

### Why Use Secrets?

- 🔐 Encrypted at rest
- 🙈 Not displayed in logs
- 🛡️ Only available in actions/workflows
- 🔑 Can't be accessed by forks (by default)

### Creating Secrets

#### Via GitHub UI

1. Go to your repository
2. Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Add name and value
5. Click "Add secret"

#### Via GitHub CLI

```bash
gh secret set DEPLOYMENT_TOKEN --body "your-token-here"
```

### Using Secrets in Workflows

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy with token
        run: curl -H "Authorization: Bearer ${{ secrets.DEPLOYMENT_TOKEN }}" https://api.example.com/deploy
```

### Common Secrets

```yaml
steps:
  - run: echo "Using secrets..."

  - name: GitHub Token
    run: echo ${{ secrets.GITHUB_TOKEN }}

  - name: Custom Secret
    run: echo ${{ secrets.MY_API_KEY }}

  - name: Azure Credentials
    run: echo ${{ secrets.AZURE_CREDENTIALS }}
```

## GitHub Token

GitHub automatically provides a `GITHUB_TOKEN` secret for each workflow run.

### Permissions

```yaml
jobs:
  my-job:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - run: gh pr comment -B "Review completed"
```

### Using GitHub Token

```yaml
- uses: actions/checkout@v3
  with:
    token: ${{ secrets.GITHUB_TOKEN }}

- name: Create issue
  run: |
    gh issue create \
      --title "Bug report" \
      --body "Found a bug" \
      --repo owner/repo
```

## Encrypted Secrets Best Practices

✅ Use **unique secrets** for different purposes  
✅ **Rotate secrets** regularly  
✅ Use **least privilege** (only needed permissions)  
✅ **Never log secrets** to output  
✅ Use **environment-specific secrets**  
✅ Document **where secrets are used**  

## Preventing Secret Leaks

### Masking Secrets

GitHub automatically masks secrets in logs, but you can manually mask:

```yaml
steps:
  - run: |
      echo "::add-mask::password123"
      echo "My password is password123"
    # Output: My password is ***
```

### Don't Debug with Secrets

```yaml
# ❌ Bad - might leak secret
- run: |
    echo "Token: ${{ secrets.API_TOKEN }}"
    npm deploy

# ✅ Good - secret is hidden
- run: |
    npm deploy --token "${{ secrets.API_TOKEN }}"
```

## Environment Variables vs Secrets

| Use Case | Variable | Secret |
|----------|----------|--------|
| **Public URLs** | ✅ | ❌ |
| **API Keys** | ❌ | ✅ |
| **Configuration** | ✅ | ❌ |
| **Tokens** | ❌ | ✅ |
| **Database URLs** | ❌ | ✅ |
| **Version Numbers** | ✅ | ❌ |

## Organization-Level Secrets

For enterprise, set secrets at organization level:

1. Go to Organization Settings
2. Secrets and variables → Actions
3. Add organization secrets
4. Grant repository access

Usage is the same:

```yaml
run: echo ${{ secrets.ORG_SECRET }}
```

## Environments

Different environments need different secrets:

```yaml
jobs:
  deploy-staging:
    environment: staging
    runs-on: ubuntu-latest
    steps:
      - run: echo ${{ secrets.STAGING_TOKEN }}

  deploy-prod:
    environment: production
    needs: deploy-staging
    runs-on: ubuntu-latest
    steps:
      - run: echo ${{ secrets.PROD_TOKEN }}
```

## Real-World Example

```yaml
name: Deploy Application

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production
    permissions:
      contents: read
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Login to Azure
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}
      
      - name: Deploy to App Service
        uses: azure/webapps-deploy@v2
        with:
          app-name: my-app
          publish-profile: ${{ secrets.AZURE_PUBLISH_PROFILE }}
      
      - name: Notify Slack
        run: |
          curl -X POST ${{ secrets.SLACK_WEBHOOK_URL }} \
            -H 'Content-Type: application/json' \
            -d '{"text":"Deployment completed"}'
```

## Azure-Specific Secrets

For Azure deployments, you'll typically need:

```yaml
secrets:
  AZURE_CREDENTIALS: |
    {
      "clientId": "...",
      "clientSecret": "...",
      "subscriptionId": "...",
      "tenantId": "..."
    }
  AZURE_APP_SERVICE_NAME: my-app
  AZURE_RESOURCE_GROUP: my-rg
```

## Security Checklist

- [ ] Never hardcode secrets in workflows
- [ ] Use GitHub Secrets for sensitive data
- [ ] Rotate secrets regularly
- [ ] Use environment-specific secrets
- [ ] Review secret access permissions
- [ ] Audit secret usage in logs
- [ ] Use branch protection with secret rotation

## Next Steps

- [Build and Test](06-build-and-test.md) - Practical CI examples
- [Deploy to Azure](07-deploy-to-azure.md) - Secure deployments
- [GitHub Actions Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

---

**Your workflows are now secure! Let's move to building and testing applications.**
