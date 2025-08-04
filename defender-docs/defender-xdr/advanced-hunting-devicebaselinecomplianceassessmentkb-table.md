---
title: DeviceBaselineComplianceAssessmentKB table in the advanced hunting schema
description: Learn about the various security configurations used by baseline compliance to assess devices in the DeviceBaselineComplianceAssessmentKB table in the advanced hunting schema.
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
f1.keywords: 
  - NOCSH
ms.author: maccruz
author: samanthagy
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.custom: 
- cx-ti
- cx-ah
appliesto:
    - Microsoft Defender XDR
    - Microsoft Sentinel in the Microsoft Defender portal
ms.topic: reference
ms.date: 03/28/2025
---

# DeviceBaselineComplianceAssessmentKB (Preview)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]




> [!IMPORTANT]
> Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The `DeviceBaselineComplianceAssessmentKB` table in the advanced hunting schema contains information about various security configurations used by baseline compliance to assess devices.

This advanced hunting table is populated by records from Microsoft Defender for Endpoint. If your organization hasn’t deployed the service in Microsoft Defender XDR, queries that use the table aren’t going to work or return any results. For more information about how to deploy Defender for Endpoint in Defender XDR, read [Deploy supported services](deploy-supported-services.md).

For information on other tables in the advanced hunting schema, see [the advanced hunting reference](advanced-hunting-schema-tables.md).

| Column name | Data type | Description |
|-------------|-----------|-------------|
| `ConfigurationId` | `string` | Unique identifier for a specific configuration |
| `ConfigurationName` | `string` | Display name of the configuration |
| `ConfigurationDescription` | `string` | Description of the configuration |
| `ConfigurationRationale` | `string` | Description of any associated risks and rationale behind the configuration |
| `ConfigurationCategory` | `string` | Category or grouping to which the configuration belongs |
| `BenchmarkProfileLevels` | `dynamic` | List of benchmark compliance levels for which the configuration is applicable |
| `CCEReference` | `string` | Unique Common Configuration Enumeration (CCE) identifier for the configuration |
| `RemediationOptions` | `string` | Recommended actions to reduce or address any associated risks |
| `ConfigurationBenchmark` | `string` | Industry benchmark recommending the configuration |
| `Source` | `dynamic` | The registry path or other location used to determine the current device setting |
| `RecommendedValue` | `dynamic` | Set of expected values for the current device setting to be compliant |


## Related topics

- [DeviceBaselineComplianceAssessment](advanced-hunting-devicebaselinecomplianceassessment-table.md)
- [Understand the schema](advanced-hunting-schema-tables.md)
- [Apply query best practices](advanced-hunting-best-practices.md)
- [Overview of Defender Vulnerability Management](/windows/security/threat-protection/microsoft-defender-atp/next-gen-threat-and-vuln-mgt)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
