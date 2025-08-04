# Microsoft Defender for Endpoint OpenAPI Specification

<img src="microsoft-windows-defender.svg" alt="Microsoft Defender" width="64" height="64">

A comprehensive OpenAPI 3.0.3 specification for the Microsoft Defender for Endpoint API, providing complete enterprise-grade security operations coverage.

> ⚠️ **AI Generated Content**: This OpenAPI specification has been generated using AI based on Microsoft's official documentation. While comprehensive, it has not been fully tested against all endpoints. Please validate endpoints and schemas in your specific environment before production use.

## 📋 Overview

This repository contains a production-ready OpenAPI specification that covers the entire Microsoft Defender for Endpoint API surface. It's designed for:

- **API Integration Platforms** (like Rewst, Zapier, etc.)
- **Code Generation** (client SDKs, server stubs)
- **API Documentation** and exploration
- **Testing and Validation** of API implementations
- **Enterprise Security Automation**

## 🚀 Quick Start

### Using the OpenAPI Specification

1. **Download the specification**: `openapi.json`
2. **Import into your tool** of choice (Postman, Insomnia, etc.)
3. **Generate client code** using OpenAPI generators
4. **Configure authentication** (see Authentication section below)

### Current Status

- **OpenAPI Version**: 3.0.3 (maximum tool compatibility)
- **API Coverage**: 104+ endpoints across 17+ categories
- **Status**: AI-generated, actively maintained
- **Authentication**: OAuth2 with Microsoft Entra ID

## 🔧 Rewst Integration Setup

This OpenAPI specification is optimized for use with [Rewst](https://rewst.io) automation platform. Follow these steps to configure it as a custom integration using Rewst's V2 custom integrations feature:

> 📝 **Note**: These instructions are based on Rewst's documentation but have not been fully tested. Please verify each step in your environment.

### Prerequisites: Create Azure App Registration

1. Follow Microsoft's guide: [Create an app registration](https://learn.microsoft.com/en-us/defender-endpoint/api/exposed-apis-create-app-webapp)
2. Note your **Tenant ID**, **Client ID**, and **Client Secret**
3. Grant appropriate API permissions for Microsoft Defender for Endpoint

### Step 1: Add Custom Integration

1. **Navigate to** Configuration → Integrations in your Rewst platform
2. **Click** "Add New Integration"
3. **Click** "Add OpenAPI Integration" (since you have the JSON file)
4. **Upload** the `openapi.json` file from this repository
5. **Click** "Submit"

### Step 2: Configure Integration Details

Fill in the basic integration information:

- **Name**: `Microsoft Defender for Endpoint`
- **Icon**: Upload the `microsoft-windows-defender.svg` file (SVG format required)
- **Description**: `Enterprise endpoint security and threat protection API`
- **Click** "Next"

### Step 3: Configure Authentication

Set up the authentication method:

1. **Hostname**: `api.securitycenter.microsoft.com` (without https://)
2. **Authentication Method**: Select `OAuth 2.0`
3. **Grant Type**: `Client Credentials`
4. **Click** "Next"

Fill out the OAuth 2.0 authentication details:

- **Token URL**: `https://login.microsoftonline.com/{YOUR_TENANT_ID}/oauth2/v2.0/token`
  - Replace `{YOUR_TENANT_ID}` with your actual Azure tenant ID
- **Client ID**: Your Azure app registration client ID
- **Client Secret**: Your Azure app registration client secret
- **Scope**: `https://api.securitycenter.microsoft.com/.default`
- **Click** "Next"

### Step 4: Configure Pagination

Select pagination settings for endpoints that return collections:

1. **Pagination Type**: Select `Link` from the dropdown
2. **Click** "Next"

Fill out the pagination details:

| Field | Value | Description |
|-------|-------|-------------|
| **Results Key** | `value` | Path to the array of results in response |
| **Page Size Param** | `$top` | Query parameter for controlling page size |
| **Default Page Size** | `100` | Default number of items per page |
| **Default Page Limit** | `10` | Maximum number of pages to fetch |
| **Next Page Key** | `@odata.nextLink` | Key containing the next page URL |
| **Next Link Location** | `JSON Response Body` | Where to find the next page link |

Leave these fields **empty** (use defaults):
- Response Header Rel
- Response Header Name

**Click** "Next"

### Step 5: Review and Finalize Actions

1. **Review** the automatically imported actions from the OpenAPI specification
2. **Edit** any actions if needed (optional - the defaults should work well)
3. **Click** "Finalize"
4. **Click** "Finalize" again to confirm

### Step 6: Set Integration Status

Choose the appropriate status for your integration:

- **Published**: Makes the integration available for installation by your organization
- **Draft**: Keeps it in development mode (can still be edited)
- **Hidden**: Hides it from the integration list

### Step 7: Install the Integration

1. **Navigate to** Configuration → Integrations
2. **Find** your "Microsoft Defender for Endpoint" integration
3. **Click** "Install" or "Configure"
4. **Enter** your specific Azure credentials:
   - Client ID
   - Client Secret
   - Tenant ID (if prompted)
5. **Test** the connection
6. **Save** the configuration

## 🔐 Authentication

All endpoints require OAuth2 authentication with Microsoft Entra ID:

```http
Authorization: Bearer {access_token}
```

### Required API Permissions

Your Azure app registration needs these Microsoft Graph permissions:

| Permission | Type | Description |
|------------|------|-------------|
| `Machine.Read.All` | Application | Read machine information |
| `Alert.Read.All` | Application | Read security alerts |
| `Alert.ReadWrite.All` | Application | Read and write security alerts |
| `File.Read.All` | Application | Read file information |
| `User.Read.All` | Application | Read user information |
| `SecurityRecommendation.Read.All` | Application | Read security recommendations |
| `Vulnerability.Read.All` | Application | Read vulnerability information |
| `AdvancedQuery.Read.All` | Application | Run advanced hunting queries |

### Permission Scopes by Category

- **Read-only operations**: `Machine.Read.All`, `Alert.Read.All`, `File.Read.All`
- **Alert management**: `Alert.ReadWrite.All`
- **Advanced hunting**: `AdvancedQuery.Read.All`
- **Machine actions**: `Machine.Isolate`, `Machine.RestrictExecution`

## 📊 API Coverage

| Category | Endpoints | Description |
|----------|-----------|-------------|
| **Alert** | 10 | Alert management and investigation |
| **Machine** | 14 | Device management and operations |
| **MachineAction** | 14 | Device actions and remediation |
| **File** | 4 | File analysis and investigation |
| **User** | 2 | User-related security data |
| **Vulnerability** | 4 | Vulnerability management |
| **Recommendation** | 5 | Security recommendations |
| **AdvancedHunting** | 1 | KQL query execution |
| **Assessment** | 5 | Security assessment exports |
| **AuthenticatedScan** | 7 | Scan management |
| **AutomatedInvestigation** | 3 | Investigation management |
| **BrowserExtensions** | 2 | Browser extension assessment |
| **CertificateInventory** | 1 | Certificate assessment |
| **DeviceHealth** | 2 | Device health reporting |
| **Domain** | 3 | Domain analysis |
| **Indicators** | 5 | Threat indicator management |
| **InformationGathering** | 1 | Information gathering assessment |
| **IP** | 2 | IP address analysis |
| **LiveResponseLibrary** | 3 | Live response file management |
| **RemediationActivity** | 3 | Remediation tracking |
| **Score** | 3 | Security scoring |
| **SecurityBaseline** | 4 | Baseline compliance |
| **Software** | 6 | Software inventory management |

## 🔍 Key Features

### OData Query Support
Many endpoints support OData queries for filtering and pagination:
- `$filter` - Filter results (e.g., `status eq 'Active'`)
- `$top` - Limit number of results (e.g., `$top=50`)
- `$skip` - Skip number of results (e.g., `$skip=100`)
- `$expand` - Expand related entities (alerts only: `$expand=evidence`)

### Rate Limiting
- **100 calls per minute**
- **1,500 calls per hour**

### Response Formats
All endpoints return JSON with consistent error handling and standard HTTP status codes.

## 📚 Common Rewst Workflow Examples

### 1. Alert Monitoring Workflow
```yaml
# Trigger: Scheduled (every 5 minutes)
# Action: Get recent alerts
GET /api/alerts?$filter=alertCreationTime gt {last_check_time}
```

### 2. Machine Investigation Workflow
```yaml
# Trigger: Alert webhook
# Actions:
# 1. Get machine details
GET /api/machines/{machine_id}
# 2. Get machine alerts
GET /api/machines/{machine_id}/alerts
# 3. Isolate machine if high severity
POST /api/machines/{machine_id}/isolate
```

### 3. Vulnerability Reporting Workflow
```yaml
# Trigger: Weekly schedule
# Actions:
# 1. Export vulnerability assessment
GET /api/machines/SoftwareVulnerabilitiesExport
# 2. Process and send report
```

## 🛠️ Development & Maintenance

### Repository Structure
```
├── openapi.json                 # Main OpenAPI specification
├── README.md                    # This file
├── amazonq.md                   # AI maintenance instructions
├── microsoft-windows-defender.svg # Integration icon
├── .gitignore                   # Git ignore rules
├── .gitmodules                  # Git submodules configuration
├── defender-docs/               # Microsoft docs submodule
└── .git/                        # Git repository
```

### Validation Commands
```bash
# Validate JSON syntax
python3 -m json.tool openapi.json > /dev/null && echo "✅ Valid JSON"

# Check endpoint count
jq '[.paths | to_entries[] | .value | to_entries[] | select(.key | test("get|post|put|delete|patch"))] | length' openapi.json

# List all categories
jq -r '.tags[].name' openapi.json

# Check current Microsoft docs version
jq -r '.info["x-microsoft-docs-commit"]' openapi.json
```

### Microsoft Documentation Tracking
This specification tracks the Microsoft documentation it's based on via git submodule:

```bash
# Check for Microsoft docs updates
git submodule update --remote defender-docs
cd defender-docs
CURRENT_COMMIT=$(jq -r '.info["x-microsoft-docs-commit"]' ../openapi.json)
git log --oneline $CURRENT_COMMIT..HEAD -- defender-endpoint/api/
```

## 🚨 Troubleshooting

### Common Integration Issues

**Authentication Failures**
- Verify tenant ID in OAuth URL
- Check client ID and secret
- Ensure proper API permissions granted
- Confirm app registration is not expired

**Pagination Not Working**
- Verify "Link" pagination type is selected
- Check that `@odata.nextLink` is set as Next Page Key
- Ensure Results Key is set to `value`

**Rate Limiting**
- Implement exponential backoff in workflows
- Use workflow delays between API calls
- Monitor rate limit headers in responses

**Missing Endpoints**
- Check if endpoint requires specific permissions
- Verify OpenAPI specification is latest version
- Confirm endpoint exists in Microsoft's documentation

**Schema Validation Errors**
- Some AI-generated schemas may not match actual API responses
- Test endpoints individually and report discrepancies
- Check Microsoft's official documentation for accurate schemas

## ⚠️ Important Disclaimers

- **AI Generated**: This specification was created using AI and may contain inaccuracies
- **Not Fully Tested**: Endpoints and schemas should be validated in your environment
- **Use at Your Own Risk**: Test thoroughly before production deployment
- **Community Contributions Welcome**: Please report issues and improvements

## 🤝 Contributing

This specification is actively maintained and synchronized with Microsoft's official documentation.

### Reporting Issues
- **Missing endpoints**: Reference Microsoft's latest API documentation
- **Schema errors**: Provide example request/response data with actual vs expected
- **Integration issues**: Include platform details and error messages
- **AI inaccuracies**: Help improve the specification by reporting discrepancies

### Updates
The specification uses Microsoft's documentation repository as a git submodule, ensuring accuracy and up-to-date coverage.

## 📄 License

This OpenAPI specification is provided under the MIT License. The underlying Microsoft Defender for Endpoint API is subject to Microsoft's API terms of use.

## 🔗 Related Links

- [Microsoft Defender for Endpoint API Documentation](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/apis-intro)
- [Azure App Registration Guide](https://learn.microsoft.com/en-us/defender-endpoint/api/exposed-apis-create-app-webapp)
- [Rewst Custom Integrations Documentation](https://docs.rewst.help/documentation/configuration/integrations/custom-integrations/custom-integrations-v2)
- [Rewst Platform](https://rewst.io)
- [OpenAPI Specification](https://spec.openapis.org/oas/v3.0.3)

---

**Built for enterprise security automation with Rewst** 🛡️ 🤖

*AI-generated specification - validate before production use*
