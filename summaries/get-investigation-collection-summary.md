# Endpoint: GET /api/investigations

**Source:** get-investigation-collection.md  
**Tags:** AutomatedInvestigation  
**Summary:** List investigations  
**OperationId:** getInvestigations

## Description
Retrieves a collection of investigations with comprehensive OData V4 query support for filtering and pagination.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on startTime, id, state, machineId, triggeringAlertId
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Investigations",
  "value": [
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
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Alert.Read.All (Application), Alert.ReadWrite.All (Application), Alert.Read (Delegated), Alert.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ✅ $filter: startTime, id, state, machineId, triggeringAlertId
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/investigations?$filter=state eq 'Running'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Investigations",
  "value": [
    {
      "id": "63017",
      "startTime": "2020-01-06T14:11:34Z",
      "endTime": null,
      "state": "Running",
      "cancelledBy": null,
      "statusDetails": null,
      "machineId": "a69a22debe5f274d8765ea3c368d00762e057b30",
      "computerDnsName": "desktop-gtrcon0",
      "triggeringAlertId": "da637139166940871892_-598649278"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Maximum page size is 10,000 investigations
- Comprehensive OData V4 query support with 5 filterable fields
- Supports automated investigation tracking and management

---
