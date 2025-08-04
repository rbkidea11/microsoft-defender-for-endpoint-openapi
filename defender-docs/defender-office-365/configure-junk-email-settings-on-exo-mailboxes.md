---
title: Configure junk email settings on Exchange Online mailboxes
ms.author: chrisda
author: chrisda
manager: deniseb
audience: Admin
ms.topic: how-to
ms.localizationpriority: medium
search.appverid: 
  - MOE150
  - MED150
  - MBS150
  - MET150
ms.collection: 
  - m365-security
  - tier2
description: Admins can learn how to configure the junk email settings in Exchange Online mailboxes. Many of these settings are available to users in Outlook or Outlook on the web.
ms.service: defender-office-365
ms.date: 07/31/2025
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# Configure junk email settings on Exchange Online mailboxes

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

All Microsoft 365 organizations with cloud mailboxes include anti-spam protection. For more information, see [Anti-spam protection](anti-spam-protection-about.md).

But, there are also specific anti-spam settings that admins can configure on individual mailboxes in Exchange Online:

- **Deliver messages to the Junk Email folder based on anti-spam policies**: When an anti-spam policy is configured with the action **Move message to Junk Email folder** for a spam filtering verdict, the message is delivered to the Junk Email folder of the mailbox. For more information about spam filtering verdicts in anti-spam policies, see [Configure anti-spam policies](anti-spam-policies-configure.md). Similarly, if zero-hour auto purge (ZAP) determines that a delivered message is spam or phishing, the message is moved to the Junk Email folder for **Move message to Junk Email folder** spam filtering verdict actions. For more information about ZAP, see [Zero-hour auto purge (ZAP) in Exchange Online](zero-hour-auto-purge.md).

- **Junk email settings that users configure for themselves in Outlook or Outlook on the web**: The _safelist collection_ is the Safe Senders list, the Safe Recipients list, and the Blocked Senders list on each mailbox. The entries in these lists determine whether the message is delivered to the Inbox or the Junk Email folder. Users can configure the safelist collection for their own mailboxes in Outlook or Outlook on the web (formerly known as Outlook Web App or OWA). Admins can configure the safelist collection on any user's mailbox.

Microsoft 365 adds the header `X-Forefront-Antispam-Report: SFV:BLK` to incoming messages from senders in a user's Blocked Senders list, and any future messages from that sender are classified as spam. The message is delivered to the user's Junk Email folder or to quarantine based on the action configured in the applicable anti-spam policy (our [recommended action](recommended-settings-for-eop-and-office365.md#anti-spam-policy-settings) is **Move message to Junk Email folder**).

If the sender is a user's Safe Senders list, the message is delivered to their Inbox.

Admins can use Exchange Online PowerShell to configure entries in the safelist collection on mailboxes (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list).

> [!NOTE]
> Messages from senders in user Safe Senders lists skip content filtering (the SCL is -1). To prevent users from adding entries to their Safe Senders lists, use Group Policy as mentioned in the [About junk email settings in Outlook](#about-outlook-junk-email-settings) section later in this article. Policy filtering, Content filtering, and Defender for Office 365 checks are still applied to the messages.
>
> Microsoft 365 uses a mail flow delivery agent to route messages to the Junk Email folder. It doesn't use the junk email rule in the mailbox. The _Enabled_ parameter on the **Set-MailboxJunkEmailConfiguration** cmdlet in Exchange Online PowerShell has no effect on mail flow in cloud mailboxes. Microsoft 365 routes messages based on the actions set in anti-spam policies. The user's Safe Senders list and Blocked Senders list continue to work as usual.

## What do you need to know before you begin?

- You can only use Exchange Online PowerShell to do the procedures in this article. To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- You need to be assigned permissions in Exchange Online before you can do the procedures in this article. Specifically, you need the **Mail Recipients** role (which is assigned to the **Organization Management**, **Recipient Management**, and **Custom Mail Recipients** role groups by default) or the **User Options** role (which is assigned to the **Organization Management** and **Help Desk** role groups by default). To add users to role groups in Exchange Online, see [Modify role groups in Exchange Online](/Exchange/permissions-exo/role-groups#modify-role-groups). Users with default permissions can do these same procedures on their own mailboxes, as long as they have [access to Exchange Online PowerShell](/powershell/exchange/disable-access-to-exchange-online-powershell).

- In hybrid environments where Exchange Online Protection (EOP) provides cloud protection of on-premises Exchange mailboxes, you need to configure Exchange mail flow rules (also known as transport rules) in your on-premises Exchange organization to recognize the spam filtering verdicts from the cloud. For details, see [Deliver cloud-detected spam to the Junk Email folder in on-premises mailboxes](/exchange/standalone-eop/configure-eop-spam-protection-hybrid).

  After you manually create the rule in Microsoft 365 to match the rule in on-premises Exchange, the rule replicates in hybrid environments.

- By design, safe senders for shared mailboxes aren't synchronized to Microsoft Entra ID or Microsoft 365.

## Use Exchange Online PowerShell to configure the safelist collection on a mailbox

The safelist collection on a mailbox includes the Safe Senders list, the Safe Recipients list, and the Blocked Senders list. By default, users can configure the safelist collection on their own mailboxes in Outlook or Outlook on the web. Admins can use the corresponding parameters on the **Set-MailboxJunkEmailConfiguration** cmdlet to configure the safelist collection on a user's mailbox. These parameters are described in the following table.

|Parameter on Set-MailboxJunkEmailConfiguration|Junk Email Options in Outlook|Junk email settings in Outlook on the web|
|---|---|---|
|_BlockedSendersAndDomains_|**Blocked Senders** tab|**Blocked Senders and domains** section|
|_ContactsTrusted_|**Safe Senders** tab \> **Also trust email from my Contacts**|**Filters** sections \> **Trust email from my contacts**|
|_TrustedListsOnly_|**Options** tab \> **Safe Lists Only: Only mail from people or domains on your Safe Senders List or Safe Recipients List will be delivered to your Inbox**|**Filters** section \> **Only trust email from addresses in my Safe senders and domains list and Safe mailing lists**|
|_TrustedSendersAndDomains_<sup>\*</sup>|**Safe Senders** tab|**Safe senders and domains** section|

<sup>\*</sup> You can't directly modify the **Safe Recipients** list by using the **Set-MailboxJunkEmailConfiguration** cmdlet (the _TrustedRecipientsAndDomains_ parameter doesn't work). You modify the Safe Senders list, and those changes are synchronized to the Safe Recipients list.

- In Exchange Online, whether entries in the Safe Senders list or _TrustedSendersAndDomains_ parameter work or don't work depends on the verdict and action in the policy that identified the message:
  - **Move messages to Junk Email folder**: Domain entries and sender email address entries are honored. Messages from those senders aren't moved to the Junk Email folder.
  - **Quarantine**: Domain entries aren't honored (messages from those senders are quarantined). Email address entries are honored (messages from those senders aren't quarantined) if either of the following statements is true:
    - The message isn't identified as malware or high confidence phishing (malware and high confidence phishing messages are quarantined).
    - The email address, URL, or file in the email message isn't in a block entry in the [Tenant Allow/Block](tenant-allow-block-list-about.md#block-entries-in-the-tenant-allowblock-list).
- With directory synchronization, domain entries aren't synchronized by default, but you can enable synchronization for domains. For more information, see [Configure Content Filtering to Use Safe Domain Data: Exchange 2013 Help | Microsoft Learn](/exchange/configure-content-filtering-to-use-safe-domain-data-exchange-2013-help).

To configure the safelist collection on a mailbox, use the following syntax:

```powershell
Set-MailboxJunkEmailConfiguration <MailboxIdentity> -BlockedSendersAndDomains <EmailAddressesOrDomains | $null> -ContactsTrusted <$true | $false> -TrustedListsOnly <$true | $false> -TrustedSendersAndDomains  <EmailAddresses | $null>
```

To enter multiple values and overwrite any existing entries for the _BlockedSendersAndDomains_ and _TrustedSendersAndDomains_ parameters, use the following syntax: `"<Value1>","<Value2>"...`. To add or remove one or more values without affecting other existing entries, use the following syntax: `@{Add="<Value1>","<Value2>"... ; Remove="<Value3>","<Value4>...}`

The following example configures the following settings for the safelist collection on Ori Epstein's mailbox:

- Add the value `shopping@fabrikam.com` to the Blocked Senders list.
- Remove the value `chris@fourthcoffee.com` from the Safe Senders list and the Safe Recipients list.
- Configure contacts in the Contacts folder to be treated as trusted senders.

```PowerShell
Set-MailboxJunkEmailConfiguration "Ori Epstein" -BlockedSendersAndDomains @{Add="shopping@fabrikam.com"} -TrustedSendersAndDomains @{Remove="chris@fourthcoffee.com"} -ContactsTrusted $true
```

The following example removes the domain contoso.com from the Blocked Senders list in all user mailboxes in the organization:

```PowerShell
$All = Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize Unlimited; $All | foreach {Set-MailboxJunkEmailConfiguration $_.Name -BlockedSendersAndDomains @{Remove="contoso.com"}}
```

For detailed syntax and parameter information, see [Set-MailboxJunkEmailConfiguration](/powershell/module/exchange/set-mailboxjunkemailconfiguration).

> [!NOTE]
> The Outlook Junk Email Filter has more safelist collection settings (for example, **Automatically add people I email to the Safe Senders list**). For more information, see [Use Junk Email Filters to control which messages you see](https://support.microsoft.com/office/274ae301-5db2-4aad-be21-25413cede077).

### How do you know you successfully configured the safelist collection on a mailbox?

To verify you successfully configured the safelist collection on a mailbox, use any of the following procedures:

- Replace _\<MailboxIdentity\>_ with the name, alias, or email address of the mailbox, and run the following command to verify the property values:

  ```PowerShell
  Get-MailboxJunkEmailConfiguration -Identity "<MailboxIdentity>" | Format-List trusted*,contacts*,blocked*
  ```

  If the list of values is too long, use this syntax:

  ```PowerShell
  (Get-MailboxJunkEmailConfiguration -Identity <MailboxIdentity>).BlockedSendersAndDomains
  ```

## About Outlook junk email settings

To enable, disable, and configure the client-side Junk Email Filter settings that are available in Outlook, use [Group Policy](https://support.microsoft.com/help/2252421). For more information, see [Administrative Template files (ADMX/ADML) and Office Customization Tool for Microsoft 365 Apps for enterprise, Office 2019, and Office 2016](https://www.microsoft.com/download/details.aspx?id=49030).

When the Outlook Junk Email Filter is set to the default value **No automatic filtering** in **Home** \> **Junk** \> **Junk E-Mail Options** \> **Options**, Outlook doesn't attempt to classify messages as spam, but still uses the safelist collection (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list) to move messages to the Junk Email folder after delivery. For more information about these settings, see [Overview of the Junk Email Filter](https://support.microsoft.com/office/5ae3ea8e-cf41-4fa0-b02a-3b96e21de089).

> [!NOTE]
> In Microsoft 365 organizations, we recommend that you leave the Junk Email Filter in Outlook set to **No automatic filtering** to prevent unnecessary conflicts (both positive and negative) with the spam filtering verdicts from Microsoft 365.

When the Outlook Junk Email Filter is set to **Low** or **High**, the Outlook Junk Email Filter uses its own SmartScreen filter technology to identify and move spam to the Junk Email folder. This spam classification is separate from the spam confidence level (SCL) from Microsoft 365. In fact, Outlook ignores the SCL from Microsoft 365 (unless Microsoft 365 marked the message to skip spam filtering) and uses its own criteria to determine whether the message is spam. It's possible that the spam verdict from Microsoft 365 and Outlook might align. For more information about these settings, see [Change the level of protection in the Junk Email Filter](https://support.microsoft.com/office/e89c12d8-9d61-4320-8c57-d982c8d52f6b).

> [!NOTE]
> In November 2016, Microsoft stopped producing spam definition updates for the SmartScreen filters in Exchange and Outlook. The existing SmartScreen spam definitions were left in place, but their effectiveness will likely degrade over time. For more information, see [Deprecating support for SmartScreen in Outlook and Exchange](https://techcommunity.microsoft.com/blog/exchange/deprecating-support-for-smartscreen-in-outlook-and-exchange/605332).

So, the Outlook Junk Email Filter is able to use the mailbox's safelist collection and its own spam classification to move messages to the Junk Email folder.

Outlook and Outlook on the web both support the safelist collection. The safelist collection is saved in the Exchange Online mailbox so that the changes to the safelist collection in Outlook appear in Outlook on the web, and vice-versa.

## Limits for junk email settings

The safelist collection (the Safe Senders list, the Safe Recipients list, and the Blocked Senders list) stored in the user's mailbox is also synchronized to Microsoft 365. With directory synchronization, the safelist collection is synchronized to Microsoft Entra ID.

- The safelist collection in the user's mailbox has a limit of 510 KB, which includes all lists, plus other junk email filter settings. If a user exceeds this limit, they receive an Outlook error that looks like the following message:

  > Cannot/Unable add to the server Junk E-mail lists. You are over the size allowed on the server. The Junk E-mail filter on the server is disabled until your Junk E-mail lists have been reduced to the size allowed by the server.

  For more information about this limit and how to change it, see [KB2669081](https://support.microsoft.com/help/2669081).

- The synchronized safelist collection in Microsoft 365 has the following synchronization limits:
  - 1,024 total entries in the Safe Senders list, the Safe Recipients list, and external contacts if **Trust email from my contacts** is enabled.
  - 65,535 total entries in the Blocked Senders list and the Blocked Domains list.

  When the 1024 entry limit is reached, the following things happen:

  - The list stops accepting entries in PowerShell and Outlook on the web, but no error is displayed.

    Outlook users can continue to add more than 1,024 entries until they reach the Outlook limit of 510 KB. Outlook can use these extra entries, as long as a Microsoft 365 filter doesn't block the message before delivery to the mailbox (mail flow rules, anti-spoofing, and so on).

- With directory synchronization, the entries are synchronized to Microsoft Entra ID in the following order:
  1. Mail contacts if **Trust email from my contacts** is enabled.
  2. The Safe Senders list and the Safe Recipient list are combined, deduplicated, and sorted alphabetically whenever a change is made for the first 1,024 entries.

  The first 1,024 entries are used, and relevant information is stamped in the message headers.

  For remaining entries over 1,024, Outlook processes unsynchronized entries, but no information is stamped in the message headers. This behavior doesn't occur in Outlook on the web.

As you can see, enabling the **Trust email from my contacts** setting reduces the number of Safe Senders and Safe Recipients that can be synchronized. If this reduction is a concern, we recommend using Group Policy to turn off this feature:

- File name: outlk16.opax
- Policy setting: **Trust e-mail from contacts**

> [!IMPORTANT]
> The following button helps identify and resolve issues with the safelist collection in user mailboxes (the Safe Senders list and Blocked Senders list) which includes individual senders and domains:
>
<div class="nextstepaction">
<p><a href="https://aka.ms/safeblockdiag" data-linktype="external">Run Tests: Mailbox safe/blocked sender list</a></p>
</div>
