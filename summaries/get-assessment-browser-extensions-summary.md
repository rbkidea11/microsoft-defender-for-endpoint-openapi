# Endpoints: Browser Extensions Assessment

**Source:** get-assessment-browser-extensions.md  
**Tags:** BrowserExtensions  

## Endpoint 1: GET /api/Machines/BrowserExtensionsInventoryByMachine

**Summary:** Export browser extensions assessment (JSON)  
**OperationId:** getBrowserExtensionsInventoryByMachine

### Description
Returns all known installed browser extensions and their details for all devices on a per-device basis via JSON response with pagination support.

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
      "DeviceId": "string",
      "DeviceName": "string",
      "RbacGroupId": 0,
      "RbacGroupName": "string",
      "InstallationTime": "2022-05-26T18:46:27.000Z",
      "BrowserName": "string",
      "ExtensionId": "string",
      "ExtensionName": "string",
      "ExtensionDescription": "string",
      "ExtensionVersion": "string",
      "ExtensionRisk": "string",
      "IsActivated": true,
      "Permissions": [
        {
          "Id": "string",
          "IsRequired": true,
          "Risk": "string"
        }
      ]
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

## Endpoint 2: GET /api/machines/browserextensionsinventoryExport

**Summary:** Export browser extensions assessment (files)  
**OperationId:** exportBrowserExtensionsInventory

### Description
Returns all browser extensions data as downloadable files from Azure Storage, recommended for large organizations with more than 100K devices.

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
GET /api/Machines/BrowserExtensionsInventoryByMachine?pageSize=5
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(contoso.windowsDefenderATP.api.AssetSoftware)",
  "value": [
    {
      "DeviceId": "1c32162b42e9efa1f5de42f951775f22f435c997",
      "DeviceName": "computerpii_1363c2e016e2225cb03974df58f14e6968067aa8.domainpii_f260e982985f7e8eee198b4332e0ae5b2a069cd6.corp.microsoft.com",
      "RbacGroupId": 86,
      "RbacGroupName": "UnassignedGroup",
      "InstallationTime": "2022-05-26T18:46:27.000Z",
      "BrowserName": "chrome",
      "ExtensionId": "dkpejdfnpdkhifgbancbammdijojoffk",
      "ExtensionName": "Logitech Smooth Scrolling",
      "ExtensionDescription": "Buttery-smooth scrolling for Logitech mice and touchpads.",
      "ExtensionVersion": "6.65.62",
      "ExtensionRisk": "High",
      "IsActivated": true,
      "Permissions": [
        {
          "Id": "tabs",
          "IsRequired": true,
          "Risk": "High"
        }
      ]
    }
  ],
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/Machines/BrowserExtensionsInventoryByMachine?pagesize=5&$skiptoken=..."
}
```

## Notes
- JSON method best for organizations with less than 100K devices
- File export method recommended for large organizations with more than 100K devices
- Files are GZIP compressed in multiline JSON format
- Each record is approximately 0.5KB of data
- Includes comprehensive browser extension risk assessment and permissions analysis

---
