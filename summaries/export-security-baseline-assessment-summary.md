# Endpoints: Security Baseline Assessment Export

**Source:** export-security-baseline-assessment.md  
**Tags:** Assessment  
**Summary:** Export security baseline assessment data  

## Endpoint 1: GET /api/machines/baselineComplianceAssessmentByMachine

**OperationId:** getBaselineComplianceAssessmentByMachine

### Description
Returns security baseline assessment data for all devices via JSON response (recommended for <100K devices).

### Parameters
### Query Parameters  
- `pageSize` (integer, optional): Number of results in response (default: 50,000, max: 200,000)
- `$top` (integer, optional): Number of results to return

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Collection(microsoft.windowsDefenderATP.api.AssetBaselineAssessment)",
  "value": [
    {
      "id": "0000682575d5d473e82ed4d8680425d152411251_9e1b90be-e83e-485b-a5ec-4a429412e734_1.1.1",
      "configurationId": "1.1.1",
      "deviceId": "0000682575d5d473242222425d152411251",
      "deviceName": "ComputerPII_365f5c0bb7202c163937dad3d017969b2d760eb4.DomainPII_29596",
      "profileId": "9e1b90be-e83e-485b-a5ec-4a429412e734",
      "osPlatform": "WindowsServer2019",
      "osVersion": "10.0.17763.2330",
      "rbacGroupId": 86,
      "rbacGroupName": "UnassignedGroup",
      "isApplicable": true,
      "isCompliant": false,
      "dataCollectionTimeOffset": "2021-12-22T00:08:02.478Z",
      "recommendedValue": ["Greater than or equal '24'"],
      "currentValue": ["24"],
      "source": ["password_hist_len"]
    }
  ]
}
```

### Rate Limits
- 30 calls per minute, 1,000 calls per hour

---

## Endpoint 2: GET /api/machines/BaselineComplianceAssessmentExport

**OperationId:** exportBaselineComplianceAssessment

### Description
Returns security baseline assessment data via file download URLs (recommended for >100K devices).

### Parameters
### Query Parameters  
- `sasValidHours` (integer, optional): Hours download URLs remain valid (max: 6, default: 1)

### Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#microsoft.windowsDefenderATP.api.ExportFilesResponse",
  "exportFiles": [
    "https://tvmexportexternalstgeus.blob.core.windows.net/temp-1ebd3d09-d06a-4aad-ab80-ebc536cec61c/2021-12-22/0500/BaselineAssessmentExport/json/OrgId=<OrgId>/_RbacGroupId=<RbacGroupId>/part-00000-c09dfd00-2278-4735-b23a-71733751fcbc.c000.json.gz"
  ],
  "generatedTime": "2021-01-11T11:01:00Z"
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
- Permission: `SecurityBaselinesAssessment.Read.All` (Application) or `SecurityBaselinesAssessment.Read` (Delegated)

### OData Support
- ✅ JSON endpoint supports pagination via @odata.nextLink
- ✅ $top parameter supported (JSON endpoint)
- ❌ File export doesn't support OData queries

## Example
```http
GET /api/machines/baselineComplianceAssessmentByMachine?pageSize=50000
Authorization: Bearer {token}

GET /api/machines/BaselineComplianceAssessmentExport?sasValidHours=6
Authorization: Bearer {token}
```

## Notes
- Files are gzip compressed in multiline JSON format
- Each record is approximately 1KB of data
- Returns separate entry for every unique combination of DeviceId, ProfileId, ConfigurationId
- Related endpoints: GET /api/baselineProfiles, GET /api/baselineConfigurations

---
