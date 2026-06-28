# Graph 1
## Graph 2
### Graph 3
#### Graph 4
Resources  
- https://learn.microsoft.com/en-us/graph/sdks/sdks-overview
- https://github.com/microsoftgraph/msgraph-sdk-powershell  
- Retired
  - https://learn.microsoft.com/en-us/graph/toolkit/overview?tabs=html
  - https://mgt.dev/?path=/docs/overview--docs 

#### REST API - CRUD Operations
GET - query data. What you query for is specified as the url path + query string parameters `https://graph.microsoft.com/v1.0/{resource}?[query parameters]` E.g.
 - `https://graph.microsoft.com/v1.0/users/{userId}`
 - `https://graph.microsoft.com/v1.0/users('{userId}')`
 - `https://graph.microsoft.com/v1.0/users('{userId}')/displayName`
 - `https://graph.microsoft.com/v1.0/users('{userId}')/displayName/$value`

**POST - Create a new entity. Body payload must at least contain all mandatory attributes**  
HTTP Status Code 201 - Created. Response is JSON of new entity

**PATCH - update entity data. Body payload need only to contains attributes to be updated**  
HTTP Status Code 204 - No Content

**PUT - overwrite entity data. Body payload must at least contain all mandatory attributes**  
Not allowed for all targets, like users

#### Metadata
- What resources can I query data for?  
  - Read the docs https://docs.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0
  - Get All Entities supported by Graph: https://graph.microsoft.com/v1.0/ returns a JSON structure of all resources  
- What data does a resource expose?  
  - https://graph.microsoft.com/v1.0/$metadata returns XML metadata about `Entities, Complex types, Enumerations`  
- Functions and Actions - `https://graph.microsoft.com/v1.0/me/sendMail`

#### REST API - Querying
Direct Query when you know the id
 - https://graph.microsoft.com/v1.0/users/{userId}
   
Return specific attributes  $select
 - https://graph.microsoft.com/v1.0/me?$select=id,identities,passwordPolicies,passwordProfile

Filter what entities you want to return - $filter
 - https://graph.microsoft.com/v1.0/users?$filter=displayName eq 'Basil Fawlty'
 - https://graph.microsoft.com/beta/users?$filter=otherMails/any(x:x eq 'basil@fawltytowers2.com')

Paging - for large datasets or parallel processing
 - First query, add $top=5 as a query string parameter. Thereafter, use @odata.nextlink to query for next set of entities

Batching - post a payload with multiple requests to be executed on the server
 - https://graph.microsoft.com/v1.0/$batch
 - `{ "requests": [ {"id": "1", "method": "GET", "url": "/me" }, { "id": "2", "method": "GET", "url": "/me/photo/$value"} ]]}`

#### Change notficiations (webhooks) | track changes (delta queries)
- Subscribe to notifications
- Subscription expiration (Maximum subscription length is 3 days for most resources.)

- Example: User updates
```
POST https://graph.microsoft.com/v1.0/subscriptions HTTP/1.1
Authorization: bearer toekn
Content-Type: application/json; charset=utf-8
Host: graph.microsoft.com
Content-Length: 199
{
  "changeType": "updated",
  "clientState": "SecretClientState",
  "notificationUrl": "https://1a3f84c2.ngrok.io/api/notifications",
  "resource": "/users",
  "expirationDateTime": "2019-03-11T04:30:28.2257768+00:00"
}
```
- Renew subscriptions
```
PATCH https://graph.microsoft.com/v1.0/subscriptions/47e861c4-2db2-
455a-8774-57658ba185a1 HTTP/1.1
Authorization: bearer token
Content-Type: application/json; charset=utf-8
Host: graph.microsoft.com
Content-Length: 134
{
  "expirationDateTime": "2019-03-14T04:33:36.2394526+00:00"
}
```
- Subscription management endpoints
  - Create a subscription - POST /subscriptions
  - List subscriptions - GET /subscriptions
  - Get a subscription - GET /subscriptions/ {id}
  - Update a subscription - PATCH /subscriptions/ {id}
  - Delete a subscription - DELETE /subscriptions/ {id}
- Track Changes with the Microsoft Graph API
  - Allows retrieving changes since you last requested them
  - Available for messages, groups, users and events
  - Use the /delta function to request changes
  - Store returned the deltaLink for subsequent requests
  - Use $select to narrow what you want changes for
- Example: User track changes
```
GET https://graph.microsoft.com/v1.0/users/delta HTTP/1.1
Authorization: bearer token
Host: graph.microsoft.com

Response:
{
  "@odata.context":
  "https://graph.microsoft.com/v1.0/$metadata#users",
  "@odata.deltaLink":
  "https://graph.microsoft.com/v1.0/users/delta?
  $skiptoken=moXwmvoHW4B2uevGNLf2Brpv8sm ... ",
}
```
- Use change notifications + track changes together
  - For robust synchronization use notifications with track changes
  - Subscribe for notifications
  - When a notification is received use track changes to retrieve changes
  - If a notification is missed changes will not be missed
  - Add a full regular query at a long interval to be 100% certain no changes have been missed
