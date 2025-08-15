# Endpoint: GET /api/Software/{Id}/vulnerabilities

**Source:** get-vuln-by-software.md  
**Tags:** Software  
**Summary:** List vulnerabilities in specific software  
**OperationId:** getSoftwareVulnerabilities

## Description
List vulnerabilities in specific software from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `Id` (string, required): Software ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Vulnerabilities",
  "value": [
    {
      "id": "CVE-2021-1234",
      "name": "CVE-2021-1234",
      "description": "Vulnerability description",
      "severity": "High",
      "cvssV3": 8.5,
      "exposedMachines": 25,
      "publishedOn": "2021-01-01T00:00:00Z",
      "updatedOn": "2021-01-02T00:00:00Z",
      "publicExploit": true,
      "exploitVerified": false,
      "exploitInKit": false
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/Software/microsoft-_-edge/vulnerabilities
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "CVE-2021-1234",
      "severity": "High",
      "exposedMachines": 25
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Shows all vulnerabilities affecting the specific software

---
