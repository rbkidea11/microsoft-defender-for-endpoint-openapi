# Endpoint: POST /api/machines/{id}/unrestrictCodeExecution

**Source:** unrestrict-code-execution.md  
**Tags:** MachineAction  
**Summary:** Remove app execution restriction from device  
**OperationId:** unrestrictCodeExecution

## Description
Removes application execution restrictions from a device, enabling execution of any application after previous code execution restrictions.

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
- Permission: Machine.RestrictExecution (Application) or Machine.RestrictExecution (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for machine action operations

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/unrestrictCodeExecution
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Unrestrict code execution since machine was cleaned and validated"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "UnrestrictCodeExecution",
  "requestor": "admin@contoso.com",
  "requestorComment": "Unrestrict code execution since machine was cleaned and validated",
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
- **Device requirements**: Windows 10 v1703+ (Full isolation), Windows 10 v1709+ (Selective isolation)
- **VPN considerations**: Devices behind full VPN tunnel may lose cloud service access; use split-tunneling VPN
- **Concurrent actions**: Multiple API calls for same device return "pending machine action" or HTTP 400
- **Related action**: Use restrict-code-execution API to apply restrictions
- **Status tracking**: Use get-machineaction-object API to monitor progress
- Essential for restoring normal device operation after threat containment

---
