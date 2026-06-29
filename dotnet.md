# .NET Guide

## Run App

### Steps to Run Application Locally

As the application would be deployed:

1. **Publish local package**
   - Go to publish folder
   - Open command prompt from the directory

2. **Set environment variables**
   ```powershell
   set ASPNETCORE_ENVIRONMENT=Development
   set IsDevelopmentMode=true
   ```

3. **Run the application**
   ```bash
   dotnet app.dll --urls http://localhost:3000
   ```

## Generate an Azure App Access Token Locally

Using the Azure CLI:

### Prerequisites

- In the app registration, ensure the Microsoft Azure CLI client ID is authorized:
  - Go to **Expose an API** → **Authorized client applications**
  - Add the Azure CLI client ID: `04b07795-8ddb-461a-bbee-02f9e1bf7b46`
  - Verify the required scopes are configured

### Steps

1. **Install the Azure CLI**
   - Download from [Azure CLI official site](https://learn.microsoft.com/en-us/cli/azure/)

2. **Open PowerShell or terminal**

3. **Sign in to Azure**
   ```powershell
   az login
   ```

4. **Create the access token**
   ```powershell
   az account get-access-token --scope "{API_SCOPE}" --query accessToken -o tsv
   ```
   
   > **Note:** Use the scope from your app registration under **Expose an API**
