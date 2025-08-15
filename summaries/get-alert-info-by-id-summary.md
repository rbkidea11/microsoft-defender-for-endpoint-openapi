# Endpoint: GET /api/alerts/{id}

**Source:** get-alert-info-by-id.md  
**Tags:** Alert  
**Summary:** Get alert information by ID  
**OperationId:** getAlertById

## Description
Retrieves a specific alert by its ID with complete alert details and metadata.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
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
  "aadTenantId": "string",
  "comments": [],
  "evidence": []
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
- ❌ Not applicable for single resource retrieval

## Example
```http
GET /api/alerts/da637472900382838869_1364969609
Authorization: Bearer {token}

Response:
{
  "id": "da637472900382838869_1364969609",
  "incidentId": 1126093,
  "investigationId": null,
  "assignedTo": null,
  "severity": "Low",
  "status": "New",
  "classification": null,
  "determination": null,
  "investigationState": "Queued",
  "detectionSource": "WindowsDefenderAtp",
  "category": "Execution",
  "title": "Low-reputation arbitrary code executed by signed executable",
  "description": "Binaries signed by Microsoft can be used to run low-reputation arbitrary code...",
  "alertCreationTime": "2021-01-26T20:33:57.7220239Z",
  "firstEventTime": "2021-01-26T20:31:32.9562661Z",
  "lastEventTime": "2021-01-26T20:31:33.0577322Z",
  "lastUpdateTime": "2021-01-26T20:33:59.2Z",
  "resolvedTime": null,
  "machineId": "4899036531e374137f63289c3267bad772c13fef",
  "computerDnsName": "mymachine1.contoso.com",
  "aadTenantId": "12345678-1234-1234-1234-123456789abc"
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period

---
