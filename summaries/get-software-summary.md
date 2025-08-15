# Endpoint: GET /api/Software

**Source:** get-software.md  
**Tags:** Software  
**Summary:** List software inventory  
**OperationId:** getSoftware

## Description
Retrieves the organization software inventory with vulnerability and exposure information, supporting comprehensive OData V4 queries.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, name, vendor
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software",
  "value": [
    {
      "id": "string",
      "name": "string",
      "vendor": "string",
      "weaknesses": 0,
      "publicExploit": false,
      "activeAlert": false,
      "exposedMachines": 0,
      "impactScore": 0
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All (Application) or Software.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: id, name, vendor
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/Software?$filter=vendor eq 'microsoft'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software",
  "value": [
    {
      "id": "microsoft-_-edge",
      "name": "edge",
      "vendor": "microsoft",
      "weaknesses": 467,
      "publicExploit": true,
      "activeAlert": false,
      "exposedMachines": 172,
      "impactScore": 2.39947438
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- Provides organizational software inventory with security context
- **Weaknesses**: Number of vulnerabilities affecting this software
- **PublicExploit**: Whether public exploits exist for vulnerabilities in this software
- **ActiveAlert**: Whether there are active alerts related to this software
- **ExposedMachines**: Number of devices with this software installed
- **ImpactScore**: Calculated impact score based on vulnerabilities and exposure
- Maximum 10,000 results per query
- Essential for software asset management and vulnerability assessment

---
