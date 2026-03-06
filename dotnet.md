### Run App
#### Steps to Run application locally as it wolud have been deployed 
- Publish local package, Go to publish folder, open cmd from dir
- Set env variables and development envs with commands like `set ASPNETCORE_ENVIRONMENT=Development`, `set IsDevelopmentMode=true`
- Run app command like `dotnet app.dll --urls http://localhost:3000`

### Tokens
#### Generate token locally using Azure CLI App
- Install Azure CLI
- Open powershell/Terminal 
- login to azure `az login`
- Create a token `az account get-access-token --scope "{API_SCOPE}" --query accessToken -o tsv`, {API_SCOPE} - E.g. From AAD App Reg - Expose an API 
