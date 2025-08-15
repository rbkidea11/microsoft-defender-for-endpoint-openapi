# Endpoint: POST /api/machines/AddOrRemoveTagForMultipleMachines

**Source:** add-or-remove-multiple-machine-tags.md  
**Tags:** MachineAction  
**Summary:** Add or remove tags for multiple machines  
**OperationId:** addOrRemoveTagForMultipleMachines

## Description
Manages tags for multiple machines in a single operation (up to 500 machines).

## Request Body
```json
{
  "MachineIds": ["string", "string"],
  "Tag": "string",
  "Action": "Add|Remove"
}
```
**Required:** MachineIds, Tag, Action

## Responses
### 200 Success
```json
{
  "MachineIds": ["string", "string"]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.ReadWrite.All` (Application) or `Machine.ReadWrite` (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/machines/AddOrRemoveTagForMultipleMachines
Authorization: Bearer {token}
Content-Type: application/json

{
  "MachineIds": ["machine1", "machine2", "machine3"],
  "Tag": "Critical Asset",
  "Action": "Add"
}
```

## Notes
- Maximum 500 machines per request
- For single machine operations, use POST /api/machines/{id}/tags
- Related endpoints: POST /api/machines/{id}/tags

---
