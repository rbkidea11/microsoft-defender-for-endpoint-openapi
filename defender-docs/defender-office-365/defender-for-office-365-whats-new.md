---
title: What's new in Microsoft Defender for Office 365
description: Learn about the new features and functionality available in the latest release of Microsoft Defender for Office 365.
keywords: what's new in Microsoft Defender for Office 365, ga, generally available, capabilities, available, new
search.appverid: met150
f1.keywords: NOCSH
ms.author: chrisda
author: chrisda
manager: deniseb
ms.localizationpriority: medium
ms.date: 7/25/2025
audience: ITPro
ms.collection:
  - m365-security
  - tier1
ms.topic: whats-new
ms.custom: seo-marvel-apr2020
ms.reviewer: vippand
ms.service: defender-office-365
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# What's new in Microsoft Defender for Office 365

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

This article lists new features in the latest release of Microsoft Defender for Office 365. Features that are currently in preview are denoted with **(preview)**.

Learn more by watching [this video](https://www.youtube.com/watch?v=Tdz6KfruDGo&list=PL3ZTgFEc7LystRja2GnDeUFqk44k7-KXf&index=3).

To search the Microsoft 365 Roadmap for Defender for Office 365 features, use [this link](https://www.microsoft.com/microsoft-365/roadmap?filters=Microsoft%20Defender%20for%20Office%20365).

For more information on what's new with other Microsoft Defender security products, see:

- [What's new in Microsoft Defender XDR](/defender-xdr/whats-new)
- [What's new in Microsoft Defender for Endpoint](/defender-endpoint/whats-new-in-microsoft-defender-endpoint)
- [What's new in Microsoft Defender for Identity](/defender-for-identity/whats-new)
- [What's new in Microsoft Defender for Cloud Apps](/cloud-app-security/release-notes)

## July 2025

- Users can report external and intra-org [Microsoft Teams messages](submissions-teams.md) from chats, standard and private channels, meeting conversations to Microsoft, the specified reporting mailbox, or both via [user reported settings](submissions-user-reported-messages-custom-mailbox.md).

## June 2025

- Defender for Office 365 is now able to detect and classify mail bombing attacks. Mail bombing is a distributed denial of service (DDoS) attack that typically subscribes recipients to a large number of legitimate newsletters and services. The resulting volume of incoming email within minutes intends to overwhelm the recipient's mailbox and email security systems, and acts as a precursor to malware, ransomware, or data exfiltration.

  Mail bombing is now an available **Detection technology** value in [Threat Explorer](threat-explorer-real-time-detections-about.md), [the Email entity page](mdo-email-entity-page.md), and the [Email summary panel](mdo-email-entity-page.md#the-email-summary-panel). Mail bombing is also an available **DetectionMethods** value in [Advanced Hunting](/defender-xdr/advanced-hunting-overview).

  For more information, see [MC1096885](https://admin.microsoft.com/AdminPortal/Home?#/MessageCenter/:/messages/MC1096885).

- AI-powered Submissions Response introduces generative AI explanations for admin email submissions to Microsoft. For more information, see [Submission result definitions](submissions-result-definitions.md).

## May 2025

- In government cloud environments, :::image type="icon" source="media/m365-cc-sc-take-actions-icon.png" border="false"::: **Take action** replaces the **Message actions** drop down list on the **Email** tab (view) of the details area of the **All email**, **Malware**, or **Phish** views in [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about.md):
  - SecOps personnel can now create organization block entries on URLs and files via the [Tenant Allow/Block List](tenant-allow-block-list-about.md) directly from Threat Explorer.
  - For 100 or fewer messages selected in Threat Explorer, SecOps personnel can take multiple actions on the selected messages from the same page. For example:
    - Purge email messages or propose email remediation.
    - Submit messages to Microsoft.
    - Trigger investigations.
    - Create block entries in the Tenant Allow/Block List.
  - Actions are contextually based on the latest delivery location of the message, but SecOps personnel can use the **Show all response actions** toggle to allow all available actions.
  - For 101 or more messages selected, only email purge and propose remediation options are available.

  > [!TIP]
  > A new panel allows SecOps personnel to look for indicators of compromise at the tenant level, and the block action is readily available.

  For more information, see [Threat hunting: Email remediation](threat-explorer-threat-hunting.md#email-remediation) and  [Remediate Malicious Email: Manual and automated remediation](remediate-malicious-email-delivered-office-365.md#manual-and-automated-remediation).

## March 2025

- **User reported messages by non-Microsoft add-ins can be sent to Microsoft for analysis**: In [user reported settings](submissions-user-reported-messages-custom-mailbox.md), admins can select **Monitor reported messages in Outlook** \> **Use a non-Microsoft add-in button**. In the **Reported message destination** section, select **Microsoft and my reporting mailbox**, and then provide the email address of the internal Exchange Online mailbox where user-reported messages by the non-Microsoft add-in are routed to. Microsoft analyzes these reported messages and provides result on the **User reported** tab of **Submissions** page at <https://security.microsoft.com/reportsubmission?viewid=user>.

- **Create allow entries directly in the Tenant Allow/Block List**: You can now create allow entries for domains & addresses and URLs directly in the [Tenant Allow/Block List](tenant-allow-block-list-about.md). This capability is available in Microsoft 365 Worldwide, GCC, GCC High, DoD, and Office 365 operated by 21Vianet.

## January 2025

- [Use the built-in Report button in Outlook](submissions-outlook-report-messages.md#use-the-built-in-report-button-in-outlook): The built-in **Report** button in Outlook for iOS version 4.2508 or, later and Android version 4.2446 or later now supports the [user reported settings](submissions-user-reported-messages-custom-mailbox.md) experience to report messages as Phishing, Junk, and Not Junk.

## December 2024

- [Considerations for integrating non-Microsoft security services with Microsoft 365](mdo-integrate-security-service.md): Considerations and recommendations for deploying a defense-in-depth email security strategy using non-Microsoft security services.

## November 2024

- **Introducing LLM-based BEC detection and classification**: Microsoft Defender for Office 365 now detects BEC attacks using large language model (LLM)-based filters to analyze an email's language and infer intent. To learn more, see our blog post [Microsoft Ignite: Redefining email security with LLMs to tackle a new era of social engineering](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/microsoft-ignite-redefining-email-security-with-llms-to-tackle-a-new-era-of-soci/4302421).

## October 2024

- **Tenant Allow/Block List in Microsoft 365 now supports IPv6 address**: The [Tenant Allow/Block List](tenant-allow-block-list-about.md) now supports [allowing and blocking IPv6 addresses](tenant-allow-block-list-ip-addresses-configure.md). It's available in Microsoft 365 Worldwide, GCC, GCC High, DoD, and Office 365 operated by 21Vianet environments.

## September 2024

- With one click, SecOps personnel can take a quarantine release action directly from Explorer (Threat Explorer) or the Email entity page (no need to go to the Quarantine page in the Defender portal). For more information, see [Remediate malicious email delivered in Office 365](remediate-malicious-email-delivered-office-365.md).
- [Use the built-in Report button in Outlook](submissions-outlook-report-messages.md#use-the-built-in-report-button-in-outlook): The built-in **Report** button in Outlook for Mac v16.89 (24090815) or later now supports the [user reported settings](submissions-user-reported-messages-custom-mailbox.md) experience to report messages as Phishing, Junk, and Not Junk.
- We're updating the end user experience for allowlist and blocklist management of their email messages. With one click, users can block email from unwanted senders and prevent those messages from appearing in their default quarantine view and in quarantine notifications. Users can also allow email from trusted and prevent future messages from those senders from being quarantined (if there are no admin overrides). Users also have visibility into any admin overrides that led to a quarantined email message. For more information, see [View quarantined email](quarantine-admin-manage-messages-files.md#view-quarantined-email).
- Admins can see [policy](anti-spam-policies-configure.md#use-the-microsoft-defender-portal-to-modify-anti-spam-policies) what-if insights for the bulk complaint level (BCL) threshold, spoof, and impersonation settings, which let them understand the implication of a setting change based on historical data. This capability lets admins confidently tune their settings without anxiety about possible repercussions on users.

## August 2024

- (Preview) You can now run [simulations](attack-simulation-training-simulations.md) with QR code payloads in [Attack simulation training](attack-simulation-training-get-started.md). You can track user responses and assign training to end users.

- [Use the built-in Report button in Outlook](submissions-outlook-report-messages.md#use-the-built-in-report-button-in-outlook): The built-in **Report** button in Outlook for Microsoft 365 now supports the [user reported settings](submissions-user-reported-messages-custom-mailbox.md) experience to report messages as Phishing, Junk, and Not Junk.

- We're rolling out new details into who or what was responsible for releasing a message from quarantine. These details are included in the email summary flyout that's accessible from the Quarantine page. For more information, see [View quarantined email](quarantine-admin-manage-messages-files.md#view-quarantined-email).

## July 2024

- **Tenant Allow/Block List in Microsoft 365 GCC, GCC High, DoD, and Office 365 operated by 21Vianet environments**: The [Tenant Allow/Block List](tenant-allow-block-list-about.md) is now available these environments. They are on parity with the WW commercial experiences.

- **45 days after last used date**: The value **Remove allow entry after** \> **45 days after last used date** is now the default on new allow entries from submissions. The existing allow entries in the [Tenant Allow/Block List](tenant-allow-block-list-about.md) can also be modified to include the value **Remove allow entry after** \> **45 days after last used date**. The allow entry is triggered and the **LastUsedDate** property is updated when the entity is encountered and identified as malicious during mail flow or at time of click. After the filtering system determines that the entity is clean, the allow entry is automatically removed after 45 days. By default, allow entries for spoofed senders never expire.

- (GA) Learning hub resources have moved from the Microsoft Defender portal to [learn.microsoft.com](https://go.microsoft.com/fwlink/?linkid=2273118). Access Microsoft Defender XDR Ninja training, learning paths, training modules and more. Browse the [list of learning paths](/training/browse/?products=m365-ems-cloud-app-security%2Cdefender-for-cloud-apps%2Cdefender-identity%2Cm365-information-protection%2Cm365-threat-protection%2Cmdatp%2Cdefender-office365&expanded=m365%2Coffice-365), and filter by product, role, level, and subject.

- (GA) SecOps personnel can now release email messages from quarantine or move messages from quarantine back to user Inboxes directly from :::image type="icon" source="media/m365-cc-sc-take-actions-icon.png" border="false"::: **Take action** in Threat Explorer, Advanced hunting, custom detection, the Email entity page, and the Email summary panel. This capability allows security operators to manage false positives more efficiently and without losing context. For more information, see [Threat hunting: Email remediation](threat-explorer-threat-hunting.md#email-remediation).

- We're introducing intra-org protection data into three of our core customer facing reports: the [Mailflow status report](reports-email-security.md#mailflow-status-report), [Threat protection status report](reports-email-security.md#threat-protection-status-report), and [Top senders and recipient report](reports-email-security.md#top-senders-and-recipients-report). Admins and security operators now have insight into how the default email protections for cloud mailboxes and Defender for Office 365 protect users from malicious email traffic inside the organization. For more information, see [Email security report changes in the Microsoft Defender portal](reports-email-security.md#email-security-report-changes-in-the-microsoft-defender-portal).

## May 2024

- **Top level domain and subdomain blocking in Tenant Allow/Block List**: You can create block entries under domains & email addresses, using the format `*.TLD`, where `TLD` can be any top-level domain or `*.SD1.TLD, *.SD2.SD1.TLD`, `*.SD3.SD2.SD1.TLD`, and similar patterns for subdomain blocking. The entries block all email received from or sent to any email addresses in the domain or subdomain during mail flow.

- **Automated end user feedback**: The user submission automatic feedback response capability in Microsoft Defender for Office 365 enables organizations to automatically respond to end user submissions of phishing based on the verdict from the automated investigation. [Learn more](air-user-automatic-feedback-response.md).

- We're introducing **Sender's copy clean-up features** in Threat Explorer, email entity, Summary Panel, and Advanced hunting. These new features streamline the process of managing Sent items, particularly for admins who use the actions **Move to mailbox folder** \> **Soft delete** and **Move to mailbox folder** \> **Inbox**. For more information, see [Threat hunting: The Take action wizard](threat-explorer-threat-hunting.md#the-take-action-wizard). Key highlights:
- Integration with Soft delete: Sender's copy clean-up is incorporated as part of the Soft delete action.
  - Wide support: This action is supported across various Defender XDR platforms including Threat Explorer, Take Action wizard from the email entity, Summary Panel, Advanced hunting, and through Microsoft Graph API.
  - Undo capability: An undo action is available, allowing you to reverse the clean-up by moving items back to the Sent folder.

## April 2024

- **Last used date** added to Tenant Allow/Block List entries for domains and email addresses, files, and URLs.
- **Enhanced clarity in submissions results**: Admins and security operators now see enhanced results within submissions across email, Microsoft Teams messages, email attachments, URLs, and user-reported messages. These updates aim to eliminate any ambiguity associated with the current submission results. The results are refined to ensure clarity, consistency, and conciseness, making the submission results more actionable for you. [Learn more](submissions-admin.md).
- :::image type="icon" source="media/m365-cc-sc-take-actions-icon.png" border="false"::: **Take action** replaces the **Message actions** drop down list on the **Email** tab (view) of the details area of the **All email**, **Malware**, or **Phish** views in [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about.md):
  - SecOps personnel can now create organization block entries on URLs and files via the [Tenant Allow/Block List](tenant-allow-block-list-about.md) directly from Threat Explorer.
  - For 100 or fewer messages selected in Threat Explorer, SecOps personnel can take multiple actions on the selected messages from the same page. For example:
    - Purge email messages or propose email remediation.
    - Submit messages to Microsoft.
    - Trigger investigations.
    - Block entries in the Tenant Allow/Block List.
  - Actions are contextually based on the latest delivery location of the message, but SecOps personnel can use the **Show all response actions** toggle to allow all available actions.
  - For 101 or more messages selected, only email purge and propose remediation options are available.

  > [!TIP]
  > A new panel allows SecOps personnel to look for indicators of compromise at the tenant level, and the block action is readily available.

  For more information, see [Threat hunting: Email remediation](threat-explorer-threat-hunting.md#email-remediation).

## March 2024

- **Copy simulation functionality in Attack simulation training**: Admins can now duplicate existing simulations and customize them to their specific requirements. This feature saves time and effort by using previously launched simulations as templates when creating new ones. [Learn more](attack-simulation-training-simulations.md#copy-simulations).
- Attack simulation training is now available in **Microsoft 365 DoD**. [Learn more](/office365/servicedescriptions/microsoft-defender-for-office-365-features#attack-simulation-training).

## February 2024

- **Hunting and responding to QR code-based attacks**: Security teams are now able to see the URLs extracted from QR codes with **QR code** as URL source on the **URL** tab of the [Email entity page](mdo-email-entity-page.md), and **QRCode** in the **UrlLocation** column of **EmailUrlInfo** table in [Advanced Hunting](/defender-xdr/advanced-hunting-overview). You can also filter for email with URLs embedded within QR codes using the **URL Source** filter value **QR code** in the **All email**, **Malware**, and **Phish** views in [Threat Explorer (Explorer)](threat-explorer-real-time-detections-about.md).

## January 2024

- **New training modules available in Attack Simulation Training**: Teach your users to recognize and protect themselves against QR code phishing attacks. For more information, see [this blog post](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/train-your-users-to-be-more-resilient-against-qr-code-phishing/4022667).
- **Providing intent while submitting is now generally available**: Admins can identify if they're submitting an item to Microsoft for a second opinion or they're submitting the message because it's malicious and was missed by Microsoft. With this change, Microsoft analyses of admin submitted messages (email and Microsoft Teams), URLs, and email attachments are further streamlined and results in a more accurate analysis. [Learn more](submissions-admin.md).

## December 2023

- **QR code related phishing protection in the default email protections for cloud mailboxes and in Microsoft Defender for Office 365**: New detection capabilities using image detection, threat signals, URL analysis now extracts QR codes from URLs and blocks QR code based phishing attacks from the body of an email. To learn more, see our [blog](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/protect-your-organizations-against-qr-code-phishing-with-defender-for-office-365/4007041).
- **Microsoft Defender XDR Unified RBAC is now generally available**: Defender XDR Unified RBAC supports all Defender for Office 365 scenarios previously controlled by [Email & collaboration permissions](mdo-portal-permissions.md) and [Exchange Online permissions](/exchange/permissions-exo/permissions-exo). To learn more about the supported workloads and data resources, see [Microsoft Defender XDR Unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

  > [!TIP]
  > Defender XDR Unified RBAC isn't generally available in Microsoft 365 Government Community Cloud High (GCC High) or Department of Defense (DoD).

## November 2023

- **Enhanced Action experience from the Email entity and Email summary panel**: As part of the change security admins can take multiple actions as part of FP/FN flows. [Learn more](mdo-email-entity-page.md).
- The [Tenant Allow/Block List](tenant-allow-block-list-about.md) supports more entries in each category (Domains & email addresses, Files, and URLs):
  - Microsoft Defender for Office 365 Plan 2 supports 10,000 block entries and 5,000 allow entries (via admin submissions) in each category.
  - Microsoft Defender for Office 365 Plan 1 supports 1,000 block entries and 1,000 allow entries (via admin submissions) in each category.
  - Default protection in Microsoft 365 remains at 500 block entries and 500 allow entries (via admin submissions) in each category.

## October 2023

- **Create and manage simulations using the Graph API** in Attack simulation training. [Learn more](/graph/api/attacksimulationroot-post-simulation)
- **Exchange Online permission management in Defender for Office 365 is now supported in Microsoft Defender XDR Unified role-based access control (RBAC)**: In addition to the existing support for [Email & collaboration permissions](mdo-portal-permissions.md), Defender XDR Unified RBAC now also supports protection-related [Exchange Online permissions](/exchange/permissions-exo/permissions-exo). To learn more about the supported Exchange Online permissions, see [Exchange Online permissions mapping](/defender-xdr/compare-rbac-roles#exchange-online-permissions-mapping).

## September 2023

- URL top-level domain blocking is available in the **Tenant allow block list**. [Learn more](tenant-allow-block-list-urls-configure.md).
- Attack simulation training is now available in **Microsoft 365 GCC High**. [Learn more](/office365/servicedescriptions/microsoft-defender-for-office-365-features#attack-simulation-training).

## August 2023

- If the [User reported settings](submissions-user-reported-messages-custom-mailbox.md) in the organization send user reported messages (email and [Microsoft Teams](submissions-teams.md)) to Microsoft (exclusively or in addition to the reporting mailbox), we now do the same checks as when admins submit messages to Microsoft for analysis from the **Submissions** page.
- **Default intra-organizational protection**: By default, messages sent between internal users that are identified as high confidence phishing are quarantined. Admins change this setting in the default anti-spam policy or in custom policies (opt-out of intra-org protection or include other spam filtering verdicts). For configuration information, see [Configure anti-spam policies](anti-spam-policies-configure.md).

## July 2023

- Use anti-phishing policies to control what happens to messages where the sender fails explicit [DMARC](email-authentication-dmarc-configure.md) checks and the DMARC policy is set to `p=quarantine` or `p=reject`. For more information, see [Spoof protection and sender DMARC policies](anti-phishing-policies-about.md#spoof-protection-and-sender-dmarc-policies).
- [User tags](user-tags-about.md) are now fully integrated with Defender for Office 365 reports, including:
  - [Threat protection status report](reports-email-security.md#threat-protection-status-report)
  - [Compromised users report](reports-email-security.md#compromised-users-report)
  - [Top senders and recipients report](reports-email-security.md#top-senders-and-recipients-report)
  - [URL protection report](reports-email-security.md#url-protection-report)

## May 2023

- Built-in reporting in Outlook on the web supports reporting messages from shared mailboxes or other mailboxes by a delegate.
  - Shared mailboxes require Send As or Send On Behalf permission for the user.
  - Other mailboxes require Send As or Send On Behalf permission _and_ Read and Manage permissions for the delegate.

## April 2023

- [Using machine learning to drive more effective simulations in Attack Simulation and Training](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/attack-simulation-training-using-machine-learning-to-drive-more-effective-simula/3791023): Make use of intelligent predicted compromise rate (PCR) and Microsoft Defender for Office 365 payload recommendations for utilizing high-quality payloads in your simulation.
- [Training only campaigns available with an expanded library](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/training-only-campaign-is-now-available-with-an-expanded-training-module-library/3795237): You can now directly assign training content to your organization without needing to tie training to a phishing simulation campaign. We also expanded our training module library to more than 70 different modules.

## March 2023

- **Collaboration security for Microsoft Teams**: With the increased use of collaboration tools like Microsoft Teams, the possibility of malicious attacks using URLs and messages has increased as well. Microsoft Defender for Office 365 is extending its [Safe Links](safe-links-about.md) protection with increased capabilities for zero-hour auto purge (ZAP), quarantine, and end user reporting of potential malicious messages to their admins. For more information, see [Microsoft Defender for Office 365 support for Microsoft Teams (Preview)](mdo-support-teams-about.md).
- **Built-in protection: Safe Links time of click protection enabled for email**: By default, Microsoft now protects URLs in email messages at time of click as part of this update to Safe Links settings (_EnableSafeLinksForEmail_) within the Built-in protection preset security policy. To learn about the specific Safe Links protections in the Built-in protection preset security policy, see [Safe Links policy settings](recommended-settings-for-eop-and-office365.md#safe-links-policy-settings).
- **Quarantine notifications enabled in preset security policies**: If your organization enabled or will enable the Standard or Strict preset security policies, the policies are automatically updated to use the new DefaultFullAccessWithNotificationPolicy quarantine policy (notifications enabled) wherever the DefaultFullAccessPolicy (notifications disabled) was used. To learn more about quarantine notifications, see [Quarantine notifications](quarantine-quarantine-notifications.md). For more information about specific settings in preset security policies, see [Recommended email and collaboration threat policy settings for cloud organizations](recommended-settings-for-eop-and-office365.md).

## January 2023

- **Automatic Tenant Allow/Block List expiration management is now available in Microsoft Defender for Office 365**: Microsoft now automatically removes allow entries from the Tenant Allow/Block List once the system has learned from it. Alternatively, Microsoft extends the expiration time of the allow entries if the system hasn't learned yet. This behavior prevents legitimate email from going to junk or quarantine.
- **Configuring non-Microsoft phishing simulations in Advanced Delivery:** We expanded "Simulation URLs to allow" limit to 30 URLs. To learn how to configure, see [Configure the delivery of non-Microsoft phishing simulations to users and unfiltered messages to SecOps mailboxes](advanced-delivery-policy-configure.md)
- [Enhanced user telemetry in the simulation reports in Attack Simulation Training](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/attack-simulation-training-new-insights-into-targeted-user-behavior/3673105): As part of our enhanced user telemetry, administrators can now view more details about how their targeted users are interacting with the phishing payload from phishing simulation campaigns.

## December 2022

- The new Microsoft Defender XDR role-based access control (RBAC) model, with support for Microsoft Defender for Office, is now available in public preview. For more information, see [Microsoft Defender XDR role-based access control (RBAC)](/defender-xdr/manage-rbac).

- [Use the built-in Report button on Outlook](submissions-outlook-report-messages.md#use-the-built-in-report-button-in-outlook): Use the built-in Report button in Outlook on the web and new Outlook for Windows client to report messages as phish, junk, and not junk.

## October 2022

- [Automated Investigations email cluster action deduplication](air-review-approve-pending-completed-actions.md): We added more checks. If the same investigation cluster is already approved during the past hour, new duplicate remediation isn't processed again.

- [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about.md):
  - With **allow expiry management** (currently in Private Preview), if Microsoft hasn't learned from the allow, Microsoft automatically extends the expiry time of allows, which are going to expire soon, by 30 days to prevent legitimate email from going to junk or quarantine again.
  - Customers in government cloud environments are now able to create allow and block entries for URLs and file attachments in the Tenant Allow/Block List using admin submissions for URLs and email attachments. The data submitted through the submissions experience doesn't leave the customer organization, thus satisfying the data residency commitments for government cloud clients.
- **Enhancement in URL click alerts:**
  - With the new lookback scenario, the "A potentially malicious URL click was detected" alert now includes any clicks during the _past 48 hours_ (for email) from the time the malicious URL verdict is identified.

## September 2022

- **Anti-spoofing enhancement for internal domains and senders:**
  - For spoofing protection, the allowed senders or domains defined in the [anti-spam policy](anti-spam-policies-configure.md) and within user allowlists must now pass email authentication for the allowed messages to be honored. The change only affects messages that are considered to be internal (the sender or sender's domain is in an accepted domain in the organization). All other messages continue to be handled as they are today.

- **Automatic redirection from Office action center to unified action center:** The action center in the Email & Collaboration section **Email & Collaboration** > **Review** > **Action center** <https://security.microsoft.com/threatincidents> is automatically redirected to **Actions & Submissions** \> **Action center** \> **History** <https://security.microsoft.com/action-center/history>.

- **Automatic redirection from Office 365 Security & Compliance Center to Microsoft Defender portal:** Automatic redirection begins for users accessing the security solutions in Office 365 Security & Compliance center (protection.office.com) to the appropriate solutions in Microsoft Defender portal (security.microsoft.com). This change is for all security workflows like (for example, Alerts, Threat Management, and Reports).

  - Redirection URLs:
    - GCC Environment:
      - From Office 365 Security & Compliance Center URL: protection.office.com
      - To Microsoft Defender XDR URL: security.microsoft.com
    - GCC-High Environment:
      - From Office 365 Security & Compliance Center URL: scc.office365.us
      - To Microsoft Defender XDR URL: security.microsoft.us
    - DoD Environment:
      - From Office 365 Security & Compliance Center URL: scc.protection.apps.mil
      - To Microsoft Defender XDR URL: security.apps.mil
- Items in the Office 365 Security & Compliance Center unrelated related to security aren't redirected to Microsoft Defender XDR. For compliance solutions redirection to Microsoft 365 Compliance Center, see Message Center post 244886.
- This change is a continuation of [Public Sector Blog - Microsoft Defender XDR delivers unified XDR experience to GCC, GCC High, and DoD customers](https://techcommunity.microsoft.com/blog/publicsectorblog/microsoft-365-defender-delivers-unified-xdr-experience-to-gcc-gcc-high-and-dod-c/3263702), announced in March 2022.
- This change enables users to view and manage other Microsoft Defender XDR security solutions in one portal.
- This change impacts all customers who use the Office 365 Security & Compliance Center (protection.office.com). For example:
  - Microsoft Defender for Office (Plan 1 or Plan 2)
  - Microsoft 365 E3 / E5
  - Office 365 E3 / E5

    For the full list, see [Microsoft 365 guidance for security & compliance](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance).

- This change impacts all users who sign in to the Office 365 Security and Compliance portal (protection.office.com), including security teams and end-users who access the Email Quarantine experience, at the **Microsoft Defender Portal** \> **Review** \> **Quarantine**.
- Redirection is enabled by default and impacts all users of the Tenant.
- Global Administrators<sup>\*</sup> and Security Administrators can turn on or off redirection in the Microsoft Defender portal by navigating to **Settings** \> **Email & collaboration** > **Portal redirection** and switch the redirection toggle.

  > [!IMPORTANT]
  > <sup>\*</sup> Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

- **Built-in protection**: A profile that enables a base level of Safe Links and Safe Attachments protection that's on by default for all Defender for Office 365 customers. To learn more about this new policy and order of precedence, see [Preset security policies](preset-security-policies.md). To learn about the specific Safe Links and Safe Attachment controls that are set, see [Safe Attachments settings](recommended-settings-for-eop-and-office365.md#safe-attachments-settings) and [Safe Links policy settings](recommended-settings-for-eop-and-office365.md#safe-links-policy-settings).
- **Bulk Complaint Level** is now available in the EmailEvents table in Advanced Hunting with numeric BCL values from 0 to 9. A higher BCL score indicates that bulk message is more likely to generate complaints and is more likely to be spam.

## July 2022

- [Introducing actions into the Email entity page](mdo-email-entity-page.md): Admins can take preventative, remediation, and submission actions from the Email entity page.

## June 2022

- [Create allow entries for spoofed senders](tenant-allow-block-list-email-spoof-configure.md#create-allow-entries-for-spoofed-senders): Create allowed spoofed sender entries using the Tenant Allow/Block List.

- [Impersonation allows using admin submission](tenant-allow-block-list-email-spoof-configure.md#about-impersonated-domains-or-senders): Add allows for impersonated senders using the **Submissions** page in Microsoft Defender XDR.

- [Submit user reported messages to Microsoft for analysis](submissions-admin.md#submit-user-reported-messages-to-microsoft-for-analysis): Configure a reporting mailbox to intercept user-reported messages without sending the messages to Microsoft for analysis.

- View the associated alerts for [user reported messages](submissions-admin.md#actions-for-user-reported-messages-in-defender-for-office-365) and [admin submissions](submissions-admin.md#actions-for-admin-submissions-in-defender-for-office-365): View the corresponding alert for each user reported phishing message and admin email submission.

- [Configurable impersonation protection custom users and domains and increased scope within Preset policies](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/configurable-impersonation-protection-and-scope-for-preset-security-policies/3294459):
  - (Choose to) Apply Preset Strict/Standard policies to entire organization and avoid the hassle of selecting specific recipient users, groups, or domains, thereby securing all recipient users of your organization.
  - Configure impersonation protection settings for custom users and custom domains within Preset Strict/Standard policies and automatically protect your targeted users and targeted domain against impersonation attacks.

- [Simplifying the quarantine experience (part two) in Microsoft Defender XDR for office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/simplifying-the-quarantine-experience---part-two/3354687): Highlights additional features to make the quarantine experience even easier to use.

- [Introducing differentiated protection for priority accounts in Microsoft Defender for Office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/introducing-differentiated-protection-for-priority-accounts-in-microsoft-defende/3283838): Introducing GCC, GCC-H, and DoD availability of differentiated protection for priority accounts.

## April 2022

- [Introducing the URLClickEvents table in Microsoft Defender XDR Advanced Hunting](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/introducing-the-urlclickevents-table-in-advanced-hunting-with-microsoft-defender/3295096): Introducing the UrlClickEvents table in advanced hunting with Microsoft Defender for Office 365.
- [Manual email remediation enhancements](remediate-malicious-email-delivered-office-365.md): Bringing manual email purge actions taken in Microsoft Defender for Office 365 to the Microsoft Defender XDR (M365D) unified Action Center using a new action-focused investigation.
- [Introducing differentiated protection for priority accounts in Microsoft Defender for Office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/introducing-differentiated-protection-for-priority-accounts-in-microsoft-defende/3283838): Introducing the general availability of differentiated protection for priority accounts.

## March 2022

- [Streamlined the submission experience in Microsoft Defender for Office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/streamlining-the-submissions-experience-in-microsoft-defender-for-office-365/3152080): Introducing the new unified and streamlined submission process to make your experience simpler.

## January 2022

- [Updated Hunting and Investigation Experiences for Microsoft Defender for Office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/updated-hunting-and-investigation-experiences-for-microsoft-defender-for-office-/3002015): Introducing the email summary panel for experiences in Defender for Office 365, along with experience updates for Threat Explorer and Real-time detections.

## October 2021

- [Advanced Delivery DKIM enhancement](advanced-delivery-policy-configure.md): Added support for DKIM domain entry as part of non-Microsoft phishing simulation configuration.
- [Secure by Default](secure-by-default.md): Extended Secure by Default for Exchange mail flow rules (also known as transport rules).

## September 2021

- [Improved reporting experience in Defender for Office 365](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/improving-the-reporting-experience-in-microsoft-defender-for-office-365/2760898)
- [Quarantine policies](quarantine-policies.md): Admins can configure granular control for recipient access to quarantined messages and customize end-user spam notifications.
  - [Video of admin experience](https://youtu.be/vnar4HowfpY)
  - [Video of end-user experience](https://youtu.be/s-vozLO43rI)
  - Other new capabilities coming to the quarantine experience are described in this blog post: [Simplifying the Quarantine experience](https://techcommunity.microsoft.com/blog/microsoftdefenderforoffice365blog/simplifying-the-quarantine-experience/2676388).
- Portal redirection by default begins, redirecting users from the Security & Compliance Center to Microsoft Defender XDR <https://security.microsoft.com>.

## August 2021

- [Admin review for reported messages](submissions-admin-review-user-reported-messages.md): Admins can now send templated messages back to end users after they review reported messages. The templates can be customized for your organization and based on your admin's verdict as well.
- You can now add allow entries to the Tenant Allow/Block List if the blocked message was submitted as part of the admin submission process. Depending on the nature of the block, the submitted URL, file, and/or sender allow entries are added to the Tenant Allow/Block List. In most cases, the allows entries are added to give the system some time and allow it naturally, if warranted. In some cases, Microsoft manages the allow entries for you. For more information, see:
  - [Report good URLs to Microsoft](submissions-admin.md#report-good-urls-to-microsoft)
  - [Report good email attachments to Microsoft](submissions-admin.md#report-good-email-attachments-to-microsoft)
  - [Report good email to Microsoft](submissions-admin.md#report-good-email-to-microsoft)

## July 2021

- [Email analysis improvements in automated investigations](email-analysis-investigations.md)
- [Advanced Delivery](advanced-delivery-policy-configure.md): Introducing a new capability for configuring the delivery of non-Microsoft phishing simulations to users and unfiltered messages to security operation mailboxes.
- [Safe Links for Microsoft Teams](safe-links-about.md#safe-links-settings-for-microsoft-teams)
- New alert policies for the following scenarios: compromised mailboxes, Forms phishing, malicious mails delivered due to overrides and rounding out ZAP
  - Suspicious email forwarding activity
  - User restricted from sharing forms and collecting responses
  - Form blocked due to potential phishing attempt
  - Form flagged and confirmed as phishing
  - [New alert policies for ZAP](/purview/new-defender-alert-policies)
- Microsoft Defender for Office 365 alerts is now integrated into Microsoft Defender XDR - [Microsoft Defender XDR Unified Alerts Queue and Unified Alerts Queue](/defender-xdr/investigate-alerts)
- [User Tags](user-tags-about.md) are now integrated into Microsoft Defender for Office 365 alerting experiences, including: the alerts queue and details in Office 365 Security & Compliance, and scoping custom alert policies to user tags to create targeted alert policies.
  - Tags are also available in the unified alerts queue in the Microsoft Defender portal (Microsoft Defender for Office 365 Plan 2)

## June 2021

- New first contact safety tip setting within anti-phishing policies. This safety tip is shown when recipients first receive an email from a sender or don't often receive email from a sender. For more information on this setting and how to configure it, see the following articles:
  - [First contact safety tip](anti-phishing-policies-about.md#first-contact-safety-tip)
  - [Configure anti-phishing policies if you don't have Microsoft Defender for Office 365](anti-phishing-policies-eop-configure.md)
  - [Configure anti-phishing policies in Microsoft Defender for Office 365](anti-phishing-policies-mdo-configure.md)

## April/May 2021

- [Email entity page](mdo-email-entity-page.md): A unified 360-degree view of an email with enriched information around threats, authentication and detections, detonation details, and a brand-new email preview experience.
- [Office 365 Management API](/office/office-365-management-api/office-365-management-activity-api-schema#email-message-events): Updates to EmailEvents (RecordType 28) to add delivery action, original and latest delivery locations, and updated detection details.
- [Threat Analytics for Defender for Office 365](/defender-xdr/threat-analytics): View active activity groups, popular techniques, and attack surfaces, along with extensive reporting from Microsoft researchers around ongoing campaigns.

## February/March 2021

- Alert ID integration (search using Alert ID and Alert-Explorer navigation) in [hunting experiences](threat-explorer-real-time-detections-about.md)
- Increasing the limits for Export of records from 9990 to 200,000 in [hunting experiences](threat-explorer-real-time-detections-about.md)
- Extending the Explorer (and Real-time detections) data retention and search limit for trial organizations from seven days (previous limit) to 30 days in [hunting experiences](threat-explorer-real-time-detections-about.md)
- New hunting pivots called **Impersonated domain** and **Impersonated user** within Explorer and Real-time detections to search for impersonation attacks against protected users or domains. For more information, see [Phish view in Threat Explorer and Real-time detections](threat-explorer-real-time-detections-about.md#phish-view-in-threat-explorer-and-real-time-detections).

## Microsoft Defender for Office 365 Plan 1 and Plan 2

Did you know that Microsoft Defender for Office 365 is available in two plans? [Learn more about what each plan includes](mdo-about.md#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet).

## See also

- [Microsoft 365 roadmap](https://www.microsoft.com/microsoft-365/roadmap?filters=Microsoft%20365)
- [Microsoft Defender for Office 365 Service Description](/office365/servicedescriptions/office-365-advanced-threat-protection-service-description)
