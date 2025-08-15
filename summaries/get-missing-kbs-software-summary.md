# Endpoint: GET /api/Software/{Id}/getmissingkbs

**Source:** get-missing-kbs-software.md  
**Tags:** Software  
**Summary:** Get missing security updates (KBs) by software ID  
**OperationId:** getMissingKBsBySoftware

## Description
Retrieves missing security updates (Knowledge Base articles) for a specific software product, essential for software-focused patch management.

## Parameters
### Path Parameters
- `Id` (string, required): Software ID (e.g., microsoft-_-edge)

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
- Permission: Software.Read.All (Application) or Software.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for missing KBs collection

## Example
```http
GET /api/Software/microsoft-_-edge/getmissingkbs
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.PublicProductFixDto)",
  "value": [
    {
      "id": "4540673",
      "name": "March 2020 Security Updates",
      "productsNames": [
        "edge"
      ],
      "url": "https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB4540673",
      "machineMissedOn": 240,
      "cveAddressed": 14
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- **Software ID format**: Usually vendor-_-product (e.g., microsoft-_-edge)
- **KB ID**: Knowledge Base article identifier (e.g., "4540673")
- **ProductsNames**: Array of products affected by this security update (typically matches the queried software)
- **URL**: Direct link to Microsoft Update Catalog for the KB
- **MachineMissedOn**: Number of machines in organization missing this update for this software
- **CveAddressed**: Number of CVEs addressed by this security update
- Essential for software-specific patch management
- Helps assess organizational exposure for specific software products
- Supports targeted update deployment strategies
- Critical for software vendor-focused vulnerability management

---
