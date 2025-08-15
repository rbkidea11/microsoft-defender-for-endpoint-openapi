# Endpoint: GET /api/Machines/InfoGatheringExport

**Source:** get-assessment-information-gathering.md  
**Tags:** InformationGathering  
**Summary:** Export information gathering assessment  
**OperationId:** exportInfoGatheringAssessment

## Description
Returns all information gathering assessments for all devices on a per-device basis as downloadable files from Azure Storage.

## Parameters
### Query Parameters
- `sasValidHours` (integer, optional): Number of hours download URLs are valid (max 6 hours, default 1 hour)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "string"
  ],
  "generatedTime": "2022-07-26T10:01:00Z"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application) or Vulnerability.Read (Delegated)

## Rate Limits
- 5 calls per minute, 20 calls per hour

## OData Support
- ❌ Not applicable for file export operations

## Example
```http
GET /api/Machines/InfoGatheringExport?sasValidHours=1
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=0/part-00001-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=...",
    "https://tvmexportexternalprdcanc.blob.core.windows.net/temp-43b2fdb7-c985-4f14-bed5-ae66959a95a5/2022-07-26/1001/InfoGatheringExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=1/part-00002-42240b35-4a40-45f7-9b46-96a5ce6d23b8.c000.json.gz?sv=2020-08-04&st=2022-07-26T13%3A36%3A30Z&se=2022-07-26T16%3A36%3A30Z&sr=b&sp=r&sig=..."
  ],
  "generatedTime": "2022-07-26T10:01:00Z"
}
```

## Notes
- File export only (no JSON response method available)
- Files are GZIP compressed in multiline JSON format
- Download URLs valid for 1 hour by default, maximum 6 hours
- Returns current snapshot of information gathering assessments per device
- Optimize download speed by using same Azure region as data storage

---
