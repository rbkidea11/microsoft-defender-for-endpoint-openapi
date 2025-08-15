# Endpoint: POST /api/machineactions/{machineactionid}/cancel

**Source:** cancel-machine-action.md  
**Tags:** MachineAction  
**Summary:** Cancel an already launched machine action  
**OperationId:** cancelMachineAction

## Description
Cancels a machine action that is currently in progress or pending execution.

## Parameters
### Path Parameters
- `machineactionid` (string, required): Machine action ID to cancel

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
  "id": "5382f7ea-7557-4ab7-9782-d50480024a4e",
  "type": "Isolate",
  "requestor": "analyst@contoso.com",
  "requestorComment": "Isolate machine due to alert 1234",
  "status": "Cancelled",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "desktop-computer",
  "creationDateTimeUtc": "2023-08-11T10:30:00.0000000Z",
  "lastUpdateTimeUtc": "2023-08-11T10:35:00.0000000Z",
  "cancellationRequestor": "admin@contoso.com",
  "cancellationComment": "False positive - cancelling isolation",
  "cancellationDateTimeUtc": "2023-08-11T10:35:00.0000000Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.Isolate` or equivalent machine action permissions

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/machineactions/5382f7ea-7557-4ab7-9782-d50480024a4e/cancel
Authorization: Bearer {token}
Content-Type: application/json

{
  "Comment": "False positive - cancelling isolation"
}
```

## Notes
- Only actions in "Pending" or "InProgress" status can be cancelled
- Cancellation comment is required for audit purposes
- Related endpoints: GET /api/machineactions, GET /api/machineactions/{id}

---
