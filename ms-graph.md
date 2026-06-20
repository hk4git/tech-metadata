# Graph
## Graph
### Graph
#### Graph
Get All Entities supported by Graph:
https://graph.microsoft.com/v1.0

#### REST API - Querying
Direct Query when you know the id
 - https://graph.microsoft.com/v1.0/users/32b6fd83-e9c2-4838-aad8-69e6030cd238
   
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
