# Endpoint: GET /api/browserextensions/permissionsinfo

**Source:** get-browser-extensions-permission-info.md  
**Tags:** BrowserExtensions  
**Summary:** Get browser extensions permission info  
**OperationId:** getBrowserExtensionsPermissionInfo

## Description
Retrieves a list of all permissions requested by browser extensions with static data descriptions to enhance browser extension assessment results.

## Parameters
### Query Parameters
- `$filter` (string, optional): OData filter on id, name, description, cvssV3, publishedOn, severity, updatedOn
- `$top` (integer, optional): Number of entries to return (max 10,000)
- `$skip` (integer, optional): Number of entries to skip

## Request Body
None

## Responses
### 200 Success
```json
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#BrowserExtension",
  "value": [
    {
      "key": "string",
      "permissionName": "string",
      "description": "string"
    }
  ]
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: Software.Read.All (Application) or Software.Read (Delegated)

## Rate Limits
- Standard API rate limits apply

## OData Support
- ✅ $filter: id, name, description, cvssV3, publishedOn, severity, updatedOn
- ✅ $top: Max 10,000
- ✅ $skip: Supported

## Example
```http
GET /api/browserextensions/permissionsinfo
Authorization: Bearer {token}

Response:
{
  "@odata.context": "https://api.securitycenter.microsoft.com/api/$metadata#BrowserExtension",
  "value": [
    {
      "key": "audioCapture",
      "permissionName": "Capture audio from attached mic or webcam",
      "description": "Capture audio from attached mic or webcam. Could be used to listen in on use."
    },
    {
      "key": "app.window.fullscreen.overrideEsc",
      "permissionName": "Prevent escape button from exiting fullscreen",
      "description": "Can prevent escape button from exiting fullscreen."
    },
    {
      "key": "browsingData",
      "permissionName": "Clear browsing data",
      "description": "Clears browsing data which could result in a forensics/logging issues."
    },
    {
      "key": "content_security_policy",
      "permissionName": "Can manipulate default Content Security Policy (CSP)",
      "description": "CSP works as a block/allow listing mechanism for resources loaded or executed by your extensions. Can manipulate default CSP."
    }
  ]
}
```

## Notes
- Static data description for browser extension permissions
- Enhances data from Export browser extensions assessment API
- Comprehensive OData V4 query support
- Useful for understanding security implications of browser extension permissions

---
