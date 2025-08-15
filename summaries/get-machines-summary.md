# Endpoint: GET /api/machines

**Source:** get-machines.md  
**Tags:** Machine  
**Summary:** List machines  
**OperationId:** getMachines

## Description
Retrieves a collection of machines that have communicated with Microsoft Defender for Endpoint cloud with comprehensive OData V4 query support.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on computerDnsName, id, version, deviceValue, aadDeviceId, machineTags, lastSeen, exposureLevel, onboardingStatus, lastIpAddress, healthStatus, osPlatform, riskScore, rbacGroupId
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Machines",
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
- ✅ $filter: computerDnsName, id, version, deviceValue, aadDeviceId, machineTags, lastSeen, exposureLevel, onboardingStatus, lastIpAddress, healthStatus, osPlatform, riskScore, rbacGroupId
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/machines?$filter=healthStatus eq 'Active'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Machines",
  "value": [
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
      "machineTags": ["test tag 1", "test tag 2"]
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Response includes only devices user has access to based on device group settings
- Returns 404 if no recent machines found
- Device availability depends on configured retention period
- Maximum page size is 10,000 machines
- Comprehensive OData V4 query support with 12 filterable fields
- Essential for device inventory and management operations

---
