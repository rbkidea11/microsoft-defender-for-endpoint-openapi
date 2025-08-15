# Endpoint: POST /api/machines/{id}/collectInvestigationPackage

**Source:** collect-investigation-package.md  
**Tags:** MachineAction  
**Summary:** Collect forensics investigation package from device  
**OperationId:** collectInvestigationPackage

## Description
Collects a forensics investigation package from a device for detailed security analysis.

## Parameters
### Path Parameters
- `id` (string, required): Machine ID to collect investigation package from

## Request Body
```json
{
  "Comment": "string"
}
```
**Required:** Comment

## Responses
### 201 Created
```json
{
  "id": "5382f7ea-7557-4ab7-9782-d50480024a4e",
  "type": "CollectInvestigationPackage",
  "requestor": "analyst@contoso.com",
  "requestorComment": "Collecting investigation package for alert 1234",
  "status": "Pending",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "desktop-computer",
  "creationDateTimeUtc": "2023-08-11T10:30:00.0000000Z",
  "lastUpdateTimeUtc": "2023-08-11T10:30:00.0000000Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.CollectForensics` or equivalent investigation permissions

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/collectInvestigationPackage
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Collecting investigation package for alert 1234"
}
```

## Notes
- Investigation package collection may take several minutes to complete
- Use GET /api/machineactions/{id}/getPackageUri to download the package once ready
- Related endpoints: GET /api/machineactions/{id}, GET /api/machineactions/{id}/getPackageUri

---
