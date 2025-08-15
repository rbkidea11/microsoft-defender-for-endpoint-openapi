# Endpoint: GET /api/alerts/{id}/ips

**Source:** get-alert-related-ip-info.md  
**Tags:** Alert  
**Summary:** Get IP addresses related to alert  
**OperationId:** getAlertRelatedIPs

## Description
Retrieves all IP addresses related to a specific alert for network threat investigation and analysis.

## Parameters
### Path Parameters
- `id` (string, required): The unique identifier of the alert

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/$metadata#Ips",
  "value": [
    {
      "id": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Ip.Read.All (Application) or Ip.Read.All (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for related resource retrieval

## Example
```http
GET /api/alerts/636688558380765161_2136280442/ips
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/$metadata#Ips",
  "value": [
    {
      "id": "104.80.104.128"
    },
    {
      "id": "23.203.232.228"
    }
  ]
}
```

## Notes
- Requires 'View Data' role permission for delegated access
- User must have access to the device associated with the alert based on device group settings
- Alert availability depends on configured retention period
- Useful for network-based threat investigation

---
