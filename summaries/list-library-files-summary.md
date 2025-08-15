# Endpoint: GET /api/libraryfiles

**Source:** list-library-files.md  
**Tags:** LiveResponseLibrary  
**Summary:** List live response library files  
**OperationId:** getLibraryFiles

## Description
Retrieves a collection of all files in the live response library including scripts, executables, and other tools available for live response sessions.

## Parameters
None

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#LibraryFiles",
  "value": [
    {
      "fileName": "string",
      "sha256": "string",
      "description": "string",
      "creationTime": "2019-10-24T10:54:23.2009016Z",
      "lastUpdatedTime": "2019-10-24T10:54:23.2009016Z",
      "createdBy": "string",
      "hasParameters": false,
      "parametersDescription": "string"
    }
  ]
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
- ❌ Not applicable for library file listing

## Example
```http
GET /api/libraryfiles
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#LibraryFiles",
  "value": [
    {
      "fileName": "script1.ps1",
      "sha256": "6e212a0db618507c44e4ec8ee7499dfef7e5767e5f8d31144df3b96fd1145caf",
      "description": null,
      "creationTime": "2019-10-24T10:54:23.2009016Z",
      "lastUpdatedTime": "2019-10-24T10:54:23.2009016Z",
      "createdBy": "admin",
      "hasParameters": true,
      "parametersDescription": "test"
    },
    {
      "fileName": "script.sh",
      "sha256": "d0f3e3b0641dbf88ee39c822516e81a909d1d06d22341dd9b1f12aa5e5c027a2",
      "description": null,
      "creationTime": "2018-10-24T11:15:35.3688259Z",
      "lastUpdatedTime": "2018-10-24T11:15:35.3688259Z",
      "createdBy": "username",
      "hasParameters": false
    },
    {
      "fileName": "memdump.exe",
      "sha256": "fa70b87730290c0d30fe255d1dfb65de82f96286ebfeeb1d88ed3cc831329825",
      "description": "Process memory dump",
      "creationTime": "2018-10-24T10:54:23.2009016Z",
      "lastUpdatedTime": "2018-10-24T10:54:23.2009016Z",
      "createdBy": "admin",
      "hasParameters": false
    }
  ]
}
```

## Notes
- **File types**: Supports PowerShell scripts (.ps1), shell scripts (.sh), executables (.exe), and other tools
- **SHA256 hashes**: Provided for file integrity verification
- **Parameters**: Scripts can have parameters (hasParameters=true) with descriptions
- **Metadata**: Includes creation time, last updated time, and creator information
- **Descriptions**: Optional descriptions for file purpose and usage
- **Related operations**: Use with upload-library and run-live-response APIs
- **Security**: Files are stored securely and validated before use in live response sessions

---
