# Endpoint: GET /api/users/{id}/machines

**Source:** get-user-related-machines.md  
**Tags:** User  
**Summary:** Get devices related to user ID  
**OperationId:** getUserRelatedMachines

## Description
Retrieves a collection of devices related to a given user ID for user-focused device management and security analysis.

## Parameters
### Path Parameters
- `id` (string, required): Username only (not full UPN) - e.g., "user1" for user1@contoso.com

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Machines",
  "value": [
    {
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
  ]
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
- ❌ Not applicable for user-specific machine collection

## Example
```http
GET /api/users/user1/machines
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Machines",
  "value": [
    {
      "id": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
      "computerDnsName": "user1-laptop.contoso.com",
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
      "machineTags": ["user-device", "laptop"]
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Response includes only devices user has access to based on device group settings
- **Important**: ID parameter is username only, not full UPN (use "user1" not "user1@contoso.com")
- Returns empty set if user doesn't exist (still returns 200 OK)
- Useful for identifying all devices associated with a specific user
- Essential for user-focused device management and security investigations
- Helps track user activity across multiple devices
- Supports insider threat detection and user behavior analysis

---
