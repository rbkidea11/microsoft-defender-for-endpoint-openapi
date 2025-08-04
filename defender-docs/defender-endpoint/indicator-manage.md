---
title: Manage indicators
ms.reviewer:
description: Manage indicators for a file hash, IP address, URLs, or domains that define the detection, prevention, and exclusion of entities.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier2
- mde-asr
ms.topic: how-to
ms.subservice: asr
search.appverid: met150
ms.date: 10/28/2024
---

# Manage indicators

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

1. In the navigation pane, select **Settings** \> **Endpoints** \> **Indicators** (under **Rules**).

2. Select the tab of the entity type you'd like to manage.

3. Update the details of the indicator and select **Save** or select the **Delete** button if you'd like to remove the entity from the list.

## Import a list of IoCs

You can also choose to upload a CSV file that defines the attributes of indicators, the action to be taken, and other details.

Download the sample CSV to know the supported column attributes.

1. In the navigation pane, select **Settings** \> **Endpoints** \> **Indicators** (under **Rules**).

2. Select the tab of the entity type you'd like to import indicators for.

3. Select **Import** \> **Choose file**.

4. Select **Import**. Repeat for all the files you'd like to import.

5. Select **Done**.

> [!NOTE]
> Only 500 indicators can be uploaded for each batch. 
> Attempting to import indicators with specific categories requires the string to be written in Pascal case convention and only accepts the category list available at the portal.

The following table shows the supported parameters.

| Parameter|Type|Description |
| ---| ---| --- |
| indicatorType|Enum|Type of the indicator. Possible values are: `FileSha1`, `FileSha256`, `IpAddress`, `DomainName`, and `Url`. <br/> **Required** |
| indicatorValue|String|Identity of the [Indicator](api/ti-indicator.md) entity. <br/> **Required** |
| action|Enum|The action that is taken if the indicator is discovered in the organization. Possible values are: `Allowed`, `Audit`, `BlockAndRemediate`, `Warn`, and `Block`. <br/> **Required** |
| title|String|Indicator alert title.<br/> **Required** |
| description|String| Description of the indicator.<br/> **Required** |
| expirationTime|DateTimeOffset|The expiration time of the indicator in the following format `YYYY-MM-DDTHH:MM:SS.0Z`. The indicator gets deleted if the expiration time passes and whatever happens at the expiration time occurs at the seconds (SS) value. <br/>**Optional** |
| severity|Enum|The severity of the indicator. Possible values are: `Informational`, `Low`, `Medium`, and `High`. <br/>**Optional** |
| recommendedActions|String|TI indicator alert recommended actions. <br/>**Optional** |
| rbacGroups|String|Comma-separated list of RBAC groups the indicator would be applied to. <br/>**Optional** |
| category|String|Category of the alert. Examples include: Execution and credential access. <br/>**Optional** |
| mitretechniques|String|MITRE techniques code/id (comma separated). For more information, see [Enterprise tactics](https://attack.mitre.org/tactics/enterprise/). <br/> **Optional** <br/>It's recommended to add a value in category when a MITRE technique. |
| GenerateAlert|String|Whether the alert should be generated. Possible Values are: `True` or `False`. <br/>**Optional** |

> [!NOTE]
> Classless Inter-Domain Routing (CIDR) notation for IP addresses is not supported. For more information, see [Microsoft Defender for Endpoint alert categories are now aligned with MITRE ATT&CK!](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/microsoft-defender-atp-alert-categories-are-now-aligned-with/ba-p/732748).
>
> Network indicators do not support the action type, `BlockAndRemediate`. If a network indicator is set to `BlockAndRemediate`, it won't import. 

Watch this video to learn how Microsoft Defender for Endpoint provides multiple ways to add and manage Indicators of compromise (IoCs). 
> [!VIDEO https://learn-video.azurefd.net/vod/player?id=a4469df9-4f31-4ed0-9577-8b26ac5293ad]

## See also

- [Create indicators](indicators-overview.md)
- [Create indicators for files](indicator-file.md)
- [Create indicators for IPs and URLs/domains](indicator-ip-domain.md)
- [Create indicators based on certificates](indicator-certificates.md)
- [Exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
