# Endpoint: POST /api/indicators

**Source:** post-ti-indicator.md  
**Tags:** Indicators  
**Summary:** Submit or update threat indicator  
**OperationId:** submitThreatIndicator

## Description
Submits or updates a new threat intelligence indicator entity with comprehensive configuration options for detection and response actions.

## Parameters
None (all parameters in request body)

## Request Body
```json
{
  "indicatorValue": "string",
  "indicatorType": "string",
  "action": "string",
  "application": "string",
  "title": "string",
  "description": "string",
  "expirationTime": "2020-12-12T00:00:00Z",
  "severity": "string",
  "recommendedActions": "string",
  "rbacGroupNames": ["string"],
  "educateUrl": "string",
  "generateAlert": true
}
```
**Required:** indicatorValue, indicatorType, action, title, description  
**Optional:** application, expirationTime, severity, recommendedActions, rbacGroupNames, educateUrl, generateAlert

## Responses
### 200 Success
```json
{
  "id": "string",
  "indicatorValue": "string",
  "indicatorType": "string",
  "action": "string",
  "application": "string",
  "title": "string",
  "description": "string",
  "creationTimeDateTimeUtc": "2020-01-01T00:00:00Z",
  "createdBy": "string",
  "expirationTime": "2020-12-12T00:00:00Z",
  "lastUpdateTime": "2020-01-01T00:00:00Z",
  "lastUpdatedBy": "string",
  "severity": "string",
  "recommendedActions": "string",
  "rbacGroupNames": ["string"],
  "educateUrl": "string",
  "generateAlert": true
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
- ❌ Not applicable for indicator submission

## Example
```http
POST /api/indicators
Authorization: Bearer {token}
Content-Type: application/json

{
  "indicatorValue": "220e7d15b011d7fac48f2bd61114db1022197f7f",
  "indicatorType": "FileSha1",
  "title": "test",
  "application": "demo-test",
  "expirationTime": "2020-12-12T00:00:00Z",
  "action": "AlertAndBlock",
  "severity": "Informational",
  "description": "test",
  "recommendedActions": "nothing",
  "rbacGroupNames": ["group1", "group2"]
}

Response:
{
  "id": "994",
  "indicatorValue": "220e7d15b011d7fac48f2bd61114db1022197f7f",
  "indicatorType": "FileSha1",
  "title": "test",
  "application": "demo-test",
  "expirationTime": "2020-12-12T00:00:00Z",
  "action": "AlertAndBlock",
  "severity": "Informational",
  "description": "test",
  "recommendedActions": "nothing",
  "rbacGroupNames": ["group1", "group2"],
  "creationTimeDateTimeUtc": "2020-09-10T08:17:03.739Z",
  "createdBy": "admin@contoso.com",
  "lastUpdateTime": "2020-09-10T08:17:03.739Z",
  "lastUpdatedBy": "admin@contoso.com",
  "generateAlert": true
}
```

## Notes
- **Tenant limit**: Maximum 15,000 active indicators per tenant
- **CIDR notation**: Not supported for IP addresses
- **Indicator types**: FileSha1, FileMd5, CertificateThumbprint, FileSha256, IpAddress, DomainName, Url
- **Actions**: Alert, Warn, Block, Audit, BlockAndRemediate, AlertAndBlock, Allowed
- **Severities**: Informational, Low, Medium, High
- **Application field**: Only works for new indicators, doesn't update existing ones
- **GenerateAlert requirement**: Must be TRUE when creating Audit action
- **educateUrl**: Supported for Block and Warn actions on URL indicators only
- **RBAC groups**: Comma-separated list for targeted application

---
