# Endpoint: GET /api/recommendations/{id}/software

**Source:** list-recommendation-software.md  
**Tags:** Recommendation  
**Summary:** Get software associated with recommendation  
**OperationId:** getRecommendationSoftware

## Description
Get software associated with a security recommendation from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Security recommendation ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Software",
  "value": [
    {
      "id": "microsoft-_-edge",
      "name": "edge",
      "vendor": "microsoft",
      "weaknesses": 10,
      "publicExploit": false,
      "activeAlert": false,
      "exposedMachines": 100,
      "impactScore": 5.2
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: SecurityRecommendation.Read.All (Application), SecurityRecommendation.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/recommendations/va-_-google-_-chrome/software
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "google-_-chrome",
      "name": "chrome",
      "vendor": "google"
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns software details related to the recommendation

---
