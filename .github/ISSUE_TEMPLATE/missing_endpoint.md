---
name: Missing Endpoint
about: Report an endpoint that should be included in the specification
title: '[MISSING] '
labels: ['missing-endpoint']
assignees: ''
---

## 📍 Missing Endpoint Details
- **HTTP Method**: GET/POST/PUT/DELETE/PATCH
- **Path**: `/api/missing/endpoint`
- **Category**: Which category should this belong to?

## 📖 Description
Brief description of what this endpoint does.

## 🔗 Microsoft Documentation
**Required**: Link to Microsoft's official documentation for this endpoint.

## 🎯 Business Value
Explain why this endpoint is important and how it would be used.

## 📊 Expected Request/Response
Based on Microsoft's documentation:

```json
// Request (if applicable)
{
  "example": "request"
}

// Response
{
  "example": "response"
}
```

## 🏷️ Suggested Schema Names
What should the request/response schemas be called?
- Request: `ExampleRequest`
- Response: `ExampleResponse`
- Collection: `ExampleCollection`

## 🔧 Parameters
List any path, query, or header parameters:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string | Yes | Resource identifier |
| `$filter` | string | No | OData filter |

## 🛡️ Security
What permissions are required for this endpoint?
- [ ] Machine.Read.All
- [ ] Alert.Read.All
- [ ] Other: ___________

## ⚡ Rate Limiting
Any specific rate limiting information from Microsoft's docs?

## ✅ Validation
- [ ] I have confirmed this endpoint exists in Microsoft's API
- [ ] I have provided a link to official Microsoft documentation
- [ ] I have checked this endpoint isn't already in the specification
- [ ] I have tested this endpoint (if possible)

## 📝 Additional Context
Any other information that would help implement this endpoint.
