# Endpoint: GET /api/vulnerabilities

**Source:** get-all-vulnerabilities.md  
**Tags:** Vulnerability  
**Summary:** List all vulnerabilities  
**OperationId:** getAllVulnerabilities

## Description
Retrieves a list of all vulnerabilities affecting the organization with comprehensive vulnerability details including CVSS scores, exploit information, and exposure metrics.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, name, description, cvssV3, publishedOn, severity, updatedOn
- `$top` (integer, optional): Number of entries to return (max 8,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Vulnerabilities",
  "value": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "severity": "string",
      "cvssV3": 0,
      "cvssVector": "string",
      "exposedMachines": 0,
      "publishedOn": "2024-07-30T00:00:00Z",
      "updatedOn": "2024-07-31T00:00:00Z",
      "firstDetected": "2024-07-31T01:55:47Z",
      "publicExploit": false,
      "exploitVerified": false,
      "exploitInKit": false,
      "exploitTypes": [],
      "exploitUris": [],
      "cveSupportability": "string",
      "tags": [],
      "epss": 0
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application) or Vulnerability.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: id, name, description, cvssV3, publishedOn, severity, updatedOn
- ✅ $top: Max 8,000
- ✅ $skip: Supported

## Example
```http
GET /api/vulnerabilities?$filter=severity eq 'High'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Vulnerabilities",
  "value": [
    {
      "id": "CVE-2024-7256",
      "name": "CVE-2024-7256",
      "description": "Summary: Google Chrome is vulnerable to a security bypass due to insufficient data validation in Dawn...",
      "severity": "High",
      "cvssV3": 8,
      "cvssVector": "CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H/E:U/RL:O/RC:C",
      "exposedMachines": 23,
      "publishedOn": "2024-07-30T00:00:00Z",
      "updatedOn": "2024-07-31T00:00:00Z",
      "firstDetected": "2024-07-31T01:55:47Z",
      "publicExploit": false,
      "exploitVerified": false,
      "exploitInKit": false,
      "exploitTypes": [],
      "exploitUris": [],
      "cveSupportability": "Supported",
      "tags": [],
      "epss": 0.632
    }
  ]
}
```

## Notes
- Comprehensive OData V4 query support with 7 filterable fields
- Maximum 8,000 results per request
- Includes detailed exploit information and EPSS scores
- Part of Microsoft Defender Vulnerability Management

---
