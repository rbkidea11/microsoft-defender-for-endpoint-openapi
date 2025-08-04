---
title: Microsoft Defender for Office 365 data retention
f1.keywords:
- NOCSH
ms.author: dansimp
author: dansimp
manager: deniseb
ms.date: 05/08/2025
audience: ITPro
ms.topic: article
ms.service: defender-office-365
ms.localizationpriority: medium
ms.collection:
- m365-security
- tier2
- essentials-compliance
- essentials-security
ms.custom:
description: Admins can learn how long Defender for Office 365 features retain data.
search.appverid: met150
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
---

# Data retention information for Microsoft Defender for Office 365

By default, data across different features is retained for a maximum of 30 days. However, for some of the features, you can specify the retention period based on policy. See the following table for the different retention periods for each feature.

> [!NOTE]
> Microsoft Defender for Office 365 comes in two different subscriptions: **Plan 1** and **Plan 2**. If you have **Threat Explorer** at <https://security.microsoft.com/threatexplorer>, you have Plan 2. Otherwise, you have **Real-time Detections** at <https://security.microsoft.com/realtimereports> as part of **Plan 1**.
>
> Your Defender for Office 365 subscription affects the tools that are available to you, so make sure you know which subscription you have as you learn.

## Defender for Office 365 Plan 1

|Feature|Retention period|
|---|---|
|Alert metadata details (Defender for Office 365 alerts)|90 days.|
|Entity metadata details (Email)|30 days.|
|Activity alert details (audit logs)|7 days.|
|Email entity page|30 days.|
|Quarantine|30 days (configurable; 30 days is the maximum).|
|Reports|90 days for aggregated data. <br/><br/> 30 days for detailed information.|
|Submissions|30 days.|
|Real-Time detections|30 days.|

## Defender for Office 365 Plan 2

Defender for Office 365 Plan 1 capabilities, plus:

|Feature|Retention period|
|---|---|
|Action Center|180 days. <br/><br/> Office Action Center 30 days.|
|Advanced Hunting|30 days.|
|AIR (Automated investigation and response)|60 days for investigations metadata. <br/><br/> 30 days for email metadata.|
|Attack simulation training data|18 months.|
|Campaigns|30 days.|
|Incidents|30 days.|
|Remediation|30 days|
|Threat Analytics|30 days.|
|Threat Explorer|30 days.|
|Threat Trackers|30 days.|
