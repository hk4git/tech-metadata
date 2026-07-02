# Security 1
## Security 2
### Security 3
#### Security 4
##### Security 5
###### Security 6

## ABC-MS Tenant
In ABC-MS tenant new Entra App registrations can be created with:  
 - Branding & properties: `Service management reference` is required.
 - Authentication: Used sample web Redirect URIs
   - For Bot: `https://teams.microsoft.com/api/platform/v1.0/oAuthRedirect`
   - For Bot: `https://token.botframework.com/.auth/web/redirect`
   - For Bot: `https://teams.microsoft.com/api/platform/v1.0/oAuthConsentRedirect`
 - Certificates & secrets: No `Certificates` or `client secrets` allowed, only `Federated credentials` allowed & used with Managed Identity
 - API permissions: For Graph only `User.Read` is allowed
 - Expose an API:
   - Application ID URI: ideally use as `api://{Application (client) ID}/`
   - Used scope as `api://{Application (client) ID}/access_as_user` consent Admin and Users
   - Authorized client applications: Used applications such as
     - Microsoft Teams: `1fec8e78-bce4-4aaf-ab1b-5451cc387264`
     - Microsoft Teams Web Client: `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`
     - Office web: `4765445b-32c6-49b0-83e6-1d93765276ca`
     - Microsoft Teams Graph Service: `ab3be6b7-f5df-413d-ac2d-abf1e3fd9c0b` - M365 Copilot?
     - Visual Studio (Enterprise Application): `04f0c124-f2bc-4f59-8241-bf6df9866bbd`
     - Microsoft Azure CLI: `04b07795-8ddb-461a-bbee-02f9e1bf7b46` - with this we can create token locally using az cli command lines
     - Visual Studio Code: `aebc6443-996d-45c2-90f0-388ff96faa56`
     - Custom Apps: `{Custom Application (client) ID}`
 - App roles: used to authorized only certain group of users to allow to access the application.
 - Manifest: Can manually edit to add multiple `identifierUris` since UI allows only one, but from this manifest file you can add multiple `Application ID URI` and use it
