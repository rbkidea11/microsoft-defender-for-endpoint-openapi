# Endpoint: GET /api/machines/{machineId}/vulnerabilities

**Source:** get-discovered-vulnerabilities.md  
**Tags:** Vulnerability  
**Summary:** Get discovered vulnerabilities for device  
**OperationId:** getDiscoveredVulnerabilities

## Description
Retrieves a collection of discovered vulnerabilities related to a specific device ID with detailed vulnerability information.

## Parameters
### Path Parameters
- `machineId` (string, required): The unique identifier of the device

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(Analytics.Contracts.PublicAPI.PublicVulnerabilityDto)",
  "value": [
    {
      "id": "string",
      "name": "string",
      "description": "string",
      "severity": "string",
      "cvssV3": 0,
      "exposedMachines": 0,
      "publishedOn": "2019-12-13T00:00:00Z",
      "updatedOn": "2019-12-13T00:00:00Z",
      "publicExploit": false,
      "exploitVerified": false,
      "exploitInKit": false,
      "exploitTypes": [],
      "exploitUris": []
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
- 50 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for device-specific vulnerability collection

## Example
```http
GET /api/machines/ac233fa6208e1579620bf44207c4006ed7cc4501/vulnerabilities
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(Analytics.Contracts.PublicAPI.PublicVulnerabilityDto)",
  "value": [
    {
      "id": "CVE-2019-1348",
      "name": "CVE-2019-1348",
      "description": "Git could allow a remote attacker to bypass security restrictions, caused by a flaw in the --export-marks option of git fast-import. By persuading a victim to import specially-crafted content, an attacker could exploit this vulnerability to overwrite arbitrary paths.",
      "severity": "Medium",
      "cvssV3": 4.3,
      "exposedMachines": 1,
      "publishedOn": "2019-12-13T00:00:00Z",
      "updatedOn": "2019-12-13T00:00:00Z",
      "publicExploit": false,
      "exploitVerified": false,
      "exploitInKit": false,
      "exploitTypes": [],
      "exploitUris": []
    }
  ]
}
```

## Notes
- Device-specific vulnerability assessment
- Includes exploit information and CVSS scores
- Part of Microsoft Defender Vulnerability Management
- Higher rate limit than general vulnerability endpoints

---
