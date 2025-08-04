---
title: Understand the client analyzer HTML report
description: Learn how to analyze the Microsoft Defender for Endpoint Client Analyzer HTML report
ms.service: defender-endpoint
f1.keywords:
- NOCSH
ms.author: ewalsh
author: emmwalshh
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.topic: concept-article
ms.subservice: onboard
search.appverid: met150
ms.date: 03/27/2025
---

# Understand the client analyzer HTML report

**Applies to:**
- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)

The client analyzer produces a report in HTML format. Learn how to review the report to identify potential sensor issues so that you can troubleshoot them.

Use the following example to understand the report.

## Example output

In this example, the [Defender for Endpoint Client Analyzer](/defender-endpoint/overview-client-analyzer) produced information about a device that was onboarded to an expired Org ID and failed to reach a required Defender for Endpoint URL:

:::image type="content" source="media/147cbcf0f7b6f0ff65d200bf3e4674cb.png" alt-text="The MDE Client Analyzer Results page" lightbox="media/147cbcf0f7b6f0ff65d200bf3e4674cb.png":::

- On top, the script version and script runtime are listed for reference

- The **Device Information** section provides basic OS and device identifiers to uniquely identify the device on which the analyzer has run.

- The **Endpoint Security Details** provides general information about Microsoft Defender for Endpoint-related processes including Microsoft Defender Antivirus and the sensor process. If important processes aren't online as expected, the color changes to red.

    :::image type="content" source="media/85f56004dc6bd1679c3d2c063e36cb80.png" alt-text="The Check Results Summary page" lightbox="media/85f56004dc6bd1679c3d2c063e36cb80.png":::

- On **Check Results Summary**, you'll have an aggregated count for error,
    warning, or informational events detected by the analyzer.

- On **Detailed Results**, you'll see a list (sorted by severity) with
    the results and the guidance based on the observations made by the analyzer.

## Open a support ticket to Microsoft and include the Analyzer results

To include analyzer result files [when opening a support ticket](contact-support.md#open-a-service-request), make sure you use the **Attachments** section and include the `MDEClientAnalyzerResult.zip` file:

:::image type="content" source="media/508c189656c3deb3b239daf811e33741.png" alt-text="An attachment prompt" lightbox="media/508c189656c3deb3b239daf811e33741.png":::

> [!NOTE]
> If the file size is larger than 25 MB, the support engineer assigned to your case will provide a dedicated secure workspace to upload large files for analysis.

## See also

- [Troubleshoot sensor health using Microsoft Defender for Endpoint Client Analyzer](overview-client-analyzer.md)


[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
