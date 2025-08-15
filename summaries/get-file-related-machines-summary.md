# Endpoint: GET /api/files/{id}/machines

**Source:** get-file-related-machines.md  
**Tags:** File  
**Summary:** Get machines related to file hash  
**OperationId:** getFileRelatedMachines

## Description
Retrieves a collection of machines related to a given file hash for threat investigation and lateral movement analysis.

## Parameters
### Path Parameters
- `id` (string, required): File hash identifier (SHA-1 only)

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
      "lastSeen": "2021-01-25T07:27:36.052313Z",
      "osPlatform": "string",
      "osProcessor": "string",
      "version": "string",
      "lastIpAddress": "string",
      "lastExternalIpAddress": "string",
      "osBuild": 0,
      "healthStatus": "string",
      "deviceValue": "string",
      "rbacGroupName": "string",
      "riskScore": "string",
      "exposureLevel": "string",
      "aadDeviceId": "string",
      "machineTags": ["string"],
      "ipAddresses": [
        {
          "ipAddress": "string",
          "macAddress": "string",
          "operationalStatus": "string"
        }
      ]
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
- ❌ Not applicable for file-specific machine collection

## Example
```http
GET /api/files/4388963aaa83afe2042a46a3c017ad50bdcdafb3/machines
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Machines",
  "value": [
    {
      "id": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
      "computerDnsName": "mymachine1.contoso.com",
      "firstSeen": "2018-08-02T14:55:03.7791856Z",
      "lastSeen": "2021-01-25T07:27:36.052313Z",
      "osPlatform": "Windows10",
      "osProcessor": "x64",
      "version": "1901",
      "lastIpAddress": "10.166.113.46",
      "lastExternalIpAddress": "167.220.203.175",
      "osBuild": 19042,
      "healthStatus": "Active",
      "deviceValue": "Normal",
      "rbacGroupName": "The-A-Team",
      "riskScore": "Low",
      "exposureLevel": "Low",
      "aadDeviceId": "fd2e4d29-7072-4195-aaa5-1af139b78028",
      "machineTags": ["Tag1", "Tag2"]
    }
  ]
}
```

## Notes
- Only SHA-1 hash function is supported (not MD5 or SHA-256)
- Requires 'View Data' role permission for delegated access
- Response includes only devices user has access to based on device group settings
- Useful for investigating file distribution and lateral movement patterns

---
