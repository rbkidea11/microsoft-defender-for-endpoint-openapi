# Endpoint: POST /api/machines/{id}/isolate

**Source:** isolate-machine.md  
**Tags:** MachineAction  
**Summary:** Isolate device from network  
**OperationId:** isolateMachine

## Description
Isolates a device from accessing external network with support for Full, Selective, or UnManagedDevice isolation types.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

## Request Body
```json
{
  "Comment": "string",
  "IsolationType": "string"
}
```
**Required:** Comment  
**Optional:** IsolationType (Full, Selective, UnManagedDevice)

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
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/isolate
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Isolate machine due to alert 1234",
  "IsolationType": "Full"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "Isolate",
  "requestor": "admin@contoso.com",
  "requestorComment": "Isolate machine due to alert 1234",
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
- **Full isolation**: Available for Windows 10 v1703+, Windows 11, and all supported Linux devices
- **Selective isolation**: Available for Windows 10 v1709+, Windows 11 (restricts limited applications)
- **UnManagedDevice isolation**: For unmanaged devices only
- **VPN considerations**: Devices behind full VPN tunnel may lose cloud service access; use split-tunneling VPN
- **Related action**: Use unisolate-machine API to release device from isolation

---
