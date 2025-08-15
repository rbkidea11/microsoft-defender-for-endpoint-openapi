# Endpoints: Device Health Export

**Source:** device-health-export-antivirus-health-report-api.md  
**Tags:** DeviceHealth  
**Summary:** Export device health and antivirus status data  

## Endpoint 1: GET /api/deviceavinfo

**OperationId:** getDeviceAntivirusInfo

### Description
Returns device antivirus health information via JSON response.

### Responses
### 200 Success
```json
{
  "value": [
    {
      "deviceId": "string",
      "deviceName": "string",
      "antivirusStatus": "string",
      "lastScanTime": "datetime",
      "definitionVersion": "string",
      "engineVersion": "string"
    }
  ]
}
```

---

## Endpoint 2: GET /api/machines/InfoGatheringExport

**OperationId:** exportInfoGathering

### Description
Returns device information gathering assessment data via file download URLs.

### Parameters
### Query Parameters  
- `sasValidHours` (integer, optional): Hours download URLs remain valid

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportexternalstgeus.blob.core.windows.net/temp-export/InfoGatheringExport.json.gz"
  ],
  "generatedTime": "2023-08-11T10:30:00Z"
}
```

---

## Common Properties

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Device health read permissions

### Rate Limits
- Standard API rate limits apply

### OData Support
- ✅ JSON endpoint may support pagination
- ❌ File export doesn't support OData queries

## Example
```http
GET /api/deviceavinfo
Authorization: Bearer {token}

GET /api/machines/InfoGatheringExport?sasValidHours=6
Authorization: Bearer {token}
```

## Notes
- Device health data includes antivirus status, scan times, and version information
- File export method provides comprehensive device information gathering data

---
