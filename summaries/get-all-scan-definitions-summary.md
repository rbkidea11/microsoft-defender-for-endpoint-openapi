# Endpoint: GET /api/DeviceAuthenticatedScanDefinitions

**Source:** get-all-scan-definitions.md  
**Tags:** AuthenticatedScan  
**Summary:** Get all scan definitions  
**OperationId:** getAllScanDefinitions

## Description
Retrieves a list of all authenticated scan definitions including Windows and Network scan types with authentication parameters, agent details, and scan status.

## Parameters
### Query Parameters
None specified in documentation

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#DeviceAuthenticatedScanDefinitions",
  "value": [
    {
      "id": "string",
      "scanType": "string",
      "scanName": "string",
      "isActive": true,
      "target": "string",
      "orgId": "string",
      "intervalInHours": 0,
      "createdBy": "string",
      "targetType": "string",
      "scanAuthenticationParams": {
        "@odata.type": "string",
        "type": "string",
        "username": "string",
        "domain": "string",
        "isGmsaUser": true
      },
      "scannerAgent": {
        "id": "string",
        "machineId": "string",
        "machineName": "string",
        "lastSeen": "2021-12-19T20:29:04.8242449Z",
        "AssignedApplicationId": "string",
        "ScannerSoftwareVersion": "string",
        "LastCommandExecutionTimestamp": "2021-12-19T20:29:04.8242449Z",
        "mdeClientVersion": "string"
      },
      "latestScan": {
        "status": "string",
        "failureReason": "string",
        "executionDateTime": "2021-12-19T20:06:55.2295854Z"
      }
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application) or Machine.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not specified in documentation

## Example
```http
GET /api/DeviceAuthenticatedScanDefinitions
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#DeviceAuthenticatedScanDefinitions",
  "value": [
    {
      "id": "60c4vv57-asdf-3454-a456-2e45t9d79ec9d",
      "scanType": "Windows",
      "scanName": "Test Windows scan",
      "isActive": true,
      "target": "127.0.0.1",
      "orgId": "47d21a0c-cccd-45d3-bffa-a93dbc0bfcaa",
      "intervalInHours": 1,
      "createdBy": "test@contoso.com",
      "targetType": "Ip",
      "scanAuthenticationParams": {
        "@odata.type": "#microsoft.windowsDefenderATP.api.WindowsAuthParams",
        "type": "Kerberos",
        "username": "username",
        "domain": "password",
        "isGmsaUser": true
      },
      "scannerAgent": {
        "id": "47d41a0c-xxx-46d3-bbea-93dbc0bfcaa_1bc268a79eedf14c4b90f77",
        "machineId": "eb663asadf345dfg4bc268a79eedf14c4b90f77",
        "machineName": "DESKTOP-TEST",
        "lastSeen": "2021-12-19T20:29:04.8242449Z",
        "AssignedApplicationId": "9E0FA0EB-0A51-4357-9C87-C21BFBE07571",
        "ScannerSoftwareVersion": "7.1.1",
        "LastCommandExecutionTimestamp": "2021-12-19T20:29:04.8242449Z",
        "mdeClientVersion": "10.8295.22621.1195"
      },
      "latestScan": {
        "status": "Fail",
        "failureReason": null,
        "executionDateTime": "2021-12-19T20:06:55.2295854Z"
      }
    }
  ]
}
```

## Notes
- Requires ViewData or TvmViewData role permission for delegated access
- Supports both Windows and Network scan types with different authentication parameters
- Includes comprehensive scan agent and execution status information

---
