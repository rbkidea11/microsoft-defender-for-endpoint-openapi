---
title: Collect diagnostic data of Microsoft Defender Antivirus
description: Use a tool to collect data to troubleshoot Microsoft Defender Antivirus.
ms.service: defender-endpoint
ms.localizationpriority: medium
author: emmwalshh
ms.author: ewalsh
ms.custom: nextgen
ms.date: 06/10/2025
ms.reviewer: pahuijbr, yongrhee
manager: deniseb
ms.subservice: ngp
ms.topic: how-to
ms.collection: 
- m365-security
- tier2
- mde-ngp
search.appverid: met150
---

# Collect Microsoft Defender Antivirus diagnostic data

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]


**Applies to:**

- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender for Business](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-business)
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- Microsoft Defender Antivirus
- [Microsoft Defender for Individuals](https://www.microsoft.com/microsoft-365/microsoft-defender-for-individuals)

This article describes how to collect diagnostic data that's used by Microsoft support and engineering teams when they help troubleshoot issues with Microsoft Defender Antivirus.

> [!NOTE]
> As part of the investigation or response process, you can collect an investigation package from a device. Here's how: [Collect investigation package from devices](/windows/security/threat-protection/microsoft-defender-atp/respond-machine-alerts#collect-investigation-package-from-devices).
>
> For performance-specific issues related to Microsoft Defender Antivirus, see: [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus.md).

## Get the diagnostic files

On at least two devices that are experiencing the same issue, obtain the `.cab` diagnostic file by taking the following steps:

1. Open Command Prompt as an administrator by following these steps:

   a. Open the **Start** menu.
   
   b. Type **cmd**. Right-click on **Command Prompt** and then select **Run as administrator**.
   
   c. Specify administrator credentials or approve the prompt.
   
1. Navigate to the directory for Microsoft Defender Antivirus: 

   `cd C:\ProgramData\Microsoft\Windows Defender\Platform\<version>`
   
   Where `<version>` is the actual version that starts with `4.18.2xxxx.x`
   
   > [!NOTE]
   > `C:\ProgramData` is a hidden folder. If you don't have a folder that starts with `4.18.2xxxx.x` in `C:\ProgramData\Microsoft\Windows Defender\Platform\`, then you will need to go to `C:\Program Files\Windows Defender\`.

1. Type the following command, and then press **Enter**

   ```Dos
   mpcmdrun.exe -GetFiles
   ```

4. A `.cab` file is generated that contains various diagnostic logs. The location of the file is specified in the output in the command prompt. By default, the location is `C:\ProgramData\Microsoft\Windows Defender\Support\MpSupportFiles.cab`.

   > [!NOTE]
   > To redirect the cab file to a different path or UNC share, use the following command:
   >
   > `mpcmdrun.exe -GetFiles -SupportLogLocation <path>`
   >
   > For more information, see [Redirect diagnostic data to a UNC share](#redirect-diagnostic-data-to-a-unc-share).

5. Copy these .cab files to a location that can be accessed by Microsoft support. An example could be a password-protected OneDrive folder that you can share with us.

## Redirect diagnostic data to a UNC share

To collect diagnostic data on a central repository, you can specify the SupportLogLocation parameter.

```Dos
mpcmdrun.exe -GetFiles -SupportLogLocation <path>
```

Copies the diagnostic data to the specified path. If the path isn't specified, the diagnostic data is copied to the location specified in the Support Log Location Configuration.

When the `SupportLogLocation` parameter is used, a folder structure like as follows will be created in the destination path:

```Dos
<path>\<MMDD>\MpSupport-<hostname>-<HHMM>.cab
```

|field|Description|
|---|---|
|path|The path as specified on the command line or retrieved from configuration|
|MMDD|Month and day when the diagnostic data was collected (for example, 0530)|
|hostname|The hostname of the device on which the diagnostic data was collected|
|HHMM|Hours and minutes when the diagnostic data was collected (for example, 1422)|

> [!NOTE]
> When using a file share please make sure that account used to collect the diagnostic package has write access to the share.

## Specify location where diagnostic data is created

You can also specify where the diagnostic `.cab` file is created using a Group Policy Object (GPO).

1. Open the Local Group Policy Editor and find the SupportLogLocation GPO at: `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\SupportLogLocation`.

2. Select **Define the directory path to copy support log files**.

   :::image type="content" source="media/GPO1-SupportLogLocationDefender.png" alt-text="The local group policy editor" lightbox="media/GPO1-SupportLogLocationDefender.png":::

   :::image type="content" source="media/GPO2-SupportLogLocationGPPage.png" alt-text="The define path for log files setting" lightbox="media/GPO2-SupportLogLocationGPPage.png":::

   :::image type="content" source="media/GPO1-SupportLogLocationDefender.png" alt-text="The local group policy editor" lightbox="media/GPO1-SupportLogLocationDefender.png"::: 
        
   :::image type="content" source="media/GPO2-SupportLogLocationGPPage.png" alt-text="The define path for configuring the log files setting" lightbox="media/GPO2-SupportLogLocationGPPage.png":::
 
3. Inside the policy editor, select **Enabled**.

4. Specify the directory path where you want to copy the support log files in the **Options** field.
   
   :::image type="content" source="media/GPO3-SupportLogLocationGPPageEnabledExample.png" alt-text="Screenshot showing the enabled directory path custom setting." lightbox="media/GPO3-SupportLogLocationGPPageEnabledExample.png":::

5. Select **OK** or **Apply**.

## See also

- [Troubleshoot Microsoft Defender Antivirus reporting](/mem/intune/protect/advanced-threat-protection-configure)
- [Performance analyzer for Microsoft Defender Antivirus](tune-performance-defender-antivirus.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
