# Endpoint: GET /api/remediationTasks/{id}/machineReferences

**Source:** get-remediation-exposed-devices-activities.md  
**Tags:** RemediationActivity  
**Summary:** List exposed devices for remediation activity  
**OperationId:** getRemediationExposedDevices

## Description
Retrieves a list of exposed devices for a specific remediation activity from Threat and Vulnerability Management.

## Parameters
### Path Parameters
- `id` (string, required): Remediation activity ID

## Request Body
Empty

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#MachineReferences",
  "value": [
    {
      "id": "e058770379bc199a9c179ce52a23e16fd44fd2ee",
      "computerDnsName": "niw_pc",
      "osPlatform": "Windows10",
      "rbacGroupName": "GroupTwo"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: RemediationTasks.Read.All (Application), RemediationTask.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for GET operations

## Example
```http
GET /api/remediationTasks/03942ef5-aewb-4w6e-b555-d6a97013844w/machineReferences
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "e058770379bc199a9c179ce52a23e16fd44fd2ee",
      "computerDnsName": "niw_pc"
    }
  ]
}
```

## Notes
- Part of Threat and Vulnerability Management
- Returns machine references for devices affected by the remediation activity

---
