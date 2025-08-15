# Endpoint: GET /api/machineactions/{id}/getPackageUri

**Source:** get-package-sas-uri.md  
**Tags:** MachineAction  
**Summary:** Get SAS URI for investigation package download  
**OperationId:** getPackageSasUri

## Description
Get a URI that allows downloading of an investigation package. The link is valid for a short time and should be used immediately.

## Parameters
### Path Parameters
- `id` (string, required): Machine action ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Edm.String",
  "value": "https://userrequests-us.securitycenter.windows.com:443/safedownload/WDATP_Investigation_Package.zip?token=..."
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.CollectForensics (Delegated)

## Rate Limits
- 2 calls per minute, 120 calls per hour

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/machineactions/7327b54fd718525cbca07dacde913b5ac3c85673/GetPackageUri
Authorization: Bearer {token}

Response:
{
  "value": "https://userrequests-us.securitycenter.windows.com:443/safedownload/WDATP_Investigation_Package.zip?token=..."
}
```

## Notes
- Only available for Windows 10 version 1703+ and Windows 11
- Returns 404 if machine action exists but isn't complete
- Download link is valid for short time only

---
