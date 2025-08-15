# Endpoint: POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId

**Source:** Get-scan-history-by-definition.md  
**Tags:** AuthenticatedScan  
**Summary:** Get scan history by definition IDs  
**OperationId:** getScanHistoryByDefinition

## Description
Get scan history by definition IDs with OData support for authenticated scan definitions.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter query
- `$top` (integer, optional): Number of entries to return
- `$skip` (integer, optional): Number of entries to skip

## Request Body
```json
{
  "scanDefinitionIds": ["string"]
}
```
**Required:** scanDefinitionIds

## Responses
### 200 Success
```json
{
  "value": [
    {
      "scanDefinitionId": "string",
      "scanSessionId": "string",
      "scanStartTime": "2023-01-01T00:00:00Z",
      "scanEndTime": "2023-01-01T01:00:00Z",
      "status": "Completed",
      "results": {}
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Appropriate permissions required

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: Supported
- ✅ $top: Supported
- ✅ $skip: Supported

## Example
```http
POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId
Authorization: Bearer {token}
Content-Type: application/json

{
  "scanDefinitionIds": ["def-123"]
}

Response:
{
  "value": [
    {
      "scanDefinitionId": "def-123",
      "status": "Completed"
    }
  ]
}
```

## Notes
- Part of authenticated scan management
- Supports OData queries for filtering and pagination

---
