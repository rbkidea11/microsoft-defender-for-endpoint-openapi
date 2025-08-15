# Endpoint: POST /api/machines/{id}/tags

**Source:** add-or-remove-machine-tags.md  
**Tags:** Machine  
**Summary:** Add or remove tags for a single machine  
**OperationId:** addOrRemoveMachineTags

## Description
Manages tags for a specific machine for device categorization, grouping, and automated workflows.

## Parameters
### Path Parameters
- `id` (string, required): Machine ID (device identifier)

## Request Body
```json
{
  "Value": "string",
  "Action": "Add|Remove"
}
```
**Required:** Value, Action

## Responses
### 200 Success
```json
{
  "id": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "desktop-computer",
  "machineTags": [
    "Demo Device",
    "Production Server",
    "Critical Asset"
  ],
  "lastUpdateTime": "2023-08-11T10:30:00Z"
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
POST /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/tags
Authorization: Bearer {token}
Content-Type: application/json

{
  "Value": "Critical Asset",
  "Action": "Add"
}
```

## Notes
- Tags are case-sensitive
- For bulk operations, use POST /api/machines/AddOrRemoveTagForMultipleMachines
- Related endpoints: GET /api/machines/{id}, PATCH /api/machines/{id}

---
