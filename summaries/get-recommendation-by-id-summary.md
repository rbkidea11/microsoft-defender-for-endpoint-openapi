# Endpoint: GET /api/recommendations/{id}

**Source:** get-recommendation-by-id.md  
**Tags:** Recommendation  
**Summary:** Get security recommendation by ID  
**OperationId:** getRecommendationById

## Description
Retrieves a security recommendation by its ID from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Security recommendation ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Recommendations/$entity",
  "id": "va-_-google-_-chrome",
  "productName": "chrome",
  "recommendationName": "Update Chrome",
  "weaknesses": 38,
  "vendor": "google",
  "recommendedVersion": "",
  "recommendationCategory": "Application",
  "subCategory": "",
  "severityScore": 0,
  "publicExploit": false,
  "activeAlert": false,
  "associatedThreats": [],
  "remediationType": "Update",
  "status": "Active",
  "configScoreImpact": 0,
  "exposureImpact": 3.9441860465116285,
  "totalMachineCount": 6,
  "exposedMachinesCount": 5,
  "nonProductivityImpactedAssets": 0,
  "relatedComponent": "Chrome",
  "tags": ["internetFacing"],
  "exposedCriticalDevices": 116
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
GET /api/recommendations/va-_-google-_-chrome
Authorization: Bearer {token}

Response:
{
  "id": "va-_-google-_-chrome",
  "productName": "chrome",
  "recommendationName": "Update Chrome",
  "status": "Active"
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns detailed recommendation information including exposure impact

---
