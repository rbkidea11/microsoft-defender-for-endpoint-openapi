---
title: Create indicators for files
ms.reviewer: yongrhee
description: Create indicators for a file hash that define the detection, prevention, and exclusion of entities.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
ms.date: 07/30/2025
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
search.appverid: met150
---

# Create indicators for files

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Endpoint Plan 1](defender-endpoint-plan-1.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business/mdb-overview)

> [!IMPORTANT]
> In Defender for Endpoint Plan 1 and Defender for Business, you can create an indicator to block or allow a file. In Defender for Business, your indicator is applied across your environment and cannot be scoped to specific devices.

> [!NOTE]
> For this feature to work on Windows Server 2016 and Windows Server 2012 R2, those devices must be onboarded using the [modern unified solution](onboard-server.md#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2). 
> Custom file indicators with the Allow, Block and Remediate actions are now also available in the [enhanced antimalware engine capabilities for macOS and Linux](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/enhanced-antimalware-engine-capabilities-for-linux-and-macos/ba-p/3292003).

File indicators prevent further propagation of an attack in your organization by banning potentially malicious files or suspected malware. If you know a potentially malicious portable executable (PE) file, you can block it. This operation will prevent it from being read, written, or executed on devices in your organization.

There are three ways you can create indicators for files:

- By creating an indicator through the settings page
- By creating a contextual indicator using the add indicator button from the file details page
- By creating an indicator through the [Indicator API](api/ti-indicator.md)

## Before you begin

Understand the following prerequisites before you create indicators for files:

- [Behavior Monitoring is enabled](behavior-monitor.md)
- [Cloud-based protection is turned on](/defender-endpoint/enable-cloud-protection-microsoft-defender-antivirus).
- [Cloud Protection network connectivity is functional](configure-network-connections-microsoft-defender-antivirus.md)
- To start blocking files, [turn on the "block or allow" feature](advanced-features.md) in Settings (in the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Endpoints** > **General** > **Advanced features** > **Allow or block file**).

### Windows prerequisites

- This feature is available if your organization uses [Microsoft Defender Antivirus](microsoft-defender-antivirus-windows.md) (in active mode) 
- The antimalware client version must be `4.18.1901.x` or later. See [Monthly platform and engine versions](microsoft-defender-antivirus-updates.md#platform-and-engine-releases)
- This feature is supported on devices running Windows 10, version 1703 or later, Windows 11, Windows Server 2012 R2, Windows Server 2016 or later, Windows Server 2019, Windows Server 2022, and Windows Server 2025.
- File hash computation is enabled by setting `Computer Configuration\Administrative Templates\Windows Components\Microsoft Defender Antivirus\MpEngine\Enable File Hash Computation` to **Enabled**. Or, you can run the following PowerShell command: `Set-MpPreference -EnableFileHashComputation $true`

> [!NOTE]
> File indicators support portable executable (PE) files, including `.exe` and `.dll` files only.

### macOS prerequisites

- Real-time protection (RTP) needs to be active.
- [File hash computation must be enabled](/defender-endpoint/mac-resources#configuring-from-the-command-line). Run the following command: `mdatp config enable-file-hash-computation --value enabled`

> [!NOTE]
> On macOS, file indicators support three types of files: Mach-O executables, POSIX shell scripts (e.g., those run by sh or bash), and AppleScript files (.scpt). (Mach-O is macOS's native executable format, comparable to .exe and .dll on Windows.)

### Linux prerequisites

- Available in Defender for Endpoint version `101.85.27` or later.
- [File hash computation must be enabled](/defender-endpoint/linux-preferences#configure-file-hash-computation-feature) in the Microsoft Defender portal or in the managed JSON
- Behavior monitoring enabled is preferred, but this feature works with any other scan (RTP or Custom).

## Create an indicator for files from the settings page

1. In the navigation pane, select **System** \> **Settings** \> **Endpoints** \> **Indicators** (under **Rules**).

2. Select the **File hashes** tab.

3. Select **Add item**.

4. Specify the following details:

   - Indicator: Specify the entity details and define the expiration of the indicator.
   - Action: Specify the action to be taken and provide a description.
   - Scope: Define the scope of the device group (scoping isn't available in [Defender for Business](/defender-business/mdb-overview)).

5. Review the details in the Summary tab, then select **Save**.

## Create a contextual indicator from the file details page

One of the options when taking [response actions on a file](respond-file-alerts.md) is adding an indicator for the file. When you add an indicator hash for a file, you can choose to raise an alert and block the file whenever a device in your organization attempts to run it.

Files automatically blocked by an indicator won't show up in the file's Action center, but the alerts will still be visible in the Alerts queue.

## Alerting on file blocking actions (preview)

> [!IMPORTANT]
> Information in this section (**Public Preview for Automated investigation and remediation engine**) relates to prerelease product which might be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

The current supported actions for file IOC are allow, audit and block, and remediate. After choosing to block a file, you can choose whether triggering an alert is needed. In this way, you'll be able to control the number of alerts getting to your security operations teams and make sure only required alerts are raised.

1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Endpoints** > **Indicators** > **Add New File Hash**.

2. Choose to block and remediate the file.

3. Specify whether to generate an alert on the file block event and define the alerts settings:

   - The alert title
   - The alert severity
   - Category
   - Description
   - Recommended actions

   :::image type="content" source="media/indicators-generate-alert.png" alt-text="The Alert settings for file indicators" lightbox="media/indicators-generate-alert.png":::

   > [!IMPORTANT]
   > - Typically, file blocks are enforced and removed within 15 minutes, average 30 minutes but can take upwards of 2 hours.
   > - If there are conflicting file IoC policies with the same enforcement type and target, the policy of the more secure hash will be applied. An SHA-256 file hash IoC policy will win over an SHA-1 file hash 
   IoC policy, which will win over an MD5 file hash IoC policy if the hash types define the same file. This is always true regardless of the device group.
   > - In all other cases, if conflicting file IoC policies with the same enforcement target are applied to all devices and to the device's group, then for a device, the policy in the device group will win.
   > - If the EnableFileHashComputation group policy is disabled, the blocking accuracy of the file IoC is reduced. However, enabling `EnableFileHashComputation` may impact device performance. For example, copying large files from a network share onto your local device, especially over a VPN connection, might have an effect on device performance.
   > For more information about the EnableFileHashComputation group policy, see [Defender CSP](/windows/client-management/mdm/defender-csp).
   > For more information on configuring this feature on Defender for Endpoint on Linux and macOS, see [Configure file hash computation feature on Linux](linux-preferences.md#configure-file-hash-computation-feature) and [Configure file hash computation feature on macOS](mac-preferences.md#configure-file-hash-computation-feature).

## Advanced hunting capabilities (preview)

> [!IMPORTANT]
> Information in this section (**Public Preview for Automated investigation and remediation engine**) relates to prerelease product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Currently in preview, you can query the response action activity in advance hunting. Below is a sample advance hunting query:

```console
search in (DeviceFileEvents, DeviceProcessEvents, DeviceEvents, DeviceRegistryEvents, DeviceNetworkEvents, DeviceImageLoadEvents, DeviceLogonEvents)
Timestamp > ago(30d)
| where AdditionalFields contains "EUS:Win32/CustomEnterpriseBlock!cl"
```

For more information about advanced hunting, see [Proactively hunt for threats with advanced hunting](/defender-xdr/advanced-hunting-overview).

Here are other threat names that can be used in the sample query:

Files:

- `EUS:Win32/CustomEnterpriseBlock!cl`
- `EUS:Win32/CustomEnterpriseNoAlertBlock!cl`

Certificates:

- `EUS:Win32/CustomCertEnterpriseBlock!cl`

The response action activity can also be viewable in the device timeline.

## Policy conflict handling

Cert and File IoC policy handling conflicts follow this order:

1. If the file isn't allowed by Windows Defender Application Control and AppLocker enforce mode policies, then **Block**.

2. Else, if the file is allowed by the Microsoft Defender Antivirus exclusions, then **Allow**.

3. Else, if the file is blocked or warned by a block or warn file IoCs, then **Block/Warn**.

4. Else, if the file is blocked by SmartScreen, then **Block**.

5. Else, if the file is allowed by an allow file IoC policy, then **Allow**.

6. Else, if the file is blocked by attack surface reduction rules, controlled folder access, or antivirus protection, then **Block**.

7. Else, **Allow** (passes Windows Defender Application Control & AppLocker policy, no IoC rules apply to it).

> [!NOTE]
> In situations when Microsoft Defender Antivirus is set to **Block**, but Defender for Endpoint indicators for file hash or certificates are set to **Allow**, the policy defaults to **Allow**.

If there are conflicting file IoC policies with the same enforcement type and target, the policy of the more secure (meaning longer) hash is applied. For example, an SHA-256 file hash IoC policy takes precedence over an MD5 file hash IoC policy if both hash types define the same file.

> [!WARNING]
> Policy conflict handling for files and certs differ from policy conflict handling for domains/URLs/IP addresses.

Microsoft Defender Vulnerability Management's block vulnerable application features uses the file IoCs for enforcement and follows the conflict handling order described earlier in this section.

### Examples

|Component|Component enforcement|File indicator Action|Result|
|---|---|---|---|
|Attack surface reduction file path exclusion|Allow|Block|Block|
|Attack surface reduction rule|Block|Allow|Allow|
|Windows Defender Application Control|Allow|Block|Allow|
|Windows Defender Application Control|Block|Allow|Block|
|Microsoft Defender Antivirus exclusion|Allow|Block|Allow|

## See also

- [Create indicators](indicators-overview.md)

- [Create indicators for IPs and URLs/domains](indicator-ip-domain.md)

- [Create indicators based on certificates](indicator-certificates.md)

- [Manage indicators](indicator-manage.md)

- [Exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
