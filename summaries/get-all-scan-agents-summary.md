# Endpoint: GET /api/DeviceAuthenticatedScanAgents

**Source:** get-all-scan-agents.md  
**Tags:** AuthenticatedScan  
**Summary:** Get all authenticated scan agents  
**OperationId:** getAllScanAgents

## Description
Retrieves a list of all authenticated scan agents with their details including machine information, versions, and last seen times.

## Parameters
### Query Parameters
None specified in documentation

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api-us.securitycenter.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents",
  "value": [
    {
      "id": "string",
      "machineId": "string",
      "lastSeen": "2022-05-08T12:18:41.538203Z",
      "computerDnsName": "string",
      "AssignedApplicationId": "string",
      "ScannerSoftwareVersion": "string",
      "LastCommandExecutionTimestamp": "2022-05-08T12:18:41.538203Z",
      "mdeClientVersion": "string"
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
GET /api/DeviceAuthenticatedScanAgents
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api-us.securitycenter.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents",
  "value": [
    {
      "id": "47df41a0c-asad-4fd6d3-bbea-a93dbc0bfcaa_4edd75b2407a5b64d704b4e53d74f15",
      "machineId": "4ejh675b240118fbehiuiy5b64d704b4e53d15",
      "lastSeen": "2022-05-08T12:18:41.538203Z",
      "computerDnsName": "TEST_DOMAIN",
      "AssignedApplicationId": "9E0FA0EB-0A51-4357-9C87-C21BFBE07571",
      "ScannerSoftwareVersion": "7.1.1",
      "LastCommandExecutionTimestamp": "2022-05-08T12:18:41.538203Z",
      "mdeClientVersion": "10.8295.22621.1195"
    }
  ]
}
```

## Notes
- Requires ViewData or TvmViewData role permission for delegated access
- Returns comprehensive scan agent information for vulnerability management

---
