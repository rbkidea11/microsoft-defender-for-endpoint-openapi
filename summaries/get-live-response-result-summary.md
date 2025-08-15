# Endpoint: GET /api/machineactions/{id}/GetLiveResponseResultDownloadLink(index={command-index})

**Source:** get-live-response-result.md  
**Tags:** LiveResponseLibrary  
**Summary:** Get live response command result download link  
**OperationId:** getLiveResponseResult

## Description
Retrieves a specific live response command result by its index, returning a download link valid for 30 minutes.

## Parameters
### Path Parameters
- `id` (string, required): Machine action ID
- `command-index` (integer, required): Index of the command result to retrieve

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Edm.String",
  "value": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.Read.All (Application), Machine.ReadWrite.All (Application), Machine.LiveResponse (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for download link retrieval

## Example
```http
GET /api/machineactions/988cc94e-7a8f-4b28-ab65-54970c5d5018/GetLiveResponseResultDownloadLink(index=0)
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Edm.String",
  "value": "https://core.windows.net/investigation-actions-data/ID/CustomPlaybookCommandOutput/4ed5e7807ad1fe59b00b664fe06a0f07?se=2021-02-04T16%3A13%3A50Z&sp=r&sv=2019-07-07&sr=b&sig=1dYGe9rPvUlXBPvYSmr6/OLXPY98m8qWqfIQCBbyZTY%3D"
}
```

## File Content Example
```json
{
  "script_name": "minidump.ps1",
  "exit_code": 0,
  "script_output": "Transcript started, output file is C:\\ProgramData\\Microsoft\\Windows Defender Advanced Threat Protection\\Temp\\PSScriptOutputs\\PSScript_Transcript_{TRANSCRIPT_ID}.txt\nC:\\windows\\TEMP\\OfficeClickToRun.dmp.zip\n51 MB",
  "script_errors": ""
}
```

## Notes
- Download link is valid for 30 minutes only
- Should be used immediately for downloading to local storage
- Expired links can be re-created with another call
- No need to run live response again for expired links
- Supports Windows 10 (various versions with specific KBs), Windows 11, Windows Server 2019/2022/2025
- Runscript transcript includes: script_name, exit_code, script_output, script_errors

---
