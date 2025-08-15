# Endpoint: POST /api/libraryfiles

**Source:** upload-library.md  
**Tags:** LiveResponseLibrary  
**Summary:** Upload file to live response library  
**OperationId:** uploadLibraryFile

## Description
Uploads a file to the live response library for use in live response sessions with support for scripts and executables.

## Parameters
None (all parameters in form-data request body)

## Request Body
```
Content-Type: multipart/form-data

file: (file content, required)
Description: (string, optional)
ParametersDescription: (string, optional)
OverrideIfExists: (boolean, optional)
```
**Required:** file  
**Optional:** Description, ParametersDescription, OverrideIfExists

## Responses
### 200 Success
```json
{
  "id": "string",
  "fileName": "string",
  "description": "string",
  "parametersDescription": "string",
  "hasParameters": true,
  "size": 0,
  "creationTime": "2021-01-26T20:33:57.7220239Z",
  "createdBy": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Library.Manage (Application) or Library.Manage (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for file upload operations

## Example
```bash
curl -X POST https://api.security.microsoft.com/api/libraryfiles \
  -H "Authorization: Bearer $token" \
  -F "file=@mdatp1.png" \
  -F "ParametersDescription=test" \
  -F "HasParameters=true" \
  -F "OverrideIfExists=true" \
  -F "Description=test description"

Response:
{
  "id": "12345",
  "fileName": "mdatp1.png",
  "description": "test description",
  "parametersDescription": "test",
  "hasParameters": true,
  "size": 2048,
  "creationTime": "2021-01-26T20:33:57.7220239Z",
  "createdBy": "admin@contoso.com"
}
```

## Notes
- **File size limit**: Maximum 20MB per file
- **Content-Type**: Must use multipart/form-data
- **OverrideIfExists**: Set to true to replace existing files with same name
- **ParametersDescription**: Describes parameters required for script execution
- **HasParameters**: Automatically determined based on ParametersDescription
- **Supported file types**: Scripts, executables, and other files for live response
- **Related operations**: Use with run-live-response API for execution

---
