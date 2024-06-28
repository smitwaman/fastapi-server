

### Step 1: Create an Azure Web App

1. **Sign in to the Azure Portal**: Go to [portal.azure.com](https://portal.azure.com) and sign in with your Azure account.

2. **Navigate to "Create a Resource"**: In the left-hand menu, click on "Create a resource".

3. **Search for "Web App"**: In the search bar, type "Web App" and select the Web App option from the list.

4. **Click "Create"**: Click the "Create" button to start the Web App creation process.

### Step 2: Configure the Basics

1. **Subscription and Resource Group**:
   - Select your subscription.
   - Create a new resource group or select an existing one.
![webapp interface](https://github.com/smitwaman/fastapi-server/blob/main/PNG/Screenshot%202024-06-28%20143857.png)
2. **Instance Details**:
   - Name: Enter a globally unique name for your web app (e.g., `my-fastapi-app`).
   - Publish: Select "Code".
   - Runtime Stack: Select "Python 3.9".
   - Operating System: Select "Linux".
   - Region: Choose a region close to your users.

### Step 3: Configure the App Service Plan

1. **Click on "Create new" under App Service Plan**: This will open a new panel to create a new App Service Plan.
   - Name: Enter a name for your App Service Plan.
   - Pricing tier: Select a pricing tier (e.g., B1 Basic for development purposes).

2. **Click "OK"**: This will save your App Service Plan configuration.

### Step 4: Review and Create

1. **Review Configuration**: Check all the configurations you have set.
2. **Click "Create"**: Start the deployment process. This will take a few minutes.

### Step 5: Deploy Your FastAPI Application

1. **Navigate to Your Web App**: Once the deployment is complete, navigate to the resource by clicking on "Go to resource".

2. **Deployment Center**: In the left-hand menu, under "Deployment", click on "Deployment Center".

3. **Select Source**:
   - Choose "GitHub" as the source.
   - Authenticate with your GitHub account if not already authenticated.

4. **Configure Repository**:
   - Select the repository and branch where your FastAPI code is stored.

5. **Review and Finish**: Review the settings and click "Save". Azure will set up the CI/CD pipeline for you.

### Step 6: Configure Application Settings

1. **Application Settings**: Go to "Configuration" under "Settings" in the left-hand menu.
   - Add any necessary environment variables for your FastAPI app such as 

2. **Save Changes**: Click "Save" after adding the necessary settings.

### Step 7: Access Your FastAPI Application

1. **Browse Your Web App**: Click on the URL provided for your Web App (e.g., `https://my-fastapi-app.azurewebsites.net`).

2. **Check Deployment**: Ensure that your FastAPI application is running by navigating to the `/docs` endpoint to view the automatically generated API documentation (e.g., `https://my-fastapi-app.azurewebsites.net/docs`).


