# Office 1
## Office 2
### Office 3
#### Office Complementary tools
Script Lab: Office Task Pane Add-in for Word, Excel, & PowerPoint
- Used to verify & test functionality of custom Add-in scripts
- Avoids having to create the plumbing for the add-in (manifest, web app)
#### Microsoft Outlook JS API capabilities
- Task pane
   - Read & compose messages (emails)
   - Read & compose meetings (everits)
     - Read = meeting attendee
     - Compose = meeting organizer
- Contextual
  - Auto activate based on text within a message
  - Match against well-known entity, or regular expression
- Module
  - Appear in Outlook's navigation bar
 

#### Outlook Add-ins & authentication
- Common need to authenticate in Add-ins to access Microsoft & non- Microsoft services
- Exchange user identity token
  - `getUserIdentityTokenAsync()` Scenarios: Exchange on-prem / access non-Microsoft service you control
- Access token obtained via OAuth2 flow
  - `displayDialogAsync()` Scenarios: access to third-party service that supports OAuth2
- Callback token (as per permissions in manifest)
  - `getCallbackTokenAsync()` Scenarios: access user's mailbox from your server via EWS/Outlook REST
- SSO
##### Office 5
###### Office 6
