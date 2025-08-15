# Endpoint: DELETE /api/indicators/{id}

**Source:** delete-ti-indicator-by-id.md  
**Tags:** Indicators  
**Summary:** Delete threat intelligence indicator by ID  
**OperationId:** deleteIndicatorById

## Description
Deletes a specific threat intelligence indicator by its unique identifier.

## Parameters
### Path Parameters
- `id` (string, required): Unique identifier of the threat intelligence indicator

## Responses
### 204 No Content
Indicator deleted successfully. No response body returned.

### Errors
Standard error responses: 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Ti.ReadWrite` or `Ti.ReadWrite.All`

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for DELETE operations

## Example
```http
DELETE /api/indicators/995
Authorization: Bearer {token}

Response: 204 No Content
```

## Notes
- Indicator deletion is permanent and cannot be undone
- Related endpoints: GET /api/indicators, POST /api/indicators, POST /api/indicators/BatchDelete

---
