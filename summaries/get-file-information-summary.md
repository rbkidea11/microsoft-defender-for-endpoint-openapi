# Endpoint: GET /api/files/{id}

**Source:** get-file-information.md  
**Tags:** File  
**Summary:** Get file information by identifier  
**OperationId:** getFileInformation

## Description
Retrieves file information by identifier (SHA1, SHA256, or MD5) including metadata, prevalence, and security details.

## Parameters
### Path Parameters
- `id` (string, required): File identifier (SHA1, SHA256, or MD5 hash)

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Files/$entity",
  "sha1": "string",
  "sha256": "string",
  "globalPrevalence": 0,
  "globalFirstObserved": "2017-09-19T03:51:27.6785431Z",
  "globalLastObserved": "2020-01-06T03:59:21.3229314Z",
  "size": 0,
  "fileType": "string",
  "isPeFile": true,
  "filePublisher": "string",
  "fileProductName": "string",
  "signer": "string",
  "issuer": "string",
  "signerHash": "string",
  "isValidCertificate": false,
  "determinationType": "string",
  "determinationValue": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: File.Read.All (Application) or File.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for single file retrieval

## Example
```http
GET /api/files/4388963aaa83afe2042a46a3c017ad50bdcdafb3
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.security.microsoft.com/api/$metadata#Files/$entity",
  "sha1": "4388963aaa83afe2042a46a3c017ad50bdcdafb3",
  "sha256": "413c58c8267d2c8648d8f6384bacc2ae9c929b2b96578b6860b5087cd1bd6462",
  "globalPrevalence": 180022,
  "globalFirstObserved": "2017-09-19T03:51:27.6785431Z",
  "globalLastObserved": "2020-01-06T03:59:21.3229314Z",
  "size": 22139496,
  "fileType": "APP",
  "isPeFile": true,
  "filePublisher": "CHENGDU YIWO Tech Development Co., Ltd.",
  "fileProductName": "EaseUS MobiSaver for Android",
  "signer": "CHENGDU YIWO Tech Development Co., Ltd.",
  "issuer": "VeriSign Class 3 Code Signing 2010 CA",
  "signerHash": "6c3245d4a9bc0244d99dff27af259cbbae2e2d16",
  "isValidCertificate": false,
  "determinationType": "Pua",
  "determinationValue": "PUA:Win32/FusionCore"
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Supports SHA1, SHA256, and MD5 file identifiers
- Returns 404 if file doesn't exist in Microsoft's database
- Includes comprehensive file metadata and security assessment
- Useful for file reputation analysis and threat investigation

---
