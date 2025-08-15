# Endpoint: GET /api/machines/{machineId}/getmissingkbs

**Source:** get-missing-kbs-machine.md  
**Tags:** Machine  
**Summary:** Get missing security updates (KBs) by device ID  
**OperationId:** getMissingKBsByMachine

## Description
Retrieves missing security updates (Knowledge Base articles) for a specific device, essential for patch management and vulnerability remediation.

## Parameters
### Path Parameters
- `machineId` (string, required): Device ID

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicProductFixDto)",
  "value": [
    {
      "id": "string",
      "name": "string",
      "productsNames": ["string"],
      "url": "string",
      "machineMissedOn": 0,
      "cveAddressed": 0
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All (Application)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for missing KBs collection

## Example
```http
GET /api/machines/2339ad14a01bd0299afb93dfa2550136057bff96/getmissingkbs
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicProductFixDto)",
  "value": [
    {
      "id": "4540673",
      "name": "March 2020 Security Updates",
      "productsNames": [
        "windows_10",
        "edge",
        "internet_explorer"
      ],
      "url": "https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4540673",
      "machineMissedOn": 1,
      "cveAddressed": 97
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- **KB ID**: Knowledge Base article identifier (e.g., "4540673")
- **ProductsNames**: Array of products affected by this security update
- **URL**: Direct link to Microsoft Update Catalog for the KB
- **MachineMissedOn**: Number of machines missing this update (typically 1 for single device query)
- **CveAddressed**: Number of CVEs addressed by this security update
- Essential for patch management and compliance tracking
- Helps prioritize security updates based on CVE count
- Supports automated patch deployment workflows
- Critical for maintaining device security posture

---
