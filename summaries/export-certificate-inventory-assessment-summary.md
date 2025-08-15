# Endpoints: Certificate Inventory Assessment Export

**Source:** export-certificate-inventory-assessment.md  
**Tags:** Assessment  
**Summary:** Export certificate inventory assessment data  

## Endpoint 1: GET /api/machines/certificateAssessmentByMachine

**OperationId:** getCertificateAssessmentByMachine

### Description
Returns certificate assessment data for all devices via JSON response (recommended for <100K devices).

### Parameters
### Query Parameters  
- `pageSize` (integer, optional): Number of results in response (default: 50,000, max: 200,000)
- `$top` (integer, optional): Number of results to return

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetCertificateAssessment)",
  "value": [
    {
      "deviceId": "49126b9e4a5473b5229c73799e9e55c48668101b",
      "deviceName": "testmachine5",
      "thumbprint": "A4B37F4F6DE956922273D5CB8E7E0AAFB7033B90",
      "path": "LocalMachine\\TestSignRoot\\A4B37F4F6DE956922273D5CB8E7E0AAFB7033B90",
      "signatureAlgorithm": "sha384ECDSA",
      "serialNumber": "6086A185EAFA2B9943B4671603F40323",
      "rbacGroupId": 4226,
      "rbacGroupName": "testO6343398Gq31"
    }
  ],
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/machines/certificateAssessmentByMachine?pagesize=1&$skiptoken=..."
}
```

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

---

## Endpoint 2: GET /api/machines/certificateAssessmentExport

**OperationId:** exportCertificateAssessment

### Description
Returns certificate assessment data via file download URLs (recommended for >100K devices).

### Parameters
### Query Parameters  
- `sasValidHours` (integer, optional): Hours download URLs remain valid (max: 24, default: 3)

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportexternalstgeus.blob.core.windows.net/temp-5c080622-f613-42bb-9fee-e17ccdff90d3/2022-03-20/1318/CertificateAssessmentExport/json/OrgId=47d41a0c-188d-46d3-bbea-a93dbc0bfcaa/_RbacGroupId=4226/part-00000-65a62a9d-7a01-4d78-bbdb-6d3e07b34cc9.c000.json.gz"
  ],
  "generatedTime": "2022-03-20T13:18:00Z"
}
```

### Rate Limits
- 5 calls per minute, 20 calls per hour

---

## Common Properties

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Vulnerability.Read.All` (Application) or `Vulnerability.Read` (Delegated)

### OData Support
- ✅ JSON endpoint supports pagination via @odata.nextLink
- ✅ $top parameter supported (JSON endpoint)
- ❌ File export doesn't support OData queries

## Example
```http
GET /api/machines/certificateAssessmentByMachine?pageSize=50000
Authorization: Bearer {token}

GET /api/machines/certificateAssessmentExport?sasValidHours=6
Authorization: Bearer {token}
```

## Notes
- Files are gzip compressed in multiline JSON format
- Each record is approximately 1KB of data
- Data represents current snapshot, not historical data

---
