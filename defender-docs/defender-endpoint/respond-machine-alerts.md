---
title: Take response actions on a device in Microsoft Defender for Endpoint
description: Take response actions on a device such as isolating devices, collecting an investigation package, managing tags, running an antivirus scan, and restricting app execution.
ms.service: defender-endpoint
ms.author: diannegali
author: diannegali
ms.localizationpriority: medium
ms.date: 07/01/2025
manager: deniseb
audience: ITPro
ms.collection:
- m365-security
- tier2
- mde-edr
ms.topic: how-to
ms.subservice: edr
search.appverid: met150
---

# Take response actions on a device

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plans 1 and 2](microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business/mdb-overview)

[!INCLUDE [Prerelease information](../includes/prerelease.md)]

Quickly respond to detected attacks by isolating devices or collecting an investigation package. After taking action on devices, you can check activity details on the Action center.

Response actions run along the top of a specific device page and include:

- Manage tags
- Initiate automated investigation
- Initiate live response Session
- Collect investigation package
- Run antivirus scan
- Restrict app execution
- Isolate device
- Contain device
- Consult a threat expert
- Action center

[![Screenshot that shows response actions across the top of a device page in the Microsoft Defender portal.](media/response-actions.png)](media/response-actions.png#lightbox)

> [!NOTE]
> [Defender for Endpoint Plan 1](defender-endpoint-plan-1.md) includes only the following manual response actions:
> - Run antivirus scan
> - Isolate device
> - Stop and quarantine a file
> - Add an indicator to block or allow a file.
>
> [Microsoft Defender for Business](/defender-business/mdb-overview) does not include the "Stop and quarantine a file" action at this time.
>
> Your subscription must include Defender for Endpoint Plan 2 to have all of the response actions described in this article.

 You can find device pages from any of the following views:

- **Alerts queue**: Select the device name beside the device icon from the alerts queue.
- **Devices list**: Select the heading of the device name from the devices list.
- **Search box**: Select **Device** from the drop-down menu and enter the device name.

> [!IMPORTANT]
> For information on availability and support for each response action, see the supported minimum operating system requirements for each feature.

## Manage tags

Add or manage tags to create a logical group affiliation. Device tags support proper mapping of the network, enabling you to attach different tags to capture context and to enable dynamic list creation as part of an incident.

For more information on device tagging, see [Create and manage device tags](machine-tags.md).

## Initiate automated investigation

You can start a new, general-purpose automated investigation on the device if needed. While an investigation is running, any other alert generated from the device is added to an ongoing automated investigation until that investigation completes. In addition, if the same threat is seen on other devices, those devices are added to the investigation.

For more information on automated investigations, see [Overview of Automated investigations](automated-investigations.md).

## Initiate live response session

Live response is a capability that gives you instantaneous access to a device by using a remote shell connection. This gives you the power to do in-depth investigative work and take immediate response actions to promptly contain identified threats in real time.

Live response is designed to enhance investigations by enabling you to collect forensic data, run scripts, send suspicious entities for analysis, remediate threats, and proactively hunt for emerging threats.

For more information on live response, see [Investigate entities on devices using live response](live-response.md).

## Collect investigation package from devices

As part of the investigation or response process, you can collect an investigation package from a device. By collecting the investigation package, you can identify the current state of the device and further understand the tools and techniques used by the attacker.

To download the package (zipped folder) and investigate the events that occurred on a device, follow these steps:

1. Select **Collect investigation package** from the row of response actions at the top of the device page.

2. Specify in the text box why you want to perform this action. Select **Confirm**.

3. The zip file downloads.

Or, use this alternate procedure:

1. Select **Collect Investigation Package** from the response actions section of the device page.

   ![Image of collect investigation package](media/collect-investigation-package.png)
   
2. Add comments and then select **Confirm**.

   ![Image of confirm comment](media/comments-confirm.png)
   
3. Select **Action center** from the response actions section of the device page.

   ![Image of action center](media/action-center-selected.png)
   
4. Select **Package collection package available** to download the collection package.

   ![Image of download package](media/download-package.png)

   > [!NOTE]
   > The collection of the investigation package may fail if a device has a low battery level or is on a metered connection.
   
### Investigation package contents for Windows devices

For Windows devices, the package contains the folders described in the following table:

|Folder|Description|
|---|---|
|Autoruns|Contains a set of files that each represent the content of the registry of a known auto start entry point (ASEP) to help identify attacker's persistency on the device. <br/><br/>If the registry key isn't found, the file contains the following message: "ERROR: The system was unable to find the specified registry key or value." |
|Installed programs|This .CSV file contains the list of installed programs that can help identify what is currently installed on the device. For more information, see [Win32_Product class](https://go.microsoft.com/fwlink/?linkid=841509).|
|Network connections|This folder contains a set of data points related to the connectivity information that can help in identifying connectivity to suspicious URLs, attacker's command and control (C&C) infrastructure, any lateral movement, or remote connections. <br/><br/>- `ActiveNetConnections.txt`: Displays protocol statistics and current TCP/IP network connections. Enables you to look for suspicious connectivity made by a process.<br/><br/>- `Arp.txt`: Displays the current address resolution protocol (ARP) cache tables for all interfaces. ARP cache can reveal other hosts on a network that were compromised or suspicious systems on the network that might be used to run an internal attack.<br/><br/>- `DnsCache.txt`: Displays the contents of the DNS client resolver cache, which includes both entries preloaded from the local Hosts file and any recently obtained resource records for name queries resolved by the computer. This can help in identifying suspicious connections.<br/><br/>- `IpConfig.txt`: Displays the full TCP/IP configuration for all adapters. Adapters can represent physical interfaces, such as installed network adapters, or logical interfaces, such as dial-up connections.<br/><br/>- `FirewallExecutionLog.txt` and `pfirewall.log`<br/><br/>The `pfirewall.log` file must exist in `%windir%\system32\logfiles\firewall\pfirewall.log`, so it's included in the investigation package. For more information on creating the firewall log file, see [Configure the Windows Firewall with Advanced Security Log](/windows/security/threat-protection/windows-firewall/configure-the-windows-firewall-log).|
|Prefetch files|Windows Prefetch files are designed to speed up the application startup process. It can be used to track all the files recently used in the system and find traces for applications that might be deleted but can still be found in the prefetch file list. <br/><br/>- `Prefetch folder`: Contains a copy of the prefetch files from `%SystemRoot%\Prefetch`. We recommend downloading a prefetch file viewer to view the prefetch files.<br/><br/>- `PrefetchFilesList.txt`: Contains the list of all the copied files that can be used to track if there were any copy failures to the prefetch folder.|
|Processes|Contains a .CSV file listing the running processes and provides the ability to identify current processes running on the device. This can be useful when identifying a suspicious process and its state.|
|Scheduled tasks|Contains a .CSV file listing the scheduled tasks, which can be used to identify routines performed automatically on a chosen device to look for suspicious code that was set to run automatically.|
|Security event log|Contains the security event log, which contains records of sign-in or sign-out activity, or other security-related events specified by the system's audit policy. <br/><br/>Open the event log file using Event viewer.|
|Services|Contains a .CSV file that lists services and their states.|
|Windows Server Message Block (SMB) sessions|Lists shared access to files, printers, and serial ports and miscellaneous communications between nodes on a network. This can help identify data exfiltration or lateral movement.<br/><br/>Contains files for `SMBInboundSessions` and `SMBOutboundSession`. If there are no sessions (inbound or outbound), you get a text file that tells you that there are no SMB sessions found.|
|System Information|Contains a `SystemInformation.txt` file that lists system information such as OS version and network cards.|
|Temp Directories|Contains a set of text files that lists the files located in `%Temp%` for every user in the system. This can help to track suspicious files that an attacker might have dropped on the system. <br/><br/>If the file contains the following message: "The system cannot find the path specified", it means that there's no temp directory for this user, and might be because the user didn't sign in to the system.|
|Users and Groups|Provides a list of files that each represent a group and its members.|
|WdSupportLogs|Provides the `MpCmdRunLog.txt` and `MPSupportFiles.cab`. This folder is only created on Windows 10, version 1709 or later with February 2020 update rollup or more recent versions installed: <br/><br/>- Win10 1709 (RS3) Build 16299.1717: [KB4537816](https://support.microsoft.com/help/4537816/windows-10-update-kb4537816)<br/><br/>- Win10 1803 (RS4) Build 17134.1345: [KB4537795](https://support.microsoft.com/help/4537795/windows-10-update-kb4537795)<br/><br/>- Win10 1809 (RS5) Build 17763.1075: [KB4537818](https://support.microsoft.com/help/4537818/windows-10-update-kb4537818)<br/><br/>- Win10 1903/1909 (19h1/19h2) Builds 18362.693 and 18363.693: [KB4535996](https://support.microsoft.com/help/4535996/windows-10-update-kb4535996)|
|CollectionSummaryReport.xls|This file is a summary of the investigation package collection, it contains the list of data points, the command used to extract the data, the execution status, and the error code if there's failure. You can use this report to track if the package includes all the expected data and identify if there were any errors.|

### Investigation package contents for Mac and Linux devices

The following table lists the contents of the collection packages for Mac and Linux devices:

|Object|macOS|Linux|
|---|---|---|
|Applications|A list of all installed applications|Not applicable|
|Disk volume|- Amount of free space<br/>- List of all mounted disk volumes<br/>- List of all partitions</li>|- Amount of free space<br/>- List of all mounted disk volumes<br/>- List of all partitions|
|File|A list of all open files with the corresponding processes using these files|A list of all open files with the corresponding processes using these files|
|History|Shell history|Not applicable|
|Kernel modules|All loaded modules|Not applicable|
|Network connections|- Active connections<br/>- Active listening connections<br/>- ARP table<br/>- Firewall rules<br/>- Interface configuration<br/>- Proxy settings<br/>- VPN settings|- Active connections<br/>- Active listening connections<br/>- ARP table<br/>- Firewall rules<br/>- IP list<br/>- Proxy settings|
|Processes|A list of all running processes|A list of all running processes|
|Services and scheduled tasks|- Certificates<br/>- Configuration profiles<br/>- Hardware information|- CPU details<br/>- Hardware information<br/>- Operating system information</li>|
|System security information|- Extensible Firmware Interface (EFI) integrity information<br/>- Firewall status<br/>- Malware Removal Tool (MRT) information<br/>- System Integrity Protection (SIP) status</li>|Not applicable|
|Users and groups|- Sign-in history<br/>- Sudoers|- Sign-in history<br/>- Sudoers|

## Run Microsoft Defender Antivirus scan on devices

As part of the investigation or response process, you can remotely initiate an antivirus scan to help identify and remediate malware that might be present on a compromised device.

> [!IMPORTANT]
>
> - This action is supported for macOS and Linux for client version 101.98.84 and above. You can also use live response to run the action. For more information on live response, see [Investigate entities on devices using live response](live-response.md)
> - A Microsoft Defender Antivirus scan can run alongside other antivirus solutions, whether Microsoft Defender Antivirus is the active antivirus solution or not. Microsoft Defender Antivirus can be in Passive mode. For more information, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility.md).

One you have selected **Run antivirus scan**, select the scan type that you'd like to run (quick or full) and add a comment before confirming the scan.

:::image type="content" source="media/run-antivirus.png" alt-text="The notification to select quick scan or full scan and add comment" lightbox="media/run-antivirus.png":::

The Action center shows the scan information and the device timeline include a new event, reflecting that a scan action was submitted on the device. Microsoft Defender Antivirus alerts reflect any detections that surfaced during the scan.

> [!NOTE]
> When triggering a scan using Defender for Endpoint response action, Microsoft Defender antivirus `ScanAvgCPULoadFactor` value applies and limits the CPU impact of the scan.
> If `ScanAvgCPULoadFactor` is not configured, the default value is a limit of 50% maximum CPU load during a scan.
> For more information, see [configure-advanced-scan-types-microsoft-defender-antivirus](/windows/security/threat-protection/microsoft-defender-antivirus/configure-advanced-scan-types-microsoft-defender-antivirus).

## Restrict app execution

In addition to containing an attack by stopping malicious processes, you can also lock down a device and prevent subsequent attempts of potentially malicious programs from running.

> [!IMPORTANT]
>
> - This action is available for devices on Windows 10, version 1709 or later, Windows 11, and Windows Server 2019 or later.
> - This feature is available if your organization uses Microsoft Defender Antivirus.
> - This action needs to meet the Windows Defender Application Control code integrity policy formats and signing requirements. For more information, see [Code integrity policy formats and signing](/windows/security/threat-protection/windows-defender-application-control/use-code-signing-to-simplify-application-control-for-classic-windows-applications)).

To restrict an application from running, a code integrity policy is applied that only allows files to run if they're signed by a Microsoft issued certificate. This method of restriction can help prevent an attacker from controlling compromised devices and performing further malicious activities.

> [!NOTE]
> You'll be able to reverse the restriction of applications from running at any time. The button on the device page will change to say **Remove app restrictions**, and then you take the same steps as restricting app execution.

Once you have selected **Restrict app execution** on the device page, type a comment and select **Confirm**. The Action center shows the scan information and the device timeline include a new event.

:::image type="content" source="media/restrict-app-execution.png" alt-text="The application restriction notification" lightbox="media/restrict-app-execution.png":::

### Notification on device user

When an app is restricted, the following notification is displayed to inform the user that an app is being restricted from running:

:::image type="content" source="media/atp-app-restriction.png" alt-text="The application restriction message" lightbox="media/atp-app-restriction.png":::

> [!NOTE]
> The notification is not available on Windows Server 2016 and Windows Server 2012 R2.

## Isolate devices from the network

Depending on the severity of the attack and the sensitivity of the device, you might want to isolate the device from the network. This action can help prevent the attacker from controlling the compromised device and performing further activities such as data exfiltration and lateral movement.

**Important points to keep in mind**: 

- Isolating devices from the network is supported for macOS for client version 101.98.84 and above. You can also use live response to run the action. For more information on live response, see [Investigate entities on devices using live response](live-response.md)
- Full isolation is available for devices running Windows 11, Windows 10, version 1703 or later, Windows Server 2025, Windows Server 2022, Windows Server 2019, Windows Server 2016 and Windows Server 2012 R2.
- Isolating devices from the network is supported when Defender is running in passive mode on all supported Windows operating systems, macOS and Linux supported versions.
- You can use the device isolation capability on all supported Microsoft Defender for Endpoint on Linux listed in [System requirements](mde-linux-prerequisites.md). Ensure that the following prerequisites are enabled:
   - `iptables`
   - `ip6tables`
   - Linux kernel with `CONFIG_NETFILTER`, `CONFID_IP_NF_IPTABLES`, and `CONFIG_IP_NF_MATCH_OWNER`
- Selective isolation is available for devices running on Windows 11, Windows 10 version 1703 or later, Windows Server 2025, Windows Server 2022, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, and macOS. For more information about selective isolation, see [Isolation exclusions](./isolation-exclusions.md).
- When isolating a device, only certain processes and destinations are allowed. Therefore, devices that are behind a full VPN tunnel won't be able to reach the Microsoft Defender for Endpoint cloud service after the device is isolated. We recommend using a split-tunneling VPN for Microsoft Defender for Endpoint and Microsoft Defender Antivirus cloud-based protection-related traffic.
- The feature supports VPN connection.
- You must have at least the `Active remediation actions` role assigned. For more information, see [Create and manage roles](user-roles.md).
- You must have access to the device based on the device group settings. For more information, see [Create and manage device groups](machine-groups.md).
- Exclusions, such as e-mail, messaging application and other applications for both macOS and Linux isolation aren't supported.
- An isolated device is removed from isolation when an administrator modifies or adds a new `iptable` rule to the isolated device.
- Isolating a server running on Microsoft Hyper-V blocks network traffic to all child virtual machines of the server.

The device isolation feature disconnects the compromised device from the network while retaining connectivity to the Defender for Endpoint service, which continues to monitor the device. On Windows 10, version 1709 or later, you can use selective isolation for more control over the network isolation level. You can also choose to enable Outlook and Microsoft Teams connectivity.

> [!NOTE]
> You'll be able to reconnect the device back to the network at any time. The button on the device page will change to say **Release from isolation**, and then you take the same steps as isolating the device.

Once you have selected **Isolate device** on the device page, type a comment and select **Confirm**. The Action center shows the scan information and the device timeline include a new event.

:::image type="content" source="media/isolate-device.png" alt-text="An isolated device details page" lightbox="media/isolate-device.png":::

> [!NOTE]
> The device will remain connected to the Defender for Endpoint service even if it is isolated from the network. If you've chosen to enable Outlook and Skype for Business communication, then you'll be able to communicate to the user while the device is isolated. Selective isolation only works on the classic versions of Outlook and Microsoft Teams.

### Forcibly release device from isolation

The device isolation feature is an invaluable tool for safeguarding devices against external threats. However, there are instances when isolated devices become unresponsive.

There's a downloadable script for these instances that you can run to forcibly release devices from isolation. The script is available through a link in the UI.

> [!NOTE]
>
> - Admins and manage security settings in Security Center permissions can forcibly release devices from isolation.
> - The script is valid for the specific device only.
> - The script will expire in three days.

To forcibly release device from isolation:

1. On the device page, select **Download script to force-release a device from isolation** from the action menu.

1. In the pane on the right, select **Download script**.

#### Minimum requirements for forcible device release

To forcibly release a device from isolation, the device must be running Windows. The following versions are supported:

- Windows 10 21H2 and 22H2 with KB KB5023773.
- Windows 11 version 21H2, all editions with KB5023774.
- Windows 11 version 22H2, all editions with KB5023778.

### Notification on device user

When a device is being isolated, the following notification is displayed to inform the user that the device is being isolated from the network:

:::image type="content" source="media/atp-notification-isolate.png" alt-text="A no network connection message" lightbox="media/atp-notification-isolate.png":::

> [!NOTE]
> The notification is not available on non-Windows platforms.

## Contain devices from the network

When you have identified an unmanaged device that is compromised or potentially compromised, you might want to contain that device from the network to prevent the potential attack from moving laterally across the network. When you contain a device any Microsoft Defender for Endpoint onboarded device blocks incoming and outgoing communication with that device. This action can help prevent neighboring devices from becoming compromised while the security operations analyst locates, identifies, and remediates the threat on the compromised device.

> [!NOTE]
> Blocking incoming and outgoing communication with a 'contained' device is supported on onboarded Microsoft Defender for Endpoint Windows 10 and Windows Server 2019+ devices.

Once devices are contained, we recommend investigating and remediating the threat on the contained devices as soon as possible. After remediation, you should remove the devices from containment.

### How to contain a device

1. Go to the **Device inventory** page and select the device to contain.

2. Select **Contain device** from the actions menu in the device flyout.

   :::image type="content" alt-text="Screenshot of the contain device popup message." source="/defender/media/defender-endpoint/contain_device.png" lightbox="/defender/media/defender-endpoint/contain_device.png":::

3. On the contain device popup, type a comment, and select **Confirm**.

   :::image type="content" alt-text="Screenshot of the contain device menu item." source="/defender/media/defender-endpoint/contain_device_popup.png" lightbox="/defender/media/defender-endpoint/contain_device_popup.png":::

> [!IMPORTANT]
> Containing a large number of devices might cause performance issues on Defender for Endpoint-onboarded devices. To prevent any issues, Microsoft recommends containing up to 100 devices at any given time.

### Contain a device from the device page

A device can also be contained from the device page by selecting **Contain device** from the action bar:

:::image type="content" alt-text="Screenshot of the contain device menu item on the device page." source="/defender/media/defender-endpoint/contain_device_page.png" lightbox="/defender/media/defender-endpoint/contain_device_page.png":::

> [!NOTE]
> It can take up to 5 minutes for the details about a newly contained device to reach Microsoft Defender for Endpoint onboarded devices.

> [!IMPORTANT]
>
> - If a contained device changes its IP address, all Microsoft Defender for Endpoint onboarded devices recognize this and start blocking communications with the new IP address. The original IP address is no longer be blocked (It may take up to 5 minutes to see these changes).
> - In cases where the contained device's IP is used by another device on the network, a warning while containing the device with a link to advanced hunting (with a pre-populated query) is displayed. This provides visibility to other devices using the same IP to help you make a conscious decision if you'd like to continue containing the device.
> - In cases where the contained device is a network device, a warning appears with a message that containment can cause network connectivity issues (for example, containing a router that is acting as a default gateway). At this point, you're able to choose whether to contain the device or not.

After you contain a device, if the behavior isn't as expected, verify the Base Filtering Engine (BFE) service is enabled on the Defender for Endpoint onboarded devices.

### Stop containing a device

You're be able to stop containing a device at any time.

1. Select the device from the **Device inventory** or open the device page.

2. Select **Release from containment** from the action menu. This action restores the device's connection to the network.

### Contain IP addresses of undiscovered devices

> [!IMPORTANT]
> Some information in this article relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Defender for Endpoint can also contain IP addresses associated with devices that are undiscovered or are not onboarded to Defender for Endpoint. The capability to contain an IP address prevents attackers from spreading attacks to other non-compromised devices. Containing an IP address results in Defender for Endpoint-onboarded devices blocking incoming and outgoing communication with devices using the contained IP address

> [!NOTE]
> Blocking incoming and outgoing communication with a 'contained' device is supported on onboarded Defender for Endpoint Windows 10, Windows 2012 R2, Windows 2016, and Windows Server 2019+ devices.

Containing an IP address associated with undiscovered devices or devices not onboarded to Defender for Endpoint is done automatically through [automatic attack disruption](/defender-xdr/automatic-attack-disruption). The Contain IP policy automatically blocks a malicious IP address when Defender for Endpoint detects the IP address to be associated with an undiscovered device or a device not onboarded.

A message indicating that the action is applied appears on the applicable incident, device, or IP page. Here’s an example.

:::image type="content" source="/defender/media/defender-endpoint/contain-ip-attack-disrupt-small.png" alt-text="Highlighting a contained IP address in the incident graph." lightbox="/defender/media/defender-endpoint/contain-ip-attack-disrupt.png":::

After an IP address is contained, you can view the action in the History view of the Action Center. You can see when the action occurred and identify the IP addresses that were contained.

:::image type="content" source="/defender/media/defender-endpoint/contain-ip-action-center-small.png" alt-text="View the contained IP address in the Action center." lightbox="/defender/media/defender-endpoint/contain-ip-action-center.png":::

If a contained IP address is part of an incident, an indicator is present on the [incident graph](/defender-xdr/investigate-incidents#attack-story) and on the incident's [evidence and response](/defender-xdr/investigate-incidents#evidence-and-response) tab. Here’s an example.

:::image type="content" source="/defender/media/defender-endpoint/contain-ip-evidence-small.png" alt-text="Highlighting a contained IP address in the Evidence and response tab of an incident." lightbox="/defender/media/defender-endpoint/contain-ip-evidence.png":::

You can stop an IP address' containment at any time. To stop containment, select the **Contain IP** action in the **Action Center**. In the flyout, select **Undo**. This action restores the IP address’ connection to the network.

### Containing critical assets

When a critical asset is compromised and used to spread threats within an organization, stopping the spread can be challenging because these assets must continue to function to avoid productivity loss. Defender for Endpoint addresses this by granularly containing the critical asset, preventing the spread of the attack while ensuring the asset remains operational for business continuity.

Through automatic attack disruption, Defender for Endpoint incriminates a malicious device, identifies the role of the device to apply a matching policy to automatically contain a critical asset. The granular containment is done by blocking only specific ports and communication directions.

You can identify critical assets by the **critical asset** tag on the device or IP page. Device containment currently supports critical asset types like domain controllers, DNS servers, and DHCP servers.

## Contain user from the network

When an identity in your network might be compromised, you must prevent that identity from accessing the network and different endpoints. Defender for Endpoint can contain an identity, blocking it from access, and helping prevent attacks-- specifically, ransomware. When an identity is contained, any supported Microsoft Defender for Endpoint onboarded device will block incoming traffic in specific protocols related to attacks (deny network logons, RPC, SMB, RDP), terminate ongoing remote sessions and logoff existing RDP connections (terminating the session itself including all its related processes), while enabling legitimate traffic. This action can significantly help to reduce the impact of an attack. When an identity is contained, security operations analysts have extra time to locate, identify and remediate the threat to the compromised identity. Once contained by automatic attack disruption, a user is automatically removed from containment in the next five days.

> [!NOTE]
> Blocking incoming communication with a "contained" user is supported on onboarded Microsoft Defender for Endpoint Windows 10 and 11 devices (Sense version 8740 and higher), Windows Server 2019+ devices, and Windows Servers 2012R2 and 2016 with the modern agent.

> [!IMPORTANT]
> Once a **Contain user** action is enforced on a domain controller, it starts a GPO update on the Default Domain Controller policy. A change of a GPO starts a sync across the domain controllers in your environment.  This is expected behavior, and if you monitor your environment for AD GPO changes, you may be notified of such changes. Undoing the **Contain user** action reverts the GPO changes to their previous state, which will then start another AD GPO synchronization in your environment. Learn more about [merging of security policies on domain controllers](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj966251(v=ws.11)#merging-of-security-policies-on-domain-controllers).

### How to contain a user

Currently, containing users is only available automatically by using automatic attack disruption. When Microsoft detects a user as being compromised a "Contain User" policy is automatically set.

### View the contain user actions

After a user is contained, you can view the action in this History view of the Action Center. Here, you can see when the action occurred, and which users in your organization were contained:

:::image type="content" source="/defender/media/defender-endpoint/user-contain-action-center.png" alt-text="View the user contain action in the action center" lightbox="/defender/media/defender-endpoint/user-contain-action-center.png":::

Furthermore, after an identity is considered "contained", that user will be blocked by Defender for Endpoint and cannot perform any malicious lateral movement or remote encryption on or to any supported Defender for Endpoint onboarded device. These blocks will show up as alerts to help you quickly see the devices the compromised user attempted access and potential attack techniques:

:::image type="content" source="/defender/media/defender-endpoint/user-contain-lateral-move-block.png" alt-text="Shows a user contain lateral movement block event" lightbox="/defender/media/defender-endpoint/user-contain-lateral-move-block.png":::

### Undo contain user actions

You can release the blocks and containment on a user at any time:

1. Select the **Contain User** action in the **Action Center**. In the side pane select **Undo**.

2. Select the user from either the user inventory, Incident page side pane or alert side pane and select **Undo**.

This action restores the user's connection to the network.

:::image type="content" source="/defender/media/defender-endpoint/undo-user-contain-action.png" alt-text="Shows user contain undo option in the action center" lightbox="/defender/media/defender-endpoint/undo-user-contain-action.png":::

### Investigation capabilities with Contain User

After a user is contained, you can investigate the potential threat by viewing the blocked actions by the compromised user. In the device timeline view, you can see information about specific events, including protocol and interface granularity, and the relevant MITRE Technique associated it.

:::image type="content" source="/defender/media/defender-endpoint/event-blocked by-contained-user.png" alt-text="Shows blocked event details for a contained users" lightbox="/defender/media/defender-endpoint/event-blocked by-contained-user.png":::

In addition, you can expand the investigation by using advanced hunting. Look for any action type starting with *contain* in the `DeviceEvents` table. Then, you can view all the different singular blocking events in relation to Contain User in your tenant, dive deeper into the context of each block, and extract the different entities and techniques associated with those events.

:::image type="content" source="/defender/media/defender-endpoint/user-contain-advanced-hunting.png" alt-text="Shows advanced hunting for user contain events" lightbox="/defender/media/defender-endpoint/user-contain-advanced-hunting.png":::

## Consult a threat expert

You can consult a Microsoft threat expert for more insights regarding a potentially compromised device or already compromised ones. Microsoft Threat Experts can be engaged directly from within the Microsoft Defender XDR for timely and accurate response. Experts provide insights not just regarding a potentially compromised device, but also to better understand complex threats, targeted attack notifications that you get, or if you need more information about the alerts, or a threat intelligence context that you see on your portal dashboard.

See [Configure and manage Endpoint Attack Notifications](configure-microsoft-threat-experts.md) for details.

## Check activity details in Action center

The Action center ([https://security.microsoft.com/action-center](https://security.microsoft.com/action-center)) provides information on actions that were taken on a device or file. You'll be able to view the following details:

- Investigation package collection
- Antivirus scan
- App restriction
- Device isolation

All other related details are also shown, for example, submission date/time, submitting user, and if the action succeeded or failed.

:::image type="content" source="media/action-center-details.png" alt-text="The action center with information" lightbox="media/action-center-details.png":::

## See also

- [Take response actions on a file](respond-file-alerts.md)
- [Manual response actions in Microsoft Defender for Endpoint Plan 1](defender-endpoint-plan-1.md#manual-response-actions)
- [Report inaccuracy](/defender-vulnerability-management/tvm-security-recommendation#report-inaccuracy)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
