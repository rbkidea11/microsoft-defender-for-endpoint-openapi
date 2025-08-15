# Endpoint: GET /api/machines/find(timestamp={time},key={IP})

**Source:** find-machine-info-by-ip.md  
**Tags:** Machine  
**Summary:** Find device by internal IP and timestamp  
**OperationId:** findMachineByIP

## Description
Finds a device by internal IP address around a specific timestamp (within 16 minutes prior and after).

## Parameters
### Query Parameters  
- `timestamp` (string, required): Timestamp in ISO 8601 format (must be within last 30 days)
- `key` (string, required): Internal IP address to search for

## Responses
### 200 Success
```json
{
  "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Machines",
  "value": [
    {
      "id": "04c99d46599f078f1c3da3783cf5b95f01ac61bb",
      "computerDnsName": "",
      "firstSeen": "2017-07-06T01:25:04.9480498Z",
      "osPlatform": "Windows10"
    }
  ]
}
```

### Errors
Standard error responses: 401 (Unauthorized), 403 (Forbidden), 404 (Not Found - no machine found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.Read.All` (Application) or `Machine.ReadWrite.All` (Application)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ❌ Not applicable for this specialized search endpoint

## Example
```http
GET /api/machines/find(timestamp=2018-06-19T10:00:00Z,key='10.166.93.61')
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://graph.microsoft.com/testwdatppreview/$metadata#Machines",
  "value": [
    {
      "id": "04c99d46599f078f1c3da3783cf5b95f01ac61bb",
      "computerDnsName": "",
      "firstSeen": "2017-07-06T01:25:04.9480498Z",
      "osPlatform": "Windows10"
    }
  ]
}
```

## Notes
- Timestamp must be within the last 30 days
- Returns devices that reported the IP address within 16 minutes of the specified timestamp
- Related endpoints: GET /api/machines/findbyip, GET /api/machines

---
