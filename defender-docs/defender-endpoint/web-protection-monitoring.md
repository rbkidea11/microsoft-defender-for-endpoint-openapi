---
title: Monitoring web browsing security in Microsoft Defender for Endpoint
description: Use web protection in Microsoft Defender for Endpoint to monitor web browsing security
search.appverid: met150
ms.service: defender-endpoint
ms.author: ewalsh
author: emmwalsh
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
ms.date: 09/21/2024
---

# Monitor web browsing security

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

Web protection lets you monitor your organization's web browsing security through reports under **Reports > Web protection** in the Microsoft Defender portal. The report contains cards that provide web threat detection statistics.

- **Web threat protection detections over time** - this trending card displays the number of web threats detected by type during the selected time period (Last 30 days, Last 3 months, Last 6 months)

  :::image type="content" source="media/wtp-blocks-over-time.png" alt-text="The card showing web threats protection detections over time" lightbox="media/wtp-blocks-over-time.png":::

- **Web threat protection summary** - this card displays the total web threat detections in the past 30 days, showing distribution across the different types of web threats. Selecting a slice opens the list of the domains that were found with malicious or unwanted websites.

  :::image type="content" source="media/wtp-summary.png" alt-text="The card showing web threats protection summary"  lightbox="media/wtp-summary.png":::

> [!NOTE]
> It can take up to 12 hours before a block is reflected in the cards or the domain list.

## Types of web threats

Web protection categorizes malicious and unwanted websites as:

- **Phishing** - websites that contain spoofed web forms and other phishing mechanisms designed to trick users into divulging credentials and other sensitive information
- **Malicious** - websites that host malware and exploit code
- **Custom indicator** - websites whose URLs or domains you've added to your [custom indicator list](indicators-overview.md) for blocking

## View the domain list

Select a specific web threat category in the **Web threat protection summary** card to open the **Domains** page. This page displays the list of the domains under that threat category. The page provides the following information for each domain:

- **Access count** - number of requests for URLs in the domain
- **Blocks** - number of times requests were blocked
- **Access trend** - change in number of access attempts
- **Threat category** - type of web threat
- **Devices** - number of devices with access attempts

Select a domain to view the list of devices that have attempted to access URLs in that domain and the list of URLs.

## Related topics

- [Web protection overview](web-protection-overview.md)
- [Web content filtering](web-content-filtering.md)
- [Web threat protection](web-threat-protection.md)
- [Respond to web threats](web-protection-response.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
