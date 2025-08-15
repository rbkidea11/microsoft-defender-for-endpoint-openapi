# Endpoint: GET /api/Software/{Id}/distributions

**Source:** get-software-ver-distribution.md  
**Tags:** Software  
**Summary:** List software version distribution  
**OperationId:** getSoftwareVersionDistribution

## Description
List software version distribution for organization showing how versions are distributed across devices.

## Parameters
### Path Parameters
- `Id` (string, required): Software ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#SoftwareDistributions",
  "value": [
    {
      "version": "1.0.0",
      "installations": 150,
      "vulnerabilities": 5
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/Software/microsoft-_-edge/distributions
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "version": "91.0.864.59",
      "installations": 150
    }
  ]
}
```

## Notes
- Shows version distribution across organization
- Useful for understanding software deployment status

---
