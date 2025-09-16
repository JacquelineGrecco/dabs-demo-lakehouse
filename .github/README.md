# Databricks Asset Bundle GitHub Actions Setup

This repository contains a GitHub Actions workflow for deploying Databricks Asset Bundle projects.

## Required Setup

### 1. GitHub Secrets

You need to configure the following secrets in your GitHub repository:

1. Go to your repository on GitHub
2. Navigate to Settings → Secrets and variables → Actions
3. Add the following repository secrets:

- `DATABRICKS_HOST`: Your Databricks workspace URL (e.g., `https://adb-1234567890123456.7.azuredatabricks.net`)
- `DATABRICKS_TOKEN`: A personal access token for your Databricks workspace

### 2. GitHub Environments

Create the following environments in your GitHub repository:

1. Go to Settings → Environments
2. Create two environments:
   - `development`
   - `production`

You can optionally add protection rules to these environments (e.g., require manual approval for production deployments).

### 3. Databricks Personal Access Token

To create a Databricks personal access token:

1. In your Databricks workspace, click on your user profile in the top right
2. Go to User Settings
3. Navigate to the "Access tokens" tab
4. Click "Generate new token"
5. Give it a name and set an expiration date
6. Copy the token and add it to your GitHub secrets

## Workflow Behavior

### Automatic Deployments

- **Pull Requests**: Deploys to the `dev` environment for testing
- **Push to main**: Deploys to both `dev` and `prod` environments (prod only after dev succeeds)

### Manual Deployments

You can manually trigger deployments from the Actions tab:

1. Go to the "Actions" tab in your GitHub repository
2. Select "Deploy Databricks Asset Bundle" workflow
3. Click "Run workflow"
4. Choose the target environment (dev or prod)

## Bundle Configuration

The workflow expects your Databricks Asset Bundle to be configured with:

- A `databricks.yml` file in the root directory
- Target configurations for `dev` and `prod` environments
- Resource definitions in the `resources/` directory

## Troubleshooting

### Common Issues

1. **Authentication failures**: Verify your `DATABRICKS_HOST` and `DATABRICKS_TOKEN` secrets are correctly set
2. **Bundle validation errors**: Check your `databricks.yml` and resource files for syntax errors
3. **Permission errors**: Ensure your Databricks token has the necessary permissions for the workspace

### Debugging

To debug deployment issues:

1. Check the Actions logs for detailed error messages
2. Run `databricks bundle validate` locally to test your configuration
3. Test deployments manually using the Databricks CLI before pushing to GitHub
