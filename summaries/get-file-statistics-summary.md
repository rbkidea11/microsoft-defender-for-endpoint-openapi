# Endpoint: GET /api/files/{id}/stats

**Source:** get-file-statistics.md  
**Tags:** File  
**Summary:** Get file statistics  
**OperationId:** getFileStatistics

## Description
Retrieves statistics for a given file including organizational prevalence and temporal information.

## Parameters
### Path Parameters
- `id` (string, required): File hash identifier

### Query Parameters
- `lookBackHours` (integer, optional): Hours to search back for statistics (default 30 days, max 720 hours/30 days)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgFileStats",
  "sha1": "string",
  "organizationPrevalence": 0,
  "orgFirstSeen": "2017-07-30T13:23:48Z",
  "orgLastSeen": "2017-08-29T13:09:05Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: File.Read.All (Application) or File.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for file statistics retrieval

## Example
```http
GET /api/files/4388963aaa83afe2042a46a3c017ad50bdcdafb3/stats?lookBackHours=48
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgFileStats",
  "sha1": "4388963aaa83afe2042a46a3c017ad50bdcdafb3",
  "organizationPrevalence": 15,
  "orgFirstSeen": "2017-07-30T13:23:48Z",
  "orgLastSeen": "2017-08-29T13:09:05Z"
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Maximum lookback period is 30 days (720 hours)
- Provides organizational context for file analysis
- Useful for understanding file usage patterns and prevalence

---
