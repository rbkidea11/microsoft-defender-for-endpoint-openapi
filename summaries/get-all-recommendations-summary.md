# Endpoint: GET /api/recommendations

**Source:** get-all-recommendations.md  
**Tags:** Recommendation  
**Summary:** List all security recommendations  
**OperationId:** getAllRecommendations

## Description
Retrieves a list of all security recommendations affecting the organization with vulnerability management details and remediation guidance.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, productName, vendor, recommendedVersion, recommendationCategory, subCategory, severityScore, remediationType, recommendedProgram, recommendedVendor, status
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Recommendations",
  "value": [
    {
      "id": "string",
      "productName": "string",
      "recommendationName": "string",
      "weaknesses": 0,
      "vendor": "string",
      "recommendedVersion": "string",
      "recommendedVendor": "string",
      "recommendedProgram": "string",
      "recommendationCategory": "string",
      "subCategory": "string",
      "severityScore": 0,
      "publicExploit": true,
      "activeAlert": false,
      "associatedThreats": ["string"],
      "remediationType": "string",
      "status": "string",
      "configScoreImpact": 0,
      "exposureImpact": 0,
      "totalMachineCount": 0,
      "exposedMachinesCount": 0,
      "nonProductivityImpactedAssets": 0,
      "relatedComponent": "string",
      "hasUnpatchableCve": false,
      "tags": ["string"],
      "exposedCriticalDevices": 0
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: SecurityRecommendation.Read.All (Application) or SecurityRecommendation.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: id, productName, vendor, recommendedVersion, recommendationCategory, subCategory, severityScore, remediationType, recommendedProgram, recommendedVendor, status
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/recommendations?$filter=status eq 'Active'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Recommendations",
  "value": [
    {
      "id": "va-_-microsoft-_-edge_chromium-based",
      "productName": "edge_chromium-based",
      "recommendationName": "Update Microsoft Edge Chromium-based to version 127.0.2651.74",
      "weaknesses": 762,
      "vendor": "microsoft",
      "recommendedVersion": "127.0.2651.74",
      "recommendationCategory": "Application",
      "severityScore": 0,
      "publicExploit": true,
      "activeAlert": false,
      "associatedThreats": ["71d9120e-7eea-4058-889a-1a60bbf7e312"],
      "remediationType": "Update",
      "status": "Active",
      "configScoreImpact": 0,
      "exposureImpact": 1.1744086343876479,
      "totalMachineCount": 261,
      "exposedMachinesCount": 193,
      "nonProductivityImpactedAssets": 0,
      "relatedComponent": "Edge Chromium-based",
      "hasUnpatchableCve": false,
      "tags": ["internetFacing"],
      "exposedCriticalDevices": 116
    }
  ]
}
```

## Notes
- Comprehensive OData V4 query support with 11 filterable fields
- Maximum 10,000 results per request
- Part of Microsoft Defender Vulnerability Management

---
