# Endpoints: Non-CPE Software Inventory Assessment

**Source:** get-assessment-non-cpe-software-inventory.md  
**Tags:** Assessment  

## Endpoint 1: GET /api/machines/SoftwareInventoryNoProductCodeByMachine

**Summary:** Export non-CPE software inventory (JSON)  
**OperationId:** getNonCpeSoftwareInventoryByMachine

### Description
Returns all installed software that doesn't have a Common Platform Enumeration (CPE) per device via JSON response with pagination support.

### Parameters
#### Query Parameters
- `pageSize` (integer, optional): Number of results in response (default 50,000, max 200,000)
- `$top` (integer, optional): Number of results to return (doesn't return @odata.nextLink)
- `sinceTime` (string, optional): Filter results since specified time

### Request Body
None

### Responses
#### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetNonCpeSoftware)",
  "value": [
    {
      "deviceId": "string",
      "rbacGroupId": 0,
      "rbacGroupName": "string",
      "deviceName": "string",
      "osPlatform": "string",
      "softwareVendor": "string",
      "softwareName": "string",
      "softwareVersion": "string",
      "softwareLastSeenTimestamp": "2021-01-30 11:31:12.271"
    }
  ],
  "@odata.nextLink": "string"
}
```

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All (Application) or Software.Read (Delegated)

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

### OData Support
- ✅ Pagination via @odata.nextLink
- ✅ $top parameter supported

---

## Endpoint 2: GET /api/machines/SoftwareInventoryNonCpeExport

**Summary:** Export non-CPE software inventory (files)  
**OperationId:** exportNonCpeSoftwareInventory

### Description
Returns all non-CPE software data as downloadable files from Azure Storage, recommended for large organizations with more than 100K devices.

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
    "string"
  ],
  "generatedTime": "2022-05-30T11:01:00Z"
}
```

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All (Application) or Software.Read (Delegated)

### Rate Limits
- 5 calls per minute, 20 calls per hour

### OData Support
- ❌ Not applicable for file export operations

---

## Common Properties

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Example
```http
GET /api/machines/SoftwareInventoryNoProductCodeByMachine?pageSize=3&sinceTime=2021-05-19
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetNonCpeSoftware)",
  "value": [
    {
      "deviceId": "1234512345123451234512345",
      "rbacGroupId": 11,
      "rbacGroupName": "London",
      "deviceName": "Device1",
      "osPlatform": "Windows11",
      "softwareVendor": "microsoft",
      "softwareName": "vs_communitymsi",
      "softwareVersion": "11.11.31111.1",
      "softwareLastSeenTimestamp": "2021-01-30 11:31:12.271"
    },
    {
      "deviceId": "232323232323232322323232323",
      "rbacGroupId": 23,
      "rbacGroupName": "Tokyo",
      "deviceName": "Device23",
      "osPlatform": "Windows10",
      "softwareVendor": "intel",
      "softwareName": "intel®_software_installer",
      "softwareVersion": "22.20.2.2",
      "softwareLastSeenTimestamp": "2022-05-30 15:35:12.271"
    }
  ],
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/machines/SoftwareInventoryNoProductCodeByMachine?pagesize=3%20%20&sincetime=2021-05-19&$skiptoken=..."
}
```

## Notes
- Covers software without Common Platform Enumeration (CPE) identifiers
- JSON method best for organizations with less than 100K devices
- File export method recommended for large organizations with more than 100K devices
- Files are GZIP compressed in multiline JSON format
- Each record is approximately 0.5KB of data
- Complements regular software inventory for complete visibility
- Vulnerability management doesn't support non-CPE software products

---
