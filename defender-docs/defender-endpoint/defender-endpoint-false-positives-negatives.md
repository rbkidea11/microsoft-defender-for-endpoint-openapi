---
title: Address false positives/negatives in Microsoft Defender for Endpoint
description: Learn how to handle false positives or false negatives in Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.subservice: ngp
ms.author: ewalsh
author: emmwalshh
ms.localizationpriority: medium
ms.date: 03/03/2025
manager: deniseb
audience: ITPro
ms.collection:
- m365-security
- m365initiative-defender-endpoint
- m365solution-overview
- m365solution-fpfn
- highpri
- tier1
ms.topic: solution-overview
ms.reviewer: ramarom, evaldm, isco, mabraitm, chriggs, yonghree, jcedola
ms.custom: 
- FPFN
- admindeeplinkDEFENDER
search.appverid: met150
---

# Address false positives/negatives in Microsoft Defender for Endpoint

**Applies to:**

- [Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- Microsoft Defender Antivirus

**Platforms**
- Windows

In endpoint protection solutions, a false positive is an entity, such as a file or a process that was detected and identified as malicious even though the entity isn't actually a threat. A false negative is an entity that wasn't detected as a threat, even though it actually is malicious. False positives/negatives can occur with any threat protection solution, including [Defender for Endpoint](microsoft-defender-endpoint.md).

 If you have Microsoft Defender XDR, review the "Alerts sources" as described in [Investigate alerts in Microsoft Defender XDR](/defender-xdr/investigate-alerts?tabs=settings). If the alert source is Defender for Endpoint, continue to read this article. 

## Identify the detection source

When you have a false positive, a good first step is to try to determine its detection source. The following table lists detection sources and potential solutions.

|Detection source| Information|
| -------- | -------- |
|Endpoint Detection and Response (EDR) | The alert is related to EDR in Defender for Endpoint <br/>- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi) <br/>- Work-around: Add an EDR exclusion or tune the alerts|
|Antivirus|The alert relates to Microsoft Defender Antivirus in active mode (primary) where it blocks. <br/>- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi) <br/>- Work-around: Add [Indicators - File hash - allow ](/defender-endpoint/indicator-file) or an [Antivirus exclusion](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions)<br/><br/>If Microsoft Defender Antivirus is in passive mode, EDR in block mode might just detect.|
| Custom TI| Custom indicators:<br/>- [File hash](/defender-endpoint/indicator-file)<br/>- [IP address or URL](/defender-endpoint/indicator-ip-domain)<br/>- [Certificates](/defender-endpoint/indicator-certificates) <br/><br/>Solution: [Manage indicators](/defender-endpoint/indicator-manage). <br/><br/> Or, if you see `CustomEnterpriseBlock`, your detection source could be one of the following capabilities in Defender for Endpoint: <br/><br/>1. [Automated investigation and remediation](automated-investigations.md)<br/>-- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi) <br/>-- Work-around: [Automation folder exclusions  ](/defender-endpoint/manage-automation-folder-exclusions)<br/><br/>2. Custom detection rules deriving from [Advanced Hunting](/defender-xdr/advanced-hunting-overview) <br/>-- Solution: [Manage existing custom detection rules  ](/defender-xdr/custom-detection-rules)<br/><br/>3. [EDR in block mode](/defender-endpoint/edr-in-block-mode) <br/>-- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi)<br/>-- Work-around: [Indicators – File hash – allow](/defender-endpoint/indicator-file) or [Antivirus exclusions](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions)<br/><br/>4. [Live response](live-response.md)<br/>-- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi)<br/>-- Work-around: [Indicators – File hash – allow](/defender-endpoint/indicator-file) or [Antivirus exclusions](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions)<br/><br/>5. [PUA protection](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus.md)<br/>-- Solution: Submit the false positive to [https://aka.ms/wdsi](https://aka.ms/wdsi)<br/>-- Work-around: [Indicators – File hash – allow](/defender-endpoint/indicator-file) or [Antivirus exclusions](/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions)|
| Smartscreen|[Smartscreen](https://feedback.smartscreen.microsoft.com/smartscreenfaq.aspx): You can [Report an unsafe site](https://www.microsoft.com/en-us/wdsi/support/report-unsafe-site) or [submit a network protection detection](https://www.microsoft.com/wdsi/support/report-exploit-guard)|

## False positives and how to address them

:::image type="content" source="media/false-positives-overview.png" alt-text="Screenshot displaying the definitions of false positives and false negatives in the Microsoft Defender portal." lightbox="media/false-positives-overview.png":::

Fortunately, steps can be taken to address and reduce these kinds of issues. 

:::image type="content" source="media/false-positives-step-diagram.png" alt-text="The steps to address false positives and negatives" lightbox="media/false-positives-step-diagram.png":::

## Part 1: Review and classify alerts

If you see an [alert](api/alerts.md) that arose because something's detected as malicious or suspicious and it shouldn't be, you can suppress the alert for that entity. You can also suppress alerts that aren't necessarily false positives, but are unimportant. We recommend that you also classify alerts.

Managing your alerts and classifying true/false positives helps to train your threat protection solution and can reduce the number of false positives or false negatives over time. Taking these steps also helps reduce noise in your queue so that your security team can focus on higher priority work items.

### Determine whether an alert is accurate

Before you classify or suppress an alert, determine whether the alert is accurate, a false positive, or benign.

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), in the navigation pane, choose **Incidents & alerts** and then select **Alerts**.

2. Select an alert to view more details about it. (To get help with this task, see [Review alerts in Defender for Endpoint](review-alerts.md).)

3. Depending on the alert status, take the steps described in the following table:

   |Alert status|What to do|
   |---|---|
   |The alert is accurate|Assign the alert, and then [investigate it](investigate-alerts.md) further.|
   |The alert is a false positive|1. [Classify the alert](#classify-an-alert) as a false positive.<br/><br/>2. [Suppress the alert](#suppress-an-alert).<br/><br/>3. [Create an indicator](#indicators-for-defender-for-endpoint) for Microsoft Defender for Endpoint.<br/><br/>4. [Submit a file to Microsoft for analysis](#part-4-submit-a-file-for-analysis).|
   |The alert is accurate, but benign (unimportant)|[Classify the alert](#classify-an-alert) as a true positive, and then [suppress the alert](#suppress-an-alert).|

### Classify an alert

Alerts can be classified as false positives or true positives in the Microsoft Defender portal. Classifying alerts helps train Defender for Endpoint so that over time, you'll see more true alerts and fewer false alerts.

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), in the navigation pane, choose **Incidents & alerts**, select **Alerts** and then select an alert.

2. For the selected alert, select **Manage alert**. A flyout pane opens.

3. In the **Manage alert** section, in the **Classification** field, classify the alert (True positive, Informational, expected activity, or False positive).

> [!TIP]
> For more information about suppressing alerts, see [Manage Defender for Endpoint alerts](manage-alerts.md). And, if your organization is using a security information and event management (SIEM) server, make sure to define a suppression rule there, too.

### Suppress an alert

If you have alerts that are either false positives or that are true positives but for unimportant events, you can suppress those alerts in Microsoft Defender XDR. Suppressing alerts helps reduce noise in your queue.

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), in the navigation pane, choose **Incidents & alerts** and then select **Alerts**.

2. Select an alert that you want to suppress to open its **Details** pane.

3. In the **Details** pane, choose the ellipsis (**...**), and then **Create suppression rule**.

4. Specify all the settings for your suppression rule, and then choose **Save**.

> [!TIP]
> Need help with suppression rules? See [Suppress an alert and create a new suppression rule](manage-alerts.md#suppress-an-alert-and-create-a-new-suppression-rule).

## Part 2: Review remediation actions

[Remediation actions](manage-auto-investigation.md#remediation-actions), such as sending a file to quarantine or stopping a process, are taken on entities (such as files) that are detected as threats. Several types of remediation actions occur automatically through automated investigation and Microsoft Defender Antivirus:

- Quarantine a file
- Remove a registry key
- Kill a process
- Stop a service
- Disable a driver
- Remove a scheduled task

Other actions, such as starting an antivirus scan or collecting an investigation package, occur manually or through [Live Response](live-response.md). Actions taken through Live Response can't be undone.

After you've reviewed your alerts, your next step is to [review remediation actions](manage-auto-investigation.md). If any actions were taken as a result of false positives, you can undo most kinds of remediation actions. Specifically, you can:

- [Restore a quarantined file from the Action Center](#restore-a-quarantined-file-from-the-action-center)
- [Undo multiple actions at one time](#undo-multiple-actions-at-one-time)
- [Remove a file from quarantine across multiple devices](#remove-a-file-from-quarantine-across-multiple-devices). and
- [Restore file from quarantine](#restore-file-from-quarantine)

When you're done reviewing and undoing actions that were taken as a result of false positives, proceed to [review or define exclusions](#part-3-review-or-define-exclusions).

### Review completed actions

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), select **Actions & submissions** and then select **Action center**.

2. Select the **History** tab to view a list of actions that were taken.

3. Select an item to view more details about the remediation action that was taken.

### Restore a quarantined file from the Action Center

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), select **Actions & submissions** and then select **Action center**.

2. On the **History** tab, select an action that you want to undo.

3. In the flyout pane, select **Undo**. If the action can't be undone with this method, you don't see an **Undo** button. (To learn more, see [Undo completed actions](manage-auto-investigation.md#undo-completed-actions).)

### Undo multiple actions at one time

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), select **Actions & submissions** and then select **Action center**.

2. On the **History** tab, select the actions that you want to undo.

3. In the flyout pane on the right side of the screen, select **Undo**.

### Remove a file from quarantine across multiple devices

> [!div class="mx-imgBorder"]
> :::image type="content" source="media/autoir-quarantine-file-1.png" alt-text="The Quarantine file" lightbox="media/autoir-quarantine-file-1.png":::

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), select **Actions & submissions** and then select **Action center**.

2. On the **History** tab, select a file that has the Action type **Quarantine file**.

3. In the pane on the right side of the screen, select **Apply to X more instances of this file**, and then select **Undo**.

### Review quarantined messages

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), in the navigation pane, under **Email & collaboration**, select **Exchange message trace**.

2. Select a message to view details.

### Restore file from quarantine

You can roll back and remove a file from quarantine if you determine that it's clean after an investigation. Run the following command on each device where the file was quarantined.

1. Open Command Prompt as an administrator on the device:

   1. Go to **Start** and type _cmd_.
   2. Right-click **Command prompt** and select **Run as administrator**.

2. Type the following command, and press **Enter**:

    ```console
    "%ProgramFiles%\Windows Defender\MpCmdRun.exe" -Restore -Name EUS:Win32/CustomEnterpriseBlock -All
    ```

    > [!IMPORTANT]
    > In some scenarios, the **ThreatName** might appear as `EUS:Win32/CustomEnterpriseBlock!cl`. Defender for Endpoint restores all custom blocked files that were quarantined on this device in the last 30 days.
    > A file that was quarantined as a potential network threat might not be recoverable. If a user attempts to restore the file after quarantine, that file might not be accessible. This can be due to the system no longer having network credentials to access the file. Typically, this is a result of a temporary sign-in a system or shared folder and the access tokens expired.

3. In the pane on the right side of the screen, select **Apply to X more instances of this file**, and then select **Undo**.

## Part 3: Review or define exclusions

> [!CAUTION]
> Before you define an exclusion, review the detailed information in [Manage exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md). Keep in mind that every exclusion that is defined lowers your level of protection. 

An exclusion is an entity, such as a file or URL, that you specify as an exception to remediation actions. The excluded entity can still get detected, but no remediation actions are taken on that entity. That is, the detected file or process isn't stopped, sent to quarantine, removed, or otherwise changed by Microsoft Defender for Endpoint.

To define exclusions across Microsoft Defender for Endpoint, perform the following tasks:

- [Create "allow" indicators for Microsoft Defender for Endpoint](#indicators-for-defender-for-endpoint)
- [Define exclusions for Microsoft Defender Antivirus](#exclusions-for-microsoft-defender-antivirus)
- For Attack Surface Reduction Rule exclusions [Configure attack surface reduction per-rule exclusions](/defender-endpoint/attack-surface-reduction-rules-deployment-test#configure-attack-surface-reduction-per-rule-exclusions) or you can leverage [ASR rule only exclusions](/defender-endpoint/enable-attack-surface-reduction#exclude-files-and-folders-from-attack-surface-reduction-rules)

> [!NOTE]
> Microsoft Defender Antivirus exclusions apply only to antivirus protection, not across other Microsoft Defender for Endpoint capabilities. To exclude files broadly, use [custom indicators](indicators-overview.md) for Microsoft Defender for Endpoint and exclusions for Microsoft Defender Antivirus.
> ASR Rules can leverage ASR Rule Exclusions where exclusions apply to all ASR Rules, ASR per rule exclusions, Microsoft Defender Antivirus exclusions, and allow indicators defined in Custom Indicators.

The procedures in this section describe how to define indicators and exclusions.

### Indicators for Defender for Endpoint

[Indicators](indicators-overview.md) (specifically, indicators of compromise, or IoCs) enable your security operations team to define the detection, prevention, and exclusion of entities. For example, you can specify certain files to be omitted from scans and remediation actions in Microsoft Defender for Endpoint. Or, indicators can be used to generate alerts for certain files, IP addresses, or URLs.

To specify entities as exclusions for Defender for Endpoint, create "allow" indicators for those entities. Such "allow" indicators apply to [next-generation protection](microsoft-defender-antivirus-windows.md) and [automated investigation & remediation](automated-investigations.md).

"Allow" indicators can be created for:

- [Files](#indicators-for-files)
- [IP addresses, URLs, and domains](#indicators-for-ip-addresses-urls-or-domains)
- [Application certificates](#indicators-for-application-certificates)

:::image type="content" source="media/false-positives-indicators.png" alt-text="The Indicator types" lightbox="media/false-positives-indicators.png":::

#### Indicators for files

When you [create an "allow" indicator for a file, such as an executable](indicator-file.md), it helps prevent files that your organization is using from being blocked. Files can include portable executable (PE) files, such as `.exe` and `.dll` files.

Before you create indicators for files, make sure the following requirements are met:

- Microsoft Defender Antivirus is configured with cloud-based protection enabled (see [Manage cloud-based protection](/windows/security/threat-protection/microsoft-defender-antivirus/deploy-manage-report-microsoft-defender-antivirus))
- Antimalware client version is 4.18.1901.x or later
- Client devices must be running Windows 11 or Windows 10, version 1703 or later
- Server devices must be running Windows Server 2025, Windows Server 2022, Windows Server 2019, or Windows Server 2016 / Windows Server 2012 R2 with the [Functionality in the modern unified solution](onboard-server.md#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2)
- The [Block or allow feature is turned on](advanced-features.md)

#### Indicators for IP addresses, URLs, or domains

When you [create an "allow" indicator for an IP address, URL, or domain](indicator-ip-domain.md), it helps prevent the sites or IP addresses your organization uses from being blocked.

Before you create indicators for IP addresses, URLs, or domains, make sure the following requirements are met:

- Network protection in Defender for Endpoint is enabled in block mode (see [Enable network protection](enable-network-protection.md))
- Antimalware client version is 4.18.1906.x or later
- Devices are running Windows 10, version 1709, or later, or Windows 11

Custom network indicators are turned on in the [Microsoft Defender XDR](/defender-xdr/microsoft-365-defender). To learn more, see [Advanced features](advanced-features.md).

#### Indicators for application certificates

When you [create an "allow" indicator for an application certificate](indicator-certificates.md), it helps prevent applications, such as internally developed applications, that your organization uses from being blocked. `.CER` or `.PEM` file extensions are supported.

Before you create indicators for application certificates, make sure the following requirements are met:

- Microsoft Defender Antivirus is configured with cloud-based protection enabled (see [Manage cloud-based protection](deploy-manage-report-microsoft-defender-antivirus.md)
- Antimalware client version is 4.18.1901.x or later
- Devices are running Windows 10, version 1703 or later, or Windows 11; Windows Server 2012 R2 and Windows Server 2016 with the [modern unified solution](onboard-server.md#functionality-in-the-modern-unified-solution-for-windows-server-2016-and-windows-server-2012-r2), or Windows Server 2019, Windows Server 2022, or Windows Server 2025
- Virus and threat protection definitions are up to date

> [!TIP]
> When you create indicators, you can define them one by one, or import multiple items at once. Keep in mind there's a limit of 15,000 indicators for a single tenant. And, you might need to gather certain details first, such as file hash information. Make sure to review the prerequisites before you [create indicators](indicators-overview.md).

### Exclusions for Microsoft Defender Antivirus

In general, you shouldn't need to define exclusions for Microsoft Defender Antivirus. Make sure that you define exclusions sparingly, and that you only include the files, folders, processes, and process-opened files that are resulting in false positives. In addition, make sure to review your defined exclusions regularly. We recommend using [Microsoft Intune](/mem/intune/fundamentals/what-is-intune) to define or edit your antivirus exclusions; however, you can use other methods, such as [Group Policy](/azure/active-directory-domain-services/manage-group-policy) (see [Manage Microsoft Defender for Endpoint](preferences-setup.md)).

> [!TIP]
> Need help with antivirus exclusions? See [Configure and validate exclusions for Microsoft Defender Antivirus](configure-exclusions-microsoft-defender-antivirus.md).

#### Use Intune to manage antivirus exclusions (for existing policies)

1. In the [Microsoft Intune admin center](https://intune.microsoft.com), choose **Endpoint security** \> **Antivirus**, and then select an existing policy. (If you don't have an existing policy, or you want to create a new policy, skip to [Use Intune to create a new antivirus policy with exclusions](#use-intune-to-create-a-new-antivirus-policy-with-exclusions).)

2. Choose **Properties**, and next to **Configuration settings**, choose **Edit**.

3. Expand **Microsoft Defender Antivirus Exclusions** and then specify your exclusions.

   - **Excluded Extensions** are exclusions that you define by file type extension. These extensions apply to any file name that has the defined extension without the file path or folder. Separate each file type in the list must be separated with a `|` character. For example, `lib|obj`. For more information, see [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#excludedextensions).
   - **Excluded Paths** are exclusions that you define by their location (path). These types of exclusions are also known as file and folder exclusions. Separate each path in the list with a `|` character. For example, `C:\Example|C:\Example1`. For more information, see [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#excludedpaths).
   - **Excluded Processes** are exclusions for files that are opened by certain processes. Separate each file type in the list with a `|` character. For example, `C:\Example. exe|C:\Example1.exe`. These exclusions aren't for the actual processes. To exclude processes, you can use file and folder exclusions. For more information, see [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#excludedprocesses).

4. Choose **Review + save**, and then choose **Save**.

#### Use Intune to create a new antivirus policy with exclusions

1. In the [Microsoft Intune admin center](https://intune.microsoft.com), choose **Endpoint security** \> **Antivirus** \> **+ Create Policy**.

2. Select a platform (such as **Windows 10, Windows 11, and Windows Server**).

3. For **Profile**, select **Microsoft Defender Antivirus exclusions**, and then choose **Create**.

4. On the **Create profile** step, specify a name and description for the profile, and then choose **Next**.

5. On the **Configuration settings** tab, specify your antivirus exclusions, and then choose **Next**.

   - **Excluded Extensions** are exclusions that you define by file type extension. These extensions apply to any file name that has the defined extension without the file path or folder. Separate each file type in the list with a `|` character. For example, `lib|obj`. For more information, see [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#excludedextensions).
   - **Excluded Paths** are exclusions that you define by their location (path). These types of exclusions are also known as file and folder exclusions. Separate each path in the list with a `|` character. For example, `C:\Example|C:\Example1`. For more information, see [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#excludedpaths).
   - **Excluded Processes** are exclusions for files that are opened by certain processes. Separate each file type in the list with a `|` character. For example, `C:\Example. exe|C:\Example1.exe`. These exclusions aren't for the actual processes. To exclude processes, you can use file and folder exclusions. For more information, see [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#excludedprocesses).

6. On the **Scope tags** tab, if you're using scope tags in your organization, specify scope tags for the policy you're creating. (See [Scope tags](/mem/intune/fundamentals/scope-tags).)

7. On the **Assignments** tab, specify the users and groups to whom your policy should be applied, and then choose **Next**. (If you need help with assignments, see [Assign user and device profiles in Microsoft Intune](/mem/intune/configuration/device-profile-assign).)

8. On the **Review + create** tab, review the settings, and then choose **Create**.

## Part 4: Submit a file for analysis

You can submit entities, such as files and fileless detections, to Microsoft for analysis. Microsoft security researchers analyze all submissions, and their results help inform Defender for Endpoint threat protection capabilities. When you sign in at the submission site, you can track your submissions.

### Submit a file for analysis

If you have a file that was either wrongly detected as malicious or was missed, follow these steps to submit the file for analysis.

1. Review the guidelines here: [Submit files for analysis](/unified-secops-platform/submission-guide).

2. [Submit files in Defender for Endpoint](admin-submissions-mde.md) or visit the [Microsoft Security Intelligence submission site](https://www.microsoft.com/wdsi/filesubmission/) and submit your files.

### Submit a fileless detection for analysis

If something was detected as malware based on behavior, and you don't have a file, you can submit your `Mpsupport.cab` file for analysis. You can get the *.cab* file by using the Microsoft Malware Protection Command-Line Utility (MPCmdRun.exe) tool on Windows 10 or Windows 11.

1. Go to `C:\ProgramData\Microsoft\Windows Defender\Platform\<version>`, and then run `MpCmdRun.exe` as an administrator.

2. Type `mpcmdrun.exe -GetFiles`, and then press **Enter**.

   A .cab file is generated that contains various diagnostic logs. The location of the file is specified in the output of the command prompt. By default, the location is `C:\ProgramData\Microsoft\Microsoft Defender\Support\MpSupportFiles.cab`.

3. Review the guidelines here: [Submit files for analysis](/unified-secops-platform/submission-guide).

4. Visit the [Microsoft Security Intelligence submission site](https://www.microsoft.com/wdsi/filesubmission), and submit your .cab files.

### What happens after a file is submitted?

Your submission is immediately scanned by our systems to give you the latest determination even before an analyst starts handling your case. It's possible that a file might have already been submitted and processed by an analyst. In those cases, a determination is made quickly.

For submissions that weren't already processed, they're prioritized for analysis as follows:

- Prevalent files with the potential to affect a large number of computers are given a higher priority.
- Authenticated customers, especially enterprise customers with valid [Software Assurance IDs (SAIDs)](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx), are given a higher priority.
- Submissions flagged as high priority by SAID holders are given immediate attention.

To check for updates regarding your submission, sign in at the [Microsoft Security Intelligence submission site](https://www.microsoft.com/wdsi/filesubmission).

> [!TIP]
> To learn more, see [Submit files for analysis](/unified-secops-platform/submission-guide#how-does-microsoft-prioritize-submissions).

## Part 5: Review and adjust your threat protection settings

Defender for Endpoint offers a wide variety of options, including the ability to fine-tune settings for various features and capabilities. If you're getting numerous false positives, make sure to review your organization's threat protection settings. You might need to make some adjustments to:

- [Cloud-delivered protection](#cloud-delivered-protection)
- [Remediation for potentially unwanted applications](#remediation-for-potentially-unwanted-applications)
- [Automated investigation and remediation](#automated-investigation-and-remediation)

### Cloud-delivered protection

Check your cloud-delivered protection level for Microsoft Defender Antivirus. By default, cloud-delivered protection is set to **Not configured**; however, we recommend turning it on. To learn more about configuring your cloud-delivered protection, see [Turn on cloud protection in Microsoft Defender Antivirus](enable-cloud-protection-microsoft-defender-antivirus.md).

You can use [Intune](/mem/intune/fundamentals/what-is-intune) or other methods, such as [Group Policy](/azure/active-directory-domain-services/manage-group-policy), to edit or set your cloud-delivered protection settings.

See [Turn on cloud protection in Microsoft Defender Antivirus](enable-cloud-protection-microsoft-defender-antivirus.md).

### Remediation for potentially unwanted applications

Potentially unwanted applications (PUA) are a category of software that can cause devices to run slowly, display unexpected ads, or install other software that might be unexpected or unwanted. Examples of PUA include advertising software, bundling software, and evasion software that behaves differently with security products. Although PUA isn't considered malware, some kinds of software are PUA based on their behavior and reputation.

To learn more about PUA, see [Detect and block potentially unwanted applications](/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

Depending on the apps your organization is using, you might be getting false positives as a result of your PUA protection settings. If necessary, consider running PUA protection in audit mode for a while, or apply PUA protection to a subset of devices in your organization. PUA protection can be configured for the Microsoft Edge browser and for Microsoft Defender Antivirus.

We recommend using [Intune](/mem/endpoint-manager-overview) to edit or set PUA protection settings; however, you can use other methods, such as [Group Policy](/azure/active-directory-domain-services/manage-group-policy).

See [Configure PUA protection in Microsoft Defender Antivirus](detect-block-potentially-unwanted-apps-microsoft-defender-antivirus.md#configure-pua-protection-in-microsoft-defender-antivirus).

### Automated investigation and remediation

[Automated investigation and remediation](automated-investigations.md) (AIR) capabilities are designed to examine alerts and take immediate action to resolve breaches. As alerts are triggered, and an automated investigation runs, a verdict is generated for each piece of evidence investigated. Verdicts can be *Malicious*, *Suspicious*, or *No threats found*.

Depending on the [level of automation](automation-levels.md) set for your organization and other security settings, remediation actions are taken on artifacts that are considered to be *Malicious* or *Suspicious*. In some cases, remediation actions occur automatically; in other cases, remediation actions are taken manually or only upon approval by your security operations team.

- [Learn more about automation levels](automation-levels.md); and then
- [Configure AIR capabilities in Defender for Endpoint](configure-automated-investigations-remediation.md).

> [!IMPORTANT]
> We recommend using *Full automation* for automated investigation and remediation. Don't turn these capabilities off because of a false positive. Instead, use ["allow" indicators to define exceptions](#indicators-for-defender-for-endpoint), and keep automated investigation and remediation set to take appropriate actions automatically. Following [this guidance](automation-levels.md#levels-of-automation) helps reduce the number of alerts your security operations team must handle.

## Still need help?

If you've worked through all the steps in this article and still need help, contact technical support.

1. In the [Microsoft Defender portal](https://go.microsoft.com/fwlink/p/?linkid=2077139), in the upper right corner, select the question mark (**?**), and then select **Microsoft support**.

2. In the **Support Assistant** window, describe your issue, and then send your message. From there, you can open a service request.

## See also

- [Manage Defender for Endpoint](preferences-setup.md)
- [Manage exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md)
- [Overview of Microsoft Defender portal](/legal/microsoft-365/api-terms-of-use)
- [Microsoft Defender for Endpoint on Mac](microsoft-defender-endpoint-mac.md)
- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux.md)
- [Configure Microsoft Defender for Endpoint on iOS features](ios-configure-features.md) 
- [Configure Defender for Endpoint on Android features](android-configure.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
