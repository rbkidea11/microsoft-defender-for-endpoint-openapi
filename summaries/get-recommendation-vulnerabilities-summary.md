# Endpoint: GET /api/recommendations/{id}/vulnerabilities

**Source:** get-recommendation-vulnerabilities.md  
**Tags:** Recommendation  
**Summary:** List vulnerabilities by security recommendation  
**OperationId:** getRecommendationVulnerabilities

## Description
Retrieves a list of vulnerabilities associated with a specific security recommendation from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Security recommendation ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(Analytics.Contracts.PublicAPI.PublicVulnerabilityDto)",
  "value": [
    {
      "id": "CVE-2019-13748",
      "name": "CVE-2019-13748",
      "description": "Insufficient policy enforcement in developer tools in Google Chrome...",
      "severity": "Medium",
      "cvssV3": 6.5,
      "exposedMachines": 0,
      "publishedOn": "2019-12-10T00:00:00Z",
      "updatedOn": "2019-12-16T12:15:00Z",
      "publicExploit": false,
      "exploitVerified": false,
      "exploitInKit": false,
      "exploitTypes": [],
      "exploitUris": []
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application), Vulnerability.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/recommendations/va-_-google-_-chrome/vulnerabilities
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "CVE-2019-13748",
      "severity": "Medium",
      "cvssV3": 6.5
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns CVE details associated with the recommendation

---
