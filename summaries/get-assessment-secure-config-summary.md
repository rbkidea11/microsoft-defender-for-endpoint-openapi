# Endpoints: Secure Configuration Assessment

**Source:** get-assessment-secure-config.md  
**Tags:** Assessment  

## Endpoint 1: GET /api/machines/SecureConfigurationsAssessmentByMachine

**Summary:** Export secure configuration assessment (JSON)  
**OperationId:** getSecureConfigurationsAssessmentByMachine

### Description
Returns all configurations and their status on a per-device basis via JSON response with pagination support.

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
  "@odata.context": "api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetConfiguration)",
  "value": [
    {
      "deviceId": "string",
      "rbacGroupName": "string",
      "deviceName": "string",
      "osPlatform": "string",
      "osVersion": "string",
      "timestamp": "2021-01-11 09:47:58.854",
      "configurationId": "string",
      "configurationCategory": "string",
      "configurationSubcategory": "string",
      "configurationImpact": 0,
      "isCompliant": true,
      "isApplicable": true,
      "isExpectedUserImpact": false,
      "configurationName": "string",
      "recommendationReference": "string"
    }
  ],
  "@odata.nextLink": "string"
}
```

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application) or Vulnerability.Read (Delegated)

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

### OData Support
- ✅ Pagination via @odata.nextLink
- ✅ $top parameter supported

---

## Endpoint 2: GET /api/machines/SecureConfigurationsAssessmentExport

**Summary:** Export secure configuration assessment (files)  
**OperationId:** exportSecureConfigurationsAssessment

### Description
Returns all secure configuration assessment data as downloadable files from Azure Storage, recommended for large organizations with more than 100K devices.

### Parameters
#### Query Parameters
- `sasValidHours` (integer, optional): Number of hours download URLs are valid (max 6 hours, default 1 hour)

### Request Body
None

### Responses
#### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#contoso.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "string"
  ],
  "generatedTime": "2021-01-11T11:01:00Z"
}
```

### Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Vulnerability.Read.All (Application) or Vulnerability.Read (Delegated)

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
GET /api/machines/SecureConfigurationsAssessmentByMachine?pageSize=5
Authorization: Bearer {token}

Response:
{
  "@odata.context": "api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetConfiguration)",
  "value": [
    {
      "deviceId": "00013ee62c6b12345b10214e1801b217b50ab455c293d",
      "rbacGroupName": "hhh",
      "deviceName": "ComputerPII_5d96860d69c73fdd06fc8d1679e1eb73eceb8330",
      "osPlatform": "Windows10",
      "osVersion": "NT kernel 6.x",
      "timestamp": "2021-01-11 09:47:58.854",
      "configurationId": "scid-10000",
      "configurationCategory": "Network",
      "configurationSubcategory": "",
      "configurationImpact": 5,
      "isCompliant": true,
      "isApplicable": true,
      "isExpectedUserImpact": false,
      "configurationName": "Disable insecure administration protocol - Telnet",
      "recommendationReference": "sca-_-scid-10000"
    }
  ],
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/machines/SecureConfigurationsAssessmentByMachine?pagesize=5&$skiptoken=..."
}
```

## Notes
- JSON method best for organizations with less than 100K devices
- File export method recommended for large organizations with more than 100K devices
- Files are GZIP compressed in multiline JSON format
- Returns entry for every unique combination of DeviceId and ConfigurationId
- Includes compliance status and impact ratings for security configurations
- Covers categories: Application, OS, Network, Accounts, Security controls

---
