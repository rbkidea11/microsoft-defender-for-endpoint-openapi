# Endpoint: POST /api/machines/{id}/restrictCodeExecution

**Source:** restrict-code-execution.md  
**Tags:** MachineAction  
**Summary:** Restrict app execution on device  
**OperationId:** restrictCodeExecution

## Description
Restricts execution of all applications on the device except a predefined set, using Windows Defender Application Control policies.

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
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/restrictCodeExecution
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Restrict code execution due to alert 1234"
}

Response:
{
  "id": "f123cb8d-1cee-4da9-8cd1-74b4d14f5dc2",
  "type": "RestrictCodeExecution",
  "requestor": "admin@contoso.com",
  "requestorComment": "Restrict code execution due to alert 1234",
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
- **Prerequisites**: Microsoft Defender Antivirus must be active
- **Technology**: Uses Windows Defender Application Control (WDAC) code integrity policies
- **Policy requirements**: Must meet WDAC code integrity policy formats and signing requirements
- **Concurrent actions**: Multiple API calls for same device return "pending machine action" or HTTP 400
- **Related action**: Use unrestrict-code-execution API to remove restrictions
- **Status tracking**: Use get-machineaction-object API to monitor progress
- Essential for containing potential threats by limiting executable code

---
