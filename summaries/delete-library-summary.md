# Endpoint: DELETE /api/libraryfiles/{fileName}

**Source:** delete-library.md  
**Tags:** LiveResponseLibrary  
**Summary:** Delete file from live response library  
**OperationId:** deleteLibraryFile

## Description
Deletes a file from the live response library used for remote device investigations and remediation activities.

## Parameters
### Path Parameters
- `fileName` (string, required): Name of the file to delete from the library

## Responses
### 204 No Content
File deleted successfully. No response body returned.

### Errors
Standard error responses: 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Library.Manage`

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for DELETE operations

## Example
```http
DELETE /api/libraryfiles/script1.ps1
Authorization: Bearer {token}

Response: 204 No Content
```

## Notes
- File deletion is permanent and cannot be undone
- Related endpoints: GET /api/libraryfiles, POST /api/libraryfiles

---
