# Endpoint: PATCH /api/alerts/{id}

**Source:** update-alert.md  
**Tags:** Alert  
**Summary:** Update alert properties  
**OperationId:** updateAlert

## Description
Updates properties of an existing alert including status, determination, classification, assignedTo, and comments.

## Parameters
### Path Parameters
- `id` (string, required): Alert ID

## Request Body
```json
{
  "status": "string",
  "assignedTo": "string",
  "classification": "string",
  "determination": "string",
  "comment": "string"
}
```
**Optional:** All fields are optional - include only fields to update

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
  "comments": [
    {
      "comment": "string",
      "createdBy": "string",
      "createdTime": "2020-01-01T00:00:00Z"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Alerts.ReadWrite.All (Application) or Alert.ReadWrite (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for alert update operations

## Example
```http
PATCH /api/alerts/121688558380765161_2136280442
Authorization: Bearer {token}
Content-Type: application/json

{
  "status": "Resolved",
  "assignedTo": "secop2@contoso.com",
  "classification": "FalsePositive",
  "determination": "Malware",
  "comment": "Resolve my alert and assign to secop2"
}

Response:
{
  "id": "121688558380765161_2136280442",
  "incidentId": 1126093,
  "investigationId": null,
  "assignedTo": "secop2@contoso.com",
  "severity": "Low",
  "status": "Resolved",
  "classification": "FalsePositive",
  "determination": "Malware",
  "investigationState": "Queued",
  "detectionSource": "WindowsDefenderAtp",
  "category": "Execution",
  "title": "Low-reputation arbitrary code executed by signed executable",
  "description": "Binaries signed by Microsoft can be used to run low-reputation arbitrary code...",
  "alertCreationTime": "2021-01-26T20:33:57.7220239Z",
  "firstEventTime": "2021-01-26T20:31:32.9562661Z",
  "lastEventTime": "2021-01-26T20:31:33.0577322Z",
  "lastUpdateTime": "2021-01-26T20:33:59.2Z",
  "resolvedTime": "2021-01-26T20:35:00.0Z",
  "machineId": "4899036531e374137f63289c3267bad772c13fef",
  "computerDnsName": "mymachine1.contoso.com",
  "aadTenantId": "12345678-1234-1234-1234-123456789abc",
  "comments": [
    {
      "comment": "Resolve my alert and assign to secop2",
      "createdBy": "admin@contoso.com",
      "createdTime": "2021-01-26T20:35:00.0Z"
    }
  ]
}
```

## Notes
- Requires 'Alerts investigation' role permission for delegated access
- User must have access to device associated with alert based on device group settings
- **Status values**: New, InProgress, Resolved
- **Classification values**: TruePositive, InformationalExpectedActivity, FalsePositive
- **Determination values vary by classification**:
  - **TruePositive**: MultiStagedAttack, MaliciousUserActivity, CompromisedUser, Malware, Phishing, UnwantedSoftware, Other
  - **InformationalExpectedActivity**: SecurityTesting, LineOfBusinessApplication, ConfirmedActivity, Other
  - **FalsePositive**: NotMalicious, InsufficientData, Other
- **Comments**: Can be submitted with or without updating other properties
- **Deprecated values**: 'Apt' and 'SecurityPersonnel' determination values deprecated as of August 29, 2022
- Only include fields that need updating for best performance

---
