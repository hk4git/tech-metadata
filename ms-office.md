# Microsoft Learn - Office Add-ins 
- https://learn.microsoft.com/en-us/office/dev/add-ins/

**Extend Office functionality**
You can add new functionality to Office applications through the following features:
- Custom ribbon buttons and menu commands (collectively called "**add-in commands**").
- Insertable **task panes** with a webview control that can do almost anything a webpage can do inside a browser.
- **Event handlers** that respond to events in the Office document or Office application.  
Custom UI, task panes, and event handlers are specified in the add-in manifest.

#### Extend Outlook functionality
Users can run Outlook add-ins when they view, reply, or create emails, meeting requests, meeting responses, meeting cancellations, or appointments. Outlook add-ins can do the following tasks:
- Extend the Office app ribbon.
- Display contextually next to an Outlook item when you're viewing or composing it.
- Perform a task when a specific event occurs, such as when a user creates a new message.  
Note: Add-ins that interact with the user's calendar, meetings, or appointments are available only if the user opens the calendar in Outlook, not Teams. However, you can create a Teams meeting app and surface it in Outlook. For more information, see Extend a Teams meeting app to Outlook.
- https://github.com/OfficeDev/Office-Add-in-samples/tree/main/Samples/hello-world/outlook-hello-world

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
Azure AAD do not allow token popup from/inside iframe, since Takspan content is iframe you can not directly use it, So essentially you can use office.js - Dialog opetion and then call Azure ADD token which would work.  
- Common need to authenticate in Add-ins to access Microsoft & non- Microsoft services
- Exchange user identity token
  - `getUserIdentityTokenAsync()` Scenarios: Exchange on-prem / access non-Microsoft service you control
- Access token obtained via OAuth2 flow
  - `displayDialogAsync()` Scenarios: access to third-party service that supports OAuth2
- Callback token (as per permissions in manifest)
  - `getCallbackTokenAsync()` Scenarios: access user's mailbox from your server via EWS/Outlook REST
- SSO


#### Persist state & settings in Office Add-ins
- Office JS includes multiple options for persisting the state & settings, Depends on the Office application you target & the type of Add-in
   - All add-ins
      - Use HTML web storage (local storage)
      - Cookies
   - Content
      - Settings: stored with document, workbook, or spreadsheet (Applies to: Word, Excel, PowerPoint)
   - Task pane
      - Settings: stored with document, workbook, or spreadsheet (CustomXmlParts: stored as XML as part of the document)
   - Mail app
      - Custom properties: stored on a message/appointment (Roaming settings: stored on user's Exchange mailbox)

#### Leverage Microsoft Graph in Office Add-ins


##### Office 5
###### Office 6
