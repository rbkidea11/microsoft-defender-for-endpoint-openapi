# Endpoint: POST /api/machines/{id}/StopAndQuarantineFile

**Source:** stop-and-quarantine-file.md  
**Tags:** MachineAction  
**Summary:** Stop execution and quarantine file by SHA1  
**OperationId:** stopAndQuarantineFile

## Description
Stops execution of a file on a device and quarantines it, removing the threat from the system.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

## Request Body
```json
{
  "Comment": "string",
  "Sha1": "string"
}
```
**Required:** Comment, Sha1

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
  "relatedFileInfo": {
    "fileIdentifier": "string",
    "fileIdentifierType": "string"
  }
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.StopAndQuarantine (Application), Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.StopAndQuarantine (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine action operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/StopAndQuarantineFile
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Stop and quarantine file on machine due to alert 441688558380765161_2136280442",
  "Sha1": "87662bc3d60e4200ceaf7aae249d1c343f4b83c9"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "StopAndQuarantineFile",
  "requestor": "admin@contoso.com",
  "requestorComment": "Stop and quarantine file on machine due to alert 441688558380765161_2136280442",
  "status": "Pending",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "mymachine1.contoso.com",
  "creationDateTimeUtc": "2021-01-26T20:33:57.7220239Z",
  "lastUpdateDateTimeUtc": "2021-01-26T20:33:59.2Z",
  "relatedFileInfo": {
    "fileIdentifier": "87662bc3d60e4200ceaf7aae249d1c343f4b83c9",
    "fileIdentifierType": "Sha1"
  }
}
```

## Notes
- Requires 'Active remediation actions' role permission for delegated access
- User must have access to device based on device group settings
- **Device requirements**: Windows 10 v1703+, Windows 11
- **File restrictions**: 
  - Cannot quarantine files from trusted third-party publishers
  - Cannot quarantine Microsoft-signed files
- **Prerequisites**: Microsoft Defender Antivirus must be running (at least in Passive mode)
- **SHA1 requirement**: Must provide SHA1 hash of the file to quarantine
- **Action scope**: Stops execution AND deletes/quarantines the file
- **Status tracking**: Use get-machineaction-object API to monitor progress
- Essential for immediate threat containment and malware removal

---
