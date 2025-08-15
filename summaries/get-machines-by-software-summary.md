# Endpoint: GET /api/Software/{Id}/machineReferences

**Source:** get-machines-by-software.md  
**Tags:** Software  
**Summary:** List devices that have specific software installed  
**OperationId:** getMachinesBySoftware

## Description
Retrieves a list of device references that have the specified software installed, useful for software inventory and compliance tracking.

## Parameters
### Path Parameters
- `Id` (string, required): Software ID (e.g., microsoft-_-edge)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineReferences",
  "value": [
    {
      "id": "string",
      "computerDnsName": "string",
      "osPlatform": "string",
      "rbacGroupName": "string"
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
- ❌ Not applicable for machine references collection

## Example
```http
GET /api/Software/microsoft-_-edge/machineReferences
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineReferences",
  "value": [
    {
      "id": "7c7e1896fa39efb0a32a2cf421d837af1b9bf762",
      "computerDnsName": "dave_desktop",
      "osPlatform": "Windows10",
      "rbacGroupName": "GroupTwo"
    },
    {
      "id": "7d5cc2e7c305e4a0a290392abf6707f9888fda0d",
      "computerDnsName": "jane_PC",
      "osPlatform": "Windows10",
      "rbacGroupName": "GroupTwo"
    }
  ]
}
```

## Notes
- Part of Microsoft Defender Vulnerability Management
- **Software ID format**: Usually vendor-_-product (e.g., microsoft-_-edge)
- **Machine references**: Simplified device information focused on software inventory
- **Platform information**: Shows OS platform (Windows10, Windows11, etc.)
- **RBAC context**: Shows which RBAC group each device belongs to
- Essential for software compliance tracking and license management
- Useful for identifying deployment scope of specific software
- Supports software asset management and security assessments

---
