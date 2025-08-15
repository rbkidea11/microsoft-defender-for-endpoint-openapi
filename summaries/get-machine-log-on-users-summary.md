# Endpoint: GET /api/machines/{id}/logonusers

**Source:** get-machine-log-on-users.md  
**Tags:** Machine  
**Summary:** Get logged on users for a specific device  
**OperationId:** getMachineLogonUsers

## Description
Retrieves a collection of users who have logged on to a specific device, useful for user activity tracking and security investigations.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Users",
  "value": [
    {
      "id": "string",
      "accountName": "string",
      "accountDomain": "string",
      "firstSeen": "2019-12-18T08:02:54Z",
      "lastSeen": "2020-01-06T08:01:48Z",
      "logonTypes": "string",
      "isDomainAdmin": true,
      "isOnlyNetworkUser": false
    }
  ]
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
- ❌ Not applicable for device-specific user collection

## Example
```http
GET /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/logonusers
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Users",
  "value": [
    {
      "id": "contoso\\user1",
      "accountName": "user1",
      "accountDomain": "contoso",
      "firstSeen": "2019-12-18T08:02:54Z",
      "lastSeen": "2020-01-06T08:01:48Z",
      "logonTypes": "Interactive",
      "isDomainAdmin": true,
      "isOnlyNetworkUser": false
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Response includes users only if device is visible to user based on device group settings
- Returns 404 if device not found
- **User identification**: Format is domain\\username
- **Logon types**: Interactive, Network, Service, etc.
- **Domain admin flag**: Indicates if user has domain administrator privileges
- **Network user flag**: Indicates if user only accessed via network (no interactive logon)
- **Time tracking**: First and last seen timestamps for user activity
- Data availability depends on configured retention period
- Essential for user activity analysis and insider threat detection
- Supports forensic investigations and compliance auditing

---
