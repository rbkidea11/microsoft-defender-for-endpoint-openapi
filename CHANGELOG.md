# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-08-03

### Added
- Initial release of Microsoft Defender for Endpoint OpenAPI 3.0.3 specification
- Complete coverage of 104+ endpoints across 17+ categories
- Support for all major endpoint categories:
  - Alert management and investigation
  - Machine management and operations
  - Machine actions and remediation
  - File analysis and investigation
  - User-related security data
  - Vulnerability management
  - Security recommendations
  - Advanced hunting (KQL queries)
  - Security assessments and exports
  - Authenticated scan management
  - Automated investigation management
  - Browser extensions assessment
  - Certificate inventory
  - Device health reporting
  - Domain analysis
  - Threat indicator management
  - Information gathering assessment
  - IP address analysis
  - Live response library management
  - Remediation activity tracking
  - Security scoring
  - Security baseline compliance
  - Software inventory management
- OAuth2 authentication with Microsoft Entra ID
- OData query support ($filter, $top, $skip, $expand for alerts)
- Comprehensive error response schemas
- Rate limiting documentation (100 calls/minute, 1,500 calls/hour)
- Rewst integration optimization with Link pagination support
- Microsoft documentation tracking via git submodule
- AI-generated content with appropriate disclaimers

### Technical Details
- OpenAPI version: 3.0.3 (maximum tool compatibility)
- Base URL: https://api.securitycenter.microsoft.com
- Authentication: OAuth2 Client Credentials flow
- Microsoft docs commit: b638ce17d127d2c83d4a7b81531c06fd4372c54c
- Microsoft docs date: 2025-07-09T17:07:38Z

### Documentation
- Comprehensive README with Rewst integration instructions
- AI maintenance instructions (amazonq.md)
- Contributing guidelines
- GitHub issue and PR templates
- MIT License with Microsoft attribution

### Notes
- This specification is AI-generated based on Microsoft's official documentation
- Not all endpoints have been fully tested against the live API
- Users should validate endpoints in their specific environment before production use
- Community contributions and corrections are welcome

[1.0.0]: https://github.com/yourusername/microsoft-defender-for-endpoint-openapi/releases/tag/v1.0.0
