# Endpoint: POST /api/advancedqueries/run

**Source:** run-advanced-query-api.md  
**Tags:** AdvancedHunting  
**Summary:** Run advanced hunting queries (KQL)  
**OperationId:** runAdvancedQuery

## Description
Executes advanced hunting queries using KQL (Kusto Query Language) to search through security data. This is an older version with limited capabilities compared to Microsoft Graph security API.

## Parameters
None (query parameters in request body)

## Request Body
```json
{
  "Query": "string"
}
```
**Required:** Query (KQL query string)

## Responses
### 200 Success
```json
{
  "Schema": [
    {
      "Name": "string",
      "Type": "string"
    }
  ],
  "Results": [
    {
      "ColumnName": "value"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: AdvancedQuery.Read.All (Application) or AdvancedQuery.Read (Delegated)

## Rate Limits
- 45 calls per minute, 1,500 calls per hour
- 10 minutes of running time every hour
- 3 hours of running time per day
- Maximum execution time: 200 seconds per request

## OData Support
- ❌ Not applicable for query execution

## Example
```http
POST /api/advancedqueries/run
Authorization: Bearer {token}
Content-Type: application/json

{
  "Query": "DeviceProcessEvents | where InitiatingProcessFileName =~ 'powershell.exe' | where ProcessCommandLine contains 'appdata' | project Timestamp, FileName, InitiatingProcessFileName, DeviceId | limit 2"
}

Response:
{
  "Schema": [
    {
      "Name": "Timestamp",
      "Type": "DateTime"
    },
    {
      "Name": "FileName", 
      "Type": "String"
    },
    {
      "Name": "InitiatingProcessFileName",
      "Type": "String"
    },
    {
      "Name": "DeviceId",
      "Type": "String"
    }
  ],
  "Results": [
    {
      "Timestamp": "2020-02-05T01:10:26.2648757Z",
      "FileName": "csc.exe",
      "InitiatingProcessFileName": "powershell.exe",
      "DeviceId": "10cbf9182d4e95660362f65cfa67c7731f62fdb3"
    }
  ]
}
```

## Notes
- **IMPORTANT**: This is an older version with limited capabilities
- **Recommended**: Use Microsoft Graph security API for more comprehensive advanced hunting
- **Data retention**: Only last 30 days of data available
- **Result limits**: Maximum 100,000 rows per query
- **Query size limit**: Maximum 124 MB result size per request
- **Execution limits**: Strict CPU time quotas (10 min/hour, 3 hours/day)
- **429 responses**: Indicate quota limit reached (requests or CPU time)
- **User requirements**: 'View Data' role in Microsoft Entra ID
- **Device access**: Based on device group settings
- **Query language**: KQL (Kusto Query Language)

---
