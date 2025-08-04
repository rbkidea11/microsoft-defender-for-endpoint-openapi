---
title: Detection exclusions in Microsoft Defender XDR
description: Learn how to configure Microsoft Defender for Identity detection exclusions in Microsoft Defender XDR.
ms.date: 03/23/2023
ms.topic: how-to
ms.reviewer: LiorShapiraa
---

# Configure Defender for Identity detection exclusions in Microsoft Defender XDR

This article explains how to configure [Microsoft Defender for Identity](/defender-for-identity) detection exclusions in [Microsoft Defender XDR](/microsoft-365/security/defender/overview-security-center).

Microsoft Defender for Identity enables the exclusion of specific IP addresses, computers, domains, or users from a number of detections.

For example, a **DNS Reconnaissance** alert could be triggered by a security scanner that uses DNS as a scanning mechanism. Creating an exclusion helps Defender for Identity ignore such scanners and reduce false positives.

> [!NOTE]
> We recommend you to [Tune an alert](/microsoft-365/security/defender/investigate-alerts#tune-an-alert) instead of using exclusions. Alert tuning rules allow more granular conditions than exclusions, and allow you to review the alerts which were tuned.

>[!NOTE]
>Of the most common domains with [Suspicious communication over DNS](other-alerts.md#suspicious-communication-over-dns-external-id-2031) alerts opened on them, we observed the domains that customers most excluded from the alert. These domains are added to the exclusions list by default, but you have the option to easily remove them.

## How to add detection exclusions

1. In [Microsoft Defender XDR](https://security.microsoft.com/), go to **Settings** and then **Identities**.

    ![Go to Settings, then Identities.](media/settings-identities.png)
   
1. You'll then see **Excluded entities** in the left-hand menu.

    ![Excluded entities.](media/excluded-entities.png)
   
   You can then set exclusions by two methods: **Exclusions by detection rule** and **Global excluded entities**.

## Exclusions by detection rule

1. In the left-hand menu, select **Exclusions by detection rule**. You'll see a list of detection rules.

    ![Exclusions by detection rule.](media/exclusions-by-detection-rule.png)
   
1. For each detection you want to configure, do the following steps:

   1. Select the rule. You can search for detections using the search bar. Once selected, a pane will open with the detection rule details.
   
       ![Detection rule details.](media/detection-rule-details.png)
      
    1. To add an exclusion, select the **Excluded entities** button, and then choose the exclusion type. Different excluded entities are available for each rule. They include users, devices, domains and IP addresses. In this example, the choices are **Exclude devices** and **Exclude IP addresses**.

        ![Exclude devices or IP addresses.](media/exclude-devices-or-ip-addresses.png)

    1. After choosing the exclusion type, you can add the exclusion. In the pane that opens, select the **+** button to add the exclusion.

        ![Add an exclusion.](media/add-exclusion.png)

    1. Then add the entity to be excluded. Select **+ Add** to add the entity to the list.

        ![Add an entity to be excluded.](media/add-excluded-entity.png)

    1. Then select **Exclude IP addresses** (in this example) to complete the exclusion.

        ![Exclude IP addresses.](media/exclude-ip-addresses.png)

    1. Once you've added exclusions, you can export the list or remove the exclusions by returning to the **Excluded entities** button. In this example, we've returned to **Exclude devices**. To export the list, select the down arrow button.

        ![Return to Exclude devices.](media/return-to-exclude-devices.png)

    1. To delete an exclusion, select the exclusion and select the trash icon.

        ![Delete an exclusion.](media/delete-exclusion.png)

## Global excluded entities

You can now also configure exclusions by **Global excluded entities**. Global exclusions allow you to define certain entities (IP addresses, subnets, devices, or domains) to be excluded across all of the detections Defender for Identity has. So for example, if you exclude a device, it will only apply to those detections that have device identification as part of the detection.

1. In the left-hand menu, select **Global excluded entities**. You'll see the categories of entities that you can exclude.

    ![Global excluded entities.](media/global-excluded-entities.png)
   
1. Choose an exclusion type. In this example, we selected **Exclude domains**.

    ![Exclude domains.](media/exclude-domains.png)
   
1. A pane will open where you can add a domain to be excluded. Add the domain you want to exclude.

    ![Add a domain to be excluded.](media/add-excluded-domain.png)
   
1. The domain will be added to the list. Select **Exclude domains** to complete the exclusion.

    ![Select exclude domains.](media/select-exclude-domains.png)
   
1. You'll then see the domain in the list of entities to be excluded from all detection rules. You can export the list, or remove the entities by choosing them and selecting the **Remove** button.

    ![List of global excluded entries.](media/global-excluded-entries-list.png)
   
## Next steps

- [Configure event collection](deploy/configure-event-collection.md)
- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)
