# Endpoint: POST /api/machines/{id}/offboard

**Source:** offboard-machine-api.md  
**Tags:** MachineAction  
**Summary:** Offboard device from Defender for Endpoint  
**OperationId:** offboardMachine

## Description
Offboards a device from Microsoft Defender for Endpoint, stopping the sensor service but not removing registry information.

## Parameters
### Path Parameters
- `id` (string, required): Device ID (40-digit alphanumeric identifier)

## Request Body
```json
{
  "Comment": "string"
}
```
**Required:** Comment

## Responses
### 200 Success
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
- Permission: Machine.Offboard (Application) or Machine.Offboard (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine action operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/offboard
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Offboard machine by automation"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "Offboard",
  "requestor": "admin@contoso.com",
  "requestorComment": "Offboard machine by automation",
  "status": "Pending",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "mymachine1.contoso.com",
  "creationDateTimeUtc": "2021-01-26T20:33:57.7220239Z",
  "lastUpdateDateTimeUtc": "2021-01-26T20:33:59.2Z",
  "relatedFileInfo": null
}
```

## Notes
- Requires appropriate role assignment for delegated access
- User must have access to device based on device group settings
- **Platform support**: 
  - ✅ Windows 11, Windows 10 v1703+
  - ✅ Windows Server 2019+, Windows Server 2012 R2/2016 (with unified agent)
  - ❌ macOS and Linux not supported
- **Important limitations**:
  - Only stops sensor service, doesn't remove registry information
  - Use offboarding script for complete removal
  - Comment parameter is required (400 error if missing)
- **Machine ID**: 40-digit alphanumeric identifier found in device URL
- **Status tracking**: Use get-machineaction-object API to monitor offboarding progress

---
