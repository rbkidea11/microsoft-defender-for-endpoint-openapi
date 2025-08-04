---
title: Manage the deception capability in Microsoft Defender XDR
description: Detect human-operated attacks with lateral movement in the early stages using high confidence signals from the deception feature in Microsoft Defender XDR.
ms.service: defender-xdr
f1.keywords: 
- NOCSH
ms.author: diannegali
author: diannegali
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier1
ms.topic: concept-article
search.appverid: 
- MOE150
- MET150
ms.date: 04/25/2025
appliesto:
- Microsoft Defender XDR
- Microsoft Defender for Endpoint
#customer intent: As a security analyst, I want to understand how to manage the deception capability in Microsoft Defender XDR to detect human-operated attacks with lateral movement.
---

# Manage the deception capability in Microsoft Defender XDR

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

> [!IMPORTANT]
> Some information in this article relates to prereleased products/services that might be substantially modified before commercially release. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Defender XDR, through built-in deception capability, delivers high confidence detections of human-operated lateral movement, preventing attacks from reaching an organization's critical assets. Various attacks like [business email compromise (BEC)](https://www.microsoft.com/security/business/security-101/what-is-business-email-compromise-bec), [ransomware](/security/ransomware/), organizational breaches, and nation-state attacks often use lateral movement and can be hard to detect with high confidence in the early stages. Defender XDR's deception technology provides high confidence detections based on deception signals correlated with Microsoft Defender for Endpoint signals.

The deception capability automatically generates authentic-looking decoy accounts, hosts, and lures. The fake assets generated are then automatically deployed to specific clients. When an attacker interacts with the decoys or lures, the deception capability raises high confidence alerts, helping in security team's investigations and allowing them to observe an attacker's methods and strategies. All alerts raised by the deception capability are automatically correlated into incidents and are fully integrated into Microsoft Defender XDR. In addition, the deception technology is integrated into Defender for Endpoint, minimizing deployment needs.

For an overview of the deception capability, watch the following video.

<iframe width="560" height="415" src="https://www.youtube.com/embed/xoEP7SFEnJc?si=OjweAYJo9cP1X-Yo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Prerequisites

The following table lists the requirements to enable the deception capability in Microsoft Defender XDR.

> [!div class="mmx-tdCol2BreakAll"]
> |Requirement|Details|
> |-------------|----------|
> |Subscription requirements|One of these subscriptions:</br> - Microsoft 365 E5</br> - Microsoft Security E5</br> - Microsoft Defender for Endpoint Plan 2|
> |Deployment requirements|Requirements:</br> - Defender for Endpoint is the primary EDR solution</br> - [Automated investigation and response capabilities in Defender for Endpoint](/defender-endpoint/configure-automated-investigations-remediation) is configured</br> - Devices are [joined](/entra/identity/devices/concept-directory-join/) or [hybrid joined](/entra/identity/devices/concept-hybrid-join/) in Microsoft Entra</br> - PowerShell is enabled on the devices (in non-restricted/non-constrained mode)</br> - The deception feature covers clients operating on Windows 10 RS5 and later in preview|
> |Permissions|You must have one of the following roles assigned in the [Microsoft Entra admin center](https://entra.microsoft.com) or in the [Microsoft 365 admin center](https://admin.microsoft.com) to configure deception capabilities:</br> - Global administrator</br> - Security administrator</br> - Manage portal system settings|

> [!NOTE]
> Microsoft recommends using roles with fewer permissions for better security. The Global Administrator role, which has many permissions, should only be used in emergencies when no other role fits.

## What is deception technology?

Deception technology is a security measure that provides immediate alerts of a potential attack to security teams, allowing them to respond in real-time. Deception technology creates fake assets like devices, users, and hosts that appear to belong to your network.

Attackers interacting with the fake network assets set up by the deception capability can help security teams prevent potential attacks from compromising an organization and monitor the attackers' actions so defenders can improve their environment's security further.

### How does the Microsoft Defender XDR deception capability work?

The built-in deception capability in the Microsoft Defender portal uses rules to make decoys and lures that match your environment. The feature applies machine learning to suggest decoys and lures that are tailored to your network. You can also use the deception feature to manually create the decoys and lures. These decoys and lures are then automatically deployed to your network and planted to devices you specify using PowerShell.

Deception technology, through high confidence detections of human-operated lateral movement, alerts security teams when an attacker interacts with fake hosts or lures. Here's the process of how the deception capability works:

:::image type="content" source="/defender/media/deception/fig1-deception.png" alt-text="Screenshot of an attack with lateral movement and where deception intercepts the attack" lightbox="/defender/media/deception/fig1-deception.png":::

**Decoys** are fake devices and accounts that appear to belong to your network. **Lures** are fake content planted on specific devices or accounts and are used to attract an attacker. The content can be a document, a configuration file, cached credentials, or any content that an attacker can likely read, steal, or interact with. Lures imitate important company information, settings, or credentials.

There are two types of lures available in the deception feature:

- Basic lures – planted documents, link files, and the like that have no or minimal interaction with the customer environment.  
- Advanced lures – planted content like cached credentials and interceptions that respond or interact with the customer environment. For example, attackers might interact with decoy credentials that were injected responses to Active Directory queries, which can be used to sign in.

> [!NOTE]
> Lures are only planted on Windows clients defined in the scope of a deception rule. However, attempts to use any decoy host or account on any Defender for Endpoint-onboarded client raises a deception alert. Learn how to onboard clients in [Onboard to Microsoft Defender for Endpoint](/defender-endpoint/onboarding). Planting lures on Windows Server 2016 and later is planned for future development.

You can specify decoys, lures, and the scope in a deception rule. See [Configure the deception feature](configure-deception.md) to learn more about how to create and modify deception rules.  

When an attacker uses a decoy on any Defender for Endpoint-onboarded client, the deception capability triggers an alert that indicates possible attacker activity, regardless of whether deception was deployed on the client or not.

## Identify incidents and alerts activated by deception

Alerts based on deception detection contain *deceptive* in the title. Some examples of alert titles are:

- Sign-in attempt with a deceptive user account
- Connection attempt to a deceptive host

The alert details contain:

- The *Deception* tag
- The decoy device or user account where the alert originated
- The type of attack like sign in attempts or lateral movement attempts

Here's an example of a deception-related alert:

:::image type="content" source="/defender/media/deception/deception-alert-small.png" alt-text="Screenshot of a deception alert highlighting the tag and the attempt" lightbox="/defender/media/deception/deception-alert.png":::

## Next step

- [Configure the deception capability in Microsoft Defender XDR](configure-deception.md)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
