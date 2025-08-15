# Endpoint: GET /api/recommendations/{id}/machineReferences

**Source:** get-recommendation-machines.md  
**Tags:** Recommendation  
**Summary:** List devices associated with security recommendation  
**OperationId:** getRecommendationMachines

## Description
Retrieves a list of devices associated with a specific security recommendation from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Security recommendation ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineReferences",
  "value": [
    {
      "id": "e058770379bc199a9c179ce52a23e16fd44fd2ee",
      "computerDnsName": "niw_pc",
      "osPlatform": "Windows10",
      "rbacGroupName": "GroupTwo"
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
GET /api/recommendations/va-_-google-_-chrome/machineReferences
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "e058770379bc199a9c179ce52a23e16fd44fd2ee",
      "computerDnsName": "niw_pc",
      "osPlatform": "Windows10"
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns machine references for devices affected by the recommendation

---
