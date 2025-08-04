---
title: SIEM integration with Microsoft Defender for Office 365
f1.keywords:
  - NOCSH
ms.author: deniseb
author: denisebmsft
manager: deniseb
audience: ITPro
ms.topic: article
ms.localizationpriority: low
search.appverid:
  - MET150
  - MOE150
ms.assetid: eb56b69b-3170-4086-82cf-ba40a530fa1b
ms.date: 6/20/2023
ms.collection:
  - m365-security
  - tier2
description: Integrate your organization's SIEM server with Microsoft Defender for Office 365 and related threat events in the Office 365 Activity Management API.
ms.custom: seo-marvel-apr2020
ms.service: defender-office-365
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# SIEM integration with Microsoft Defender for Office 365

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

If your organization is using a security information and event management (SIEM) server, you can integrate Microsoft Defender for Office 365 with your SIEM server. You can set up this integration by using the [Office 365 Activity Management API](/office/office-365-management-api/office-365-management-activity-api-reference).

SIEM integration enables you to view information, such as malware or phish detected by Microsoft Defender for Office 365, in your SIEM server reports.

- To see an example of SIEM integration with Microsoft Defender for Office 365, see [this blog post](https://techcommunity.microsoft.com/blog/microsoftsecurityandcompliance/improve-the-effectiveness-of-your-soc-with-office-365-atp-and-the-o365-managemen/1525185).
- To learn more about the Office 365 Management APIs, see [Office 365 Management APIs overview](/office/office-365-management-api/office-365-management-apis-overview).

## How SIEM integration works

The Office 365 Activity Management API retrieves information about user, admin, system, and policy actions and events from your organization's Microsoft 365 and Microsoft Entra activity logs. If your organization has Microsoft Defender for Office 365 Plan 1 or 2, or Office 365 E5, you can use the [Microsoft Defender for Office 365 schema](/office/office-365-management-api/office-365-management-activity-api-schema#office-365-advanced-threat-protection-and-threat-investigation-and-response-schema).

Recently, events from automated investigation and response capabilities in [Microsoft Defender for Office 365 Plan 2](mdo-about.md#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet) were added to the Office 365 Management Activity API. In addition to including data about core investigation details such as ID, name and status, the API also contains high-level information about investigation actions and entities.

The SIEM server or other similar system polls the **audit.general** workload to access detection events. To learn more, see [Get started with Office 365 Management APIs](/office/office-365-management-api/get-started-with-office-365-management-apis).

## Enum: AuditLogRecordType - Type: Edm.Int32

### AuditLogRecordType

The following table summarizes the values of **AuditLogRecordType** that are relevant for Microsoft Defender for Office 365 events:

|Value|Member name|Description|
|---|---|---|
|28|ThreatIntelligence|Phishing and malware events from the default email protections for cloud mailboxes and from Microsoft Defender for Office 365.|
|41|ThreatIntelligenceUrl|Safe Links time-of-click and block override events from Microsoft Defender for Office 365.|
|47|ThreatIntelligenceAtpContent|Phishing and malware events for files in SharePoint, OneDrive, and Microsoft Teams, from Microsoft Defender for Office 365.|
|64|AirInvestigation|Automated investigation and response events, such as investigation details and relevant artifacts, from Microsoft Defender for Office 365 Plan 2.|

> [!IMPORTANT]
> You must have either the Global Administrator<sup>\*</sup> or Security Administrator role assigned to set up SIEM integration with Microsoft Defender for Office 365. For more information, see [Permissions in the Microsoft Defender portal](mdo-portal-permissions.md).
>
> <sup>\*</sup>Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.
>
> Audit logging must be turned on for your Microsoft 365 environment (it's on by default). To verify that audit logging is turned on or to turn it on, see [Turn auditing on or off](/purview/audit-log-enable-disable).

## See also

[Office 365 threat investigation and response](office-365-ti.md)

[Automated investigation and response (AIR) in Office 365](air-about.md)
