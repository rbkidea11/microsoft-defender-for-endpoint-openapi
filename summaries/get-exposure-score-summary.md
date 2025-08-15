# Endpoint: GET /api/exposureScore

**Source:** get-exposure-score.md  
**Tags:** Score  
**Summary:** Get organizational exposure score  
**OperationId:** getExposureScore

## Description
Retrieves the organizational exposure score indicating the level of vulnerability exposure across the organization.

## Parameters
None

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#ExposureScore/$entity",
  "time": "2019-12-03T07:23:53.280499Z",
  "score": 0
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Score.Read.All (Application) or Score.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for single score retrieval

## Example
```http
GET /api/exposureScore
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#ExposureScore/$entity",
  "time": "2019-12-03T07:23:53.280499Z",
  "score": 33.491554051195706
}
```

## Notes
- Organizational-level vulnerability exposure measurement
- Part of Microsoft Defender Vulnerability Management
- Lower scores indicate better security posture
- Reflects cumulative vulnerability exposure across all managed devices

---
