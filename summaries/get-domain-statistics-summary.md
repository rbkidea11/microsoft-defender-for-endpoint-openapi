# Endpoint: GET /api/domains/{domain}/stats

**Source:** get-domain-statistics.md  
**Tags:** Domain  
**Summary:** Get domain statistics  
**OperationId:** getDomainStatistics

## Description
Retrieves statistics on a given domain including organizational prevalence and first/last seen timestamps.

## Parameters
### Path Parameters
- `domain` (string, required): The domain address to get statistics for

### Query Parameters
- `lookBackHours` (integer, optional): Hours to search back for statistics (default 30 days, max 720 hours/30 days)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgDomainStats",
  "host": "string",
  "organizationPrevalence": 0,
  "orgFirstSeen": "2017-07-30T13:23:48Z",
  "orgLastSeen": "2017-08-29T13:09:05Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: URL.Read.All (Application) or URL.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for domain statistics retrieval

## Example
```http
GET /api/domains/example.com/stats?lookBackHours=48
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgDomainStats",
  "host": "example.com",
  "organizationPrevalence": 4070,
  "orgFirstSeen": "2017-07-30T13:23:48Z",
  "orgLastSeen": "2017-08-29T13:09:05Z"
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Returns prevalence set to 0 if domain doesn't exist
- Maximum lookback period is 30 days (720 hours)
- Useful for understanding domain usage patterns within organization
- Provides temporal context for domain-based threat analysis

---
