# Endpoints: Software Inventory Assessment

**Source:** get-assessment-software-inventory.md  
**Tags:** Assessment  

## Endpoint 1: GET /api/machines/SoftwareInventoryByMachine

**Summary:** Export software inventory assessment (JSON)  
**OperationId:** getSoftwareInventoryByMachine

### Description
Returns all installed software that has a Common Platform Enumeration (CPE) per device via JSON response with pagination support.

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
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(contoso.windowsDefenderATP.api.AssetSoftware)",
  "value": [
    {
      "deviceId": "string",
      "rbacGroupName": "string",
      "deviceName": "string",
      "osPlatform": "string",
      "softwareVendor": "string",
      "softwareName": "string",
      "softwareVersion": "string",
      "numberOfWeaknesses": 0,
      "diskPaths": ["string"],
      "registryPaths": ["string"],
      "softwareFirstSeenTimestamp": "2019-04-07 02:06:47",
      "endOfSupportStatus": "string",
      "endOfSupportDate": "2020-12-30T00:00:00+00:00"
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

## Endpoint 2: GET /api/machines/SoftwareInventoryExport

**Summary:** Export software inventory assessment (files)  
**OperationId:** exportSoftwareInventory

### Description
Returns all CPE software inventory data as downloadable files from Azure Storage, recommended for large organizations with more than 100K devices.

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
  "generatedTime": "2021-01-11T11:01:00Z"
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
GET /api/machines/SoftwareInventoryByMachine?pageSize=5&sinceTime=2021-05-19T18%3A35%3A49.924Z
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(contoso.windowsDefenderATP.api.AssetSoftware)",
  "value": [
    {
      "deviceId": "00044f68765bbaf712342dbe6db733b6a9c59ab4",
      "rbacGroupName": "hhh",
      "deviceName": "ComputerPII_18993b45912eeb224b2be2f5ea3142726e63f16a.DomainPII_21eeb80d086e79dbfa178eadfa25e8de9acfa346.corp.contoso.com",
      "osPlatform": "Windows10",
      "softwareVendor": "microsoft",
      "softwareName": "windows_10",
      "softwareVersion": "10.0.17763.1637",
      "numberOfWeaknesses": 58,
      "diskPaths": [],
      "registryPaths": [],
      "softwareFirstSeenTimestamp": "2020-12-30 11:07:15",
      "endOfSupportStatus": "Upcoming EOS Version",
      "endOfSupportDate": "2021-05-11T00:00:00+00:00"
    }
  ],
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/machines/SoftwareInventoryByMachine?pagesize=5&$skiptoken=..."
}
```

## Notes
- Covers software with Common Platform Enumeration (CPE) identifiers
- JSON method best for organizations with less than 100K devices
- File export method recommended for large organizations with more than 100K devices
- Files are GZIP compressed in multiline JSON format
- Each record is approximately 0.5KB of data
- Includes vulnerability counts, installation paths, and end-of-support information
- Complements non-CPE software inventory for complete visibility

---
