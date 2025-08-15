# Endpoint: GET /api/investigations/{id}

**Source:** get-investigation-object.md  
**Tags:** AutomatedInvestigation  
**Summary:** Get investigation by ID  
**OperationId:** getInvestigationById

## Description
Retrieves a specific investigation by its ID. The ID can be either the investigation ID or the investigation triggering alert ID.

## Parameters
### Path Parameters
- `id` (string, required): Investigation ID or triggering alert ID

## Request Body
None

## Responses
### 200 Success
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
- Permission: Alert.Read.All (Application), Alert.ReadWrite.All (Application), Alert.Read (Delegated), Alert.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for single resource retrieval

## Example
```http
GET /api/investigations/63017
Authorization: Bearer {token}

Response:
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
```

## Notes
- Requires 'View Data' role permission for delegated access
- ID can be investigation ID or triggering alert ID
- Returns single investigation entity with complete details

---
