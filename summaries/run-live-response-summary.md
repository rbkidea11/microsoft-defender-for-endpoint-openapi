# Endpoint: POST /api/machines/{id}/runliveresponse

**Source:** run-live-response.md  
**Tags:** MachineAction  
**Summary:** Run live response commands on device  
**OperationId:** runLiveResponse

## Description
Run live response commands on device including PutFile, RunScript, and GetFile operations.

## Parameters
### Path Parameters
- `id` (string, required): Machine ID

## Request Body
```json
{
  "Commands": [
    {
      "type": "RunScript",
      "params": [
        {
          "key": "ScriptName",
          "value": "minidump.ps1"
        },
        {
          "key": "Args",
          "value": "OfficeClickToRun"
        }
      ]
    }
  ],
  "Comment": "Investigate suspicious activity"
}
```
**Required:** Commands

## Responses
### 201 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineActions/$entity",
  "id": "2e9da30d-27f6-4208-81f2-9cd3d67893ba",
  "type": "LiveResponse",
  "requestor": "analyst@contoso.com",
  "requestorComment": "Investigate suspicious activity",
  "status": "InProgress",
  "machineId": "f70f9fe6b29cd9511652434919c6530618f06606",
  "computerDnsName": "desktop-test",
  "creationDateTimeUtc": "2018-12-04T12:18:27.1293487Z",
  "lastUpdateTimeUtc": "2018-12-04T12:18:27.1293487Z",
  "relatedFileInfo": null,
  "commands": [
    {
      "index": 0,
      "startTime": null,
      "endTime": null,
      "commandStatus": "Created",
      "errors": [],
      "command": {
        "type": "RunScript",
        "params": [
          {
            "key": "ScriptName",
            "value": "minidump.ps1"
          }
        ]
      }
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Machine.LiveResponse

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/machines/f70f9fe6b29cd9511652434919c6530618f06606/runliveresponse
Authorization: Bearer {token}
Content-Type: application/json

{
  "Commands": [
    {
      "type": "GetFile",
      "params": [
        {
          "key": "Path",
          "value": "C:\\temp\\test.txt"
        }
      ]
    }
  ],
  "Comment": "Get suspicious file"
}

Response:
{
  "id": "2e9da30d-27f6-4208-81f2-9cd3d67893ba",
  "type": "LiveResponse",
  "status": "InProgress"
}
```

## Notes
- Supports PutFile, RunScript, and GetFile commands
- Commands are executed sequentially
- Use GetLiveResponseResultDownloadLink to retrieve results

---
