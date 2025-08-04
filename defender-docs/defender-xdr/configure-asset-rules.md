---
title: Create dynamic rules for devices in asset rule management
description: Use asset rule management in Microsoft Defender for Endpoint to configure dynamic tagging for devices.
ms.service: defender-xdr
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- m365-security
- tier2
ms.topic: how-to
search.appverid: met150
ms.date: 02/19/2025
appliesto:
- Microsoft Defender XDR
- Microsoft Defender for Endpoint Plan 1
- Microsoft Defender for Endpoint Plan 2
- Microsoft Defender for Business
#customer intent: As a security administrator, I want to create dynamic rules for devices in asset rule management so that I can automatically assign tags and device values based on certain criteria.
---

# Create dynamic rules for devices in asset rule management

> [!IMPORTANT]
> Some information in this article relates to prereleased products/services that might be substantially modified before they are commercially released. Microsoft makes no warranties, express or implied, for the information provided here.

Dynamic rules for devices can help manage device context by assigning tags and device values automatically based on certain criteria, saving time and ensuring accuracy of the device inventory. Dynamic rules also ensure devices remain relevant by removing tags or updating values when criteria are no longer met.

Maintaining an accurate inventory of devices in a constantly changing corporate environment is a critical task for security and IT teams. Failing to effectively manage device context, such as device value and tags, which many organizations use in their security workflows can lead to security vulnerabilities.

Devices might also require updates, replacements, or reconfigurations due to changing business needs. This can create a significant challenge for security and IT teams who are responsible for the ongoing management of the device inventory, and ensuring devices are effectively tracked and managed over time.

You can create dynamic rules in the **Asset rule management** in the Microsoft Defender portal to help you create steps in managing devices, like tagging devices with a specific OS version or assigning a value to devices with a particular naming convention.

## Create a new dynamic rule

A rule can be based on device name, domain, OS platform, internet facing status, onboarding status and manual device tags. You can select or create a tag that will be applied based on the conditions you've set.

> [!IMPORTANT]
> Use of [dynamic device tagging](/defender-xdr/configure-asset-rules) capabilities in Defender for Endpoint to tag devices with `MDE-Management` isn't currently supported with security settings management. Devices tagged through this capability don't successfully enroll. This is currently under investigation.

The following steps guide you on how to create a new dynamic rule in Microsoft Defender XDR:

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) as a user who can view and perform actions on all devices.

2. In the navigation pane, select **Settings** \> **Microsoft Defender XDR** \> **Asset Rule Management**.

3. Select **Create a new rule**.

4. Enter a **Rule name** and **Description***.

5. Select **Next** to choose the conditions you want to assign:

   :::image type="content" source="/defender/media/defender/rule-conditions.png" alt-text="Screenshot of the Rule conditions page" lightbox="/defender/media/defender/rule-conditions.png":::

6. Select **Next** and choose the tag to apply to this rule.

   :::image type="content" source="/defender/media/defender/actions-to-apply.png" alt-text="Screenshot of the actions page" lightbox="/defender/media/defender/actions-to-apply.png":::

7. Select **Next** to review and finish creating the rule and then select **Submit**.

   >[!NOTE]
   > It may take up to 1 hour for changes to be reflected in the portal.

### Dynamic tags in the Device Inventory

You can see the dynamic tags assigned in the Device Inventory view.

> [!NOTE]
> Dynamic tags are not supported by [security baseline assessments](/defender-vulnerability-management/tvm-security-baselines).

To see tags on individual devices:

1. Select **Devices** from the **Assets** navigation menu in the [Microsoft Defender portal](https://security.microsoft.com).

2. In the **Device Inventory** page, select the device name that you want to view.

3. Select **Manage tags**.

   :::image type="content" source="/defender/media/defender/manage-machine-tags.png" alt-text="Screenshot of the machine tags page" lightbox="/defender/media/defender/manage-machine-tags.png":::

### Updating rules

Dynamic tags and device values set by dynamic rules can't be manually updated. To edit, delete or turn off a rule, in the **Asset Rule Management** page select the rule and choose an action.

:::image type="content" source="/defender/media/defender/update-rule.png" alt-text="Screenshot of the rule details page" lightbox="/defender/media/defender/update-rule.png":::
