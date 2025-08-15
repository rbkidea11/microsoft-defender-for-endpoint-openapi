# Endpoint: GET /api/machines/{machineId}/recommendations

**Source:** get-security-recommendations.md  
**Tags:** Machine  
**Summary:** Get security recommendations for device  
**OperationId:** getMachineRecommendations

## Description
Get security recommendations for a specific device from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `machineId` (string, required): Machine ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Recommendations",
  "value": [
    {
      "id": "va-_-google-_-chrome",
      "productName": "chrome",
      "recommendationName": "Update Chrome",
      "weaknesses": 38,
      "vendor": "google",
      "recommendationCategory": "Application",
      "severityScore": 0,
      "publicExploit": false,
      "activeAlert": false,
      "status": "Active",
      "exposureImpact": 3.9441860465116285,
      "relatedComponent": "Chrome"
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
GET /api/machines/e058770379bc199a9c179ce52a23e16fd44fd2ee/recommendations
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "va-_-google-_-chrome",
      "recommendationName": "Update Chrome",
      "status": "Active"
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns recommendations specific to the device

---
