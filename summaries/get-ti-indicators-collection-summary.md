# Endpoint: GET /api/indicators

**Source:** get-ti-indicators-collection.md  
**Tags:** Indicators  
**Summary:** List all active threat indicators  
**OperationId:** getThreatIndicators

## Description
Retrieves a collection of all active threat intelligence indicators with comprehensive OData V4 query support for filtering and pagination.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on application, createdByDisplayName, expirationTime, generateAlert, title, rbacGroupNames, rbacGroupIds, indicatorValue, indicatorType, creationTimeDateTimeUtc, createdBy, action, severity
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Indicators",
  "value": [
    {
      "id": "string",
      "indicatorValue": "string",
      "indicatorType": "string",
      "action": "string",
      "application": "string",
      "source": "string",
      "sourceType": "string",
      "title": "string",
      "creationTimeDateTimeUtc": "2018-10-24T11:15:35.3688259Z",
      "createdBy": "string",
      "expirationTime": "2020-12-12T00:00:00Z",
      "lastUpdateTime": "2019-10-24T10:54:23.2009016Z",
      "lastUpdatedBy": "string",
      "severity": "string",
      "description": "string",
      "recommendedActions": "string",
      "rbacGroupNames": ["string"]
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Ti.ReadWrite (Application), Ti.ReadWrite.All (Application), Ti.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ✅ $filter: application, createdByDisplayName, expirationTime, generateAlert, title, rbacGroupNames, rbacGroupIds, indicatorValue, indicatorType, creationTimeDateTimeUtc, createdBy, action, severity
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/indicators?$filter=action eq 'AlertAndBlock'&$top=100
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Indicators",
  "value": [
    {
      "id": "997",
      "indicatorValue": "111e7d15b0b3d7fac48f2bd61114db1022197f7f",
      "indicatorType": "FileSha1",
      "action": "AlertAndBlock",
      "application": null,
      "source": "TestPrdApp",
      "sourceType": "AadApp",
      "title": "test",
      "creationTimeDateTimeUtc": "2018-10-24T10:54:23.2009016Z",
      "createdBy": "45097602-1234-5678-1234-9f453233e62c",
      "expirationTime": "2020-12-12T00:00:00Z",
      "lastUpdateTime": "2019-10-24T10:54:23.2009016Z",
      "lastUpdatedBy": "TestPrdApp",
      "severity": "Informational",
      "description": "test",
      "recommendedActions": "TEST",
      "rbacGroupNames": ["Group1", "Group2"]
    }
  ]
}
```

## Notes
- **Permission scope**: Ti.ReadWrite.All shows all indicators; Ti.ReadWrite shows only indicators created by the application
- **Indicator types**: FileSha1, FileMd5, CertificateThumbprint, FileSha256, IpAddress, DomainName, Url
- **Actions**: Alert, Warn, Block, Audit, BlockAndRemediate, AlertAndBlock, Allowed
- **Severities**: Informational, Low, Medium, High
- **Source types**: AadApp, User
- **RBAC groups**: Can be filtered and targeted for specific groups
- **Expiration**: Indicators can have expiration times
- **Maximum 10,000 results** per query
- **Comprehensive filtering**: 12 filterable fields for precise queries
- Essential for threat intelligence management and IOC tracking

---
