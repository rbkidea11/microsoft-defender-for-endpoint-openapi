# Endpoint: POST /api/machines/{machineId}/setDeviceValue

**Source:** set-device-value.md  
**Tags:** Machine  
**Summary:** Set device value (Normal/Low/High)  
**OperationId:** setDeviceValue

## Description
Sets the device value of a specific machine for vulnerability management prioritization and risk assessment.

## Parameters
### Path Parameters
- `machineId` (string, required): Device ID

## Request Body
```json
{
  "DeviceValue": "string"
}
```
**Required:** DeviceValue (Normal, Low, High)

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
- ❌ Not applicable for device value setting

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/setDeviceValue
Authorization: Bearer {token}
Content-Type: application/json

{
  "DeviceValue": "High"
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
  "machineTags": ["test tag 1", "test tag 2"],
  "deviceValue": "High"
}
```

## Notes
- Requires 'Manage security setting' role permission for delegated access
- User must have access to machine based on machine group settings
- **Device values**: 
  - **Normal**: Standard business device
  - **Low**: Lower priority device (e.g., test machines)
  - **High**: Critical business device (e.g., domain controllers, executives)
- **Purpose**: Used for vulnerability management prioritization and risk assessment
- **Impact**: Affects exposure score calculations and remediation prioritization
- Device availability depends on configured retention period
- Part of Microsoft Defender Vulnerability Management
- Essential for business-context-aware security management

---
