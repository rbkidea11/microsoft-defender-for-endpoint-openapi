# Endpoint: POST /api/alerts/batchUpdate

**Source:** batch-update-alerts.md  
**Tags:** Alert  
**Summary:** Batch update multiple alerts  
**OperationId:** batchUpdateAlerts

## Description
Updates multiple alerts in a single batch operation for status, determination, classification, and assignment.

## Request Body
```json
{
  "alertIds": ["string", "string"],
  "status": "New|InProgress|Resolved",
  "assignedTo": "string",
  "classification": "TruePositive|FalsePositive|Informational",
  "determination": "Malware|Phishing|SuspiciousActivity|Unwanted|Other",
  "comment": "string"
}
```
**Required:** alertIds

## Responses
### 200 Success
```json
{
  "value": [
    {
      "id": "da637472900382838869_1364969609",
      "status": "InProgress",
      "assignedTo": "analyst@contoso.com",
      "classification": "TruePositive",
      "determination": "Malware",
      "lastUpdateTime": "2023-08-11T10:35:00.0000000Z"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Alert.ReadWrite.All` (Application) or `Alert.ReadWrite` (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for POST operations

## Example
```http
POST /api/alerts/batchUpdate
Authorization: Bearer {token}
Content-Type: application/json

{
  "alertIds": ["da637472900382838869_1364969609", "da637472900382838869_1364969610"],
  "status": "InProgress",
  "assignedTo": "analyst@contoso.com",
  "classification": "TruePositive",
  "determination": "Malware",
  "comment": "Investigating suspicious activity"
}
```

## Notes
- All specified alerts will be updated with the same values
- For individual alert updates, use PATCH /api/alerts/{id}
- Related endpoints: GET /api/alerts, PATCH /api/alerts/{id}

---
