# Endpoint: GET /api/vulnerabilities/machinesVulnerabilities

**Source:** get-all-vulnerabilities-by-machines.md  
**Tags:** Vulnerability  
**Summary:** List vulnerabilities by machine and software  
**OperationId:** getVulnerabilitiesByMachines

## Description
Retrieves a list of all vulnerabilities affecting the organization by machine and software, including fixing KB information when available.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, cveId, machineId, fixingKbId, productName, productVersion, severity, productVendor
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicAssetVulnerabilityDto)",
  "value": [
    {
      "id": "string",
      "cveId": "string",
      "machineId": "string",
      "fixingKbId": "string",
      "productName": "string",
      "productVendor": "string",
      "productVersion": "string",
      "severity": "string"
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
- ✅ $filter: id, cveId, machineId, fixingKbId, productName, productVersion, severity, productVendor
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/vulnerabilities/machinesVulnerabilities?$filter=severity eq 'High'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicAssetVulnerabilityDto)",
  "value": [
    {
      "id": "5afa3afc92a7c63d4b70129e0a6f33f63a427e21-_-CVE-2020-6494-_-microsoft-_-edge_chromium-based-_-81.0.416.77-_-",
      "cveId": "CVE-2020-6494",
      "machineId": "5afa3afc92a7c63d4b70129e0a6f33f63a427e21",
      "fixingKbId": null,
      "productName": "edge_chromium-based",
      "productVendor": "microsoft",
      "productVersion": "81.0.416.77",
      "severity": "Low"
    },
    {
      "id": "7a704e17d1c2977c0e7b665fb18ae6e1fe7f3283-_-CVE-2016-3348-_-microsoft-_-windows_server_2012_r2-_-6.3.9600.19728-_-3185911",
      "cveId": "CVE-2016-3348",
      "machineId": "7a704e17d1c2977c0e7b665fb18ae6e1fe7f3283",
      "fixingKbId": "3185911",
      "productName": "windows_server_2012_r2",
      "productVendor": "microsoft",
      "productVersion": "6.3.9600.19728",
      "severity": "Low"
    }
  ]
}
```

## Notes
- Excellent for Power BI integration
- Includes fixing KB information when available
- Comprehensive OData V4 query support with 8 filterable fields
- Maximum 10,000 results per request

---
