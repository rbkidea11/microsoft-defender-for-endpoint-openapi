# Endpoint: POST /api/machines/{id}/unisolate

**Source:** unisolate-machine.md  
**Tags:** MachineAction  
**Summary:** Release device from isolation  
**OperationId:** unisolateMachine

## Description
Releases a device from network isolation, undoing the isolation action and restoring normal network connectivity.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

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
- Permission: Machine.Isolate (Application) or Machine.Isolate (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine action operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/unisolate
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Unisolate machine since it was clean and validated"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "Unisolate",
  "requestor": "admin@contoso.com",
  "requestorComment": "Unisolate machine since it was clean and validated",
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
- **Device support**: 
  - **Full isolation**: Windows 10 v1703+, Windows 11, Linux (public preview)
  - **Selective isolation**: Windows 10 v1709+, Windows 11
- **VPN considerations**: Devices behind full VPN tunnel may lose cloud service access during isolation; use split-tunneling VPN
- **Concurrent actions**: Multiple API calls for same device return "pending machine action" or HTTP 400
- **Related action**: Use isolate-machine API to isolate device
- **Status tracking**: Use get-machineaction-object API to monitor unisolation progress

---
