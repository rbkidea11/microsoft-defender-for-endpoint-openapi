# Endpoint: PATCH /api/machines/{machineId}

**Source:** update-machine-method.md  
**Tags:** Machine  
**Summary:** Update machine properties (tags and deviceValue)  
**OperationId:** updateMachine

## Description
Updates properties of an existing machine including tags and device value for enhanced device management and categorization.

## Parameters
### Path Parameters
- `machineId` (string, required): Machine ID

## Request Body
```json
{
  "machineTags": ["string"],
  "deviceValue": "string"
}
```
**Optional:** All fields are optional - include only fields to update

## Responses
### 200 Success
```json
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
  "machineTags": ["string"],
  "deviceValue": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.ReadWrite.All (Application) or Machine.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine update operations

## Example
```http
PATCH /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07
Authorization: Bearer {token}
Content-Type: application/json

{
  "deviceValue": "Normal",
  "machineTags": [
    "Demo Device",
    "Generic User Machine - Attack Source",
    "Windows 10",
    "Windows Insider - Fast"
  ]
}

Response:
{
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
  "machineTags": [
    "Demo Device",
    "Generic User Machine - Attack Source",
    "Windows 10",
    "Windows Insider - Fast"
  ],
  "deviceValue": "Normal"
}
```

## Notes
- Requires 'Alerts investigation' role permission for delegated access
- User must have access to device based on device group settings
- **Tag behavior**: 
  - Update appends tags to existing collection
  - Must include existing tags in request to preserve them
  - Omitting existing tags will remove them
- **Device values**: Normal, Low, High
- **Updatable properties**: Only machineTags and deviceValue can be updated
- **Performance tip**: Only include fields that need updating
- Returns 404 if machine with specified ID not found
- Essential for device categorization and management workflows

---
