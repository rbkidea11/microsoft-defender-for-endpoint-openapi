---
title: Migrate to Microsoft Defender for Endpoint - Setup
description: Move to Defender for Endpoint. Review the setup process, which includes installing Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: ewalsh
author: emmwalshh
ms.localizationpriority: medium
ms.date: 05/08/2025
manager: deniseb
audience: ITPro
ms.collection:
  - m365-security
  - m365solution-migratetomdatp
  - m365solution-mcafeemigrate
  - m365solution-symantecmigrate
  - highpri
  - tier1
ms.topic: how-to
ms.custom: migrationguides
ms.reviewer: jesquive, chventou, jonix, chriggs, owtho, yongrhee
search.appverid: met150
---

# Migrate to Microsoft Defender for Endpoint - Phase 2: Setup

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

|[![Phase 1: Prepare.](media/phase-diagrams/prepare.png#lightbox)](switch-to-mde-phase-1.md)<br/>[Phase 1: Prepare](switch-to-mde-phase-1.md)|![Phase 2: Set up.](media/phase-diagrams/setup.png#lightbox)<br/>Phase 2: Set up|[![Phase 3: Onboard3.](media/phase-diagrams/onboard.png#lightbox)](switch-to-mde-phase-3.md)<br/>[Phase 3: Onboard](switch-to-mde-phase-3.md)|
|---|---|---|
||*You're here!*||

**Welcome to the Setup phase of [migrating to Defender for Endpoint](switch-to-mde-overview.md#the-migration-process)**. This phase includes the following steps:

1. Reinstall/enable Microsoft Defender Antivirus on your endpoints.
2. Add Defender for Endpoint to the exclusion list for your existing solution.
3. Configure Defender for Endpoint Plan 1 or Plan 2.
4. Set up your device groups, device collections, and organizational units.

[!INCLUDE [side-by-side-scenarios](includes/side-by-side-scenarios.md)]

## Step 1: Reinstall/enable Microsoft Defender Antivirus on your endpoints

On certain versions of Windows, Microsoft Defender Antivirus was likely uninstalled or disabled when your non-Microsoft antivirus/antimalware solution was installed. When endpoints running Windows are onboarded to Defender for Endpoint, Microsoft Defender Antivirus can run in passive mode alongside a non-Microsoft antivirus solution. To learn more, see [Antivirus protection with Defender for Endpoint](microsoft-defender-antivirus-compatibility.md#antivirus-protection-without-defender-for-endpoint).

As you're making the switch to Defender for Endpoint, you might need to take certain steps to reinstall or enable Microsoft Defender Antivirus. The following table describes what to do on your Windows clients and servers.

|Endpoint type|What to do|
|---|---|
|Windows clients (such as endpoints running Windows 10 and Windows 11)|In general, you don't need to take any action for Windows clients as the Microsoft Defender Antivirus feature cannot be removed. If you are running a non-Microsoft antimalware solution, Microsoft Defender Antivirus is most likely in the automatic disabled state at this point of the migration process. <br/><br/>When client endpoints are onboarded to Defender for Endpoint, if those endpoints are still running a non-Microsoft antivirus solution, Microsoft Defender Antivirus goes into passive mode instead of the disabled state.<br/><br/>If the non-Microsoft antivirus solution is then uninstalled, Microsoft Defender Antivirus goes into active mode automatically.|
|Windows servers|On Windows Server, you may need to reinstall the Microsoft Defender Antivirus feature and set it to passive mode manually. On Windows servers, when a non-Microsoft antivirus/antimalware is installed, Microsoft Defender Antivirus can't run alongside the non-Microsoft antivirus solution. In those cases, Microsoft Defender Antivirus is disabled or uninstalled manually. <br/><br/> To reinstall or enable Microsoft Defender Antivirus on Windows Server, perform the following tasks: <br/>- [Re-enable Defender Antivirus on Windows Server if it was disabled](enable-update-mdav-to-latest-ws.md#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-disabled)<br/>- [Re-enable Defender Antivirus on Windows Server if it was uninstalled](enable-update-mdav-to-latest-ws.md#re-enable-microsoft-defender-antivirus-on-windows-server-if-it-was-uninstalled)<br/>- [Set Microsoft Defender Antivirus to passive mode on Windows Server](#manually-set-microsoft-defender-antivirus-to-passive-mode-on-windows-server) <br/><br/>If you run into issues reinstalling or re-enabling Microsoft Defender Antivirus on Windows Server, see [Troubleshooting: Microsoft Defender Antivirus is getting uninstalled on Windows Server](switch-to-mde-troubleshooting.md#microsoft-defender-antivirus-is-getting-uninstalled-on-windows-server). If Microsoft Defender Antivirus features and installation files were previously removed from Windows Server operating systems, follow the guidance in [Configure a Windows Repair Source](/windows-hardware/manufacture/desktop/configure-a-windows-repair-source) to restore the feature installation files.|

> [!TIP]
> To learn more about Microsoft Defender Antivirus states with non-Microsoft antivirus protection, see [Microsoft Defender Antivirus compatibility](microsoft-defender-antivirus-compatibility.md).

### Manually set Microsoft Defender Antivirus to passive mode on Windows Server

> [!TIP]
> You can now run Microsoft Defender Antivirus in passive mode on Windows Server 2012 R2 and 2016. For more information, see [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server.md).

1. Open Registry Editor, and then navigate to `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`.

1. Edit (or create) a DWORD entry called **ForceDefenderPassiveMode**, and specify the following settings:

   - Set the DWORD's value to **1**.
      
   - Under **Base**, select **Hexadecimal**.
      
> [!NOTE]
> To validate that passive mode was set as expected, search for **Event 5007** in the **Microsoft-Windows-Windows Defender Operational** log (located at `C:\Windows\System32\winevt\Logs`) and confirm that either the **ForceDefenderPassiveMode** or **PassiveMode** registry keys were set to **0x1**.

## Step 2: Add Microsoft Defender for Endpoint to the exclusion list for your existing solution

This step of the setup process involves adding Defender for Endpoint to the exclusion list for your existing endpoint protection solution and any other security products your organization is using. Make sure to refer to your solution provider's documentation to add exclusions.

Select the tab for information about exclusions for that operating system.

### [**Windows**](#tab/Windows)

The specific exclusions to configure depend on which version of Windows your endpoints or devices are running, and are listed in the following table.

| OS | Exclusions |
|--|--|
| Windows 11<br/>Windows 10, version 1803 or later (See Windows 10 release information)<br/>Windows 10, version 1703 or 1709 with KB4493441 installed<br/>Windows Server 2025<br/>Windows Server 2022<br/>Windows Server 2019<br/>Windows Server, version 1803<br/>Windows Server 2016 running the modern unified solution<br/>Windows Server 2012 R2 running the modern unified solution | **EDR exclusions**: <br/>`C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseCncProxy.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseSampleUploader.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseIR.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseCM.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseNdr.exe`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\Classification\SenseCE.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection`<br/>`C:\Program Files\Windows Defender Advanced Threat Protection\SenseTVM.exe` <br/><br/> **Antivirus exclusions**:<br/>`C:\Program Files\Windows Defender\MsMpEng.exe`<br/>`C:\Program Files\Windows Defender\NisSrv.exe`<br/>`C:\Program Files\Windows Defender\ConfigSecurityPolicy.exe`<br/>`C:\Program Files\Windows Defender\MpCmdRun.exe`<br/>`C:\Program Files\Windows Defender\MpDefenderCoreService.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MsMpEng.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\NisSrv.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\ConfigSecurityPolicy.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCopyAccelerator.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpCmdRun.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDefenderCoreService.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\mpextms.exe` <br/><br/> **Endpoint Data Loss Prevention (Endpoint DLP) exclusions**:<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpService.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MpDlpCmd.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\MipDlp.exe`<br/>`C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.*\DlpUserAgent.exe`|
| Windows Server 2016 or Windows Server 2012 R2 running the [modern unified solution](/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fswitch-to-mde-phase-2.md/main/76b249d7-f914-4c03-3eaf-48aa43b2fa4a/onboard-server.md) | The following **additional** exclusions are required after updating the Sense EDR component using [KB5005292](https://support.microsoft.com/topic/microsoft-defender-for-endpoint-update-for-edr-sensor-f8f69773-f17f-420f-91f4-a8e5167284ac): <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\MsSense.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCnCProxy.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseIR.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCE.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseSampleUploader.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseCM.exe` <br/>`C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\DataCollection`<br/> `C:\ProgramData\Microsoft\Windows Defender Advanced Threat Protection\Platform\*\SenseTVM.exe`|
| [Windows 8.1](/windows/release-health/status-windows-8.1-and-windows-server-2012-r2) [Windows 7](/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) [Windows Server 2008 R2 SP1](/windows/release-health/status-windows-7-and-windows-server-2008-r2-sp1) | `C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Monitoring Host Temporary Files 6\45\MsSenseS.exe` <br/>( Monitoring Host Temporary Files 6\45 can be different numbered subfolders.) <br/>`C:\Program Files\Microsoft Monitoring Agent\Agent\AgentControlPanel.exe`<br/> `C:\Program Files\Microsoft Monitoring Agent\Agent\HealthService.exe`<br/>`C:\Program Files\Microsoft Monitoring Agent\Agent\HSLockdown.exe`<br/>`C:\Program Files\Microsoft Monitoring Agent\Agent\MOMPerfSnapshotHelper.exe`<br/>`C:\Program Files\Microsoft Monitoring Agent\Agent\MonitoringHost.exe`<br/>`C:\Program Files\Microsoft Monitoring Agent\Agent\TestCloudConnection.exe` |

### [**macOS**](#tab/macOS)

For macOS devices, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
|--|--|
| `wdavdaemon_enterprise`<br/>EDR engine | `/Library/Application Support/Microsoft/Defender/` |  
| `wdavdaemon_unprivileged`<br/>Antivirus engine | `/Library/Application Support/Microsoft/Defender/` |
| `telemetryd_v1`<br/>Telemetry daemon for EDR | `/Library/Application Support/Microsoft/Defender/`  |
| `Netext`<br/>Network extension  | `/Library/SystemExtensions/*/com.microsoft.wdav.netext.systemextension/Contents/MacOS/` |
| `Epsext` <br/>Endpoint security extension | `/Library/SystemExtensions/*/com.microsoft.wdav.epsext.systemextension/Contents/MacOS/`  |
| `msupdate`<br/>Microsoft AutoUpdate update tool | `/Library/Application\ Support/Microsoft/MAU2.0/Microsoft\ AutoUpdate.app/Contents/MacOS` |

### [**Linux**](#tab/Linux)

For Linux servers, the following table lists processes to exclude in your non-Microsoft antivirus/antimalware solution:

| Process | Location |
|---|---|
| `wdavdaemon`<br/>Core daemon (service). Uses FANotify for both antimalware and EDR purposes (TALPA on older RHEL). | `/opt/microsoft/mdatp/sbin/` |
| `wdavdaemon enterprise`<br/>EDR engine. Used for enrichment. | `/opt/microsoft/mdatp/sbin/`  |
| `wdavdaemon unprivileged`<br/> Antivirus engine  | `/opt/microsoft/mdatp/sbin/` |
| `crashpad_handler`<br/>Collects crash dumps  | `/opt/microsoft/mdatp/sbin/` |
| `mdatp` <br/>Command line utility| `/opt/microsoft/mdatp/sbin/Wdavdaemonclient`  |
| `telemetryd_v2`<br/>Telemetry daemon for EDR | `/opt/microsoft/mdatp/sbin/` |
| `mde_netfilter` <br/>Packet filter for Network protection, also used for response capabilities | `/opt/microsoft/mde_netfilter/sbin` |

---

> [!IMPORTANT]
> As a best practice, keep your organization's devices and endpoints up to date. Make sure to get the **[latest updates for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](/editor/MicrosoftDocs/defender-docs-pr/defender-endpoint%2Fswitch-to-mde-phase-2.md/main/76b249d7-f914-4c03-3eaf-48aa43b2fa4a/microsoft-defender-antivirus-updates.md)**, and keep your organization's operating systems and productivity apps up to date.

## Step 3: Configure Defender for Endpoint

This article describes how to configure your Defender for Endpoint capabilities before devices are onboarded.

- If you have Defender for Endpoint Plan 1, complete steps 1-5 in the following procedure.
- If you have Defender for Endpoint Plan 2, complete steps 1-7 in the following procedure.

1. Make sure Defender for Endpoint is provisioned. As a Security Administrator, go to the Microsoft Defender portal ([https://security.microsoft.com](https://security.microsoft.com)) and sign in. Then, in the navigation pane, select **Assets** > **Devices**. 

   The following table shows what your screen might look like and what it means.

   | Screen | What it means |
   |---|:---|
   | :::image type="content" source="media/mde-hangon-provisioning.png" alt-text="Screenshot showing message that says hang on because MDE isn't provisioned yet." lightbox="media/mde-hangon-provisioning.png"::: | Defender for Endpoint isn't finished provisioning yet. You might have to wait a little while for the process to finish. |
   | :::image type="content" source="media/device-inventory-empty.png" alt-text="Screenshot showing device inventory page with no device onboarded yet." lightbox="media/device-inventory-empty.png"::: | Defender for Endpoint is provisioned. In this case, proceed to the next step. |

2. Turn on [tamper protection](prevent-changes-to-security-settings-with-tamper-protection.md). We recommend turning tamper protection on for your whole organization. You can do this task in the Microsoft Defender portal ([https://security.microsoft.com](https://security.microsoft.com)).

   1. In the Microsoft Defender portal, choose **Settings** > **Endpoints**.

   2. Go to **General** > **Advanced features**, and then set the toggle for tamper protection to **On**.

   3. Select **Save**.

   [Learn more about tamper protection](prevent-changes-to-security-settings-with-tamper-protection.md).

3. If you're using either [Microsoft Intune](/mem/intune/fundamentals/what-is-intune) or [Microsoft Endpoint Configuration Manager](/mem/endpoint-manager-overview) to onboard devices and configure device policies, set up integration with Defender for Endpoint by following these steps: <br/>

   1. In the Microsoft Intune admin center ([https://intune.microsoft.com](https://intune.microsoft.com)), go to **Endpoint security**.

   2. Under **Setup**, choose **Microsoft Defender for Endpoint**.

   3. Under **Endpoint Security Profile Settings**, set the toggle for **Allow Microsoft Defender for Endpoint to enforce Endpoint Security Configurations** to **On**.

   4. Near the top of the screen, select **Save**.

   5. In the Microsoft Defender portal ([https://security.microsoft.com](https://security.microsoft.com)), choose **Settings** > **Endpoints**.

   6. Scroll down to **Configuration management**, and select **Enforcement scope**. 

   7. Set the toggle for **Use MDE to enforce security configuration settings from MEM** to **On**, and then select the options for both Windows client and Windows Server devices. 

   8. If you're planning to use Configuration Manager, set the toggle for **Manage Security settings using Configuration Manager** to **On**. (If you need help with this step, see [Coexistence with Microsoft Endpoint Configuration Manager](/mem/intune/protect/mde-security-integration#co-existence-with-microsoft-endpoint-configuration-manager).)

   9. Scroll down and select **Save**.

4. Configure your initial [attack surface reduction capabilities](overview-attack-surface-reduction.md). At a minimum, enable the standard protection rules that are listed in the following table right away:

   | Standard protection rules | Configuration methods |
   |:---|:---|
   | [Block credential stealing from the Windows local security authority subsystem (lsass.exe)](attack-surface-reduction-rules-reference.md#block-credential-stealing-from-the-windows-local-security-authority-subsystem) <br/><br/>[Block abuse of exploited vulnerable signed drivers](attack-surface-reduction-rules-reference.md#block-abuse-of-exploited-vulnerable-signed-drivers)<br/><br/>[Block persistence through Windows Management Instrumentation (WMI) event subscription](attack-surface-reduction-rules-reference.md#block-persistence-through-wmi-event-subscription) | [Intune](enable-attack-surface-reduction.md#intune) (Device configuration profiles or Endpoint Security policies) <br/><br/>[Mobile Device Management (MDM)](enable-attack-surface-reduction.md#mdm) (Use the [./Vendor/MSFT/Policy/Config/Defender/AttackSurfaceReductionRules](/windows/client-management/mdm/policy-csp-defender#defender-attacksurfacereductionrules) configuration service provider (CSP) to individually enable and set the mode for each rule.)<br/><br/>[Group Policy](enable-attack-surface-reduction.md#group-policy) or [PowerShell](enable-attack-surface-reduction.md#powershell) (only if you're not using Intune, Configuration Manager, or another enterprise-level management platform) |

   [Learn more about attack surface reduction capabilities](overview-attack-surface-reduction.md).

5. Configure your [next-generation protection capabilities](next-generation-protection.md).

   | Capability | Configuration methods |
   |---|---|
   |[Intune](/mem/intune/fundamentals/tutorial-walkthrough-endpoint-manager) |1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** \> **Configuration profiles**, and then select the profile type you want to configure. If you haven't yet created a **Device restrictions** profile type, or if you want to create a new one, see [Configure device restriction settings in Microsoft Intune](/mem/intune/configuration/device-restrictions-configure).<br/><br/>2. Select **Properties**, and then select **Configuration settings: Edit**<br/><br/>3. Expand **Microsoft Defender Antivirus**.<br/><br/>4. Enable **Cloud-delivered protection**.<br/><br/>5. In the **Prompt users before sample submission** dropdown, select **Send all samples automatically**.<br/><br/>6. In the **Detect potentially unwanted applications** dropdown, select **Enable** or **Audit**.<br/><br/>7. Select **Review + save**, and then choose **Save**. <br/><br/> **TIP**: For more information about Intune device profiles, including how to create and configure their settings, see [What are Microsoft Intune device profiles?](/mem/intune/configuration/device-profiles).|
   |[Configuration Manager](/mem/configmgr)|See [Create and deploy antimalware policies for Endpoint Protection in Configuration Manager](/mem/configmgr/protect/deploy-use/endpoint-antimalware-policies). <br/><br/> When you create and configure your antimalware policies, make sure to review the [real-time protection settings](/mem/configmgr/protect/deploy-use/endpoint-antimalware-policies#real-time-protection-settings) and [enable block at first sight](configure-block-at-first-sight-microsoft-defender-antivirus.md).
   |[Advanced Group Policy Management](/microsoft-desktop-optimization-pack/agpm/) <br/> or <br/> [Group Policy Management Console](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus)|1. Go to **Computer configuration** \> **Administrative templates** \> **Windows components** \> **Microsoft Defender Antivirus**.<br/><br/>2. Look for a policy called **Turn off Microsoft Defender Antivirus**.<br/><br/>3. Choose **Edit policy setting**, and make sure that policy is disabled. This action enables Microsoft Defender Antivirus. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)|
   |Control Panel in Windows|Follow the guidance here: [Turn on Microsoft Defender Antivirus](/mem/intune/user-help/turn-on-defender-windows). (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)|

   *If you have Defender for Endpoint Plan 1, your initial setup and configuration is complete. If you have Defender for Endpoint Plan 2, continue through steps 6-7.*

6. Configure your endpoint detection and response (EDR) policies in the Intune admin center ([https://intune.microsoft.com](https://intune.microsoft.com)). To get help with this task, see [Create EDR policies](/mem/intune/protect/endpoint-security-edr-policy#create-edr-policies).

7. Configure your automated investigation and remediation capabilities in the Microsoft Defender portal ([https://security.microsoft.com](https://security.microsoft.com)). To get help with this task, see [Configure automated investigation and remediation capabilities in Microsoft Defender for Endpoint](configure-automated-investigations-remediation.md).

   *At this point, initial setup and configuration of Defender for Endpoint Plan 2 is complete.*

## Step 4: Add your existing solution to the exclusion list for Microsoft Defender Antivirus

During this step of the setup process, you add your existing solution to the list of exclusions for Microsoft Defender Antivirus. You can choose from several methods to add your exclusions to Microsoft Defender Antivirus, as listed in the following table: 

|Method|What to do|
|---|---|
|[Intune](/mem/intune/fundamentals/tutorial-walkthrough-endpoint-manager) |1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and sign in.<br/><br/>2. Select **Devices** \> **Configuration profiles**, and then select the profile that you want to configure.<br/><br/>3. Under **Manage**, select **Properties**.<br/><br/>4. Select **Configuration settings: Edit**.<br/><br/>5. Expand **Microsoft Defender Antivirus**, and then expand **Microsoft Defender Antivirus Exclusions**.<br/><br/>6. Specify the files, folders, and processes to exclude from Microsoft Defender Antivirus scans. For reference, see [Microsoft Defender Antivirus exclusions](/mem/intune/configuration/device-restrictions-windows-10#microsoft-defender-antivirus-exclusions).<br/><br/>7. Choose **Review + save**, and then choose **Save**.|
|[Microsoft Endpoint Configuration Manager](/mem/configmgr/)|1. Using the [Configuration Manager console](/mem/configmgr/core/servers/manage/admin-console), go to **Assets and Compliance** \> **Endpoint Protection** \> **Antimalware Policies**, and then select the policy that you want to modify.<br/><br/>2. Specify exclusion settings for files, folders, and processes to exclude from Microsoft Defender Antivirus scans.|
|[Group Policy Object](/previous-versions/windows/desktop/Policy/group-policy-objects)|1. On your Group Policy management computer, open the [Group Policy Management Console](https://technet.microsoft.com/library/cc731212.aspx). Right-click the Group Policy Object you want to configure and then select **Edit**.<br/><br/>2. In the **Group Policy Management Editor**, go to **Computer configuration** and select **Administrative templates**.<br/><br/>3. Expand the tree to **Windows components \> Microsoft Defender Antivirus \> Exclusions**. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)<br/><br/>4. Double-click the **Path Exclusions** setting and add the exclusions.<br/><br/>5. Set the option to **Enabled**.<br/><br/>6. Under the **Options** section, select **Show...**.<br/><br/>7. Specify each folder on its own line under the **Value name** column. If you specify a file, make sure to enter a fully qualified path to the file, including the drive letter, folder path, filename, and extension. Enter **0** in the **Value** column.<br/><br/>8. Select **OK**.<br/><br/>9. Double-click the **Extension Exclusions** setting and add the exclusions.<br/><br/>10. Set the option to **Enabled**.<br/><br/>11. Under the **Options** section, select **Show...**.<br/><br/>12. Enter each file extension on its own line under the **Value name** column. Enter **0** in the **Value** column.<br/><br/>13. Select **OK**.|
|Local group policy object|1. On the endpoint or device, open the Local Group Policy Editor.<br/><br/>2. Go to **Computer Configuration** \> **Administrative Templates** \> **Windows Components** \> **Microsoft Defender Antivirus** \> **Exclusions**. (You might see *Windows Defender Antivirus* instead of *Microsoft Defender Antivirus* in some versions of Windows.)<br/><br/>3. Specify your path and process exclusions.|
|Registry key|1. Export the following registry key: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\exclusions`.<br/><br/>2. Import the registry key. Here are two examples:<br/>- Local path: `regedit.exe /s c:\temp\MDAV_Exclusion.reg`<br/>- Network share: `regedit.exe /s \\FileServer\ShareName\MDAV_Exclusion.reg`|

[Learn more about exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md).

### Keep the following points about exclusions in mind

When you add [exclusions to Microsoft Defender Antivirus scans](/windows/security/threat-protection/microsoft-defender-antivirus/configure-exclusions-microsoft-defender-antivirus), you should add path and process exclusions.

- *Path exclusions* exclude specific files and whatever those files access.
- *Process exclusions* exclude whatever a process touches, but doesn't exclude the process itself.
- List your process exclusions using their full path and not by their name only. (The name-only method is less secure.)
- If you list each executable (.exe) as both a path exclusion and a process exclusion, the process and whatever it touches are excluded.

## Step 5: Set up your device groups, device collections, and organizational units

Device groups, device collections, and organizational units enable your security team to manage and assign security policies efficiently and effectively. The following table describes each of these groups and how to configure them. Your organization might not use all three collection types.

> [!NOTE]
> Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

|Collection type|What to do|
|---|---|
|[Device groups](machine-groups.md) (formerly called *machine groups*) enable your security operations team to configure security capabilities, such as automated investigation and remediation. <br/><br/> Device groups are also useful for assigning access to those devices so that your security operations team can take remediation actions if needed. <br/><br/> Device groups are created while the attack was detected and stopped, alerts, such as an "initial access alert," were triggered and appeared in the [Microsoft Defender portal](/defender-xdr/microsoft-365-defender).|1. Go to the Microsoft Defender portal (<https://security.microsoft.com>).<br/><br/>2. In the navigation pane on the left, choose **Settings** \> **Endpoints** \> **Permissions** \> **Device groups**.<br/><br/>3. Choose **+ Add device group**.<br/><br/>4. Specify a name and description for the device group.<br/><br/>5. In the **Automation level** list, select an option. (We recommend **Full - remediate threats automatically**.) To learn more about the various automation levels, see [How threats are remediated](automated-investigations.md#how-threats-are-remediated).<br/><br/>6. Specify conditions for a matching rule to determine which devices belong to the device group. For example, you can choose a domain, OS versions, or even use [device tags](machine-tags.md).<br/><br/>7. On the **User access** tab, specify roles that should have access to the devices that are included in the device group.<br/><br/>8. Choose **Done**.|
|[Device collections](/mem/configmgr/core/clients/manage/collections/introduction-to-collections) enable your security operations team to manage applications, deploy compliance settings, or install software updates on the devices in your organization. <br/><br/> Device collections are created by using [Configuration Manager](/mem/configmgr/).|Follow the steps in [Create a collection](/mem/configmgr/core/clients/manage/collections/create-collections#bkmk_create).|
|[Organizational units](/azure/active-directory-domain-services/create-ou) enable you to logically group objects such as user accounts, service accounts, or computer accounts. <br/><br/> You can then assign administrators to specific organizational units, and apply group policy to enforce targeted configuration settings. <br/><br/> Organizational units are defined in [Microsoft Entra Domain Services](/azure/active-directory-domain-services).|Follow the steps in [Create an Organizational Unit in a Microsoft Entra Domain Services managed domain](/azure/active-directory-domain-services/create-ou).|

## Next step

**Congratulations**! You've completed the Setup phase of [migrating to Defender for Endpoint](switch-to-mde-overview.md#the-migration-process)!

- [Proceed to Phase 3: Onboard to Defender for Endpoint](switch-to-mde-phase-3.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
