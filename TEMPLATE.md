# Endpoint Summary Template

Use this streamlined template for each Microsoft API documentation file, focused on OpenAPI specification generation.

---

# Endpoint: [METHOD] [PATH]

**Source:** [microsoft-doc-filename.md]  
**Tags:** [Category]  
**Summary:** [Brief description <50 chars]  
**OperationId:** [camelCaseOperationId]

## Description
[Concise business description - 1-2 sentences max focusing on what the endpoint does and its primary use case]

## Parameters
### Path Parameters
- `param1` (string, required): Description
- `param2` (string, optional): Description

### Query Parameters  
- `$filter` (string, optional): OData filter query
- `$top` (integer, optional): Number of entries to return
- `customParam` (string, required): Custom parameter description

## Request Body
```json
{
  "property1": "string",
  "property2": 123,
  "property3": ["array", "values"]
}
```
**Required:** property1, property2  
**Optional:** property3

## Responses
### 200 Success
```json
{
  "value": [
    {
      "id": "string",
      "name": "string"
    }
  ],
  "@odata.nextLink": "string"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`

## Rate Limits
- 100 calls per minute, 1,500 calls per hour

## OData Support
- ✅ $filter: field1, field2, field3
- ✅ $top: Max 10,000
- ❌ $expand: Not supported

## Example
```http
GET /api/example?$filter=status eq 'Active'&$top=50
Authorization: Bearer {token}

Response:
{
  "value": [
    {
      "id": "12345",
      "status": "Active"
    }
  ]
}
```

## Notes
- Key limitations or special considerations only
- Related endpoints if relevant

---

## Template Usage:
1. Replace all `[PLACEHOLDER]` values
2. Remove sections that don't apply (e.g., Request Body for GET requests)
3. Include actual examples from Microsoft docs
4. Focus on information needed for OpenAPI generation
5. Keep descriptions concise and technical
