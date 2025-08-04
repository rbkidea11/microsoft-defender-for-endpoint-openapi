---
title: Get notified about remediation actions
description: Get an overview of remediation actions that follow automated investigations in the Microsoft Defender portal
search.appverid: met150
ms.service: defender-xdr
f1.keywords: 
  - NOCSH
ms.author: diannegali
author: diannegali
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
  - m365-security
  - tier3
ms.topic: concept-article
ms.custom: autoir
ms.reviewer: evaldm, isco
ms.date: 04/28/2025
appliesto:
  - Microsoft Defender XDR
#customer intent: As a SOC analyst, I want to understand the remediation actions that follow automated investigations in Microsoft Defender XDR
---

# Get notified about remediation actions

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

During and after an automated investigation, remediation actions are identified for malicious or suspicious items. Some kinds of remediation actions are taken on devices, also referred to as endpoints. Other remediation actions are taken on identities, accounts, and email content. In addition, some types of remediation actions can occur automatically, whereas other types of remediation actions are taken manually by your organization's security team. When an automated investigation results in one or more remediation actions, the investigation completes only when the remediation actions are taken, approved, or rejected.

> [!IMPORTANT]
> Whether remediation actions are taken automatically or only upon approval depends on certain settings, such as automation levels. To learn more, see the following articles:
>
> - [Configure your automated investigation and response capabilities in Microsoft Defender XDR](m365d-configure-auto-investigation-response.md)
> - [Configure action accounts in Microsoft Defender for Identity](/defender-for-identity/manage-action-accounts)
> - [How threats are remediated on devices](/defender-endpoint/automated-investigations)
> - [Threats and remediation actions on email & collaboration content](/defender-office-365/air-remediation-actions#threats-and-remediation-actions)

The following table summarizes remediation actions that are currently supported in Microsoft Defender XDR.

|Device (endpoint) remediation actions  |Email remediation actions  |Users (accounts)  |
|:---------|:---------|----------|
|- Collect investigation package <br/>- Isolate device (this action can be undone)<br/>- Offboard machine <br/>- Release code execution <br/>- Release from quarantine <br/>- Request sample <br/>- Restrict code execution (this action can be undone) <br/>- Run antivirus scan <br/>- Stop and quarantine <br/>- Contain devices from the network     |- Block URL (time-of-click)<br/>- Soft delete email messages or clusters<br/>- Quarantine email<br/>- Quarantine an email attachment<br/>- Turn off external mail forwarding          |- Disable user<br />- Reset user password<br />- Confirm user as compromised          |

Remediation actions, whether pending approval or already complete, can be viewed in the [Action center](m365d-action-center.md).

## Remediation actions that follow automated investigations

When an automated investigation completes, a verdict is reached for every piece of evidence involved. Depending on the verdict, remediation actions are identified. In some cases, remediation actions are taken automatically; in other cases, remediation actions await approval. It all depends on how [automated investigation and response is configured](m365d-configure-auto-investigation-response.md).

The following table lists possible verdicts and outcomes:

| Verdict    | Affected entities    | Outcomes|
|------|------|------|
| Malicious    | Devices (endpoints)    | Remediation actions are taken automatically (assuming your organization's [device groups](m365d-configure-auto-investigation-response.md#review-or-change-the-automation-level-for-device-groups) are set to **Full - remediate threats automatically**)|
| Compromised | Users | Remediation actions are taken automatically |
| Malicious    | Email content (URLs or attachments) | Recommended remediation actions are pending approval|
| Suspicious    | Devices or email content | Recommended remediation actions are pending approval|
| No threats found    | Devices or email content    | No remediation actions are needed|

## Remediation actions that are taken manually

In addition to remediation actions that follow automated investigations, your security operations team can take certain remediation actions manually. These actions include:

- Manual device action, such as device isolation or file quarantine
- Manual email action, such as soft-deleting email messages
- Manual user action, such as disable user or reset user password
- [Advanced hunting](advanced-hunting-overview.md) action on devices, users, or email
- [Explorer](/defender-office-365/threat-explorer-real-time-detections-about) action on email content, such as moving email to junk, soft-deleting email, or hard-deleting email
- Manual [live response](/windows/security/threat-protection/microsoft-defender-atp/live-response) action, such as deleting a file, stopping a process, and removing a scheduled task
- Live response action with [Microsoft Defender for Endpoint APIs](/defender-endpoint/api/management-apis#microsoft-defender-for-endpoint-apis), such as isolating a device, running an antivirus scan, and getting information about a file

## Next steps

- [Visit the Action center](m365d-action-center.md)
- [View and manage remediation actions](m365d-autoir-actions.md)
- [Address false positives or false negatives](m365d-autoir-report-false-positives-negatives.md)
- [Contain devices from the network](/defender-endpoint/respond-machine-alerts#contain-devices-from-the-network)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
