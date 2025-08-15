# Endpoint: POST /api/indicators/import

**Source:** import-ti-indicators.md  
**Tags:** Indicators  
**Summary:** Import batch of threat indicators  
**OperationId:** importThreatIndicators

## Description
Submits or updates a batch of threat intelligence indicators with support for up to 500 indicators per request.

## Parameters
None (all parameters in request body)

## Request Body
```json
{
  "Indicators": [
    {
      "indicatorValue": "string",
      "indicatorType": "string",
      "title": "string",
      "application": "string",
      "expirationTime": "2021-12-12T00:00:00Z",
      "action": "string",
      "severity": "string",
      "description": "string",
      "recommendedActions": "string",
      "rbacGroupNames": ["string"]
    }
  ]
}
```
**Required:** Indicators (array of indicator objects)

## Responses
### 200 Success
```json
{
  "value": [
    {
      "id": "string",
      "indicator": "string",
      "isFailed": false,
      "failureReason": null
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
- 30 calls per minute

## OData Support
- ❌ Not applicable for batch import operations

## Example
```http
POST /api/indicators/import
Authorization: Bearer {token}
Content-Type: application/json

{
  "Indicators": [
    {
      "indicatorValue": "220e7d15b011d7fac48f2bd61114db1022197f7f",
      "indicatorType": "FileSha1",
      "title": "demo",
      "application": "demo-test",
      "expirationTime": "2021-12-12T00:00:00Z",
      "action": "Alert",
      "severity": "Informational",
      "description": "demo2",
      "recommendedActions": "nothing",
      "rbacGroupNames": ["group1", "group2"]
    },
    {
      "indicatorValue": "2233223322332233223322332233223322332233223322332233223322332222",
      "indicatorType": "FileSha256",
      "title": "demo2",
      "application": "demo-test2",
      "expirationTime": "2021-12-12T00:00:00Z",
      "action": "Alert",
      "severity": "Medium",
      "description": "demo2",
      "recommendedActions": "nothing",
      "rbacGroupNames": []
    }
  ]
}

Response:
{
  "value": [
    {
      "id": "2841",
      "indicator": "220e7d15b011d7fac48f2bd61114db1022197f7f",
      "isFailed": false,
      "failureReason": null
    },
    {
      "id": "2842",
      "indicator": "2233223322332233223322332233223322332233223322332233223322332222",
      "isFailed": false,
      "failureReason": null
    }
  ]
}
```

## Notes
- **Batch size limit**: Maximum 500 indicators per API call
- **Tenant limit**: Maximum 15,000 active indicators per tenant
- **Rate limit**: 30 calls per minute (lower than single indicator API)
- **CIDR notation**: Not supported for IP addresses
- **Response format**: Returns success/failure status for each indicator
- **Failure handling**: Individual indicators can fail while others succeed
- **Indicator types**: FileSha1, FileMd5, CertificateThumbprint, FileSha256, IpAddress, DomainName, Url
- **Actions**: Alert, Warn, Block, Audit, BlockAndRemediate, AlertAndBlock, Allowed
- **Severities**: Informational, Low, Medium, High
- **Efficient bulk operations**: Preferred method for importing large numbers of indicators

---
