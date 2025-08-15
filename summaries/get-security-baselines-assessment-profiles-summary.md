# Endpoint: GET /api/baselineProfiles

**Source:** get-security-baselines-assessment-profiles.md  
**Tags:** SecurityBaseline  
**Summary:** List security baseline profiles  
**OperationId:** getBaselineProfiles

## Description
List all security baselines assessment profiles with OData V4 support.

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
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#BaselineProfiles",
  "value": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "isActive": true,
      "createdOn": "2023-01-01T00:00:00Z",
      "lastModifiedOn": "2023-01-01T00:00:00Z",
      "configurationCount": 100
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
GET /api/baselineProfiles?$filter=isActive eq true
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "profile-123",
      "name": "Windows Security Baseline",
      "isActive": true
    }
  ]
}
```

## Notes
- Part of security baseline assessment
- Returns all available baseline profiles

---
