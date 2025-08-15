# Endpoint: GET /api/users/{id}/alerts

**Source:** get-user-related-alerts.md  
**Tags:** User  
**Summary:** Get alerts related to user ID  
**OperationId:** getUserRelatedAlerts

## Description
Retrieves a collection of alerts related to a given user ID for user-focused security investigation and analysis.

## Parameters
### Path Parameters
- `id` (string, required): Username only (not full UPN) - e.g., "user1" for user1@contoso.com

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Alerts",
  "value": [
    {
      "id": "string",
      "incidentId": 0,
      "investigationId": 0,
      "assignedTo": "string",
      "severity": "string",
      "status": "string",
      "classification": "string",
      "determination": "string",
      "investigationState": "string",
      "detectionSource": "string",
      "category": "string",
      "title": "string",
      "description": "string",
      "alertCreationTime": "2020-01-01T00:00:00Z",
      "firstEventTime": "2020-01-01T00:00:00Z",
      "lastEventTime": "2020-01-01T00:00:00Z",
      "lastUpdateTime": "2020-01-01T00:00:00Z",
      "resolvedTime": "2020-01-01T00:00:00Z",
      "machineId": "string",
      "computerDnsName": "string",
      "aadTenantId": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Alert.Read.All (Application), Alert.ReadWrite.All (Application), Alert.Read (Delegated), Alert.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for user-specific alert collection

## Example
```http
GET /api/users/user1/alerts
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Alerts",
  "value": [
    {
      "id": "da637472900382838869_1364969609",
      "incidentId": 1126093,
      "investigationId": null,
      "assignedTo": null,
      "severity": "Medium",
      "status": "New",
      "classification": null,
      "determination": null,
      "investigationState": "Queued",
      "detectionSource": "WindowsDefenderAtp",
      "category": "SuspiciousActivity",
      "title": "Suspicious user activity detected",
      "description": "User performed suspicious activities...",
      "alertCreationTime": "2021-01-26T20:33:57.7220239Z",
      "firstEventTime": "2021-01-26T20:31:32.9562661Z",
      "lastEventTime": "2021-01-26T20:31:33.0577322Z",
      "lastUpdateTime": "2021-01-26T20:33:59.2Z",
      "resolvedTime": null,
      "machineId": "4899036531e374137f63289c3267bad772c13fef",
      "computerDnsName": "mymachine1.contoso.com",
      "aadTenantId": "12345678-1234-1234-1234-123456789abc"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- Response includes only alerts from devices user has access to based on device group settings
- **Important**: ID parameter is username only, not full UPN (use "user1" not "user1@contoso.com")
- Returns empty set if user doesn't exist (still returns 200 OK)
- Useful for investigating user-focused security incidents
- Alerts may span multiple devices associated with the user
- Essential for user behavior analysis and insider threat detection

---
