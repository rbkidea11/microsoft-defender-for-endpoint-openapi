# Endpoint: GET /api/remediationTasks

**Source:** get-remediation-all-activities.md  
**Tags:** RemediationActivity  
**Summary:** List all remediation activities  
**OperationId:** getRemediationActivities

## Description
Returns information about all remediation activities from Threat and Vulnerability Management.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on createdOn and status properties
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.windows.com/api/$metadata#RemediationTasks",
  "value": [
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
  ]
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
- ✅ $filter: createdOn, status
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/remediationTasks?$filter=status eq 'Active'&$top=50
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "03942ef5-aewb-4w6e-b555-d6a97013844w",
      "title": "Update Microsoft Silverlight",
      "status": "Active"
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Supports comprehensive OData filtering and pagination

---
