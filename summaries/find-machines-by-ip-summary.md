# Endpoint: GET /api/machines/findbyip(ip='{IP}',timestamp={TimeStamp})

**Source:** find-machines-by-ip.md  
**Tags:** Machine  
**Summary:** Find devices by internal IP and timestamp  
**OperationId:** findMachinesByIP

## Description
Finds devices seen with the requested internal IP within 15 minutes prior and after a given timestamp.

## Parameters
### Query Parameters  
- `ip` (string, required): Internal IP address to search for
- `timestamp` (string, required): Timestamp in ISO 8601 format (must be within past 30 days)

## Responses
### 200 Success
```json
{
  "value": [
    {
      "id": "string",
      "computerDnsName": "string",
      "firstSeen": "datetime",
      "osPlatform": "string",
      "lastIpAddress": "string",
      "lastExternalIpAddress": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request - timestamp not within 30 days), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.Read.All` or `Machine.ReadWrite.All` (Application), `Machine.Read` or `Machine.ReadWrite` (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for this specialized search endpoint

## Example
```http
GET /api/machines/findbyip(ip='10.248.240.38',timestamp=2019-09-22T08:44:05Z)
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "04c99d46599f078f1c3da3783cf5b95f01ac61bb",
      "computerDnsName": "machine1.contoso.com",
      "firstSeen": "2019-09-22T08:30:00Z",
      "osPlatform": "Windows10"
    }
  ]
}
```

## Notes
- Timestamp must be within the past 30 days
- Returns devices within 15 minutes of the specified timestamp
- Response filtered by user's device group access (for delegated permissions)
- Related endpoints: GET /api/machines/find, GET /api/machines

---
