---
title: Microsoft Secure score data storage and privacy
description: Learn about how Microsoft Secure score handles privacy and data that it collects.
ms.service: defender-xdr
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- m365-security
- tier2
ms.topic: concept-article
search.appverid: met150
ms.date: 04/28/2025
#customer intent: As an IT admin, I want to learn about how Microsoft Secure score handles privacy and data that it collects so that I can understand how my data is being used.
---

# Microsoft Secure Score data storage and privacy

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

This section covers frequently asked questions regarding privacy and data handling for Secure Score.

## Data storage location

Secure score operates in the Microsoft Azure datacenters in the European Union, the United Kingdom, or in the United States. Customer data collected by the service may be stored in: (a) the geo-location of the tenant as identified during provisioning or, (b) if Secure Score uses another Microsoft online service to process such data, the geolocation as defined by the data storage rules of that other online service.

Customer data in pseudonymized form may also be stored in the central storage and processing systems in the United States.

Once configured, you can't change the location where your data is stored. This provides a convenient way to minimize compliance risk by actively selecting the geographic locations where your data resides.

## How long does Microsoft store my data? What is Microsoft's data retention policy?

### At service onboarding

By default, data is retained for 90 days based on your active licenses.

### At contract termination or expiration

Your data is kept and is available to you while the license is under grace period or suspended mode. At the end of this period, data that is associated to an expired or terminated license is erased from Microsoft's systems to make it unrecoverable, no later than 90 days from the associated contract termination or expiration.

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
