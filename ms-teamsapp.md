## TeamsApp: Capabilities: {Tabs, Bots, Connectors, Messaging Extensions} 
Materials: https://www.youtube.com/watch?v=kruUnaZgQaY

###### SSO: get auth token:
- Teams App **client side code / client/user token**: is generic token which has very basic info of user & **can't be used to call graph/backend-api/service etc.**
- Team app **server side / access token**: do token exchange, exchange client side token to get server side token **to call downestream services.**

  Exchange the Teams SSO access token for an API token using the **on-behalf-of flow**:
  The getAuthToken() is valid only for consenting to a limited set of user-level APIs, such as email, profile, offline_access, and OpenId.
  It isn't used for other Graph scopes such as User.Read or Mail.Read.
  Tabs are Teams-aware web pages. To enable SSO in a webpage hosted inside a tab app, add Teams JavaScript client library and call microsoftTeams.initialize(). After initialization, call microsoftTeams.getAuthToken() to get the access token for your app.
  Use server-side code for Microsoft Graph calls: Always use the server-side code to make Microsoft Graph calls, or other calls that require passing an access token. Never return the OBO token to the client to enable the client to make direct calls to Microsoft Graph. This helps protect the token from being intercepted or leaked.
  You need to acquire an access token for Microsoft Graph. You can do so by using Microsoft Entra on-behalf-of (OBO) flow.
  The current implementation for single sign-on (SSO) is limited to user-level permissions, which aren't usable for making Graph calls. To get the permissions and scopes needed to make a Graph call, SSO apps must implement a custom web service to exchange the token received from the Teams JavaScript library for a token that includes the needed scopes. You can use Microsoft Authentication Library (MSAL) for fetching the token from the client side.
  Access token: OBO flow {server side}

###### Tabs: {Teams Tab, Personal Tab(Static Tabs)}
Personal Tab
-> can Add eixsting static web app, just create teams manifaste file. WebSite: provide web app URL
AAD ID MUST BE IN FORMAT: api://${{TAB_DOMAIN}}/${{AAD_APP_CLIENT_ID}} TO RESOLVE BELOW ERRORS:
-> Enter your app's subdomain URI and the application ID URI that you created in Microsoft Entra ID when creating scope. You can copy it from the Microsoft Entra ID > Expose an API section.
-> Configure your app's subdomain URI in resource to ensure that the authentication request using getAuthToken() is from the domain given in app manifest.

"webApplicationInfo": 
{
"id": "{Azure AD AppId}",
"resource": "api://subdomain.example.com/botid-{Azure AD AppId}"
}

app’s identifier URL (the “resource” in your manifest) and the domain of the page loaded in the Teams tab (the “iframe origin”)
I was able to fix the issue by changing the Application URI to this format: api://FQDN/{AppID}. I also changed the webApplicationInfo.resource to match the Application URI

Note: Teams App: Application ID URI: Maximum length is 100
AAD App registration: Application ID URI: Less than 120 characters in length

Reference:
https://learn.microsoft.com/en-us/microsoftteams/platform/bots/how-to/authentication/bot-sso-manifest

###### DEPLYOMENT:
- IF DEPLYOMENT FAILS FROM VS CODE
  ->Azure portal -> Environment variables ->  `SET WEBSITE_RUN_FROM_PACKAGE = 1`

FOR LINUX ENV: Settings -> General Settings -> Startup Command, add following
`pm2 serve /home/site/wwwroot/ --no-daemon --spa`

ENV VARIABLES ISSUE:
Azure Static Web Apps App Settings represent runtime variables, accessible by the managed functions backends. Build time variables, such as the ones you are referring to, must be set in your build pipeline such as your GitHub Action
