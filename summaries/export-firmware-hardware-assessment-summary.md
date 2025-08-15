# Endpoints: Hardware and Firmware Assessment Export

**Source:** export-firmware-hardware-assessment.md  
**Tags:** Assessment  
**Summary:** Export hardware and firmware inventory data  

## Endpoint 1: GET /api/machines/HardwareFirmwareInventoryByMachine

**OperationId:** getHardwareFirmwareInventoryByMachine

### Description
Returns hardware and firmware assessment data for all devices via JSON response (recommended for <100K devices).

### Parameters
### Query Parameters  
- `pageSize` (integer, optional): Number of results in response (default: 50,000, max: 200,000)
- `$top` (integer, optional): Number of results to return

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetHardwareFirmware)",
  "value": [
    {
      "deviceId": "49126b9e4a5473b5229c73799e9e55c48668101b",
      "rbacGroupId": 39,
      "rbacGroupName": "testO6343398Gq31",
      "deviceName": "testmachine5",
      "componentType": "Hardware",
      "manufacturer": "razer",
      "componentName": "blade_15_advanced_model_(mid_2021)_-_rz09-0409",
      "componentVersion": "7.04",
      "additionalFields": "{\"SystemSKU\":\"RZ09-0409CE53\",\"BaseBoardManufacturer\":\"Razer\"}"
    }
  ]
}
```

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

---

## Endpoint 2: GET /api/machines/HardwareFirmwareInventoryExport

**OperationId:** exportHardwareFirmwareInventory

### Description
Returns hardware and firmware assessment data via file download URLs (recommended for >100K devices).

### Parameters
### Query Parameters  
- `sasValidHours` (integer, optional): Hours download URLs remain valid (max: 6, default: 1)

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportstrprdcane.blob.core.windows.net/tvm-firmware-export/2022-07-11/1101/FirmwareHardwareExport/json/OrgId=3837d1f5-0d51-40cb-a99d-69ebedc9dcc8/_RbacGroupId=39/part-00999-71eea973-1bb1-4d0a-829d-80cb07aff5d8.c000.json.gz"
  ],
  "generatedTime": "2022-07-11T11:01:00Z"
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
- Permission: `Software.Read.All` (Application) or `Software.Read` (Delegated)

### OData Support
- ✅ JSON endpoint supports pagination via @odata.nextLink
- ✅ $top parameter supported (JSON endpoint)
- ❌ File export doesn't support OData queries

## Example
```http
GET /api/machines/HardwareFirmwareInventoryByMachine?pageSize=50000
Authorization: Bearer {token}

GET /api/machines/HardwareFirmwareInventoryExport?sasValidHours=6
Authorization: Bearer {token}
```

## Notes
- Files are gzip compressed in multiline JSON format
- Each record is approximately 1KB of data
- Returns separate entry for every unique combination of deviceId and componentType

---
