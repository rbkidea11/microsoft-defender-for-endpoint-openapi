# Endpoint: GET /api/machines/{id}/alerts

**Source:** get-machine-related-alerts.md  
**Tags:** Machine  
**Summary:** Get all alerts related to a specific device  
**OperationId:** getMachineRelatedAlerts

## Description
Retrieves all alerts related to a specific device for comprehensive device-focused security investigation and analysis.

## Parameters
### Path Parameters
- `id` (string, required): Device ID

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
- ❌ Not applicable for device-specific alert collection

## Example
```http
GET /api/machines/1e5bc9d7e413ddd7902c2932e418702b84d0cc07/alerts
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
      "title": "Suspicious activity detected on device",
      "description": "Suspicious activities were detected on this device...",
      "alertCreationTime": "2021-01-26T20:33:57.7220239Z",
      "firstEventTime": "2021-01-26T20:31:32.9562661Z",
      "lastEventTime": "2021-01-26T20:31:33.0577322Z",
      "lastUpdateTime": "2021-01-26T20:33:59.2Z",
      "resolvedTime": null,
      "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
      "computerDnsName": "mymachine1.contoso.com",
      "aadTenantId": "12345678-1234-1234-1234-123456789abc"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to device based on device group settings
- Returns 404 if device not found
- Data availability depends on configured retention period
- **Alert categories**: Execution, Persistence, PrivilegeEscalation, DefenseEvasion, CredentialAccess, Discovery, LateralMovement, Collection, CommandAndControl, Exfiltration, Impact, InitialAccess, SuspiciousActivity
- **Severity levels**: Informational, Low, Medium, High
- **Status values**: New, InProgress, Resolved
- Essential for device-focused incident response and investigation
- Provides complete alert history for a specific device
- Critical for understanding device compromise timeline and attack patterns

---
