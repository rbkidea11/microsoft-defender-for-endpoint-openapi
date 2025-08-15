# Endpoint: GET /api/exposureScore/ByMachineGroups

**Source:** get-machine-group-exposure-score.md  
**Tags:** Score  
**Summary:** List exposure score by device group  
**OperationId:** getExposureScoreByMachineGroups

## Description
Retrieves the exposure score for each device group, providing vulnerability exposure metrics segmented by RBAC groups.

## Parameters
None

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#ExposureScore",
  "value": [
    {
      "time": "2019-12-03T09:51:28.214338Z",
      "score": 0,
      "rbacGroupName": "string"
    }
  ]
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
- ❌ Not applicable for exposure score collection

## Example
```http
GET /api/exposureScore/ByMachineGroups
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#ExposureScore",
  "value": [
    {
      "time": "2019-12-03T09:51:28.214338Z",
      "score": 41.38041766305988,
      "rbacGroupName": "GroupOne"
    },
    {
      "time": "2019-12-03T09:51:28.2143399Z",
      "score": 37.403726933165366,
      "rbacGroupName": "GroupTwo"
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- **Exposure score**: Calculated metric representing vulnerability exposure risk
- **Time**: Timestamp when the score was calculated
- **RBAC segmentation**: Provides scores broken down by device groups
- **Score range**: Typically 0-100, higher scores indicate greater exposure
- Essential for understanding security posture across different organizational units
- Supports risk-based prioritization and resource allocation
- Helps identify which device groups need the most attention
- Critical for executive reporting and compliance tracking

---
