# Endpoint: GET /api/configurationScore

**Source:** get-device-secure-score.md  
**Tags:** Score  
**Summary:** Get organizational device secure score  
**OperationId:** getDeviceSecureScore

## Description
Retrieves the organizational Microsoft Secure Score for Devices indicating endpoint resilience against cybersecurity threats.

## Parameters
None

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#ConfigurationScore/$entity",
  "time": "2019-12-03T09:15:58.1665846Z",
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
GET /api/configurationScore
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#ConfigurationScore/$entity",
  "time": "2019-12-03T09:15:58.1665846Z",
  "score": 340
}
```

## Notes
- Higher scores indicate more resilient endpoints
- Part of Microsoft Secure Score for Devices
- Provides organizational-level security posture measurement
- Score reflects configuration security across all managed devices

---
