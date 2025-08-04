# Contributing to Microsoft Defender for Endpoint OpenAPI Specification

Thank you for your interest in contributing! This OpenAPI specification is AI-generated and community-maintained.

## 🚨 Important Notes

- This specification is **AI-generated** and may contain inaccuracies
- Always **validate endpoints** against Microsoft's actual API before submitting changes
- We welcome corrections, improvements, and additions based on real-world testing

## 🐛 Reporting Issues

### Found a Bug or Inaccuracy?
1. **Check existing issues** to avoid duplicates
2. **Test against Microsoft's API** to confirm the issue
3. **Use the bug report template** when creating an issue
4. **Include**:
   - Specific endpoint affected
   - Expected vs actual behavior
   - Example request/response if possible

### Missing Endpoint?
1. **Verify the endpoint exists** in Microsoft's documentation
2. **Check it's not already in the spec** (search the JSON file)
3. **Use the missing endpoint template**
4. **Include**:
   - Link to Microsoft's documentation
   - HTTP method and path
   - Brief description of functionality

## 🔧 Making Changes

### Small Fixes (typos, descriptions, etc.)
1. **Fork the repository**
2. **Make your changes**
3. **Test JSON validity**: `python3 -m json.tool openapi.json`
4. **Submit a pull request**

### Adding New Endpoints
1. **Reference Microsoft's official documentation**
2. **Follow existing patterns** in the specification
3. **Include all required fields**:
   - `tags`, `summary`, `description`, `operationId`
   - Proper `responses` with error codes
   - `security` requirements
4. **Update the API version** if adding significant functionality
5. **Test the endpoint** if possible

### Schema Changes
1. **Ensure backward compatibility** when possible
2. **Follow OpenAPI 3.0.3 standards**
3. **Use consistent naming conventions**:
   - `camelCase` for parameters
   - `PascalCase` for schemas
   - Descriptive `operationId`s

## 📋 Pull Request Process

1. **Update documentation** if needed
2. **Ensure JSON is valid**
3. **Follow the PR template**
4. **Reference any related issues**
5. **Be patient** - reviews may take time

## 🎯 What We're Looking For

### High Priority
- **Corrections** to existing endpoints based on real API testing
- **Missing endpoints** from Microsoft's official documentation
- **Schema fixes** where AI generation was incorrect
- **Rewst integration improvements**

### Medium Priority
- **Better descriptions** and examples
- **Additional OData parameter support**
- **Response schema improvements**

### Low Priority
- **Cosmetic changes** to descriptions
- **Reorganization** without functional benefit

## 🚫 What We Won't Accept

- **Speculative endpoints** not in Microsoft's documentation
- **Breaking changes** without strong justification
- **Untested modifications** to working endpoints
- **Changes that break OpenAPI 3.0.3 compatibility**

## 📚 Resources

- [Microsoft Defender for Endpoint API Documentation](https://docs.microsoft.com/en-us/microsoft-365/security/defender-endpoint/apis-intro)
- [OpenAPI 3.0.3 Specification](https://spec.openapis.org/oas/v3.0.3)
- [Rewst Custom Integrations Documentation](https://docs.rewst.help/documentation/configuration/integrations/custom-integrations/custom-integrations-v2)

## 🤝 Code of Conduct

- **Be respectful** and constructive
- **Focus on the technical merit** of contributions
- **Help others** learn and improve
- **Remember** this is a community effort to improve security automation

## 🙋 Questions?

- **Check existing issues** first
- **Create a discussion** for general questions
- **Tag issues appropriately** for faster response

Thank you for helping make this specification better! 🛡️
