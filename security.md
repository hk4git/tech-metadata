# Security 1
## Security 2
### Security 3
#### Security 4
##### Security 5
###### Security 6

# Authentication and Authorization
## ABC-MS Tenant : Entra ID
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

## Custom Engine Agents (created by M365 Agents SDK) configurations

### Entra ID SSO authentication configurations
Refer - [Implement Authentication with Federated Identity Credentials - Bot Service | Microsoft Learn](https://learn.microsoft.com/en-us/azure/bot-service/bot-builder-authentication-federated-credential?view=azure-bot-service-4.0&tabs=csharp)

#### 1) Entra app changes - For **Teams SSO** open the existing App Registration for the Agent/Azure Bot.
- Open [Microsoft Entra admin center](https://entra.microsoft.com/). 
- On the **Authentication** pane if you don't see a **Web** platform, selct **+ Add a platform**.
    - Select **Web**
    - Enter the **Redirect URI** as 
     ```
     https://token.botframework.com/.auth/web/redirect
     https://teams.microsoft.com/api/platform/v1.0/oAuthConsentRedirect
     https://teams.microsoft.com/api/platform/v1.0/oAuthRedirect

     ```
    - Click **Save**
- In the navigation pane, select **Certificates & secrets** to add credentials for your application.
  - Under **Federated Credentials**, select **Add Credentials**.
    - Choose the **Federated credential scenario** to **Other Issuer**
    - **Issuer** : `https://login.microsoftonline.com/{tenant ID}/v2.0`
    - **Type**: select **Explicit subject identifier**
    - **Value**: Should be in format - `/eid1/c/pub/t/{base64 encoded customer tenant ID}/a/{base64 encoded first-party app client ID}/{unique-identifier-for-projected-identity}`  
     - **Name**: Name of your choice, eg. "agent-sso-oauth"
     - **Description**: Description of your choice
     - Audience: `api://AzureADTokenExchange`
- Add/Update **API permissions**
  - Click on **+ Add a permission**
  - **Select an API**: select **APIs my organization uses**
    - Search AAD APP Name / Client Id
  - Select **Delegated permissions**
    - Select **access_as_user** [Select for which Admin consent is not required]
  - Click **Add Permission**
- Update Manifest, Click **Manifest** in the left rail
  - Add/Update **identifierUris** array, Add Bot App API URI, This format is REQUIRED `api://botid-{appid}`
  - Click on **Save**  

#### 2) Azure Bot Services Configuration
##### OAuth Configuration: default-sso
Click on **Add OAuth Connection Settings**
- **Name:** Provide exactly as `default-sso`
- **Service Provider:** select **AAD v2 with Federated Credentials**
- **Client ID:** `{AAD Client Id}`
- **Unique Subject Identifier:** From Entra Id App Reg -> Certificates & secrets -> `Subject identifier or claims matching expression`
- **Token Exchange URL:** Format `api://botid-{appid}`
- **Login URL:** 
- **Tenant ID:** `{tenant ID}`
- **Scopes:** `api://{AAD Client Id}/access_as_user`

## Declarative Agent - Microsoft Entra ID SSO authentication
Refer - [Configure Authentication for API plugins in Agents in Microsoft 365 Copilot | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/api-plugin-authentication)

### 1) Entra app registration
- Open [Microsoft Entra admin center](https://entra.microsoft.com/). 
- Create **+ New Registration** from **App registrations**
- Provide appropriate **Name**
- Provide appropriate **Service Tree ID**
- Click on **Register** button. Note value of  `Application (client) ID`

### 2) Register an SSO client in Teams developer portal
1.  Open [Teams developer portal](https://dev.teams.microsoft.com/tools). Select **Tools** -> **Microsoft Entra SSO client ID registration**. 
2.  If you have no existing registrations, select **Register client ID**. If you have existing registrations, select **New client registration**.
3.  Fill in the following fields.
    *   **Registration name**: A friendly name for your registration. E.g. `agent-sso`
    *   **Base URL**: Your API's base URL. This value should correspond to an entry in your OpenAPI document. E.g. `https://devtunnel:port/api`
    *   **Restrict usage by org**: Select which Microsoft 365 organization has access to your app to access API endpoints. Select: `Any Microsoft 365 organization`
    *   **Restrict usage by app**: Select `Any Teams app` if you don’t know your final app ID. After you publish your app, bind this registration with your published app ID.
    *   **Client ID**: The client ID of the app registered in Microsoft Entra. Use `Application (client) ID` value from Step 1
4.  Select **Save**.
5.  Completing the registration generates a **Microsoft Entra SSO registration ID** and an **Application ID URI**.

### 3) Update the Entra app registration
1) Open [Microsoft Entra admin center](https://entra.microsoft.com/). 
2)  Select **Authentication** under **Manage** go to the **Redirect URIs** in the **Web** platform.
  - Add `https://teams.microsoft.com/api/platform/v1.0/oAuthConsentRedirect`
2) Select **Certificates & secrets** add **Federated credentials**
   - **Click + Add a Credential**, select appropriate option of User Managed Identity.  
3)  Select **Expose an API** under **Manage**. Click **+ Add a Scope** add appropriate scope like `access_as_user` Select **Add a client application** and add the client ID of Microsoft's enterprise token store. 

```
ab3be6b7-f5df-413d-ac2d-abf1e3fd9c0b
5e3ce6c0-2b1f-4285-8d4b-75ee78787346
1fec8e78-bce4-4aaf-ab1b-5451cc387264
```

4) Update **Manifest** The Entra app registration that secures your API with the **Application ID URI** generated by the Teams developer portal. If you have an existing application ID URI mapped to the app registration, you can use the manifest editor to add another URI in the **identifierUris** section.
```
"identifierUris": [
  "<<URI1>>"
  "<<URI2>>"
]
```

## M365 Declarative Agent - Configurations setup Steps - to run locally

### Install Tools and Extensions 
 - Install **Microsoft 365 Agents Toolkit** in VS code extension
 - Install **Microsoft dev tunnel**

### Follow below steps
1. Create Teams App from [Developer Portal](https://dev.teams.microsoft.com/home) Note `App ID`
2. SSO Configuration: Refer - [Configure Authentication for API plugins in Agents in Microsoft 365 Copilot | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365-copilot/extensibility/api-plugin-authentication)
Settings:
- **Client ID**: use existing app id `{App / client Id}`
- **Which app (client) is this registration for?** select- `Any Teams app (for testing and store validation only)`
- **Update the Microsoft Entra app registration** - use existing local application app id `{App / client Id}` and just configure "**identifierUris**"
Note `Registration ID`, `Application ID URI`
3. From repository, open solution "**src\app.sln**" .net solution and run it. Note the `URL:PORT`
4. Open powershell and run command "**devtunnel host -p {PORT} --protocol https/http --allow-anonymous**" This will provide URL click on URL and select approve and Copy this `DevTunnelURL`  
You may need to sign-in to devtunnel using command `devtunnel login` first
5. From repository, open solution "**m365-agent**" folder independently in VS Code to enable **Microsoft 365 Agents Toolkit** settings. 
- Open "**.env.dev**" file & do following env file updates:
    - **TEAMS_APP_ID**: update value of `App ID` from step 1
    - **API_BASE_URL**: update value of `DevTunnelURL` from step 4
    - **TEAMS_APP_REFERENCE_ID**: update value of `Registration ID` from step 2
6. For Solution open in VS Code, from Left Panel click on **Microsoft 365 Agents Toolkit**, Provision, select "dev", this will raise few popup for sign-in, sign-in with your account for all popups, then it should successfully run and click build package like "agent-dev.zip".
7. Install "agent-dev.zip" package
 - Open your MS Teams
 - Click on **+Apps** from left panel
 - Click on **Manager your apps**
 - Click on **Upload an app**, select **Upload a custom app**, select above zip package created.
 - Click an open with Copilot & it should look something like below:
8. Ask agent a question and it should hit your local app api (solution that run in step 3)
 
