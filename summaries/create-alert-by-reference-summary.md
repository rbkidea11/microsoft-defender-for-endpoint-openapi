# Endpoint: POST /api/alerts/CreateAlertByReference

**Source:** create-alert-by-reference.md  
**Tags:** Alert  
**Summary:** Create new alert from event  
**OperationId:** createAlertByReference

## Description
Creates a new alert based on an existing event with specified event time, machine ID, and report ID.

## Request Body
```json
{
  "eventTime": "2023-08-11T10:30:00.0000000Z",
  "reportId": "string",
  "machineId": "string",
  "severity": "Low|Medium|High",
  "title": "string",
  "description": "string",
  "recommendedAction": "string",
  "category": "string"
}
```
**Required:** eventTime, machineId, reportId

## Responses
### 201 Created
```json
{
  "id": "da637472900382838869_1364969609",
  "incidentId": 1126093,
  "severity": "Medium",
  "status": "New",
  "classification": null,
  "determination": null,
  "title": "Custom Alert Title",
  "description": "Custom alert description",
  "category": "CustomDetection",
  "alertCreationTime": "2023-08-11T10:30:00.0000000Z",
  "firstEventTime": "2023-08-11T10:30:00.0000000Z",
  "lastEventTime": "2023-08-11T10:30:00.0000000Z",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "computerDnsName": "desktop-computer"
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
POST /api/alerts/CreateAlertByReference
Authorization: Bearer {token}
Content-Type: application/json

{
  "eventTime": "2023-08-11T10:30:00.0000000Z",
  "reportId": "12345",
  "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
  "severity": "High",
  "title": "Suspicious Activity Detected",
  "description": "Custom detection rule triggered",
  "category": "CustomDetection"
}
```

## Notes
- Event time, machine ID, and report ID are required for alert creation
- Created alerts will appear in the standard alerts workflow
- Related endpoints: GET /api/alerts, PATCH /api/alerts/{id}

---
