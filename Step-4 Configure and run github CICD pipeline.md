Create deploy.yaml file in manual action workflow and copy following github action pipeline.

Make changes in to your resource group and webapp name as per your resource created.

![]()

```
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

This will trigger your pipeline start deploying code to your fastapi server on azure 
![](https://github.com/smitwaman/fastapi-server/blob/main/PNG/Screenshot%202024-06-28%20170456.png)
on run with url you will find folowing output 
