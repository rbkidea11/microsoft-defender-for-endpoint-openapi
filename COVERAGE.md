# Microsoft Defender API Documentation Coverage

## Status Legend
- ✅ Summarized
- 🔄 In Progress  
- ❌ Not Started
- 🚫 Skipped (not API endpoint)

## Coverage Tracking

| Microsoft Doc | Status | Summary File | Endpoint | Notes |
|---------------|--------|--------------|----------|-------|
| add-a-new-scan-definition.md | ✅ | summaries/add-a-new-scan-definition-summary.md | POST /api/DeviceAuthenticatedScanDefinitions, PATCH /api/DeviceAuthenticatedScanDefinitions/{id}, POST /api/DeviceAuthenticatedScanDefinitions/BatchDelete | 3 endpoints: add, update, delete scans |
| add-or-remove-machine-tags.md | ✅ | summaries/add-or-remove-machine-tags-summary.md | POST /api/machines/{id}/tags | Add or remove tags for a single machine |
| add-or-remove-multiple-machine-tags.md | ✅ | summaries/add-or-remove-multiple-machine-tags-summary.md | POST /api/machines/AddOrRemoveTagForMultipleMachines | Add or remove tags for multiple machines (up to 500) |
| alerts.md | 🚫 | - | - | Schema documentation |
| api-explorer.md | 🚫 | - | - | API explorer tool |
| api-hello-world.md | 🚫 | - | - | Tutorial documentation |
| api-power-bi.md | 🚫 | - | - | Power BI integration guide |
| api-release-notes.md | 🚫 | - | - | Release notes (references endpoints) |
| apis-intro.md | 🚫 | - | - | Introduction documentation |
| batch-delete-ti-indicators.md | ✅ | summaries/batch-delete-ti-indicators-summary.md | POST /api/indicators/BatchDelete | Batch delete up to 500 TI indicators |
| batch-update-alerts.md | ✅ | summaries/batch-update-alerts-summary.md | POST /api/alerts/batchUpdate | Batch update multiple alerts (status, determination, classification, assignedTo) |
| cancel-machine-action.md | ✅ | summaries/cancel-machine-action-summary.md | POST /api/machineactions/{machineactionid}/cancel | Cancel an already launched machine action |
| collect-investigation-package.md | ✅ | summaries/collect-investigation-package-summary.md | POST /api/machines/{id}/collectInvestigationPackage | Collect forensics investigation package from device |
| common-errors.md | 🚫 | - | - | Error documentation |
| create-alert-by-reference.md | ✅ | summaries/create-alert-by-reference-summary.md | POST /api/alerts/CreateAlertByReference | Create new alert from event (requires eventTime, machineId, reportId) |
| delete-library.md | ✅ | summaries/delete-library-summary.md | DELETE /api/libraryfiles/{fileName} | Delete file from live response library |
| delete-ti-indicator-by-id.md | ✅ | summaries/delete-ti-indicator-by-id-summary.md | DELETE /api/indicators/{id} | Delete threat intelligence indicator by ID |
| device-health-api-methods-properties.md | 🚫 | - | - | Properties documentation |
| device-health-export-antivirus-health-report-api.md | ✅ | summaries/device-health-export-antivirus-health-report-api-summary.md | GET /api/deviceavinfo, GET /api/machines/InfoGatheringExport | 2 endpoints: device health JSON response and file export |
| export-certificate-inventory-assessment.md | ✅ | summaries/export-certificate-inventory-assessment-summary.md | GET /api/machines/certificateAssessmentByMachine, GET /api/machines/certificateAssessmentExport | 2 endpoints: certificate assessment JSON (30/min, 1000/hr, pageSize 50K) and file export (5/min, 20/hr, gzip compressed) |
| export-firmware-hardware-assessment.md | ✅ | summaries/export-firmware-hardware-assessment-summary.md | GET /api/machines/HardwareFirmwareInventoryByMachine, GET /api/machines/HardwareFirmwareInventoryExport | 2 endpoints: hardware/firmware JSON (30/min, 1000/hr, Software.Read.All) and file export (5/min, 20/hr, 1hr URL validity, max 6hr) |
| export-security-baseline-assessment.md | ✅ | summaries/export-security-baseline-assessment-summary.md | GET /api/machines/baselineComplianceAssessmentByMachine, GET /api/machines/BaselineComplianceAssessmentExport | 2 endpoints: security baseline JSON (30/min, 1000/hr, SecurityBaselinesAssessment.Read.All, compliance data) and file export (5/min, 20/hr) |
| exposed-apis-create-app-nativeapp.md | 🚫 | - | - | App registration guide |
| exposed-apis-create-app-partners.md | 🚫 | - | - | Partner app guide |
| exposed-apis-create-app-webapp.md | 🚫 | - | - | Web app guide |
| exposed-apis-full-sample-powershell.md | 🚫 | - | - | PowerShell samples |
| exposed-apis-list.md | 🚫 | - | - | API list overview |
| exposed-apis-odata-samples.md | 🚫 | - | - | OData samples |
| fetch-alerts-mssp.md | 🚫 | - | - | MSSP guidance |
| files.md | 🚫 | - | - | Schema documentation |
| find-machine-info-by-ip.md | ✅ | summaries/find-machine-info-by-ip-summary.md | GET /api/machines/find(timestamp={time},key={IP}) | Find device by internal IP within 30 days, returns devices within 16 minutes of timestamp |
| find-machines-by-ip.md | ✅ | summaries/find-machines-by-ip-summary.md | GET /api/machines/findbyip(ip='{IP}',timestamp={TimeStamp}) | Find devices by internal IP within 15 minutes of timestamp, must be within past 30 days |
| find-machines-by-tag.md | ✅ | summaries/find-machines-by-tag-summary.md | GET /api/machines/findbytag?tag={tag}&useStartsWithFilter={true/false} | Find devices by tag with optional startswith filter |
| Get-agent-details.md | ✅ | summaries/Get-agent-details-summary.md | GET /api/DeviceAuthenticatedScanAgents/{id} | Get scan agent details by ID |
| get-alert-info-by-id.md | ✅ | summaries/get-alert-info-by-id-summary.md | GET /api/alerts/{id} | Get specific alert by ID |
| get-alert-related-domain-info.md | ✅ | summaries/get-alert-related-domain-info-summary.md | GET /api/alerts/{id}/domains | Get all domains related to a specific alert |
| get-alert-related-files-info.md | ✅ | summaries/get-alert-related-files-info-summary.md | GET /api/alerts/{id}/files | Get all files related to a specific alert |
| get-alert-related-ip-info.md | ✅ | summaries/get-alert-related-ip-info-summary.md | GET /api/alerts/{id}/ips | Get all IP addresses related to a specific alert |
| get-alert-related-machine-info.md | ✅ | summaries/get-alert-related-machine-info-summary.md | GET /api/alerts/{id}/machine | Get device information related to a specific alert |
| get-alert-related-user-info.md | ✅ | summaries/get-alert-related-user-info-summary.md | GET /api/alerts/{id}/user | Get user information related to a specific alert |
| get-alerts.md | ✅ | summaries/get-alerts-summary.md | GET /api/alerts | List alerts with OData V4 support, $expand=evidence, max 10K page size, comprehensive filtering |
| get-all-recommendations.md | ✅ | summaries/get-all-recommendations-summary.md | GET /api/recommendations | List all security recommendations with OData V4 support, 11 filterable fields, max 10K results |
| get-all-scan-agents.md | ✅ | summaries/get-all-scan-agents-summary.md | GET /api/DeviceAuthenticatedScanAgents | Get all authenticated scan agents with machine details, versions, last seen times |
| get-all-scan-definitions.md | ✅ | summaries/get-all-scan-definitions-summary.md | GET /api/DeviceAuthenticatedScanDefinitions | Get all scan definitions (Windows/Network types) with auth params, agent details, scan status |
| get-all-vulnerabilities-by-machines.md | ✅ | summaries/get-all-vulnerabilities-by-machines-summary.md | GET /api/vulnerabilities/machinesVulnerabilities | List vulnerabilities by machine/software with fixing KB, OData V4, 8 filterable fields, Power BI ready |
| get-all-vulnerabilities.md | ✅ | summaries/get-all-vulnerabilities-summary.md | GET /api/vulnerabilities | List all vulnerabilities with OData V4, 7 filterable fields, max 8K results |
| get-assessment-browser-extensions.md | ✅ | summaries/get-assessment-browser-extensions-summary.md | GET /api/Machines/BrowserExtensionsInventoryByMachine, GET /api/machines/browserextensionsinventoryExport | 2 endpoints: browser extensions JSON (30/min, 1K/hr) and file export (5/min, 20/hr), risk levels, permissions |
| get-assessment-information-gathering.md | ✅ | summaries/get-assessment-information-gathering-summary.md | GET /api/Machines/InfoGatheringExport | Information gathering assessment file export only (5/min, 20/hr), per device |
| get-assessment-non-cpe-software-inventory.md | ✅ | summaries/get-assessment-non-cpe-software-inventory-summary.md | GET /api/machines/SoftwareInventoryNoProductCodeByMachine, GET /api/machines/SoftwareInventoryNonCpeExport | 2 endpoints: non-CPE software JSON (30/min, 1K/hr) and file export (5/min, 20/hr) |
| get-assessment-secure-config.md | ✅ | summaries/get-assessment-secure-config-summary.md | GET /api/machines/SecureConfigurationsAssessmentByMachine, GET /api/machines/SecureConfigurationsAssessmentExport | 2 endpoints: secure config assessment JSON (30/min, 1K/hr) and file export (5/min, 20/hr) |
| get-assessment-software-inventory.md | ✅ | summaries/get-assessment-software-inventory-summary.md | GET /api/machines/SoftwareInventoryByMachine, GET /api/machines/SoftwareInventoryExport | 2 endpoints: CPE software inventory JSON (30/min, 1K/hr) and file export (5/min, 20/hr) |
| get-assessment-software-vulnerabilities.md | ✅ | summaries/get-assessment-software-vulnerabilities-summary.md | GET /api/machines/SoftwareVulnerabilitiesByMachine, GET /api/machines/SoftwareVulnerabilitiesExport, GET /api/machines/SoftwareVulnerabilityChangesByMachine | 3 endpoints: software vulnerabilities JSON (30/min, 1K/hr), file export (5/min, 20/hr), delta changes (30/min, 1K/hr, max 14 days) |
| get-assessment-methods-properties.md | 🚫 | - | - | Assessment methods documentation |
| get-authenticated-scan-properties.md | 🚫 | - | - | Properties documentation |
| get-browser-extensions-permission-info.md | ✅ | summaries/get-browser-extensions-permission-info-summary.md | GET /api/browserextensions/permissionsinfo | Get browser extensions permission information with OData V4 support, static data for extension permissions |
| get-device-secure-score.md | ✅ | summaries/get-device-secure-score-summary.md | GET /api/configurationScore | Get organizational device secure score (Microsoft Secure Score for Devices) |
| get-discovered-vulnerabilities.md | ✅ | summaries/get-discovered-vulnerabilities-summary.md | GET /api/machines/{machineId}/vulnerabilities | Get discovered vulnerabilities for a specific device (50/min, 1500/hr) |
| get-domain-related-alerts.md | ✅ | summaries/get-domain-related-alerts-summary.md | GET /api/domains/{domain}/alerts | Get alerts related to a specific domain |
| get-domain-related-machines.md | ✅ | summaries/get-domain-related-machines-summary.md | GET /api/domains/{domain}/machines | Get machines that communicated with a domain (limited to 500 devices) |
| get-domain-statistics.md | ✅ | summaries/get-domain-statistics-summary.md | GET /api/domains/{domain}/stats | Get domain statistics with lookBackHours parameter (max 30 days) |
| get-exposure-score.md | ✅ | summaries/get-exposure-score-summary.md | GET /api/exposureScore | Get organizational exposure score |
| get-file-information.md | ✅ | summaries/get-file-information-summary.md | GET /api/files/{id} | Get file information by identifier |
| get-file-related-alerts.md | ✅ | summaries/get-file-related-alerts-summary.md | GET /api/files/{id}/alerts | Get alerts related to a file hash (SHA-1 only) |
| get-file-related-machines.md | ✅ | summaries/get-file-related-machines-summary.md | GET /api/files/{id}/machines | Get machines related to a file hash (SHA-1 only) |
| get-file-statistics.md | ✅ | summaries/get-file-statistics-summary.md | GET /api/files/{id}/stats | Get file statistics with lookBackHours parameter (max 30 days) |
| get-installed-software.md | ✅ | summaries/get-installed-software-summary.md | GET /api/machines/{machineId}/software | Get installed software for a specific device |
| get-investigation-collection.md | ✅ | summaries/get-investigation-collection-summary.md | GET /api/investigations | List investigations with OData V4 support, 5 filterable fields, max 10K results |
| get-investigation-object.md | ✅ | summaries/get-investigation-object-summary.md | GET /api/investigations/{id} | Get investigation by ID (can use investigation ID or triggering alert ID) |
| get-ip-related-alerts.md | ✅ | summaries/get-ip-related-alerts-summary.md | GET /api/ips/{ip}/alerts | Get alerts related to a specific IP address |
| get-ip-statistics.md | ✅ | summaries/get-ip-statistics-summary.md | GET /api/ips/{ip}/stats | Get IP statistics with lookBackHours parameter (max 30 days) |
| get-live-response-result.md | ✅ | summaries/get-live-response-result-summary.md | GET /api/machineactions/{id}/GetLiveResponseResultDownloadLink(index={command-index}) | Get live response command result download link (valid for 30 minutes) |
| get-machine-by-id.md | ✅ | summaries/get-machine-by-id-summary.md | GET /api/machines/{id} | Get machine by device ID or computer name |
| get-machine-group-exposure-score.md | ✅ | summaries/get-machine-group-exposure-score-summary.md | GET /api/exposureScore/ByMachineGroups | List exposure score by device group |
| get-machine-log-on-users.md | ✅ | summaries/get-machine-log-on-users-summary.md | GET /api/machines/{id}/logonusers | Get logged on users for a specific device |
| get-machine-related-alerts.md | ✅ | summaries/get-machine-related-alerts-summary.md | GET /api/machines/{id}/alerts | Get all alerts related to a specific device |
| get-machineaction-object.md | ✅ | summaries/get-machineaction-object-summary.md | GET /api/machineactions/{id} | Get specific machine action by ID |
| get-machineactions-collection.md | ✅ | summaries/get-machineactions-collection-summary.md | GET /api/machineactions | List machine actions with OData V4 support, 6 filterable fields, max 10K results |
| get-machines-by-software.md | ✅ | summaries/get-machines-by-software-summary.md | GET /api/Software/{Id}/machineReferences | List devices that have specific software installed |
| get-machines-by-vulnerability.md | ✅ | summaries/get-machines-by-vulnerability-summary.md | GET /api/vulnerabilities/{cveId}/machineReferences | List devices affected by a specific vulnerability |
| get-machines.md | ✅ | summaries/get-machines-summary.md | GET /api/machines | List machines with OData V4 support, 12 filterable fields, max 10K results |
| get-missing-kbs-machine.md | ✅ | summaries/get-missing-kbs-machine-summary.md | GET /api/machines/{machineId}/getmissingkbs | Get missing security updates (KBs) by device ID |
| get-missing-kbs-software.md | ✅ | summaries/get-missing-kbs-software-summary.md | GET /api/Software/{Id}/getmissingkbs | Get missing security updates (KBs) by software ID |
| get-package-sas-uri.md | ✅ | summaries/get-package-sas-uri-summary.md | GET /api/machineactions/{id}/getPackageUri | Get SAS URI for downloading investigation package (2/min, 120/hr rate limit) |
| get-recommendation-by-id.md | ✅ | summaries/get-recommendation-by-id-summary.md | GET /api/recommendations/{id} | Get security recommendation by ID |
| get-recommendation-machines.md | ✅ | summaries/get-recommendation-machines-summary.md | GET /api/recommendations/{id}/machineReferences | List devices associated with a security recommendation |
| get-recommendation-vulnerabilities.md | ✅ | summaries/get-recommendation-vulnerabilities-summary.md | GET /api/recommendations/{id}/vulnerabilities | List vulnerabilities associated with a security recommendation |
| get-remediation-all-activities.md | ✅ | summaries/get-remediation-all-activities-summary.md | GET /api/remediationTasks | List all remediation activities with OData V4 support, 2 filterable fields, max 10K results |
| get-remediation-exposed-devices-activities.md | ✅ | summaries/get-remediation-exposed-devices-activities-summary.md | GET /api/remediationTasks/{id}/machineReferences | List exposed devices for a specific remediation activity |
| get-remediation-methods-properties.md | 🚫 | - | - | Remediation methods documentation |
| get-remediation-one-activity.md | ✅ | summaries/get-remediation-one-activity-summary.md | GET /api/remediationTasks/{id} | Get one remediation activity by ID |
| Get-scan-history-by-definition.md | ✅ | summaries/Get-scan-history-by-definition-summary.md | POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryByScanDefinitionId | Get scan history by definition IDs with OData support |
| Get-scan-history-by-session.md | ✅ | summaries/Get-scan-history-by-session-summary.md | POST /api/DeviceAuthenticatedScanDefinitions/GetScanHistoryBySessionId | Get scan history by session ID |
| get-security-baselines-assessment-configurations.md | ✅ | summaries/get-security-baselines-assessment-configurations-summary.md | GET /api/baselineConfigurations | List configurations in active baseline profiles with OData V4 support |
| get-security-baselines-assessment-profiles.md | ✅ | summaries/get-security-baselines-assessment-profiles-summary.md | GET /api/baselineProfiles | List all security baselines assessment profiles with OData V4 support |
| get-security-recommendations.md | ✅ | summaries/get-security-recommendations-summary.md | GET /api/machines/{machineId}/recommendations | Get security recommendations for a specific device |
| get-software-by-id.md | ✅ | summaries/get-software-by-id-summary.md | GET /api/Software/{Id} | Get software details by ID |
| get-software-ver-distribution.md | ✅ | summaries/get-software-ver-distribution-summary.md | GET /api/Software/{Id}/distributions | List software version distribution for organization |
| get-software.md | ✅ | summaries/get-software-summary.md | GET /api/Software | List software inventory with OData V4 support, 3 filterable fields, max 10K results |
| get-ti-indicators-collection.md | ✅ | summaries/get-ti-indicators-collection-summary.md | GET /api/indicators | List all active threat indicators with OData V4 support, 12 filterable fields |
| get-user-related-alerts.md | ✅ | summaries/get-user-related-alerts-summary.md | GET /api/users/{id}/alerts | Get alerts related to a specific user ID (username only, not full UPN) |
| get-user-related-machines.md | ✅ | summaries/get-user-related-machines-summary.md | GET /api/users/{id}/machines | Get devices related to a specific user ID (username only, not full UPN) |
| get-vuln-by-software.md | ✅ | summaries/get-vuln-by-software-summary.md | GET /api/Software/{Id}/vulnerabilities | List vulnerabilities in specific software |
| get-vulnerability-by-id.md | ✅ | summaries/get-vulnerability-by-id-summary.md | GET /api/vulnerabilities/{cveId} | Get vulnerability information by CVE ID |
| import-ti-indicators.md | ✅ | summaries/import-ti-indicators-summary.md | POST /api/indicators/import | Import batch of threat indicators (max 500, 30/min rate limit, 15K active limit) |
| initiate-autoir-investigation.md | ✅ | summaries/initiate-autoir-investigation-summary.md | POST /api/machines/{id}/startInvestigation | Start automated investigation on device (50/hr rate limit) |
| investigation.md | 🚫 | - | - | Schema documentation |
| isolate-machine.md | ✅ | summaries/isolate-machine-summary.md | POST /api/machines/{id}/isolate | Isolate device from network (Full/Selective/UnManagedDevice types) |
| list-library-files.md | ✅ | summaries/list-library-files-summary.md | GET /api/libraryfiles | List live response library files |
| list-recommendation-software.md | ✅ | summaries/list-recommendation-software-summary.md | GET /api/recommendations/{id}/software | Get software associated with a security recommendation |
| machine.md | 🚫 | - | - | Schema documentation |
| machineaction.md | 🚫 | - | - | Schema documentation |
| management-apis.md | 🚫 | - | - | Overview documentation |
| offboard-machine-api.md | ✅ | summaries/offboard-machine-api-summary.md | POST /api/machines/{id}/offboard | Offboard device from Defender for Endpoint (Windows only, not macOS/Linux) |
| post-ti-indicator.md | ✅ | summaries/post-ti-indicator-summary.md | POST /api/indicators | Submit or update threat indicator (15K active limit, 100/min rate limit) |
| raw-data-export-event-hub.md | 🚫 | - | - | Configuration guide |
| raw-data-export-storage.md | 🚫 | - | - | Configuration guide |
| raw-data-export.md | 🚫 | - | - | Overview documentation |
| recommendation.md | 🚫 | - | - | Schema documentation |
| restrict-code-execution.md | ✅ | summaries/restrict-code-execution-summary.md | POST /api/machines/{id}/restrictCodeExecution | Restrict app execution on device (Windows 10 1709+, requires Defender Antivirus) |
| run-advanced-query-api.md | ✅ | summaries/run-advanced-query-api-summary.md | POST /api/advancedqueries/run | Run advanced hunting queries (KQL) with limitations (30 days, 100K rows, rate limits) |
| run-advanced-query-sample-powershell.md | 🚫 | - | - | Sample code |
| run-advanced-query-sample-python.md | 🚫 | - | - | Sample code |
| run-av-scan.md | ✅ | summaries/run-av-scan-summary.md | POST /api/machines/{id}/runAntiVirusScan | Run antivirus scan on device (Quick/Full scan types) |
| run-live-response.md | ✅ | summaries/run-live-response-summary.md | POST /api/machines/{id}/runliveresponse | Run live response commands on device (PutFile, RunScript, GetFile) |
| score.md | 🚫 | - | - | Schema documentation |
| set-device-value.md | ✅ | summaries/set-device-value-summary.md | POST /api/machines/{machineId}/setDeviceValue | Set device value (Normal/Low/High) |
| software.md | 🚫 | - | - | Schema documentation |
| stop-and-quarantine-file.md | ✅ | summaries/stop-and-quarantine-file-summary.md | POST /api/machines/{id}/StopAndQuarantineFile | Stop execution and quarantine file by SHA1 |
| ti-indicator.md | 🚫 | - | - | Schema documentation |
| unisolate-machine.md | ✅ | summaries/unisolate-machine-summary.md | POST /api/machines/{id}/unisolate | Release device from isolation |
| unrestrict-code-execution.md | ✅ | summaries/unrestrict-code-execution-summary.md | POST /api/machines/{id}/unrestrictCodeExecution | Remove app execution restriction from device |
| update-alert.md | ✅ | summaries/update-alert-summary.md | PATCH /api/alerts/{id} | Update alert properties (status, determination, classification, assignedTo, comment) |
| update-machine-method.md | ✅ | summaries/update-machine-method-summary.md | PATCH /api/machines/{machineId} | Update machine properties (tags and deviceValue) |
| upload-library.md | ✅ | summaries/upload-library-summary.md | POST /api/libraryfiles | Upload file to live response library (20MB max, multipart/form-data) |
| user.md | 🚫 | - | - | Schema documentation |
| vulnerability.md | 🚫 | - | - | Schema documentation |

## Progress Summary
- **Total Microsoft Docs**: 136 files
- **API Documentation Files**: 102 files
- **Non-API Documentation Files**: 34 files (skipped - schemas, guides, tutorials)
- **Summary Files Created**: 102/102 (100%) ✅
- **API Documentation Files Without Summaries**: 0/102 (0%) 🎉
- **Documentation Review Coverage**: 102/102 (100%) - All API docs reviewed and documented
- **In Progress**: 0/102 (0%)
- **Remaining Summary Work**: 0 files - ALL COMPLETE! 🎉

## Recent Findings from Manual Review
- ✅ **Additional endpoints discovered**: Found multiple endpoints in some documentation files
- ✅ **Detailed parameter information**: Parameter names, rate limits, permissions documented
- ✅ **Request/response examples**: All files contain comprehensive examples
- ✅ **Accurate endpoint paths**: Corrected several endpoint path variations
- ✅ **Standardized summaries**: All summaries use streamlined format focused on OpenAPI generation
- ✅ **API DOCUMENTATION REVIEW COMPLETE**: All 102 API documentation files reviewed and documented

## Discovered Additional Endpoints
Some documentation files contain multiple related endpoints:

1. **add-a-new-scan-definition.md**: 3 endpoints (not 1) - POST, PATCH, POST BatchDelete
2. **device-health-export**: 2 endpoints (not 1) - deviceavinfo + InfoGatheringExport  
3. **export-certificate-inventory**: 2 endpoints - JSON + file export
4. **export-firmware-hardware**: 2 endpoints - JSON + file export
5. **export-security-baseline**: 2 endpoints - JSON + file export
6. **get-assessment-software-vulnerabilities**: 3 endpoints - JSON, file export, delta changes

**Note**: The total number of actual API endpoints is higher than the number of documentation files due to some files documenting multiple related endpoints.

## Next Steps
1. ✅ Create summary template
2. ✅ Start with high-priority endpoints (alerts, machines, etc.)
3. 🔄 Generate OpenAPI spec from summaries
4. 🔄 Validate against Microsoft docs

**🎉 MILESTONE ACHIEVED: 100% DOCUMENTATION COVERAGE COMPLETE! 🎉**

All 102 Microsoft Defender for Endpoint API documentation files have been reviewed and documented. Each file now has a comprehensive summary ready for OpenAPI specification generation.

## Summary Files Complete (102/102) - 100% ✅

All API documentation files now have comprehensive summary files created and are ready for OpenAPI specification generation!
