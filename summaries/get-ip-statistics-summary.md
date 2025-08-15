# Endpoint: GET /api/ips/{ip}/stats

**Source:** get-ip-statistics.md  
**Tags:** IP  
**Summary:** Get IP statistics  
**OperationId:** getIPStatistics

## Description
Retrieves statistics for a given IP address including organizational prevalence and first/last seen timestamps.

## Parameters
### Path Parameters
- `ip` (string, required): The IP address to get statistics for

### Query Parameters
- `lookBackHours` (integer, optional): Hours to search back for statistics (default 30 days, max 720 hours/30 days)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgIPStats",
  "ipAddress": "string",
  "organizationPrevalence": 0,
  "orgFirstSeen": "2017-07-30T13:36:06Z",
  "orgLastSeen": "2017-08-29T13:32:59Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Ip.Read.All (Application) or Ip.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for IP statistics retrieval

## Example
```http
GET /api/ips/10.209.67.177/stats?lookBackHours=48
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.InOrgIPStats",
  "ipAddress": "10.209.67.177",
  "organizationPrevalence": 63515,
  "orgFirstSeen": "2017-07-30T13:36:06Z",
  "orgLastSeen": "2017-08-29T13:32:59Z"
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Returns organizationPrevalence 0 if IP is valid but doesn't exist
- Returns HTTP 400 if IP address is invalid
- Maximum lookback period is 30 days (720 hours)
- Organization prevalence = distinct count of devices that opened network connection to this IP
- Statistical information based on data from past 30 days
- Useful for understanding IP usage patterns within organization

---
