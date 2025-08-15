# Endpoint: GET /api/machines/findbytag

**Source:** find-machines-by-tag.md  
**Tags:** Machine  
**Summary:** Find devices by tag with optional starts-with filter  
**OperationId:** findMachinesByTag

## Description
Finds devices by tag name with optional starts-with filtering for partial tag matching.

## Parameters
### Query Parameters  
- `tag` (string, required): The tag name to search for
- `useStartsWithFilter` (boolean, optional): When true, finds devices with tag names that start with the given tag (default: false)

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
      "machineTags": ["string"],
      "lastIpAddress": "string",
      "lastExternalIpAddress": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: `Machine.Read.All` or `Machine.ReadWrite.All` (Application), `Machine.Read` or `Machine.ReadWrite` (Delegated)

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ❌ Not applicable for this specialized search endpoint

## Example
```http
GET /api/machines/findbytag?tag=testTag&useStartsWithFilter=true
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "04c99d46599f078f1c3da3783cf5b95f01ac61bb",
      "computerDnsName": "machine1.contoso.com",
      "firstSeen": "2019-09-22T08:30:00Z",
      "osPlatform": "Windows10",
      "machineTags": ["testTag", "production"]
    }
  ]
}
```

## Notes
- Supports starts-with query when useStartsWithFilter=true
- Response filtered by user's device group access (for delegated permissions)
- Related endpoints: GET /api/machines, POST /api/machines/{id}/tags

---
