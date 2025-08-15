# Endpoints: Software Vulnerabilities Assessment

**Source:** get-assessment-software-vulnerabilities.md  
**Tags:** Assessment  

## Endpoint 1: GET /api/machines/SoftwareVulnerabilitiesByMachine

**Summary:** Export software vulnerabilities assessment (JSON response)  
**OperationId:** getSoftwareVulnerabilitiesByMachine

### Description
Retrieves all known software vulnerabilities and their details for all devices on a per-device basis as JSON responses with pagination support.

### Parameters
#### Query Parameters
- `pageSize` (integer, optional): Number of results in response (default 50,000, max 200,000)
- `$top` (integer, optional): Number of results to return (doesn't return @odata.nextLink)

### Request Body
None

### Responses
#### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetVulnerability)",
  "value": [
    {
      "id": "string",
      "deviceId": "string",
      "rbacGroupName": "string",
      "deviceName": "string",
      "osPlatform": "string",
      "osVersion": "string",
      "osArchitecture": "string",
      "softwareVendor": "string",
      "softwareName": "string",
      "softwareVersion": "string",
      "cveId": "string",
      "vulnerabilitySeverityLevel": "string",
      "recommendedSecurityUpdate": "string",
      "recommendedSecurityUpdateId": "string",
      "diskPaths": ["string"],
      "registryPaths": ["string"],
      "lastSeenTimestamp": "2020-12-30 14:17:26",
      "firstSeenTimestamp": "2020-12-30 11:07:15",
      "exploitabilityLevel": "string",
      "recommendationReference": "string",
      "securityUpdateAvailable": true
    }
  ],
  "@odata.nextLink": "string"
}
```

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

### Notes
- Best for small organizations with less than 100K devices
- Each record is approximately 1KB of data
- Maximum page size is 200,000 records
- Supports pagination with @odata.nextLink

---

## Endpoint 2: GET /api/machines/SoftwareVulnerabilitiesExport

**Summary:** Export software vulnerabilities assessment (via files)  
**OperationId:** getSoftwareVulnerabilitiesExport

### Description
Exports all software vulnerabilities data as downloadable files from Azure Storage, recommended for large organizations with more than 100K devices.

### Parameters
#### Query Parameters
- `sasValidHours` (integer, optional): Number of hours download URLs are valid (max 6 hours, default 1 hour)

### Request Body
None

### Responses
#### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportstrstgeus.blob.core.windows.net/tvm-export/..."
  ],
  "generatedTime": "2021-05-20T08:00:00Z"
}
```

### Rate Limits
- 5 calls per minute, 20 calls per hour

### Notes
- Files are GZIP compressed in multiline JSON format
- Download URLs valid for 1 hour (unless sasValidHours specified)
- Recommended for organizations with 100K+ devices
- Download from same Azure region for maximum speed

---

## Endpoint 3: GET /api/machines/SoftwareVulnerabilityChangesByMachine

**Summary:** Delta export software vulnerabilities assessment (JSON response)  
**OperationId:** getSoftwareVulnerabilityChangesByMachine

### Description
Returns changes in software vulnerabilities between a selected date and current date, showing new, fixed, and updated vulnerabilities.

### Parameters
#### Query Parameters
- `sinceTime` (string, required): Start time for data changes (max 14 days back)
- `pageSize` (integer, optional): Number of results in response (default 50,000, max 200,000)
- `$top` (integer, optional): Number of results to return (doesn't return @odata.nextLink)

### Request Body
None

### Responses
#### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.DeltaAssetVulnerability)",
  "value": [
    {
      "id": "string",
      "deviceId": "string",
      "rbacGroupName": "string",
      "deviceName": "string",
      "osPlatform": "string",
      "softwareVendor": "string",
      "softwareName": "string",
      "softwareVersion": "string",
      "cveId": "string",
      "vulnerabilitySeverityLevel": "string",
      "exploitabilityLevel": "string",
      "status": "string",
      "eventTimestamp": "2020-11-03 10:13:34.8476880",
      "firstSeenTimestamp": "2020-11-03 10:13:34.8476880",
      "lastSeenTimestamp": "2020-11-03 10:13:34.8476880"
    }
  ],
  "@odata.nextLink": "string"
}
```

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

### Notes
- **Status values**: New, Fixed, Updated
- **EventTimestamp**: When the delta event was found
- **RBAC duplicates**: Devices moving between RBAC groups appear twice
- **Recommended pattern**: Use full export for baseline, delta for staying current
- **Data refresh**: Full export refreshed every 6 hours
- **Maximum lookback**: 14 days

---

## Common Properties

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application) or Vulnerability.Read (Delegated)

### OData Support
- ✅ Pagination support with @odata.nextLink (endpoints 1 & 3)
- ❌ File export endpoint returns download URLs only

### Common Notes
- Part of Microsoft Defender Vulnerability Management
- Returns current snapshot of vulnerability state (not historic data)
- **ExploitabilityLevel values**: NoExploit, ExploitIsPublic, ExploitIsVerified, ExploitIsInKit
- **Severity levels**: Critical, High, Medium, Low, Informational
- **Platform support**: Windows 10, Windows 11, and other supported platforms
- Essential for comprehensive vulnerability management and remediation tracking

---
