---
title: Deploy and manage device control in Microsoft Defender for Endpoint with Group Policy           
description: Learn how to deploy and manage device control in Defender for Endpoint using Group Policy
author: emmwalshh
ms.author: ewalsh
manager: deniseb 
ms.date: 01/31/2025
ms.topic: overview
ms.service: defender-endpoint
ms.subservice: asr
audience: ITPro
ms.collection: 
- m365-security
- tier2
- mde-asr
ms.custom: 
- partner-contribution
ms.reviewer: joshbregman, tdoucette
search.appverid: MET150
f1.keywords: NOCSH 
---

# Deploy and manage device control in Microsoft Defender for Endpoint using Group Policy

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](/defender-business)

If you're using Group Policy to manage Defender for Endpoint settings, you can use it to deploy and manage device control.

## Enable or disable removable storage access control

:::image type="content" source="media/deploy-dc-gpo/enable-disable-rsac.png" alt-text="Screenshot of enable disable rsac." lightbox="media/deploy-dc-gpo/enable-disable-rsac.png":::

1. On a device running Windows, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus** > **Features** > **Device Control**.

2. In the **Device Control** window, select **Enabled**.

> [!NOTE]
> If you don't see these Group Policy Objects, you need to add the Group Policy Administrative Templates (ADMX). You can download administrative template ([WindowsDefender.adml](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/WindowsDefender.adml) and [WindowsDefender.admx](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/WindowsDefender.admx)) from [mdatp-devicecontrol / Windows samples](https://github.com/microsoft/mdatp-devicecontrol/tree/main/windows) in GitHub.

## Set default enforcement

You can set default access, such as `Deny` or `Allow` for all device control features including `RemovableMediaDevices`, `CdRomDevices`, `WpdDevices`, and `PrinterDevices`.

:::image type="content" source="media/set-default-enforcement-deny-gp.png" alt-text="Screenshot of set default enforcement." lightbox="media/set-default-enforcement-deny-gp.png":::

For example, you can have either a `Deny` or an `Allow` policy for `RemovableMediaDevices`, but not for `CdRomDevices` or `WpdDevices`. If you set `Default Deny` through this policy, then Read/Write/Execute access to `CdRomDevices` or `WpdDevices` is blocked. If you only want to manage storage, make sure to create `Allow` policy for printers. Otherwise, default enforcement (Deny) is applied to printers, too.

1. On a device running Windows, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus** > **Features** > **Device Control** > **Select Device Control Default Enforcement Policy**.

2. In the **Select Device Control Default Enforcement Policy** window, select **Default Deny**.

## Configure device types

:::image type="content" source="media/deploy-dc-gpo/configure-device.png" alt-text="Screenshot of configure device types." lightbox="media/deploy-dc-gpo/configure-device.png":::

To configure the device types that a device control policy is applied, follow these steps:

1. On a computer running Windows, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus** > **Device Control** > **Turn on device control for specific device types**.

2. In the **Turn on device control for specific types** window, specify the product family IDs, separate by a pipe (`|`). This setting must be a single string with no spaces or it will be parsed incorrectly by the device control engine causing unexpected behaviors. Product family IDs include `RemovableMediaDevices`, `CdRomDevices`, `WpdDevices`, or `PrinterDevices`.

## Define groups

:::image type="content" source="media/deploy-dc-gpo/define-groups.png" alt-text="Screenshot of define groups." lightbox="media/deploy-dc-gpo/define-groups.png":::

1. Create one XML file for each removable storage group. 

2. Use the properties in your removable storage group to create an XML file for each removable storage group.

   Make sure the root node of the XML is PolicyGroups, for example, the following XML:

   ```xml
    <PolicyGroups>
        <Group Id="{d8819053-24f4-444a-a0fb-9ce5a9e97862}" Type="Device">
             
        </Group>
    </PolicyGroups>
    ```

3. Save the XML file to your network share.

4. Define the settings as follows:

   1. On a device running Windows, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus** > **Device Control** > **Define device control policy groups**.

   2. In the **Defined device control policy groups** window, specify the network share file path containing the XML groups data.

You can create different group types. Here's one group example XML file for any removable storage and CD-ROM, Windows portable devices, and approved USBs group: [XML file](https://github.com/microsoft/mdatp-devicecontrol/blob/main/windows/device/Group%20Policy/Scenario%202%20GPO%20Removable%20Storage%20Group.xml)

> [!NOTE]
> Comments using XML comment notation `<!--COMMENT-->` can be used in the Rule and Group XML files, but they must be inside the first XML tag, not the frontline of the XML file.

## Define Policies

:::image type="content" source="media/deploy-dc-gpo/define-policies.png" alt-text="Screenshot of define policies." lightbox="media/deploy-dc-gpo/define-policies.png":::


1. Create one XML file for access policy rule.

2. Use the properties in removable storage access policy rules to create an XML for each group's removable storage access policy rule. 

   Ensure root node of the XML is PolicyRules, for example, the following XML:

   ```xml
   <PolicyRules>
     <PolicyRule Id="{d8819053-24f4-444a-a0fb-9ce5a9e97862}">
         ...
      </PolicyRule> 
   </PolicyRules>
   ```

3. Save the XML file to network share.

4. Define the settings as follows:

   1. On a device running Windows, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus** > **Device Control** > **Define device control policy rules**.

   2. In the **Define device control policy rules** window, select **Enabled**, and then specify the network share file path containing the XML rules data.

## Validating XML files

Mpcmdrun built in functionality to validate XML files that are used for GPO deployments. This feature enables customers to detect any syntax errors the DC engine might encounter while parsing the settings. To perform this validation, administrators should copy the following PowerShell script and provide the appropriate file path for their XML files containing the Device Control rules and groups.

```
#Path to PolicyRules xml. Provide the filepath of the device control rules XML file
$RulesXML="C:\Policies\PolicyRules.xml"

#Path to Groups XML. Provide the filepath of the device control groups XML file
$GroupsXML="C:\Policies\Groups.xml"

#Retrieve the install path from Defender
$DefenderPath=(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows Defender" -Name "InstallLocation").InstallLocation

#Test PolicyRules
& $DefenderPath\mpcmdrun.exe -devicecontrol -testpolicyxml $RulesXML -rules

#Test Groups
& $DefenderPath\mpcmdrun.exe -devicecontrol -testpolicyxml $GroupsXML -groups
```


If there are no errors, the following output will be printed in the PowerShell console:


```
DC policy rules parsing succeeded
Verifying absolute rules data against the original data
Rules verified with success
DC policy groups parsing succeeded
Verifying absolute groups data against the original data
Groups verified with success
Has Group Dependency Loop: no
```

> [!NOTE]
> To capture evidence of files being copied or printed, use [Endpoint DLP.](/purview/dlp-copy-matched-items-get-started?tabs=purview-portal%2Cpurview)
> 
> Comments using XML comment notation `<!-- COMMENT -->` can be used in the Rule and Group XML files, but they must be inside the first XML tag, not the frontline of the XML file.

## See also

- [Device control in Defender for Endpoint](device-control-overview.md)
- [Device control policies in and settings](device-control-policies.md)
- [Device Control for macOS](mac-device-control-overview.md)

