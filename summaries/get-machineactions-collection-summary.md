# Endpoint: GET /api/machineactions

**Source:** get-machineactions-collection.md  
**Tags:** MachineAction  
**Summary:** List machine actions  
**OperationId:** getMachineActions

## Description
Retrieves a collection of machine actions with comprehensive OData V4 query support for filtering and pagination.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, status, machineId, type, requestor, creationDateTimeUtc
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions",
  "value": [
    {
      "id": "string",
      "type": "string",
      "scope": "string",
      "requestor": "string",
      "requestorComment": "string",
      "status": "string",
      "machineId": "string",
      "computerDnsName": "string",
      "creationDateTimeUtc": "2018-12-04T12:43:57.2011911Z",
      "lastUpdateTimeUtc": "2018-12-04T12:45:25.4049122Z",
      "relatedFileInfo": {
        "fileIdentifier": "string",
        "fileIdentifierType": "string"
      }
    }
  ]
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
- ✅ $filter: id, status, machineId, type, requestor, creationDateTimeUtc
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/machineactions?$filter=machineId eq 'f46b9bb259ed4a7fb9981b73510e3cc7aa81ec1f'&$top=2
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions",
  "value": [
    {
      "id": "69dc3630-1ccc-4342-acf3-35286eec741d",
      "type": "CollectInvestigationPackage",
      "scope": null,
      "requestor": "Analyst@contoso.com",
      "requestorComment": "test",
      "status": "Succeeded",
      "machineId": "f46b9bb259ed4a7fb9981b73510e3cc7aa81ec1f",
      "computerDnsName": "desktop-39g9tgl",
      "creationDateTimeUtc": "2018-12-04T12:43:57.2011911Z",
      "lastUpdateTimeUtc": "2018-12-04T12:45:25.4049122Z",
      "relatedFileInfo": null
    },
    {
      "id": "2e9da30d-27f6-4208-81f2-9cd3d67893ba",
      "type": "RunAntiVirusScan",
      "scope": "Full",
      "requestor": "Analyst@contoso.com",
      "requestorComment": "Check machine for viruses due to alert 3212",
      "status": "Succeeded",
      "machineId": "f46b9bb259ed4a7fb9981b73510e3cc7aa81ec1f",
      "computerDnsName": "desktop-39g9tgl",
      "creationDateTimeUtc": "2018-12-04T12:18:27.1293487Z",
      "lastUpdateTimeUtc": "2018-12-04T12:18:57.5511934Z",
      "relatedFileInfo": null
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Maximum page size is 10,000 machine actions
- Comprehensive OData V4 query support with 6 filterable fields
- Action types include: CollectInvestigationPackage, RunAntiVirusScan, StopAndQuarantineFile, Isolate, etc.
- Status values include: Pending, InProgress, Succeeded, Failed, TimeOut, Cancelled
- RelatedFileInfo included for file-related actions
- Essential for tracking and managing device remediation activities

---
