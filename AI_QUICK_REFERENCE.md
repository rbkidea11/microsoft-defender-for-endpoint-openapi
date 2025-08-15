# AI Agent Quick Reference: Summary Creation

## Workflow Checklist

1. ✅ **Check COVERAGE.md** for next ❌ endpoint
2. ✅ **Read source file** from `defender-docs/defender-endpoint/api/`
3. ✅ **Use TEMPLATE.md** format (streamlined, not verbose)
4. ✅ **Create summary** in `summaries/[filename]-summary.md`
5. ✅ **Update COVERAGE.md** to ✅ with summary path
6. ✅ **Update progress counter** in COVERAGE.md

## Template Structure (Copy Exactly)

```markdown
# Endpoint: [METHOD] [PATH]

**Source:** [filename.md]  
**Tags:** [Category]  
**Summary:** [<50 chars]  
**OperationId:** [camelCaseId]

## Description
[1-2 sentences max]

## Parameters
### Path Parameters
- `param` (type, required/optional): Description

### Query Parameters  
- `param` (type, required/optional): Description

## Request Body
```json
{"property": "value"}
```
**Required:** field1, field2

## Responses
### 200 Success
```json
{"result": "schema"}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: [specific permissions]

## Rate Limits
- X calls per minute, Y calls per hour

## OData Support
- ✅/❌ [capabilities]

## Example
```http
[request/response]
```

## Notes
- [Essential info only]

---
```

## Common Values

### Tags (Categories)
Alert, Machine, MachineAction, File, User, Vulnerability, Recommendation, AdvancedHunting, Assessment, AuthenticatedScan, AutomatedInvestigation, BrowserExtensions, CertificateInventory, DeviceHealth, Domain, Indicators, InformationGathering, IP, LiveResponseLibrary, RemediationActivity, Score, SecurityBaseline, Software

### OperationId Patterns
- `GET /api/alerts` → `getAlerts`
- `GET /api/alerts/{id}` → `getAlertById`
- `POST /api/machines/{id}/isolate` → `isolateMachine`
- `DELETE /api/indicators/{id}` → `deleteIndicatorById`

### Rate Limits
- **Standard**: "100 calls per minute, 1,500 calls per hour"
- **Export files**: "5 calls per minute, 20 calls per hour"
- **Assessment JSON**: "30 calls per minute, 1,000 calls per hour"
- **TI indicators**: "30 calls per minute, 1,500 calls per hour"

### Permissions
- **Alerts**: `Alert.Read.All`, `Alert.ReadWrite.All`
- **Machines**: `Machine.Read.All`, `Machine.ReadWrite.All`
- **Actions**: `Machine.Isolate`, `Machine.Scan`
- **Indicators**: `Ti.ReadWrite`, `Ti.ReadWrite.All`
- **Vulnerabilities**: `Vulnerability.Read.All`

### OData Support
- **GET collections**: "✅ $filter, $top, $skip"
- **GET /api/alerts**: "✅ $filter, $top, $skip, $expand: evidence"
- **POST/PUT/DELETE**: "❌ Not applicable for [METHOD] operations"

## Don'ts
- ❌ Don't use verbose original template
- ❌ Don't add excessive business context
- ❌ Don't include multiple examples
- ❌ Don't forget to update COVERAGE.md
- ❌ Don't make up information if unclear

## Do's
- ✅ Follow template exactly
- ✅ Keep descriptions to 1-2 sentences
- ✅ Extract accurate rate limits
- ✅ Use consistent OperationId patterns
- ✅ Update progress tracking
