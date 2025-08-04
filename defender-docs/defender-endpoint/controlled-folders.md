---
title: Protect important folders from ransomware from encrypting your files with controlled folder access
description: Files in default folders can be protected from changes through malicious apps. Prevent ransomware from encrypting your files.
ms.service: defender-endpoint
ms.localizationpriority: medium
ms.date: 06/05/2025
author: denisebmsft
ms.author: deniseb
audience: ITPro
ms.reviewer: sugamar 
manager: deniseb
ms.custom: asr
ms.subservice: asr
ms.topic: how-to
ms.collection: 
- m365-security
- tier2
- mde-asr
search.appverid: met150
---

# Protect important folders with controlled folder access

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- Microsoft Defender Antivirus

**Applies to**
- Windows

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

Platforms

- Windows

## What is controlled folder access?

Controlled folder access helps protect your valuable data from malicious apps and threats, such as ransomware. Controlled folder access protects your data by checking apps against a list of known, trusted apps. Controlled folder access can be configured by using Microsoft Defender for Endpoint Security Settings Management, Microsoft Intune, Microsoft Endpoint Configuration Manager, or the Windows Security App. 

Controlled folder access works best with [Microsoft Defender for Endpoint](microsoft-defender-endpoint.md), which gives you detailed reporting into controlled folder access events and blocks as part of the usual [alert investigation scenarios](investigate-alerts.md).

## Requirements for controlled folder access

Controlled folder access is supported on:

- Windows 11
- Windows 10
- Windows Server 2025
- Windows Server 2022
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

Controlled folder access requires:

- [Microsoft Defender Antivirus to be the primary antivirus (active mode)](configure-real-time-protection-microsoft-defender-antivirus.md).

- Real-Time Protection (RTP) needs to be on.

> [!TIP]
> Controlled folder access blocks don't generate alerts in the [Alerts queue](alerts-queue.md). However, you can view information about controlled folder access blocks in the [device timeline view](investigate-machines.md), while using [advanced hunting](/defender-xdr/advanced-hunting-overview), or with [custom detection rules](/defender-xdr/custom-detection-rules).

## How does controlled folder access work?

Controlled folder access works by only allowing trusted apps to access protected folders. Protected folders are specified when controlled folder access is configured. Typically, commonly used folders, such as those used for documents, pictures, downloads, and so on, are included in the list of controlled folders.

Controlled folder access works with a list of trusted apps. Apps that are included in the list of trusted software work as expected. Apps that aren't included in the list are prevented from making any changes to files inside protected folders.

Apps are added to the list based upon their prevalence and reputation. Apps that are highly prevalent throughout your organization and that haven't ever displayed any behavior deemed malicious are considered trustworthy. Those apps are added to the list automatically.

Apps can also be added manually to the trusted list by using Configuration Manager or Intune. Other actions can be performed in the Microsoft Defender portal.

## Why controlled folder access is important

Controlled folder access is especially useful in helping to protect your documents and information from [ransomware](https://www.microsoft.com/wdsi/threats). In a ransomware attack, your files can get encrypted and held hostage. With controlled folder access in place, a notification appears on the computer where an app attempted to make changes to a file in a protected folder. You can [customize the notification](attack-surface-reduction-rules-deployment-implement.md#customize-attack-surface-reduction-rules) with your company details and contact information. You can also enable the rules individually to customize what techniques the feature monitors.

The [protected folders](#review-controlled-folder-access-events-in-windows-event-viewer) include common system folders (including boot sectors), and you can [add more folders](customize-controlled-folders.md#protect-additional-folders). You can also [allow apps](customize-controlled-folders.md#allow-specific-apps-to-make-changes-to-controlled-folders) to give them access to the protected folders.

You can use [audit mode](overview-attack-surface-reduction.md) to evaluate how controlled folder access would impact your organization if it were enabled.

## Windows system folders are protected by default

Windows system folders are protected by default, along with several other folders:

The protected folders include common system folders (including boot sectors), and you can add other folders. You can also allow apps to give them access to the protected folders. The Windows systems folders that are protected by default are:

- `c:\Users\<username>\Documents`
- `c:\Users\Public\Documents`
- `c:\Users\<username>\Pictures`
- `c:\Users\Public\Pictures`
- `c:\Users\Public\Videos`
- `c:\Users\<username>\Videos`
- `c:\Users\<username>\Music`
- `c:\Users\Public\Music`
- `c:\Users\<username>\Favorites`

Default folders appear in the user's profile, under **This PC**, as shown in the following image:

![Protected Windows default systems folders](media/defaultfolders.png)

The same profile folders are also protected for system accounts, such as `LocalService`, `NetworkService`, `systemprofile`, and so on. For example, `C:\Windows\System32\config\systemprofile\Documents` is also protected (if it exists).

> [!NOTE]
> You can configure more folders as protected, but you can't remove Windows system folders that are protected by default.

> [!NOTE]
> Scripting engines like PowerShell aren't trusted by controlled folder access, even if you create an "allow" indicator by using [certificate and file indicators](indicator-certificates.md). The only way to allow script engines to modify protected folders is by adding them as an allowed app. See [Allow specific apps to make changes to controlled folders](/defender-endpoint/customize-controlled-folders).  

## Review controlled folder access events in the Microsoft Defender portal

> [!TIP]
> Controlled folder access blocks don't generate alerts in the **[Alerts queue](/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fcontrolled-folders.md/main/1f8f3424-7307-8178-dc20-b5160d121a7d/alerts-queue.md)**. However, you can view information about controlled folder access blocks in the **[device timeline view](/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fcontrolled-folders.md/main/1f8f3424-7307-8178-dc20-b5160d121a7d/investigate-machines.md)**, while using **[advanced hunting](/defender-xdr/advanced-hunting-overview)**, or with **[custom detection rules](/defender-xdr/custom-detection-rules)**.

Defender for Endpoint provides detailed reporting into events and blocks as part of its [alert investigation scenarios](investigate-alerts.md) in the Microsoft Defender portal. For more information, see [Microsoft Defender for Endpoint in Microsoft Defender XDR](/defender-xdr/microsoft-365-security-center-mde).

You can query Microsoft Defender for Endpoint data by using [Advanced hunting](/defender-xdr/advanced-hunting-overview). If you're using [audit mode](overview-attack-surface-reduction.md), you can use [advanced hunting](/defender-xdr/advanced-hunting-overview) to see how controlled folder access settings would affect your environment if they were enabled.

Example query:

```
DeviceEvents
| where ActionType in ('ControlledFolderAccessViolationAudited','ControlledFolderAccessViolationBlocked')
```

## Review controlled folder access events in Windows Event Viewer

You can review the Windows event log to see events that are created when controlled folder access blocks (or audits) an app:

1. Download the [Evaluation Package](https://aka.ms/mp7z2w) and extract the file *cfa-events.xml* to an easily accessible location on the device.

2. Type **Event viewer** in the Start menu to open the Windows Event Viewer.

3. On the left panel, under **Actions**, select **Import custom view...**.

4. Navigate to where you extracted *cfa-events.xml* and select it. Alternatively, [copy the XML directly](overview-attack-surface-reduction.md).

5. Select **OK**.

   The following table shows events related to controlled folder access:

   |Event ID|Description|
   |---|---|
   |`5007`|Event when settings are changed|
   |`1124`|Audited controlled folder access event|
   |`1123`|Blocked controlled folder access event|
   |`1127`|Blocked controlled folder access sector write block event|
   |`1128`|Audited controlled folder access sector write block event|

## Controlled folder access experience

A user tries to install an application that triggers Controlled folder access, if the software or application has an unknown reputation, a toast notification presents the user with the following:


```
Virus & threat protection
Unauthorized changes blocked
Controlled folder access blocked C:\...
\ApplicationName... from making changes to memory.
```

And in the Protection history, you will see:


```
Protected memory access blocked
MM/DD/YEAR HH:MM AM/PM
```

## View or change the list of protected folders

You can use the Windows Security app to view the list of folders that are protected by controlled folder access.

1. On your Windows 10 or Windows 11 device, open the Windows Security app.

2. Select **Virus & threat protection**.

3. Under **Ransomware protection**, select **Manage ransomware protection**.

4. If controlled folder access is turned off, you need to turn it on. Select **protected folders**.

5. Take one of the following steps:

   - To add a folder, select **+ Add a protected folder**.
   - To remove a folder, select it, and then select **Remove**.

   > [!IMPORTANT]
   > Don't add local share paths (loopbacks) as protected folders. Use the local path instead. For example, if you have shared `C:\demo` as `\\mycomputer\demo`, don't add `\\mycomputer\demo` to the list of protected folders. Instead add `C:\demo`.

[Windows system folders](#windows-system-folders-are-protected-by-default) are protected by default, and you can't remove them from the list. Subfolders are also included in protection when you add a new folder to the list.

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
