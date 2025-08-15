# Endpoint: GET /api/DeviceAuthenticatedScanAgents/{id}

**Source:** Get-agent-details.md  
**Tags:** AuthenticatedScan  
**Summary:** Get scan agent details by ID  
**OperationId:** getScanAgentById

## Description
Retrieves detailed information for a specific authenticated scan agent by its ID.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the scan agent

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents/$entity",
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
- ❌ Not applicable for single resource retrieval

## Example
```http
GET /api/DeviceAuthenticatedScanAgents/7f3d76a6976818553e996875dc91f55df6b26625
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#DeviceAuthenticatedScanAgents/$entity",
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
- Documentation shows inconsistency between endpoint path and example URL

---
