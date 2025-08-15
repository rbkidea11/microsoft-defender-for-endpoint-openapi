# Endpoint: POST /api/machines/{id}/startInvestigation

**Source:** initiate-autoir-investigation.md  
**Tags:** AutomatedInvestigation  
**Summary:** Start automated investigation on device  
**OperationId:** startAutomatedInvestigation

## Description
Initiates an automated investigation (AIR) on a device to automatically analyze and respond to potential threats.

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
  "startTime": "2020-01-06T14:11:34Z",
  "endTime": "2020-01-06T15:30:00Z",
  "state": "string",
  "cancelledBy": "string",
  "statusDetails": "string",
  "machineId": "string",
  "computerDnsName": "string",
  "triggeringAlertId": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Alert.ReadWrite.All (Application) or Alert.ReadWrite (Delegated)

## Rate Limits
- 50 calls per hour

## OData Support
- ❌ Not applicable for investigation initiation

## Example
```http
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/startInvestigation
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "Test investigation"
}

Response:
{
  "id": "63017",
  "startTime": "2020-01-06T14:11:34Z",
  "endTime": null,
  "state": "Running",
  "cancelledBy": null,
  "statusDetails": null,
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "mymachine1.contoso.com",
  "triggeringAlertId": null
}
```

## Notes
- Requires 'Active remediation actions' role permission for delegated access
- User must have access to device based on device group settings
- **Rate limit**: Lower than standard (50/hour vs typical 100/min)
- **OS requirements**: 
  - Windows 11
  - Windows 10 v1803+ (with specific KBs for older versions)
  - Windows Server 2019/2022/2025
- **AIR capabilities**: Automated threat analysis, evidence collection, and response actions
- **Investigation states**: Running, Completed, Failed, Cancelled
- **Related operations**: Use get-investigation-object API to monitor progress
- Essential for automated threat response and investigation workflows

---
