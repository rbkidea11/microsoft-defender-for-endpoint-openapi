# Endpoint: GET /api/alerts/{id}/machine

**Source:** get-alert-related-machine-info.md  
**Tags:** Alert  
**Summary:** Get device related to alert  
**OperationId:** getAlertRelatedMachine

## Description
Retrieves device information related to a specific alert including system details, network configuration, and security status.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
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
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.Read (Delegated), Machine.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for related resource retrieval

## Example
```http
GET /api/alerts/636688558380765161_2136280442/machine
Authorization: Bearer {token}

Response:
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
  "machineTags": ["Tag1", "Tag2"],
  "ipAddresses": [
    {
      "ipAddress": "10.166.113.47",
      "macAddress": "8CEC4B897E73",
      "operationalStatus": "Up"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period
- Provides comprehensive device context for alert investigation

---
