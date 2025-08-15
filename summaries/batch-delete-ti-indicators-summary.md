# Endpoint: POST /api/indicators/BatchDelete

**Source:** batch-delete-ti-indicators.md  
**Tags:** Indicators  
**Summary:** Batch delete up to 500 threat intelligence indicators  
**OperationId:** batchDeleteIndicators

## Description
Deletes multiple threat intelligence indicators in a single batch operation (up to 500 indicators).

## Request Body
```json
{
  "indicatorIds": ["string", "string", "string"]
}
```
**Required:** indicatorIds

## Responses
### 200 Success
```json
{
  "value": [
    {
      "id": "995",
      "indicator": "12.13.14.15",
      "isFailed": false,
      "failureReason": null
    },
    {
      "id": "997",
      "indicator": "invalid-indicator-id",
      "isFailed": true,
      "failureReason": "Indicator not found"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Ti.ReadWrite` or `Ti.ReadWrite.All`

## Rate Limits
- 30 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/indicators/BatchDelete
Authorization: Bearer {token}
Content-Type: application/json

{
  "indicatorIds": ["995", "996", "997", "998"]
}
```

## Notes
- Maximum 500 indicators per batch request
- Partial failures supported - some indicators may be deleted while others fail
- Related endpoints: DELETE /api/indicators/{id}, POST /api/indicators

---
