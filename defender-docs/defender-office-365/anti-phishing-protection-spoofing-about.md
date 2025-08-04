---
title: Anti-spoofing protection
f1.keywords: 
  - NOCSH
ms.author: chrisda
author: chrisda
manager: deniseb
audience: ITPro
ms.topic: overview
search.appverid: 
  - MET150
ms.assetid: d24bb387-c65d-486e-93e7-06a4f1a436c0
ms.collection: 
  - m365-security
  - Strat_O365_IP
  - m365initiative-defender-office365
  - EngageScoreSep2022
  - ContentEngagementFY23
  - tier2
ms.custom: 
  - TopSMBIssues
  - seo-marvel-apr2020
ms.localizationpriority: high
description: Admins can learn how the default anti-spoofing protection features in all organizations with cloud mailboxes can help mitigate against phishing attacks from spoofed senders and domains.
ms.service: defender-office-365
ms.date: 07/02/2025
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# Anti-spoofing protection for cloud mailboxes

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

All organizations with cloud mailboxes include features to help protect against spoofed (forged) senders Spoofing is a common technique used by attackers. **Spoofed messages appear to originate from someone or somewhere other than the actual source**. This technique is often used in phishing campaigns designed to get user credentials.

Anti-spoofing technology in Microsoft 365 specifically examines forgery of the From header in the message body (also known as the `5322.From` address, From address or P2 sender), because email clients show the From header value as the message sender. When Microsoft 365 has high confidence the From header is forged, the message is identified as spoofed.

The following anti-spoofing technologies are available in the default email protections for cloud mailboxes:

- **Email authentication**: An integral part of any anti-spoofing effort is the use of email authentication (also known as email validation) by SPF, DKIM, and DMARC records in DNS. You can configure these records for your domains so destination email systems can check the validity of messages that claim to be from senders in your domains. For inbound messages, Microsoft 365 requires email authentication of sender domains. For more information, see [Email authentication](email-authentication-about.md).

  Microsoft 365 analyzes and blocks messages based on the combination of standard email authentication methods and sender reputation techniques.

  :::image type="content" source="media/eop-anti-spoofing-protection.png" alt-text="Diagram showing Microsoft 365 anti-spoofing checks." lightbox="media/eop-anti-spoofing-protection.png":::

- **Spoof intelligence insight**: Review detected spoofed messages from senders in internal and external domains during the last seven days. For more information, see [Spoof intelligence insight](anti-spoofing-spoof-intelligence.md).

- **Allow or block spoofed senders in the Tenant Allow/Block List**: When you override the verdict in the spoof intelligence insight, the spoofed sender becomes a manual allow or block entry that only appears on the **Spoofed senders** tab on the **Tenant Allow/Block Lists** page at <https://security.microsoft.com/tenantAllowBlockList?viewid=SpoofItem>. You can also manually create allow or block entries for spoof senders before spoof intelligence detects them. For more information, see [Spoofed senders in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure.md#spoofed-senders-in-the-tenant-allowblock-list).

- **Anti-phishing policies**: In the default email protections for cloud mailboxes and in Microsoft Defender for Office 365, anti-phishing policies contain the following anti-spoofing settings:
  - Turn spoof intelligence on or off.
  - Turn unauthenticated sender indicators in Outlook on or off.
  - Specify the action for blocked spoofed senders.

  For more information, see [Spoof settings in anti-phishing policies](anti-phishing-policies-about.md#spoof-settings).

  Anti-phishing policies in Defender for Office 365 contain addition protections, including _impersonation_ protection. For more information, see [Exclusive settings in anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-about.md#exclusive-settings-in-anti-phishing-policies-in-microsoft-defender-for-office-365).

- **Spoof detections report**: For more information, see [Spoof Detections report](reports-email-security.md#spoof-detections-report).

  Microsoft 365 organizations with Defender for Office 365 (included or in add-on subscriptions) have Real-time detections (Plan 1) or Threat Explorer (Plan 2) to view information about phishing attempts. For more information, see [Microsoft 365 threat investigation and response](office-365-ti.md).

> [!TIP]
> It's important to understand that a [composite authentication](email-authentication-about.md#composite-authentication) failure doesn't directly result in blocking a message. Microsoft 365 using a holistic evaluation strategy that considers the overall suspicious nature of a message along with composite authentication results. This method is designed to mitigate the risk of incorrectly blocking legitimate email from domains that might not strictly adhere to email authentication protocols. This balanced approach helps distinguish genuinely malicious email from message senders that simply fail to conform to standard email authentication practices.

## How spoofing is used in phishing attacks

Spoofed senders in messages have the following negative implications for users:

- **Deception**: Messages from spoofed senders might trick the recipient into giving up their credentials, downloading malware, or replying to a message with sensitive content (known as business email compromise or BEC).

  The following message is an example of phishing that uses the spoofed sender `msoutlook94@service.outlook.com`:

  :::image type="content" source="media/1a441f21-8ef7-41c7-90c0-847272dc5350.jpg" alt-text="Phishing message impersonating service.outlook.com." lightbox="media/1a441f21-8ef7-41c7-90c0-847272dc5350.jpg":::

  This message didn't come from service.outlook.com, but the attacker spoofed the **From** header field to make it look like it did. The sender attempted to trick the recipient into selecting the **change your password** link and providing their credentials.

  The following message is an example of BEC that uses the spoofed email domain contoso.com:

  :::image type="content" source="media/da15adaa-708b-4e73-8165-482fc9182090.jpg" alt-text="Phishing message - business email compromise." lightbox="media/da15adaa-708b-4e73-8165-482fc9182090.jpg":::

  The message looks legitimate, but the sender is spoofed.

- **Confusion**: Even users who know about phishing might have difficulty seeing the differences between real messages and messages from spoofed senders.

  The following message is an example of a real password reset message from the Microsoft Security account:

  :::image type="content" source="media/58a3154f-e83d-4f86-bcfe-ae9e8c87bd37.jpg" alt-text="Microsoft legitimate password reset." lightbox="media/58a3154f-e83d-4f86-bcfe-ae9e8c87bd37.jpg":::

  The message really did come from Microsoft, but users are conditioned to be suspicious. Because it's difficult to the difference between a real password reset message and a fake one, users might ignore the message, report it as spam, or unnecessarily report the message to Microsoft as phishing.

## Different types of spoofing

Microsoft differentiates between two different types of spoofed senders in messages:

- **Intra-org spoofing**: Also known as _self-to-self_ spoofing. For example:

  - The sender and recipient are in the same domain:

    ```text
    From: chris@contoso.com
    To: michelle@contoso.com
    ```

  - The sender and the recipient are in subdomains of the same domain:

    ```text
    From: laura@marketing.fabrikam.com
    To: julia@engineering.fabrikam.com
    ```

  - The sender and recipient are in different domains that belong to the same organization (that is, both domains are configured as [accepted domains](/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains) in the same organization):

    ```text
    From: cindy@tailspintoys.com
    To: steve@wingtiptoys.com
    ```

  Messages that fail [composite authentication](email-authentication-about.md#composite-authentication) due to intra-org spoofing contain the following header values:

  `Authentication-Results: ... compauth=fail reason=6xx`

  `X-Forefront-Antispam-Report: ...CAT:SPOOF;...SFTY:9.11`

  - `reason=6xx` indicates intra-org spoofing.
  - `SFTY` is the safety level of the message.
    - `9` indicates phishing.
    - `.11` indicates intra-org spoofing.

- **Cross-domain spoofing**: The sender and recipient domains are different, and have no relationship to each other (also known as external domains). For example:

  ```text
  From: chris@contoso.com
  To: michelle@tailspintoys.com
  ```

  Messages that fail [composite authentication](email-authentication-about.md#composite-authentication) due to cross-domain spoofing contain the following headers values:

  `Authentication-Results: ... compauth=fail reason=000/001`

  `X-Forefront-Antispam-Report: ...CAT:SPOOF;...SFTY:9.22`

  - `reason=000` indicates the message failed explicit email authentication. `reason=001` indicates the message failed implicit email authentication.

  - `SFTY` is the safety level of the message.
    - `9` indicates phishing.
    - `.22` indicates cross-domain spoofing.

  For more information about **Authentication-Results** and `compauth` values, see [Authentication-results message header fields](message-headers-eop-mdo.md#authentication-results-message-header-fields).

## Problems with anti-spoofing protection

Mailing lists (also known as discussion lists) are known to have problems with anti-spoofing protection because of how they forward and modify messages.

For example, Gabriela Laureano (`glaureano@contoso.com`) is interested in bird watching, so she joins the mailing list `birdwatchers@fabrikam.com`, and sends the following message to the list:

```text
From: "Gabriela Laureano" <glaureano@contoso.com> 
To: Birdwatcher's Discussion List <birdwatchers@fabrikam.com>
Subject: Great viewing of blue jays at the top of Mt. Rainier this week

Anyone want to check out the viewing this week from Mt. Rainier?
```

The mailing list server receives the message, modifies its content, and replays it to the members of list. The replayed message has the same From address (`glaureano@contoso.com`), but a tag is added to the subject line, and a footer is added to the bottom of the message. This type of modification is common in mailing lists, and might result in false positives for spoofing.

```text
From: "Gabriela Laureano" <glaureano@contoso.com>
To: Birdwatcher's Discussion List <birdwatchers@fabrikam.com>
Subject: [BIRDWATCHERS] Great viewing of blue jays at the top of Mt. Rainier this week

Anyone want to check out the viewing this week from Mt. Rainier?

This message was sent to the Birdwatchers Discussion List. You can unsubscribe at any time.
```

To help mailing list messages pass anti-spoofing checks, do the following steps based on your circumstance:

- **Your organization owns the mailing list**:
  - Check the FAQ at DMARC.org: [I operate a mailing list and I want to interoperate with DMARC, what should I do?](https://dmarc.org/wiki/FAQ#I_operate_a_mailing_list_and_I_want_to_interoperate_with_DMARC.2C_what_should_I_do.3F).
  - Read the instructions at this blog post: [A tip for mailing list operators to interoperate with DMARC to avoid failures](/archive/blogs/tzink/a-tip-for-mailing-list-operators-to-interoperate-with-dmarc-to-avoid-failures).
  - Consider updating your mailing list server so it supports ARC. For more information, see <http://arc-spec.org>.

- **Your organization doesn't own the mailing list**:
  - Ask the maintainer of the mailing list to configure email authentication for the domain that the mailing list is relaying email from. The owners are more likely to act if enough members ask them to set up email authentication. While Microsoft also works with domain owners to publish the required records, it helps even more when individual users request it.
  - Create [Inbox rules](https://support.microsoft.com/office/c24f5dea-9465-4df4-ad17-a50704d66c59) in your email client that move messages to the Inbox.
  - Use the Tenant Allow/Block List to create an allow entry for the mailing list to treat it as legitimate. For more information, see [Create allow entries for spoofed senders](tenant-allow-block-list-email-spoof-configure.md#create-allow-entries-for-spoofed-senders).

If all else fails, you can report the message as a false positive to Microsoft. For more information, see [Report messages and files to Microsoft](submissions-report-messages-files-to-microsoft.md).

## Considerations for anti-spoofing protection

Admins of organizations that regularly send email to Microsoft 365 need to ensure the email is properly authenticated. Otherwise, it might be marked as spam or phishing. For more information, see [How to avoid email authentication failures when sending mail to Microsoft 365](email-authentication-about.md#how-to-avoid-email-authentication-failures-when-sending-mail-to-microsoft-365).

In Microsoft 365, senders in user allowlists bypass parts of the filtering stack, including spoof protection. For more information, see [Outlook Safe Senders](create-safe-sender-lists-in-office-365.md#use-outlook-safe-senders).

If possible, admins should avoid using allowed sender lists or allowed domain lists in anti-spam policies. These senders bypass most of the filtering stack (high confidence phishing and malware messages are always quarantined). For more information, see [Use allowed sender lists or allowed domain lists](create-safe-sender-lists-in-office-365.md#use-allowed-sender-lists-or-allowed-domain-lists-in-anti-spam-policies).
