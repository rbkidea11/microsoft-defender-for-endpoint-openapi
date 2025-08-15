# Endpoint: GET /api/machines/{id}

**Source:** get-machine-by-id.md  
**Tags:** Machine  
**Summary:** Get machine by device ID or computer name  
**OperationId:** getMachineById

## Description
Retrieves a specific machine by its device ID or computer name with complete device information and security status.

## Parameters
### Path Parameters
- `id` (string, required): Device ID or computer name

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Machine",
  "id": "string",
  "computerDnsName": "string",
  "firstSeen": "2018-08-02T14:55:03.7791856Z",
  "lastSeen": "2018-08-02T14:55:03.7791856Z",
  "osPlatform": "string",
  "version": "string",
  "osProcessor": "string",
  "lastIpAddress": "string",
  "lastExternalIpAddress": "string",
  "osBuild": 0,
  "healthStatus": "string",
  "rbacGroupId": 0,
  "rbacGroupName": "string",
  "riskScore": "string",
  "exposureLevel": "string",
  "isAadJoined": true,
  "aadDeviceId": "string",
  "machineTags": ["string"]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.Read (Delegated), Machine.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for single machine retrieval

## Example
```http
GET /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Machine",
  "id": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "mymachine1.contoso.com",
  "firstSeen": "2018-08-02T14:55:03.7791856Z",
  "lastSeen": "2018-08-02T14:55:03.7791856Z",
  "osPlatform": "Windows10",
  "version": "1709",
  "osProcessor": "x64",
  "lastIpAddress": "172.17.230.209",
  "lastExternalIpAddress": "167.220.196.71",
  "osBuild": 18209,
  "healthStatus": "Active",
  "rbacGroupId": 140,
  "rbacGroupName": "The-A-Team",
  "riskScore": "Low",
  "exposureLevel": "Medium",
  "isAadJoined": true,
  "aadDeviceId": "80fe8ff8-2624-418e-9591-41f0491218f9",
  "machineTags": ["test tag 1", "test tag 2"]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to device based on device group settings
- Returns 404 if machine with specified ID not found
- Device availability depends on configured retention policy
- Accepts both device ID and computer name as identifier
- Provides comprehensive device information including security posture

---
