# Endpoint: POST /api/machines/{id}/runAntiVirusScan

**Source:** run-av-scan.md  
**Tags:** MachineAction  
**Summary:** Run antivirus scan on device  
**OperationId:** runAntiVirusScan

## Description
Initiates Microsoft Defender Antivirus scan on a device with support for Quick or Full scan types.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

## Request Body
```json
{
  "Comment": "string",
  "ScanType": "string"
}
```
**Required:** Comment, ScanType  
**ScanType values:** Quick, Full

## Responses
### 201 Created
```json
{
  "id": "string",
  "type": "string",
  "requestor": "string",
  "requestorComment": "string",
  "status": "string",
  "machineId": "string",
  "computerDnsName": "string",
  "creationDateTimeUtc": "2021-01-26T20:33:57.7220239Z",
  "lastUpdateDateTimeUtc": "2021-01-26T20:33:59.2Z",
  "relatedFileInfo": null
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Scan (Application) or Machine.Scan (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine action operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/runAntiVirusScan
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Check machine for viruses due to alert 3212",
  "ScanType": "Full"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "RunAntiVirusScan",
  "requestor": "admin@contoso.com",
  "requestorComment": "Check machine for viruses due to alert 3212",
  "status": "Pending",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "mymachine1.contoso.com",
  "creationDateTimeUtc": "2021-01-26T20:33:57.7220239Z",
  "lastUpdateDateTimeUtc": "2021-01-26T20:33:59.2Z",
  "relatedFileInfo": null
}
```

## Notes
- Requires 'Active remediation actions' role permission for delegated access
- User must have access to device based on device group settings
- **Device requirements**: Windows 10 v1709+, Windows 11
- **Scan types**: 
  - **Quick**: Fast scan of common malware locations
  - **Full**: Comprehensive scan of entire device
- **Compatibility**: Works alongside other antivirus solutions, even when Defender Antivirus is in Passive mode
- **Concurrent scans**: Multiple API calls for same device return "pending machine action" or HTTP 400
- **Status tracking**: Use get-machineaction-object API to monitor scan progress

---
