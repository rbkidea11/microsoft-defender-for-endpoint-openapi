# Endpoint: GET /api/Software/{Id}

**Source:** get-software-by-id.md  
**Tags:** Software  
**Summary:** Get software details by ID  
**OperationId:** getSoftwareById

## Description
Retrieves detailed information about a specific software by its ID including vulnerability and exposure metrics.

## Parameters
### Path Parameters
- `Id` (string, required): Software ID

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software/$entity",
  "id": "string",
  "name": "string",
  "vendor": "string",
  "weaknesses": 0,
  "publicExploit": false,
  "activeAlert": false,
  "exposedMachines": 0,
  "impactScore": 0
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
- ❌ Not applicable for single software retrieval

## Example
```http
GET /api/Software/microsoft-_-edge
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Software/$entity",
  "id": "microsoft-_-edge",
  "name": "edge",
  "vendor": "microsoft",
  "weaknesses": 467,
  "publicExploit": true,
  "activeAlert": false,
  "exposedMachines": 172,
  "impactScore": 2.39947438
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- **Weaknesses**: Number of vulnerabilities affecting this software
- **PublicExploit**: Whether public exploits exist for vulnerabilities in this software
- **ActiveAlert**: Whether there are active alerts related to this software
- **ExposedMachines**: Number of devices with this software installed
- **ImpactScore**: Calculated impact score based on vulnerabilities and exposure
- **Software ID format**: Usually vendor-_-product (e.g., microsoft-_-edge)
- Essential for detailed software security assessment

---
