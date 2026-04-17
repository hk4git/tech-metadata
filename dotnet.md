### Run App
#### Steps to Run application locally as it wolud have been deployed 
- Publish local package, Go to publish folder, open cmd from dir
- Set env variables and development envs with commands like `set ASPNETCORE_ENVIRONMENT=Development`, `set IsDevelopmentMode=true`
- Run app command like `dotnet app.dll --urls http://localhost:3000`

#### Generate an Azure app access token locally using the Azure CLI
- Prerequisite: In the app registration (Expose an API → Authorized client applications), ensure the Microsoft Azure CLI client ID `04b07795-8ddb-461a-bbee-02f9e1bf7b46` is listed and the required scopes are configured.
- Install the Azure CLI.
- Open PowerShell or a terminal.
- Sign in to Azure: `az login`
- Create the token: `az account get-access-token --scope "{API_SCOPE}" --query accessToken -o tsv` (use the scope from the app registration: Expose an API).
