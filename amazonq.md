# Amazon Q - Microsoft Defender for Endpoint OpenAPI Maintenance Instructions

This file provides context and instructions for Amazon Q when updating the Microsoft Defender for Endpoint OpenAPI specification based on new or changed documentation.

## Project Context

### Overview
This repository contains a comprehensive OpenAPI 3.0.3 specification for the Microsoft Defender for Endpoint API. The specification provides complete enterprise-grade security operations coverage.

### Current Status Discovery
Use these commands to check current state:
```bash
# Check OpenAPI version
jq -r '.openapi' openapi.json

# Check API version  
jq -r '.info.version' openapi.json

# Count total endpoints
jq '[.paths | to_entries[] | .value | to_entries[] | select(.key | test("get|post|put|delete|patch"))] | length' openapi.json

# List all categories
jq -r '.tags[].name' openapi.json

# Validate JSON syntax
python3 -m json.tool openapi.json > /dev/null && echo "✅ Valid JSON" || echo "❌ Invalid JSON"
```

### Repository Structure
```
├── openapi.json                 # Main OpenAPI specification file
├── amazonq.md                   # This file - Amazon Q instructions
├── .gitignore                   # Git ignore rules
├── .gitmodules                  # Git submodules configuration
├── defender-docs/               # Microsoft docs submodule
└── .git/                        # Git repository
```

### Microsoft Documentation Tracking

The OpenAPI specification includes tracking fields to record which Microsoft docs commit it's based on:

```json
"x-microsoft-docs-commit": "2396f29e7c01cbbc639be84c45e276c115de5f41",
"x-microsoft-docs-date": "2025-08-06T07:31:11Z",
"x-microsoft-docs-url": "https://github.com/MicrosoftDocs/defender-docs/commit/2396f29e7c01cbbc639be84c45e276c115de5f41"
```

#### When to Update Tracking Fields

Update these fields when:
- **Syncing from new Microsoft documentation**
- **Adding endpoints based on recent Microsoft docs changes**
- **Major updates that incorporate multiple Microsoft docs commits**

#### How to Update Tracking Fields

```bash
# Update the Microsoft docs submodule to latest
git submodule update --remote defender-docs

# Get the latest commit for API docs
cd defender-docs
COMMIT_HASH=$(git log -1 --format="%H" -- defender-endpoint/api/)
COMMIT_DATE=$(git log -1 --format="%ci" -- defender-endpoint/api/ | sed 's/ [+-][0-9]\{4\}$/Z/' | sed 's/ /T/')
COMMIT_URL="https://github.com/MicrosoftDocs/defender-docs/commit/$COMMIT_HASH"
cd ..

# Update the OpenAPI spec with new commit info:
# "x-microsoft-docs-commit": "$COMMIT_HASH"
# "x-microsoft-docs-date": "$COMMIT_DATE" 
# "x-microsoft-docs-url": "$COMMIT_URL"

# Commit both the submodule update and OpenAPI changes together
git add defender-docs openapi.json
git commit -m "Update OpenAPI spec based on Microsoft docs update

- Updated to Microsoft docs commit $COMMIT_HASH
- [Describe your OpenAPI changes here]"
```

#### Checking for Updates

```bash
# Check if Microsoft docs submodule has updates
git submodule update --remote defender-docs

# Check what's changed since our last sync
cd defender-docs
CURRENT_COMMIT=$(jq -r '.info["x-microsoft-docs-commit"]' ../openapi.json)
git log --oneline $CURRENT_COMMIT..HEAD -- defender-endpoint/api/

# See specific changes in a commit
git show <commit-hash> -- defender-endpoint/api/
```

### Microsoft Documentation Source
- **Repository**: https://github.com/MicrosoftDocs/defender-docs
- **API Path**: `/defender-endpoint/api/`
- **Branch**: `public`

## Amazon Q Instructions

### When Asked to Update the OpenAPI Specification

#### 1. **Analyze Microsoft Documentation Changes**
When provided with Microsoft documentation or asked to check for updates:

```bash
# Update Microsoft docs submodule to latest
git submodule update --remote defender-docs

# Check what's changed since our last tracked commit
cd defender-docs
CURRENT_COMMIT=$(jq -r '.info["x-microsoft-docs-commit"]' ../openapi.json)
git log --oneline $CURRENT_COMMIT..HEAD -- defender-endpoint/api/

# See specific changes
git show <commit-hash> -- defender-endpoint/api/

# Check what files changed between commits
git diff --name-only $CURRENT_COMMIT..HEAD -- defender-endpoint/api/
```

#### 2. **Understand the Request**
Identify what type of change is being requested:
- **New Endpoint**: Adding a completely new API endpoint
- **Modified Endpoint**: Changes to existing endpoint (parameters, responses, etc.)
- **Schema Changes**: Updates to request/response schemas
- **Deprecated Endpoint**: Marking endpoints as deprecated
- **Documentation Updates**: Non-functional improvements

#### 3. **Analyze the Documentation**
When provided with Microsoft documentation:
- **Read the entire document** to understand the endpoint's purpose
- **Identify HTTP method** (GET, POST, PUT, DELETE, PATCH)
- **Extract the URL path** and parameters
- **Understand request/response schemas**
- **Note permissions and rate limits**
- **Identify the appropriate category/tag** (check existing tags first)

#### 4. **Determine Impact and Version**
- **Breaking Changes**: Require major version increment (x.0.0)
- **New Features**: Require minor version increment (1.x.0)
- **Bug Fixes/Docs**: Require patch version increment (1.1.x)

#### 5. **Update Process**

##### Step 1: Check Existing Categories
```bash
# List current categories to see if new tag is needed
jq -r '.tags[] | "\(.name): \(.description)"' openapi.json
```

If introducing a new category, add to the `tags` array:
```json
{
  "name": "NewCategory",
  "description": "Description of the new endpoint category"
}
```

##### Step 2: Add/Update Schemas
Add new schemas to `components.schemas`:
```json
"NewResourceType": {
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Resource identifier"
    }
  },
  "required": ["id"]
}
```

##### Step 3: Add/Update Endpoints
Add to the `paths` object:
```json
"/api/new-endpoint": {
  "get": {
    "tags": ["CategoryName"],
    "summary": "Brief endpoint description",
    "description": "Detailed endpoint description with business value",
    "operationId": "uniqueOperationId",
    "parameters": [
      // ... parameters if any
    ],
    "responses": {
      "200": {
        "description": "Successful response",
        "content": {
          "application/json": {
            "schema": {
              "$ref": "#/components/schemas/ResponseSchema"
            }
          }
        }
      }
    },
    "security": [{"oauth2": ["https://api.securitycenter.microsoft.com/.default"]}]
  }
}
```

##### Step 4: Update Version and Metadata
- Increment version in `info.version`
- Update `info.description` if significant changes
- Update Microsoft docs tracking fields if syncing from new documentation

#### 6. **Standard Response Codes to Include**
Always include these standard responses for endpoints:
```json
"responses": {
  "200": {
    "description": "Successful response"
  },
  "400": {
    "$ref": "#/components/responses/400"
  },
  "401": {
    "$ref": "#/components/responses/401"
  },
  "403": {
    "$ref": "#/components/responses/403"
  },
  "404": {
    "$ref": "#/components/responses/404"
  },
  "429": {
    "$ref": "#/components/responses/429"
  },
  "500": {
    "$ref": "#/components/responses/500"
  }
}
```

#### 7. **Naming Conventions**

##### Operation IDs
- Use camelCase
- Be descriptive and unique
- Pattern: `verbResourceName` (e.g., `getMachineById`, `listAlerts`)
- Check existing operationIds to avoid conflicts:
```bash
jq -r '[.. | .operationId? | select(. != null)] | unique[]' openapi.json
```

##### Schema Names
- Use PascalCase
- Be descriptive
- For collections: `ResourceNameCollection`
- For requests: `CreateResourceNameRequest`, `UpdateResourceNameRequest`
- Check existing schemas:
```bash
jq -r '.components.schemas | keys[]' openapi.json
```

##### Parameter Names
- Use camelCase for query parameters
- Use lowercase for path parameters
- Be consistent with Microsoft's documentation

#### 8. **Required Elements for Each Endpoint**

Every endpoint must have:
- ✅ **tags**: Array with appropriate category
- ✅ **summary**: Brief description (< 50 chars)
- ✅ **description**: Detailed description with business value
- ✅ **operationId**: Unique identifier
- ✅ **responses**: At minimum 200 and error responses
- ✅ **security**: OAuth2 security requirement
- ✅ **parameters**: If the endpoint takes parameters

#### 9. **Schema Best Practices**

- **Use proper data types**: string, integer, boolean, array, object
- **Include descriptions**: Every property should have a description
- **Use format specifiers**: date-time, email, uri, etc.
- **Mark required fields**: Use `required` array
- **Use enums**: For fixed value sets
- **Use nullable**: `"nullable": true` for optional fields that can be null
- **Reference common schemas**: Use `$ref` for reusable components

#### 10. **Documentation Standards**

##### Descriptions Should Include:
- **What the endpoint does**
- **Business value/use case**
- **Any special considerations**
- **Rate limiting information** (check Microsoft docs for current limits)
- **Permission requirements**

##### Example Good Description:
```json
"description": "Retrieves a collection of alerts related to a given IP address. Useful for investigating network-based threats and understanding the security impact of specific IP addresses. Supports standard OData queries for filtering and pagination."
```

### Common Microsoft Defender API Patterns

#### Authentication
All endpoints use OAuth2 Bearer token authentication:
```json
"security": [
  {
    "oauth2": ["https://api.securitycenter.microsoft.com/.default"]
  }
]
```

#### OData Support
Many endpoints support OData queries (check existing patterns):
```bash
# Find endpoints with OData parameters
jq -r '.paths[][] | select(.parameters[]?.name | test("\\$")) | .operationId' openapi.json
```

Standard OData parameters:
```json
"parameters": [
  {
    "name": "$filter",
    "in": "query",
    "description": "OData filter query",
    "schema": {
      "type": "string"
    },
    "example": "status eq 'Active'"
  },
  {
    "name": "$top",
    "in": "query",
    "description": "Number of entries to return",
    "schema": {
      "type": "integer"
    }
  },
  {
    "name": "$skip",
    "in": "query",
    "description": "Number of entries to skip",
    "schema": {
      "type": "integer"
    }
  }
]
```

#### $expand Parameter (IMPORTANT)
**ONLY** add `$expand` parameter to `GET /api/alerts` endpoint:
```json
{
  "name": "$expand",
  "in": "query",
  "description": "Expand related entities. Supported: evidence",
  "schema": {
    "type": "string"
  },
  "example": "evidence"
}
```

**DO NOT** add `$expand` to other endpoints - testing confirmed it only works on alerts.

#### Collection Responses
Use the standard ODataResponse pattern (check existing schemas):
```bash
# Find existing collection patterns
jq -r '.components.schemas | keys[] | select(test("Collection$"))' openapi.json
```

```json
"SomeResourceCollection": {
  "allOf": [
    {
      "$ref": "#/components/schemas/ODataResponse"
    },
    {
      "type": "object",
      "properties": {
        "value": {
          "type": "array",
          "items": {
            "$ref": "#/components/schemas/SomeResource"
          }
        }
      }
    }
  ]
}
```

### Quality Checklist

Before completing any update, verify:

- [ ] **JSON is valid** (no syntax errors)
- [ ] **All references work** (no broken `$ref` paths)
- [ ] **Version is incremented** appropriately
- [ ] **New schemas are defined** if needed
- [ ] **Endpoint has all required fields**
- [ ] **Descriptions are comprehensive**
- [ ] **Naming conventions followed**
- [ ] **Standard error responses included**
- [ ] **Tags exist and are appropriate**
- [ ] **Security requirements included**
- [ ] **Business value is clear**
- [ ] **Follows existing patterns** in the specification

### Example Update Workflow

When asked to add a new endpoint:

1. **Check Microsoft docs git history** for context
2. **Analyze the documentation** provided
3. **Check existing categories and schemas** for reuse
4. **Determine the category** (existing or new)
5. **Create/update schemas** as needed
6. **Add the endpoint** with all required fields
7. **Update the version** appropriately
8. **Validate the changes**
9. **Provide a summary** of what was changed

### Communication Style

When providing updates:
- **Be concise but thorough**
- **Explain the reasoning** behind decisions
- **Highlight any assumptions** made
- **Note any potential issues** or considerations
- **Provide validation confirmation**
- **Reference Microsoft docs commit/changes** when relevant
- **Suggest next steps** if appropriate

### Error Handling

If there are issues with the request:
- **Ask for clarification** if documentation is unclear
- **Check Microsoft's git history** for additional context
- **Suggest alternatives** if the request seems problematic
- **Explain limitations** if something can't be done
- **Provide guidance** on how to resolve issues

### Discovery Commands Reference

```bash
# Current specification state
jq -r '.openapi' openapi.json                    # OpenAPI version
jq -r '.info.version' openapi.json               # API version
jq '.tags | length' openapi.json                 # Category count
jq '.components.schemas | keys | length' openapi.json  # Schema count

# Find patterns
jq -r '.tags[].name' openapi.json                # All categories
jq -r '[.. | .operationId? | select(. != null)] | unique[]' openapi.json  # All operation IDs
jq -r '.paths | keys[]' openapi.json             # All paths

# Validation
python3 -m json.tool openapi.json > /dev/null && echo "✅ Valid JSON"
jq -e '.paths' openapi.json > /dev/null && echo "✅ Has paths"

# Microsoft docs monitoring
cd defender-docs && CURRENT_COMMIT=$(jq -r '.info["x-microsoft-docs-commit"]' ../openapi.json) && git log --oneline $CURRENT_COMMIT..HEAD -- defender-endpoint/api/
```

---

**Remember**: The goal is to maintain a high-quality, comprehensive, and accurate OpenAPI specification that serves as the definitive reference for the Microsoft Defender for Endpoint API. Always check the current state of the specification and Microsoft's documentation changes before making updates.
