# Endpoint: GET /api/alerts/{id}/user

**Source:** get-alert-related-user-info.md  
**Tags:** Alert  
**Summary:** Get user related to alert  
**OperationId:** getAlertRelatedUser

## Description
Retrieves user information related to a specific alert including account details, logon history, and security context.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Users/$entity",
  "id": "string",
  "accountName": "string",
  "accountDomain": "string",
  "accountSid": "string",
  "firstSeen": "2019-12-08T06:33:39Z",
  "lastSeen": "2020-01-05T06:58:34Z",
  "mostPrevalentMachineId": "string",
  "leastPrevalentMachineId": "string",
  "logonTypes": "string",
  "logOnMachinesCount": 0,
  "isDomainAdmin": false,
  "isOnlyNetworkUser": false
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: User.Read.All (Application) or User.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for related resource retrieval

## Example
```http
GET /api/alerts/636688558380765161_2136280442/user
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Users/$entity",
  "id": "contoso\\user1",
  "accountName": "user1",
  "accountDomain": "contoso",
  "accountSid": "S-1-5-21-72051607-1745760036-109187956-93922",
  "firstSeen": "2019-12-08T06:33:39Z",
  "lastSeen": "2020-01-05T06:58:34Z",
  "mostPrevalentMachineId": "0111b647235c26159bec3e5eb6c8c3a0cc3ab766",
  "leastPrevalentMachineId": "0111b647235c26159bec3e5eb6c8c3a0cc3ab766",
  "logonTypes": "Network",
  "logOnMachinesCount": 1,
  "isDomainAdmin": false,
  "isOnlyNetworkUser": false
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period
- Provides user context for security incident investigation

---
