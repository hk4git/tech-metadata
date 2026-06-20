# Graph 1
## Graph 2
### Graph 3
#### Graph 4

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
