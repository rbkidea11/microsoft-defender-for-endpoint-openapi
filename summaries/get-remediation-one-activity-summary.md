# Endpoint: GET /api/remediationTasks/{id}

**Source:** get-remediation-one-activity.md  
**Tags:** RemediationActivity  
**Summary:** Get remediation activity by ID  
**OperationId:** getRemediationActivityById

## Description
Returns information about a specific remediation activity by its ID from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Remediation activity ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "id": "03942ef5-aewb-4w6e-b555-d6a97013844w",
  "title": "Update Microsoft Silverlight",
  "createdOn": "2021-02-10T13:20:36.4718166Z",
  "requesterId": "65548a1d-ef00-4a7a-8d19-1b967b5c36f4",
  "requesterEmail": "user1@contoso.com",
  "status": "Active",
  "statusLastModifiedOn": "2021-02-10T13:20:36.4719698Z",
  "description": "Update Silverlight to a later version...",
  "relatedComponent": "Microsoft Silverlight",
  "targetDevices": 18511,
  "fixedDevices": 2866,
  "dueOn": "2021-02-11T00:00:00Z",
  "category": "Software",
  "priority": "Medium",
  "type": "Update",
  "productId": "microsoft-_-silverlight",
  "vendorId": "microsoft"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: RemediationTasks.Read.All (Application), RemediationTask.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/remediationTasks/03942ef5-aewb-4w6e-b555-d6a97013844w
Authorization: Bearer {token}

Response:
{
  "id": "03942ef5-aewb-4w6e-b555-d6a97013844w",
  "title": "Update Microsoft Silverlight",
  "status": "Active"
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns detailed information about a specific remediation activity

---
