# Endpoint: GET /api/baselineConfigurations

**Source:** get-security-baselines-assessment-configurations.md  
**Tags:** SecurityBaseline  
**Summary:** List security baseline configurations  
**OperationId:** getBaselineConfigurations

## Description
List configurations in active baseline profiles with OData V4 support for security baseline assessment.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter query
- `$top` (integer, optional): Number of entries to return
- `$skip` (integer, optional): Number of entries to skip

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#BaselineConfigurations",
  "value": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "profileId": "string",
      "profileName": "string",
      "category": "string",
      "severity": "string",
      "isCompliant": true
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: SecurityBaselinesAssessment.Read.All

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: Supported
- ✅ $top: Supported
- ✅ $skip: Supported

## Example
```http
GET /api/baselineConfigurations?$filter=isCompliant eq false
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "config-123",
      "name": "Windows Firewall Configuration",
      "isCompliant": false
    }
  ]
}
```

## Notes
- Part of security baseline assessment
- Returns configuration details from active baseline profiles

---
