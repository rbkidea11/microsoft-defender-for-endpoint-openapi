---
title: Spam confidence level
f1.keywords: 
  - NOCSH
ms.author: chrisda
author: chrisda
manager: deniseb
audience: ITPro
ms.topic: article
ms.localizationpriority: medium
search.appverid: 
  - MET150
ms.assetid: 34681000-0022-4b92-b38a-e32b3ed96bf6
ms.collection: 
  - m365-security
  - tier2
ms.custom: 
  - seo-marvel-apr2020
description: Admins can learn about the spam confidence level (SCL) that applied to messages in Microsoft 365 by anti-spam filtering.
ms.service: defender-office-365
ms.date: 07/03/2025
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# Spam confidence level (SCL) in cloud organizations

In all organizations with cloud mailboxes, inbound messages go through spam filtering and get a spam score. That score is mapped to an individual spam confidence level (SCL) value added to the message in an X-header. A higher SCL value indicates a message is more likely to be spam. Microsoft 365 takes action on the message based on the SCL value.

The following table describes what the SCL values mean and the default action taken on those messages:

|SCL value|Definition|Default action|
|:---:|---|---|
|-1|The message skipped spam filtering. For example, the message is from a safe sender, was sent to a safe recipient, or is from an email source server on the IP Allow List. For more information, see [Create sender allowlists](create-safe-sender-lists-in-office-365.md).|Deliver the message to recipient Inbox folders.|
|0, 1|Spam filtering determined the message wasn't spam.|Deliver the message to recipient Inbox folders.|
|5, 6|Spam filtering marked the message as **Spam**|**Default anti-spam policy, new anti-spam policies, and [Standard preset security policy](preset-security-policies.md)**: Deliver the message to recipient Junk Email folders. <br/><br/> **Strict preset security policy**: [Quarantine the message](quarantine-end-user.md).|
|7, 8, 9|Spam filtering marked the message as **High confidence spam**|**Default anti-spam policy and new anti-spam policies**: Deliver the message to recipient Junk Email folders. <br/><br/> **Standard and Strict preset security policies**: [Quarantine the message](quarantine-end-user.md).|

> [!TIP]
> Spam filtering never stamps messages with the SCL values 2, 3, or 4.
>
> Typically, spam filtering itself doesn't stamp messages with the SCL value 7, but other features might. For example:
>
> - Human message grading by an analyst.
> - DMARC failures.
> - [Mail flow rules (also known as transport rules)](/exchange/security-and-compliance/mail-flow-rules/use-rules-to-set-scl).

For more information about actions you can take on messages based on the spam filtering verdict, see [Configure anti-spam policies](anti-spam-policies-configure.md).

Similar to the SCL, the bulk complaint level (BCL) identifies bad bulk email (also known as _gray mail_). A higher BCL value indicates the message is more likely to exhibit undesirable spam-like behavior. You configure the BCL threshold in anti-spam policies. For more information, see [Configure anti-spam policies](anti-spam-policies-configure.md), [Bulk complaint level (BCL)](anti-spam-bulk-complaint-level-bcl-about.md), and [What's the difference between junk email and bulk email?](anti-spam-spam-vs-bulk-about.md).

****

:::image type="content" source="media/eac8a413-9498-4220-8544-1e37d1aaea13.png" alt-text="The short icon for LinkedIn Learning."::: **New to Microsoft 365?** Discover free video courses for **Microsoft 365 admins and IT pros**, brought to you by LinkedIn Learning.
