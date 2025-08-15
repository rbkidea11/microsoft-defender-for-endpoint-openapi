# AI Agent Guide: Creating Microsoft Defender API Endpoint Summaries

This guide provides step-by-step instructions for AI agents to create consistent, high-quality endpoint summaries for OpenAPI specification generation.

## Overview

**Purpose**: Create standardized summaries from Microsoft Defender for Endpoint API documentation files that can be used to generate OpenAPI specifications.

**Input**: Microsoft documentation files in `defender-docs/defender-endpoint/api/`
**Output**: Streamlined summary files in `summaries/` directory
**Template**: Use `TEMPLATE.md` as the standard format

## Prerequisites

1. **Check COVERAGE.md** to identify which endpoints need summaries
2. **Use the streamlined template** from `TEMPLATE.md` (not verbose format)
3. **Focus on OpenAPI generation needs** - avoid excessive narrative

## Step-by-Step Process

### Step 1: Identify Next Endpoint

```bash
# Check COVERAGE.md for next endpoint marked with ❌ (Not Started)
# Look for entries like:
# | filename.md | ❌ | - | METHOD /api/path | Description |
```

### Step 2: Read Source Documentation

```bash
# Read the Microsoft documentation file
fs_read defender-docs/defender-endpoint/api/[filename.md]
```

**Key sections to extract:**
- Title (from frontmatter: `title: ...`)
- API description (under `## API description`)
- HTTP request (under `## HTTP request`)
- Permissions (from permissions table)
- Rate limitations (under `## Limitations`)
- Request body (under `## Request body`)
- Response format (under `## Response`)
- Examples (under `## Example` or `### Request`/`### Response`)

### Step 3: Determine Endpoint Category

**Map to existing OpenAPI tags:**
- Alert, Machine, MachineAction, File, User, Vulnerability
- Recommendation, AdvancedHunting, Assessment, AuthenticatedScan
- AutomatedInvestigation, BrowserExtensions, CertificateInventory
- DeviceHealth, Domain, Indicators, InformationGathering
- IP, LiveResponseLibrary, RemediationActivity, Score
- SecurityBaseline, Software

### Step 4: Create OperationId

**Format**: `camelCaseOperationId`
**Pattern**: `[verb][ResourceName][ById/ByMachine/etc]`

**Examples:**
- `GET /api/alerts` → `getAlerts`
- `GET /api/alerts/{id}` → `getAlertById`
- `POST /api/machines/{id}/isolate` → `isolateMachine`
- `DELETE /api/indicators/{id}` → `deleteIndicatorById`

### Step 5: Extract Key Information

#### HTTP Method and Path
```
# Look for patterns like:
GET /api/alerts/{id}
POST https://api.securitycenter.microsoft.com/api/machines/{id}/isolate
```

#### Rate Limits
```
# Look for patterns like:
"Rate limitations for this API are 100 calls per minute and 1500 calls per hour"
# Format as: "100 calls per minute, 1,500 calls per hour"
```

#### Permissions
```
# Extract from permission tables:
|Permission type|Permission|Permission display name|
|Application|Alert.Read.All|'Read all alerts'|
# Format as: Alert.Read.All (Application) or Alert.Read (Delegated)
```

#### Request Body Schema
```
# Extract JSON structure and required fields
# Note required vs optional parameters
```

#### Response Schema
```
# Extract successful response format (usually 200/201)
# Include key properties and structure
```

### Step 6: Create Summary File

**Filename**: `summaries/[source-filename]-summary.md`

**Use TEMPLATE.md structure exactly:**

```markdown
# Endpoint: [METHOD] [PATH]

**Source:** [source-filename.md]  
**Tags:** [Category]  
**Summary:** [Brief description <50 chars]  
**OperationId:** [camelCaseOperationId]

## Description
[1-2 sentences describing what the endpoint does and primary use case]

## Parameters
### Path Parameters
- `param` (type, required/optional): Description

### Query Parameters  
- `param` (type, required/optional): Description

## Request Body
```json
{
  "property": "value"
}
```
**Required:** field1, field2

## Responses
### 200 Success
```json
{
  "result": "schema"
}
```

### Errors
Standard error responses: 400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)

## Security
- OAuth2: `https://api.securitycenter.microsoft.com/.default`
- Permission: [specific permissions]

## Rate Limits
- X calls per minute, Y calls per hour

## OData Support
- ✅/❌ [specific OData capabilities]

## Example
```http
[Clean request/response example]
```

## Notes
- [Key limitations or considerations only]
- [Related endpoints if relevant]

---
```

### Step 7: Handle Special Cases

#### Multi-Endpoint Files
Some files document multiple related endpoints (e.g., export assessments with JSON + file methods):

```markdown
# Endpoints: [Category Name]

## Endpoint 1: [METHOD] [PATH]
**OperationId:** [operationId1]
[Full endpoint details]

---

## Endpoint 2: [METHOD] [PATH]  
**OperationId:** [operationId2]
[Full endpoint details]

---

## Common Properties
[Shared errors, security, etc.]
```

#### Missing Information
- If rate limits not specified: "Standard API rate limits apply"
- If permissions unclear: "Appropriate permissions required"
- If request body empty: Remove Request Body section entirely
- If no OData support: "❌ Not applicable for [METHOD] operations"

### Step 8: Update COVERAGE.md

```bash
# Change status from ❌ to ✅ and add summary file path:
# | filename.md | ✅ | summaries/filename-summary.md | METHOD /api/path | Description |
```

### Step 9: Update Progress Counter

```bash
# Update the progress summary in COVERAGE.md:
# - **Completed**: X/84 (Y%)
# - **Remaining**: Z/84 (W%)
```

## Quality Checklist

Before completing each summary, verify:

- [ ] **Follows TEMPLATE.md format exactly**
- [ ] **OperationId is unique and follows camelCase pattern**
- [ ] **HTTP method and path are accurate**
- [ ] **Description is concise (1-2 sentences)**
- [ ] **Required vs optional parameters clearly marked**
- [ ] **JSON examples are valid and realistic**
- [ ] **Rate limits extracted accurately**
- [ ] **Permissions specified correctly**
- [ ] **OData support documented accurately**
- [ ] **Notes contain only essential information**
- [ ] **COVERAGE.md updated with ✅ status**

## Common Patterns to Recognize

### Standard Error Responses
Always include: `400 (Bad Request), 401 (Unauthorized), 403 (Forbidden), 404 (Not Found), 429 (Rate Limited), 500 (Server Error)`

### OAuth2 Security
Always: `OAuth2: https://api.securitycenter.microsoft.com/.default`

### OData Support Patterns
- **GET endpoints with collections**: Usually support `$filter`, `$top`, `$skip`
- **GET /api/alerts**: Special case - supports `$expand=evidence`
- **POST/PUT/DELETE**: Usually "❌ Not applicable for [METHOD] operations"

### Rate Limit Patterns
- **Most endpoints**: "100 calls per minute, 1,500 calls per hour"
- **Export endpoints**: "5 calls per minute, 20 calls per hour" (file exports)
- **Assessment endpoints**: "30 calls per minute, 1,000 calls per hour" (JSON)
- **TI indicators**: "30 calls per minute, 1,500 calls per hour"

### Permission Patterns
- **Alerts**: `Alert.Read.All`, `Alert.ReadWrite.All`
- **Machines**: `Machine.Read.All`, `Machine.ReadWrite.All`
- **Machine Actions**: `Machine.Isolate`, `Machine.Scan`, etc.
- **Indicators**: `Ti.ReadWrite`, `Ti.ReadWrite.All`
- **Vulnerabilities**: `Vulnerability.Read.All`
- **Software**: `Software.Read.All`

## Troubleshooting

### If Documentation is Unclear
1. **Check related endpoints** for similar patterns
2. **Look at existing summaries** for comparable endpoints
3. **Use conservative defaults** (mark as optional if unsure)
4. **Add note** about uncertainty for future review

### If Multiple Endpoints in One File
1. **Create multi-endpoint summary** using the pattern above
2. **Give each endpoint unique OperationId**
3. **Share common properties** at the end

### If File is Very Complex
1. **Focus on the core API functionality**
2. **Simplify complex examples** to essential elements
3. **Prioritize information needed for OpenAPI generation**

## Success Metrics

- **Consistency**: All summaries follow identical format
- **Completeness**: All required fields populated
- **Accuracy**: Information matches source documentation
- **Conciseness**: Focused on OpenAPI generation needs
- **Maintainability**: Easy to update and modify

## Final Notes

- **Always use the streamlined template** - not the verbose original format
- **Focus on OpenAPI generation** - avoid excessive business context
- **Maintain consistency** - follow existing patterns exactly
- **Update tracking** - always update COVERAGE.md progress
- **Quality over speed** - accurate summaries are more valuable than fast ones

---

**Remember**: These summaries are the foundation for OpenAPI specification generation. Accuracy and consistency are critical for successful automation.
