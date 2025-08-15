# Endpoint: GET /api/alerts/{id}/files

**Source:** get-alert-related-files-info.md  
**Tags:** Alert  
**Summary:** Get files related to alert  
**OperationId:** getAlertRelatedFiles

## Description
Retrieves all files related to a specific alert including file hashes, metadata, and security information.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Files",
  "value": [
    {
      "sha1": "string",
      "sha256": "string",
      "md5": "string",
      "globalPrevalence": 0,
      "globalFirstObserved": "2019-03-23T23:54:06.0135204Z",
      "globalLastObserved": "2019-04-23T00:43:20.0489831Z",
      "size": 0,
      "fileType": "string",
      "isPeFile": true,
      "filePublisher": "string",
      "fileProductName": "string",
      "signer": "string",
      "issuer": "string",
      "signerHash": "string",
      "isValidCertificate": true,
      "determinationType": "string",
      "determinationValue": "string"
    }
  ]
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
- ❌ Not applicable for related resource retrieval

## Example
```http
GET /api/alerts/636688558380765161_2136280442/files
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Files",
  "value": [
    {
      "sha1": "f2a00fd2f2de1be0214b8529f1e9f67096c1aa70",
      "sha256": "dcd71ef5fff4362a9f64cf3f96f14f2b11d6f428f3badbedcb9ff3361e7079aa",
      "md5": "8d5b7cc9a832e21d22503057e1fec8e9",
      "globalPrevalence": 29,
      "globalFirstObserved": "2019-03-23T23:54:06.0135204Z",
      "globalLastObserved": "2019-04-23T00:43:20.0489831Z",
      "size": 113984,
      "fileType": null,
      "isPeFile": true,
      "filePublisher": "Microsoft Corporation",
      "fileProductName": "Microsoft© Windows© Operating System",
      "signer": "Microsoft Corporation",
      "issuer": "Microsoft Code Signing PCA",
      "signerHash": "9dc17888b5cfad98b3cb35c1994e96227f061675",
      "isValidCertificate": true,
      "determinationType": "Unknown",
      "determinationValue": null
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period
- Provides comprehensive file metadata for threat analysis

---
