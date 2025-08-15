# Endpoint: GET /api/alerts/{id}/domains

**Source:** get-alert-related-domain-info.md  
**Tags:** Alert  
**Summary:** Get domains related to alert  
**OperationId:** getAlertRelatedDomains

## Description
Retrieves all domains related to a specific alert for threat investigation and analysis.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/$metadata#Domains",
  "value": [
    {
      "host": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: URL.Read.All (Application) or URL.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for related resource retrieval

## Example
```http
GET /api/alerts/636688558380765161_2136280442/domains
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/$metadata#Domains",
  "value": [
    {
      "host": "www.example.com"
    },
    {
      "host": "www.example2.com"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period

---
