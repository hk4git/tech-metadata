## Architechure Cloud

Azure FrontDoor (Global) -> Azure Application Gateways (Regional) / API Management Service

## AAD:
### Workload identity federation: 
You create a trust relationship between an external identity provider (IdP) and an app in Microsoft Entra ID by configuring a federated identity credential.

The user-assigned managed identity or app registration in Microsoft Entra ID becomes an identity for software workloads running, 
	for example, in on-premises Kubernetes or GitHub Actions workflows. 
Once that trust relationship is created, your external software workload exchanges trusted tokens from the external IdP for access tokens from Microsoft identity platform. 

Your software workload uses that access token to access the Microsoft Entra protected resources to which the workload has been granted access. 
	You eliminate the maintenance burden of manually managing credentials and eliminates the risk of leaking secrets or having certificates expire.

The federated identity credential creates a trust relationship between a user-assigned managed identity and an external identity provider (IdP).

https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-config-app-trust-managed-identity?tabs=microsoft-entra-admin-center

The combination of issuer and subject must be unique on the app.
issuer: is the URL of the Microsoft Entra tenant's Authority URL in the form https://login.microsoftonline.com/{tenant}/v2.0
subject: is the GUID of the Managed Identity's Object ID (Principal ID) assigned to the Azure workload.
audience: list the audiences that can appear in the external token (Required)

### Microsoft specific
MISE: MISE stands for Microsoft.Identity.ServiceEssentials which is a Microsoft internal nuget package provided by AAD team for token validation and acquisition, 
and we will use it to replace our custom code for token validation.  
Microsoft Identity Security Essentials [Microsoft.Identity.ServiceEssentials.AspNetCore][existing: Microsoft.Identity.Web]
 -> S2S for internal Microsoft services
 -> not fot user auth, can use MASL

Known issue:
-> MISE SDK dependencies can break existing apps due to .NET 8 packages being used in .NET 6​
-> MSAL still needed for on-behalf flows for users, or for getting tokens via federation with managed identity

"AzureAd": {​
  "Instance": "https://login.microsoftonline.com/",​
  "TenantId": "<tenant_id>",​
  "ClientId": "<client_id>",​
  "Audience": "api://<client_id>",​
},


## Azure App Service / Web API :

### Trouableshooting
###### How to return JSON data from api which is calling another api via httpclient or so?
Ans: return Content(res-data, response.Content.Headers.ContentType?.ToString() ?? "application/json");

###### Azure - App service – API not working – App getting stopped
In such conditions azure app is getting stopped due to some unhandled exception which are not logged since app is not running itself, to troubleshoot this **we can run app as console in Azure, which will give unhandled exceptions if any on console log**.


###### ENVIRONMENTS:
Production is the default value if DOTNET_ENVIRONMENT and ASPNETCORE_ENVIRONMENT have not been set. Apps deployed to Azure are Production by default.
In production, appsettings.Production.json configuration overwrites values found in appsettings.json. For example, when deploying the app to Azure.
To set the environment in an Azure App Service: provide Settings -> Environment variables, ASPNETCORE_ENVIRONMENT for the Name. For Value, provide the environment (for example, Staging)

## Azure Synapse: Pipilines & Connections
For M365 agent / Copilot: Data enngineering, filtering, can be done via synapse pipiline. Process data from main database, transform for AI to query etc.


