# fastapi-server
Demo Server

In this demo we are deploying fasyapi server
For deploying "Hello world" on it using Github CICD pipeline.

Step to achieve this target

first prepare all creadential ready for authenticating azure with github actions with following steps:

To set up GitHub Actions to log in to Azure using OpenID Connect (OIDC), you need to follow these steps:

1. **Create a Service Principal with Federated Credentials**: Configure Azure AD to allow GitHub Actions to authenticate using OIDC.
2. **Configure GitHub Secrets**: Store necessary Azure credentials securely.
3. **Create a GitHub Actions Workflow**: Use the `azure/login` action to authenticate and deploy your resources.

### Step 1: Create a Service Principal with Federated Credentials

1. **Register an Application in Azure AD**:
   - Go to the Azure Portal.
   - Navigate to **Azure Active Directory** > **App registrations** > **New registration**.
   - Give your application a name and register it.

2. **Create a Federated Credential**:
   - Navigate to your application.
   - Go to **Certificates & secrets** > **Federated credentials**.
   - Click on **Add credential** and select **GitHub Actions**.
   - Fill in the required details:
     - **Issuer**: `https://token.actions.githubusercontent.com`
     - **Subject Identifier**: `repo:<your-organization>/<your-repository>:ref:refs/heads/<your-branch>`
     - **Audience**: `api://AzureADTokenExchange`
   - Click **Add**.

3. **Assign Roles to the Service Principal**:
   - Navigate to your application.
   - Go to **API permissions** > **Add a permission** > **Azure Management API** > **User.Read**.
   - Grant admin consent for your organization.
   - Assign the `Contributor` role to your service principal:
     ```bash
     az role assignment create --assignee <app-client-id> --role Contributor --scope /subscriptions/<your-subscription-id>
     ```

### Step 2: Configure GitHub Secrets

1. **Store Azure Credentials in GitHub Secrets**:
   - Go to your GitHub repository.
   - Navigate to **Settings** > **Secrets and variables** > **Actions**.
   - Add the following secrets:
     - **AZURE_CLIENT_ID**: The client ID of your Azure AD application.
     - **AZURE_TENANT_ID**: The tenant ID of your Azure AD.
     - **AZURE_SUBSCRIPTION_ID**: Your Azure subscription ID.

### Step 3: Create a GitHub Actions Workflow

1. **Create a Workflow File**:
   - Create a new file in your repository at `.github/workflows/deploy.yml`.

2. **Configure the Workflow**:

```yaml
name: Deploy to Azure

on:
  push:
    branches:
      - main

permissions:
  id-token: write
  contents: read

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'

    - name: Login to Azure using OIDC
      uses: azure/login@v1
      with:
        client-id: ${{ secrets.AZURE_CLIENT_ID }}
        tenant-id: ${{ secrets.AZURE_TENANT_ID }}
        subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
        allow-no-subscriptions: true

    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: 'your-web-app-name'
        package: .
        runtime-stack: 'PYTHON|3.9'

    - name: Restart Azure Web App
      run: az webapp restart --name your-web-app-name --resource-group your-resource-group
```

### Summary

1. **Create a Service Principal**: Register an app in Azure AD and configure federated credentials for OIDC.
2. **Configure GitHub Secrets**: Store the necessary Azure credentials in GitHub Secrets.
3. **Create a Workflow**: Set up a GitHub Actions workflow to log in to Azure and deploy your application.

By following these steps, you can set up a secure and automated CI/CD pipeline to deploy your application to Azure from GitHub Actions.
