# Endpoint: GET /api/machineactions/{id}

**Source:** get-machineaction-object.md  
**Tags:** MachineAction  
**Summary:** Get machine action by ID  
**OperationId:** getMachineActionById

## Description
Retrieves a specific machine action by its ID with complete action details and status information.

## Parameters
### Path Parameters
- `id` (string, required): Machine action ID

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions/$entity",
  "id": "string",
  "type": "string",
  "scope": "string",
  "requestor": "string",
  "requestorComment": "string",
  "status": "string",
  "machineId": "string",
  "computerDnsName": "string",
  "creationDateTimeUtc": "2019-01-02T14:39:38.2262283Z",
  "lastUpdateDateTimeUtc": "2019-01-02T14:40:44.6596267Z",
  "relatedFileInfo": {
    "fileIdentifier": "string",
    "fileIdentifierType": "string"
  }
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.Read (Delegated), Machine.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for single resource retrieval

## Example
```http
GET /api/machineactions/2e9da30d-27f6-4208-81f2-9cd3d67893ba
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions/$entity",
  "id": "5382f7ea-7557-4ab7-9782-d50480024a4e",
  "type": "Isolate",
  "scope": "Selective",
  "requestor": "Analyst@TestPrd.onmicrosoft.com",
  "requestorComment": "test for docs",
  "status": "Succeeded",
  "machineId": "7b1f4967d9728e5aa3c06a9e617a22a4a5a17378",
  "computerDnsName": "desktop-test",
  "creationDateTimeUtc": "2019-01-02T14:39:38.2262283Z",
  "lastUpdateDateTimeUtc": "2019-01-02T14:40:44.6596267Z",
  "relatedFileInfo": null
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Returns 404 if machine action with specified ID not found
- Action types include: Isolate, Unisolate, CollectInvestigationPackage, RunAntiVirusScan, StopAndQuarantineFile, etc.
- Status values include: Pending, InProgress, Succeeded, Failed, TimeOut, Cancelled
- Scope values depend on action type (e.g., "Selective" or "Full" for isolation)
- RelatedFileInfo populated for file-related actions
- Essential for tracking individual remediation action progress

---
