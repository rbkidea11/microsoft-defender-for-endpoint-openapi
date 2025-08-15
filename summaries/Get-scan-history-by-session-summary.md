# Endpoint: POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId

**Source:** Get-scan-history-by-session.md  
**Tags:** AuthenticatedScan  
**Summary:** Get scan history by session ID  
**OperationId:** getScanHistoryBySession

## Description
Get scan history by session ID for authenticated scan definitions.

## Parameters
None

## Request Body
```json
{
  "sessionId": "string"
}
```
**Required:** sessionId

## Responses
### 200 Success
```json
{
  "sessionId": "string",
  "scanDefinitionId": "string",
  "scanStartTime": "2023-01-01T00:00:00Z",
  "scanEndTime": "2023-01-01T01:00:00Z",
  "status": "Completed",
  "results": {},
  "machineId": "string"
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
- ❌ Not applicable for POST operations

## Example
```http
POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId
Authorization: Bearer {token}
Content-Type: application/json

{
  "sessionId": "session-123"
}

Response:
{
  "sessionId": "session-123",
  "status": "Completed"
}
```

## Notes
- Part of authenticated scan management
- Returns detailed scan history for a specific session

---
