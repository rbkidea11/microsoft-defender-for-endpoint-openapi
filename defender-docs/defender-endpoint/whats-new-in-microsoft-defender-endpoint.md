---
title: What's new in Microsoft Defender for Endpoint
description: See what features are generally available (GA) in the latest release of Microsoft Defender for Endpoint, and security features in Windows 10 and Windows Server.
search.appverid: met150
ms.service: defender-endpoint
ms.author: ewalsh
author: emmwalshh
ms.reviewer: noamhadash, pahuijbr, yongrhee
ms.localizationpriority: medium
ms.date: 05/19/2025
manager: deniseb
audience: ITPro
ms.collection:
- m365-security
- tier1
ms.topic: whats-new
---

# What's new in Microsoft Defender for Endpoint

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

The following features are in preview or generally available (GA) in the latest release of Microsoft Defender for Endpoint. For more information on preview features, see [Preview features](/defender-xdr/preview).

For more information on Microsoft Defender for Endpoint on specific operating systems:

- [What's new in Defender for Endpoint on Windows](windows-whatsnew.md)
- [What's new in Defender for Endpoint on macOS](mac-whatsnew.md)
- [What's new in Defender for Endpoint on Linux](linux-whatsnew.md)
- [What's new in Defender for Endpoint on Android](android-whatsnew.md)
- [What's new in Defender for Endpoint on iOS](ios-whatsnew.md)

For more information on what's new with other Microsoft Defender security products, see:

- [What's new in Microsoft Defender XDR](/defender-xdr/whats-new)
- [What's new in Microsoft Defender for Office 365](/defender-office-365/defender-for-office-365-whats-new)
- [What's new in Microsoft Defender for Identity](/defender-for-identity/whats-new)
- [What's new in Microsoft Defender for Cloud Apps](/cloud-app-security/release-notes)
- [What's new in Microsoft Defender Vulnerability Management](/defender-vulnerability-management/whats-new-in-microsoft-defender-vulnerability-management)

## April 2025

- (Preview) **Contain IP addresses of undiscovered devices**: Containing IP addresses associated with devices that are undiscovered or are not onboarded to Defender for Endpoint is now in preview. Containing an IP address prevents attackers from spreading attacks to other non-compromised devices. See [Contain IP addresses of undiscovered devices](respond-machine-alerts.md#contain-ip-addresses-of-undiscovered-devices) for more information.

- (GA) **Attack Surface Reduction (ASR) Rules**

Two new ASR rules are now generally available:

  - [Block rebooting machine in Safe Mode](/defender-endpoint/attack-surface-reduction-rules-reference): This rule prevents the execution of commands to restart machines in Safe Mode.
  - [Block use of copied or impersonated system tools](/defender-endpoint/attack-surface-reduction-rules-reference): This rule blocks the use of executable files that are identified as copies of Windows system tools. These files are either duplicates or impostors of the original system tools.

- (GA) Defender for Endpoint supports ARM64-based Linux servers across various Linux distributions, including Ubuntu, RHEL, Debian, SUSE Linux, Amazon Linux, and Oracle Linux. All product capabilities that are supported on AMD64 devices are now supported on ARM64-based Linux servers. For more information, see the following articles:

   - [Tech Community Blog: Defender for Endpoint extends support to ARM-based Linux servers](https://techcommunity.microsoft.com/blog/microsoftdefenderatpblog/defender-for-endpoint-extends-support-to-arm-based-linux-servers/4364066)
   - [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux.md)
    
## February 2025

- (GA) **Aggregated reporting in Microsoft Defender for Endpoint** is now generally available. For more information, see [Aggregated reporting in Microsoft Defender for Endpoint](aggregated-reporting.md).

## January 2025

- (Preview) **Aggregated reporting in Microsoft Defender for Endpoint**: Aggregated reporting extends signal reporting intervals to significantly reduce the size of reported events while preserving essential event properties. This feature is available for Microsoft Defender for Endpoint Plan 2. For more information, see [Aggregated reporting in Microsoft Defender for Endpoint](aggregated-reporting.md).

## November-December 2024

- [Five new demonstration scenarios](defender-endpoint-demonstrations.md) were added:
   - [AMSI demos](mde-demonstration-amsi.md)
   - [Cloud protection demo](/defender-endpoint/defender-endpoint-demonstration-cloud-delivered-protection)
   - [Controlled folder access (block ransomware) demo](/defender-endpoint/defender-endpoint-demonstration-controlled-folder-access)
   - [Endpoint detection and response (EDR) detection test](/defender-endpoint/edr-detection)
   - [URL reputation (SmartScreen) demo](/defender-endpoint/defender-endpoint-demonstration-smartscreen-url-reputation)

## August 2024

- **Network Protection feature is enabled by default** in Microsoft Defender for Endpoint on Android. As a result, users are able to see a network protection card in the Defender for Endpoint app, along with App Protection and Web Protection. Users are also required to provide location permission to complete the setup process. Admins can change the default value for network protection if they decide not to use it via the Intune App Configuration policies. This feature was already enabled by default earlier on Microsoft Defender for Endpoint on iOS. For more information, see [network protection](/defender-endpoint/android-configure#network-protection).
    
## July 2024

- (Preview) **Monitor OT devices in the device inventory**: You can now monitor OT devices in addition to IoT devices in the device inventory, as part of the integration with [Microsoft Defender for IoT in the Defender portal](/defender-for-iot/device-discovery). As part of this integration:
    - We've added the **All devices** tab and renamed the **IoT devices** tab to **IoT/OT devices**.
    - We've added the **Device type**, **Device subtype**, **Vendor**, **Model**, and **Site** filters and columns to the device inventory. Some of these filters are only visible on specific tabs, and only for customers with a Defender for IoT license. [Learn more](machines-view-overview.md#use-filters-to-customize-the-device-inventory-views).
    - We've added the ability to search Mac devices and Mac addresses.
    - We've added a system tag that shows the production site name (read only), used for the Defender for IoT [site security](/defender-for-iot/site-security-overview) feature, as part of the [device group](/defender-for-iot/set-up-sites#add-device-group).
    - If OT devices are discovered but a Defender for IoT license isn't set up, the device inventory displays partial data on the OT/IoT devices, and a message that indicates the number of unprotected OT devices. [Learn more about the initial device inventory view with detected OT devices](/defender-for-iot/device-discovery#device-inventory-initial-view).
- (GA) Learning hub resources have moved from the Microsoft Defender portal to [learn.microsoft.com](https://go.microsoft.com/fwlink/?linkid=2273118). Access Microsoft Defender XDR Ninja training, learning paths, training modules and more. Browse the [list of learning paths](/training/browse/?products=m365-ems-cloud-app-security%2Cdefender-for-cloud-apps%2Cdefender-identity%2Cm365-information-protection%2Cm365-threat-protection%2Cmdatp%2Cdefender-office365&expanded=m365%2Coffice-365), and filter by product, role, level, and subject.     

## June 2024

- (Preview) [BitLocker support for Device control](device-control-overview.md#control-access-to-bitlocker-encrypted-removable-media-preview):  Allows device control to apply policy based on the BitLocker encrypted state of a device.  

## May 2024

- (GA) [Microsoft Defender for Endpoint plug-in for Windows Subsystem for Linux (WSL)](/defender-endpoint/mde-plugin-wsl) is now generally available (GA version - 1.24.522.2). The plug-in enables Defender for Endpoint to provide more visibility into all running WSL containers by plugging into the isolated subsystem.

- (Preview) **Turn preview options on in the main Microsoft 365 Defender settings** together with other Microsoft 365 Defender preview features. Customers who aren't using preview features yet continue to see the legacy settings under **Settings > Endpoints > Advanced features > Preview features**. For more information, see [Microsoft 365 Defender preview features](/defender-xdr/preview).

- (GA) [Streamlined device connectivity for Defender for Endpoint](configure-device-connectivity.md) is now generally available for Windows, macOS, and Linux. This experience makes it easier to configure and manage Defender for Endpoint services by reducing the number of URLs required for connectivity, providing IP & Azure service tag support, and simplifying post-deployment network management.

- (GA) [Microsoft Defender Core service](/defender-endpoint/microsoft-defender-core-service-overview) is now generally available on Windows clients.  Helps with the stability and performance of Microsoft Defender Antivirus.

## April 2024

**Microsoft Defender for Endpoint on macOS** feature now in GA:

- **Troubleshooting mode for macOS** : Troubleshooting mode helps you identify instances where antivirus might be causing issues with your applications or system resources. To learn more, see [Troubleshooting mode in Microsoft Defender for Endpoint on macOS](mac-troubleshoot-mode.md).

## March 2024

- (GA) **Built-in Scheduled scan for macOS**: For information on Scheduled Scan built-in for Microsoft Defender for Endpoint on macOS, see [How to schedule scans with Microsoft Defender for Endpoint on macOS](mac-schedule-scan.md)

## February 2024

**Attack Surface Reduction (ASR) Rules**

Two new ASR rules are now in public preview:

- [Block rebooting machine in Safe Mode](attack-surface-reduction-rules-reference.md#block-rebooting-machine-in-safe-mode): This rule prevents the execution of commands to restart machines in Safe Mode.
- [Block use of copied or impersonated system tools](attack-surface-reduction-rules-reference.md#block-use-of-copied-or-impersonated-system-tools): This rule blocks the use of executable files that are identified as copies of Windows system tools. These files are either duplicates or impostors of the original system tools.

**Microsoft Defender for Endpoint on macOS** features are in public preview:

- **Built-in Scheduled Scan for macOS** (preview): Scheduled Scan built-in for Microsoft Defender for Endpoint on macOS is now available in public preview. To learn more, see [How to schedule scans with Microsoft Defender for Endpoint on macOS](mac-schedule-scan.md).

- **Troubleshooting mode for macOS** (preview): Troubleshooting mode for macOS is now available in public preview. Troubleshooting mode helps you identify instances where antivirus might be causing issues with your applications or system resources. To learn more, see [Troubleshooting mode in Microsoft Defender for Endpoint on macOS](mac-troubleshoot-mode.md).

## January 2024

- **Defender Boxed is available for a limited period of time**. Defender Boxed highlights your organization's security successes, improvements, and response actions during 2023. Take a moment to celebrate your organization's improvements in security posture, overall response to detected threats (manual and automatic), blocked emails, and more.

   - Defender Boxed opens automatically when you go to the **Incidents** page in the Microsoft Defender portal.
   - If you close Defender Boxed and you want to reopen it, in the Microsoft Defender portal, go to **Incidents**, and then select **Your Defender Boxed**.
   - Act quickly! Defender Boxed is available only for a short period of time.
- (GA) [User Contain](https://www.microsoft.com/en-us/security/blog/2023/10/11/microsoft-defender-for-endpoint-now-stops-human-operated-attacks-on-its-own) can now contain compromised users automatically stopping Human Operated Ransomware in its track using [Automatic Attack Disruption](/defender-xdr/automatic-attack-disruption).

## November 2023

- [Microsoft Defender Core service overview](microsoft-defender-core-service-overview.md) is now available for consumers and is planned to begin rolling out to enterprise customers in early 2024.
- The [Microsoft Defender for Endpoint plug-in for Windows Subsystem for Linux (WSL)](mde-plugin-wsl.md) is now available in public preview.
- Support for [mixed-license scenarios](defender-endpoint-subscription-settings.md) is now generally available in Defender for Endpoint.

## October 2023

- (GA) The device isolation and run antivirus scan responses in macOS and Linux are now generally available. You can now remotely [run an AV scan](respond-machine-alerts.md#run-microsoft-defender-antivirus-scan-on-devices) or [isolate devices](respond-machine-alerts.md#isolate-devices-from-the-network) when responding to attacks.
- (Public Preview) [Streamlined device connectivity for Defender for Endpoint](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/announcing-a-streamlined-device-connectivity-experience-for/ba-p/3956236) is available in public preview for Windows, macOS, and Linux. This experience makes it easier to configure and manage Defender for Endpoint services by reducing the number of URLs required for connectivity, providing IP & Azure service tag support, and simplifying post-deployment network management.
- (Public Preview) [User Contain](https://www.microsoft.com/en-us/security/blog/2023/10/11/microsoft-defender-for-endpoint-now-stops-human-operated-attacks-on-its-own) can now contain compromised users automatically stopping Human Operated Ransomware in its track using Automatic Attack Disruption.

## September 2023

(GA) [Protecting Dev Drive using performance mode](microsoft-defender-endpoint-antivirus-performance-mode.md) is now generally available. The goal of Performance mode is to improve functional performance for developers who use Windows 11.  Performance mode reduces the performance impact of Microsoft Defender Antivirus scans for files stored on designated Dev Drive.

## August 2023

- (GA) The [Monthly security summary report](monthly-security-summary-report.md) is now generally available. The report helps organizations get a visual summary of key findings and overall preventative actions taken to enhance the organization's overall security posture completed in the last month.

## July 2023

- The eBPF-based sensor for Microsoft Defender for Endpoint on Linux is available for public preview on all supported Linux devices. For more information, see [Use eBPF-based sensor for Microsoft Defender for Endpoint on Linux](linux-support-ebpf.md).
- [Manage endpoint security policies in Defender for Endpoint is now in public preview](manage-security-policies.md)  <br> You can now configure security settings directly in Microsoft Defender XDR.
- A new file page is now available in Defender for Endpoint. The file page now includes information like file details and file content and capabilities. For more information, see [Investigate files](investigate-files.md).

## June 2023

- Microsoft Defender Antivirus scan response action is supported for macOS and Linux for client version 101.98.84 and above. It is in preview. See [Run Microsoft Defender Antivirus scan on devices](respond-machine-alerts.md#run-microsoft-defender-antivirus-scan-on-devices).
- Isolating devices from the network is supported for macOS for client version 101.98.84 and above. It is in preview. See [Isolate devices from the network](respond-machine-alerts.md#isolate-devices-from-the-network).
- Forcibly releasing devices from isolation is now available for public preview. This new capability allows you to forcibly release devices from isolation, when isolated devices become unresponsive. For more information, see [Forcibly release device from isolation](respond-machine-alerts.md#forcibly-release-device-from-isolation).

## May 2023

- Performance mode for Microsoft Defender Antivirus is now available for public preview. This new capability provides asynchronous scanning on a Dev Drive, and doesn't change the security posture of your system drive or other drives. For more information, see [Protecting Dev Drive using performance mode](microsoft-defender-endpoint-antivirus-performance-mode.md).

## March 2023

- Support for mixed-licensing scenarios is now in preview! With these capabilities, you can [Manage Microsoft Defender for Endpoint subscription settings across client devices (preview!)](defender-endpoint-subscription-settings.md).

## February 2023

- The Microsoft Defender for Identity integration toggle is now removed from the Microsoft Defender for Endpoint Settings > Advanced features page. Because Defender for Identity is now integrated with Microsoft Defender XDR, this toggle is no longer required. You don't need to manually configure integration between services. See [What's new - Microsoft Defender for Identity](/defender-for-identity/whats-new#defender-for-identity-release-2194).

## January 2023

- [Tamper protection](prevent-changes-to-security-settings-with-tamper-protection.md) can now protect exclusions when deployed with Microsoft Intune. See [Protect Microsoft Defender Antivirus exclusions from tampering](prevent-changes-to-security-settings-with-tamper-protection.md#protect-microsoft-defender-antivirus-exclusions)

- Live Response is now generally available for macOS and Linux. For more information, see [Investigate entities on devices using live response](live-response.md).

- [Live response API and library API for Linux and macOS is now generally available](api/run-live-response.md) <br/> You can now run live response API commands on Linux and macOS.

## Prior to 2023

For information about features released prior to 2023, see [Archive - What's new in Defender for Endpoint, December 2022 and earlier](whats-new-mde-archive.md#whats-new-in-microsoft-defender-for-endpoint---before-2023).
