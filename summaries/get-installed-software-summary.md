# Endpoint: GET /api/machines/{machineId}/software

**Source:** get-installed-software.md  
**Tags:** Software  
**Summary:** Get installed software for device  
**OperationId:** getInstalledSoftware

## Description
Retrieves a collection of installed software related to a given device ID for vulnerability management and inventory purposes.

## Parameters
### Path Parameters
- `machineId` (string, required): The unique identifier of the device

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Software",
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
- ❌ Not applicable for device-specific software collection

## Example
```http
GET /api/machines/ac233fa6208e1579620bf44207c4006ed7cc4501/software
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Software",
  "value": [
    {
      "id": "microsoft-_-internet_explorer",
      "name": "internet_explorer",
      "vendor": "microsoft",
      "weaknesses": 67,
      "publicExploit": true,
      "activeAlert": false,
      "exposedMachines": 42115,
      "impactScore": 46.2037163
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- Provides device-specific software inventory
- Includes vulnerability and exploit information
- Useful for asset management and security assessment

---
