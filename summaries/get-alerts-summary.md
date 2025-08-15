# Endpoint: GET /api/alerts

**Source:** get-alerts.md  
**Tags:** Alert  
**Summary:** List alerts with OData V4 support and evidence expansion  
**OperationId:** getAlerts

## Description
Retrieves security alerts with comprehensive filtering, sorting, and pagination through OData V4 queries.

## Parameters
### Query Parameters  
- `$filter` (string, optional): OData filter query - supports 15+ filterable fields
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip
- `$expand` (string, optional): Expand related entities (supported: evidence)
- `$orderby` (string, optional): Sort results by specified fields
- `$select` (string, optional): Select specific fields to return

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#Alerts",
  "@odata.nextLink": "https://api.securitycenter.microsoft.com/api/alerts?$skip=100",
  "value": [
    {
      "id": "da637472900382838869_1364969609",
      "incidentId": 1126093,
      "investigationId": 1234567,
      "assignedTo": "analyst@contoso.com",
      "severity": "Medium",
      "status": "New",
      "classification": null,
      "determination": null,
      "investigationState": "Running",
      "detectionSource": "WindowsDefenderAv",
      "category": "Malware",
      "title": "Malware detected",
      "description": "A malware was detected on the device",
      "alertCreationTime": "2023-08-11T10:30:00.0000000Z",
      "firstEventTime": "2023-08-11T10:25:00.0000000Z",
      "lastEventTime": "2023-08-11T10:30:00.0000000Z",
      "lastUpdateTime": "2023-08-11T10:35:00.0000000Z",
      "machineId": "1e5bc9d7e413ddd7902c2932e418702b84d0cc07",
      "computerDnsName": "desktop-computer",
      "rbacGroupName": "UnassignedGroup",
      "aadTenantId": "12345678-1234-1234-1234-123456789012",
      "threatFamilyName": "Trojan:Win32/Skeeyah.A!rfn",
      "mitreTechniques": ["T1055"],
      "relatedUser": {
        "userName": "user@contoso.com",
        "domainName": "contoso"
      }
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Alert.Read.All` or `Alert.ReadWrite.All` (Application), `Alert.Read` or `Alert.ReadWrite` (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ✅ $filter: severity, status, category, detectionSource, assignedTo, alertCreationTime, machineId, and 8+ more
- ✅ $top: Max 10,000 (page size limit)
- ✅ $skip: Supported for pagination
- ✅ $expand: evidence (provides detailed investigation data)
- ✅ $orderby: Supported for sorting results
- ✅ $select: Supported for field selection

## Example
```http
GET /api/alerts?$filter=severity eq 'High' and status eq 'New'&$expand=evidence&$top=10
Authorization: Bearer {token}

Response with Evidence:
{
  "value": [
    {
      "id": "da637472900382838869_1364969609",
      "severity": "High",
      "status": "New",
      "evidence": [
        {
          "entityType": "File",
          "sha1": "4388963aaa83afe2042a46a3c017ad50bdcdafb3",
          "fileName": "malware.exe",
          "filePath": "C:\\temp\\malware.exe"
        }
      ]
    }
  ]
}
```

## Notes
- Maximum page size is 10,000 alerts per request
- Use $expand=evidence for detailed investigation data (unique to alerts endpoint)
- Related endpoints: GET /api/alerts/{id}, PATCH /api/alerts/{id}, POST /api/alerts/batchUpdate

---
