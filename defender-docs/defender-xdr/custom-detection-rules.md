---
title: Create custom detection rules in Microsoft Defender XDR
description: Learn how to create custom detections rules based on advanced hunting queries.
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
f1.keywords:
  - NOCSH
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
manager: orspodek
audience: ITPro
ms.collection:
  - m365-security
  - m365initiative-m365-defender
  - tier2
ms.custom:
- cx-ti
- cx-ah
appliesto:
    - Microsoft Defender XDR
    - Microsoft Sentinel in the Microsoft Defender portal
ms.topic: how-to
ms.date: 07/29/2025
---

# Create custom detection rules

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]



Custom detection rules are rules you can design and tweak using [advanced hunting](advanced-hunting-overview.md) queries. These rules let you proactively monitor various events and system states, including suspected breach activity and misconfigured endpoints. You can set them to run at regular intervals, generating alerts and taking response actions whenever there are matches.

## Required permissions for managing custom detections

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

To manage custom detections, you need to be assigned one of these roles:

- **Security settings (manage)** - Users with this [Microsoft Defender XDR permission](manage-rbac.md) can manage security settings in the Microsoft Defender portal.

- **Security Administrator** - Users with this [Microsoft Entra role](/azure/active-directory/roles/permissions-reference#security-administrator) can manage security settings in the Microsoft Defender portal and other portals and services.

- **Security Operator** - Users with this [Microsoft Entra role](/azure/active-directory/roles/permissions-reference#security-operator) can manage alerts and have global read-only access to security-related features, including all information in the Microsoft Defender portal. This role is sufficient for managing custom detections only if role-based access control (RBAC) is turned off in Microsoft Defender for Endpoint. If you have RBAC configured, you also need the *Manage Security Settings permission for Defender for Endpoint.

You can manage custom detections that apply to data from specific Microsoft Defender XDR solutions if you have the right permissions for them. For example, if you only have manage permissions for Microsoft Defender for Office 365, you can create custom detections using `Email*` tables but not `Identity*` tables.

Likewise, since the `IdentityLogonEvents` table holds authentication activity information from both Microsoft Defender for Cloud Apps and Defender for Identity, you need to have manage permissions for both services to manage custom detections querying the said table.

> [!NOTE]
> To manage custom detections, Security Operators must have the Manage Security Settings permission in Microsoft Defender for Endpoint if RBAC is turned on.

To manage required permissions, a Global Administrator can:

- Assign the Security Administrator or Security Operator role in [Microsoft 365 admin center](https://admin.microsoft.com/) under **Roles** \> **Security Administrator**.

- Check RBAC settings for Microsoft Defender for Endpoint in [Microsoft Defender XDR](https://security.microsoft.com/) under **Settings** \> **Permissions** > **Roles**. Select the corresponding role to assign the **manage security settings** permission.

> [!NOTE]
> A user also needs to have the appropriate permissions for the devices in the [device scope](#5-set-the-rule-scope) of a custom detection rule that they're creating or editing before they can proceed. A user can't edit a custom detection rule that is scoped to run on all devices, if the same user doesn't have permissions for all devices. 

## Create a custom detection rule

### 1. Prepare the query

In the Microsoft Defender portal, go to **Advanced hunting** and select an existing query or create a new query. When using a new query, run the query to identify errors and understand possible results.

> [!IMPORTANT]
> To prevent the service from returning too many alerts, each rule is limited to generating only 100 alerts whenever it runs. Before creating a rule, tweak your query to avoid alerting for normal, day-to-day activity.

#### Required columns in the query results


To create a custom detection rule, the query must return the following columns:
1. `Timestamp` - This column is used to set the timestamp for generated alerts. The `Timestamp` that is returned from the query should not have been manipulated in the query and should be returned exactly as it appears in the raw event.
   
3. A column or combination of columns that uniquely identify the event in Defender XDR tables:
      - For Microsoft Defender for Endpoint tables, the `Timestamp`, `DeviceId`, and `ReportId` columns must appear in the same event
      - For Alert* tables, `Timestamp` must appear in the event
      - For Observation* tables, `Timestamp`and `ObservationId` must appear in the same event
      - For all others, `Timestamp` and `ReportId` must appear in the same event
4. One of the following columns that contain a strong identifier for an impacted asset:
      - `DeviceId`
      - `DeviceName`
      - `RemoteDeviceName`
      - `RecipientEmailAddress`
      - `SenderFromAddress` (envelope sender or Return-Path address)
      - `SenderMailFromAddress` (sender address displayed by email client)
      - `RecipientObjectId`
      - `AccountObjectId`
      - `AccountSid`
      - `AccountUpn`
      - `InitiatingProcessAccountSid`
      - `InitiatingProcessAccountUpn`
      - `InitiatingProcessAccountObjectId`

> [!NOTE]
> Support for more entities will be added as new tables are added to the [advanced hunting schema](advanced-hunting-schema-tables.md).



Simple queries, such as those that don't use the `project` or `summarize` operator to customize or aggregate results, typically return these common columns.

There are various ways to ensure more complex queries return these columns. For example, if you prefer to aggregate and count by entity under a column such as `DeviceId`, you can still return `Timestamp` and `ReportId` by getting it from the most recent event involving each unique `DeviceId`.

> [!IMPORTANT]
> Avoid filtering custom detections using the `Timestamp` column. The data used for custom detections is prefiltered based on the detection frequency.

The sample query below counts the number of unique devices (`DeviceId`) with antivirus detections and uses this count to find only the devices with more than five detections. To return the latest `Timestamp` and the corresponding `ReportId`, it uses the `summarize` operator with the `arg_max` function.

```kusto
DeviceEvents
| where ingestion_time() > ago(1d)
| where ActionType == "AntivirusDetection"
| summarize (Timestamp, ReportId)=arg_max(Timestamp, ReportId), count() by DeviceId
| where count_ > 5
```

> [!TIP]
> For better query performance, set a time filter that matches your intended run frequency for the rule. Since the least frequent run is _every 24 hours_, filtering for the past day covers all new data.

### 2. Create new rule and provide alert details

With the query in the query editor, select **Create detection rule** and specify the following alert details:

- **Detection name** - Name of the detection rule; should be unique
- **Frequency** - Interval for running the query and taking action. [See more guidance in the rule frequency section](#rule-frequency)
- **Alert title** - Title displayed with alerts triggered by the rule; should be unique and in plaintext. Strings are sanitized for security purposes so HTML, Markdown, and other code won't work. Any URLs included in the title should follow the [percent-encoding format](https://en.m.wikipedia.org/wiki/Percent-encoding) for them to display properly.
- **Severity** - Potential risk of the component or activity identified by the rule.
- **Category** - Threat component or activity identified by the rule.
- **MITRE ATT&CK techniques** - One or more attack techniques identified by the rule as documented in the [MITRE ATT&CK framework](https://attack.mitre.org/). This section is hidden for certain alert categories, including malware, ransomware, suspicious activity, and unwanted software.
- **Threat analytics report** - Link the generated alert to an existing threat analytics report so that it appears in the [Related incidents](threat-analytics.md#set-up-custom-detections-and-link-them-to-threat-analytics-reports) tab in threat analytics
- **Description** - More information about the component or activity identified by the rule. Strings are sanitized for security purposes so HTML, Markdown, and other code won't work. Any URLs included in the description should follow the percent-encoding format for them to display properly.
- **Recommended actions** - Additional actions that responders might take in response to an alert.


#### Rule frequency

When you save a new rule, it runs and checks for matches from the past 30 days of data. The rule then runs again at fixed intervals, applying a lookback period based on the frequency you choose:

- **Every 24 hours** - Runs every 24 hours, checking data from the past 30 days.
- **Every 12 hours** - Runs every 12 hours, checking data from the past 48 hours.
- **Every 3 hours** - Runs every 3 hours, checking data from the past 12 hours.
- **Every hour** - Runs hourly, checking data from the past 4 hours.
- **Continuous (NRT)** - Runs continuously, checking data from events as they're collected and processed in near real-time (NRT), see [Continuous (NRT) frequency](custom-detection-rules.md#continuous-nrt-frequency).

> [!TIP]
> Match the time filters in your query with the lookback period. Results outside of the lookback period are ignored.

When you edit a rule, the changes are applied in the next run time scheduled according to the frequency you set. The rule frequency is based on the event timestamp and not the ingestion time. There might also be small delays in specific runs, whereby the configured frequency is not 100% accurate.


##### Continuous (NRT) frequency

Setting a custom detection to run in Continuous (NRT) frequency allows you to increase your organization's ability to identify threats faster. Using the Continuous (NRT) frequency has minimal to no impact to your resource usage and should thus be considered for any qualified custom detection rule in your organization.

From the custom detection rules page, you can migrate custom detections rules that fit the Continuous (NRT) frequency with a single button, **Migrate now**:

:::image type="content" source="media/custom-detection-migrate-now.png" alt-text="Screenshot of the migrate now button in advanced hunting." lightbox="media/custom-detection-migrate-now.png":::


Selecting **Migrate now** gives you a list of all compatible rules according to their KQL query. You can choose to migrate all or selected rules only according to your preferences:

:::image type="content" source="media/custom-detection-compatible-queries.png" alt-text="Screenshot of the continuous frequency compatible queries in advanced hunting." lightbox="media/custom-detection-compatible-queries.png":::

Once you click **Save**, the selected rules' frequency gets updated to Continuous (NRT) frequency.

###### Queries you can run continuously

You can run a query continuously as long as:

- The query references one table only.
- The query uses an operator from the list of **[Supported KQL features](/azure/azure-monitor/essentials/data-collection-transformations-structure#supported-kql-features)**. (For `matches regex`, regular expressions must be encoded as string literals and follow the string quoting rules. For example, the regular expression `\A` is represented in KQL as `"\\A"`. The extra backslash indicates that the other backslash is part of the regular expression `\A`.)
- The query doesn't use joins, unions, or the `externaldata` operator.
- The query doesn't include any comments line/information.

###### Tables that support Continuous (NRT) frequency

Near real-time detections are supported for the following tables:

- `AlertEvidence`
- `CloudAppEvents`
- `DeviceEvents`
- `DeviceFileCertificateInfo`
- `DeviceFileEvents`
- `DeviceImageLoadEvents`
- `DeviceLogonEvents`
- `DeviceNetworkEvents`
- `DeviceNetworkInfo`
- `DeviceInfo`
- `DeviceProcessEvents`
- `DeviceRegistryEvents`
- `EmailAttachmentInfo`
- `EmailEvents` (except `LatestDeliveryLocation` and `LatestDeliveryAction` columns)
- `EmailPostDeliveryEvents`
- `EmailUrlInfo`
- `IdentityDirectoryEvents`
- `IdentityLogonEvents`
- `IdentityQueryEvents`
- `UrlClickEvents`

> [!NOTE]
> Only columns that are generally available can support **Continuous (NRT)** frequency.

### 3. Choose the impacted entities

Identify the columns in your query results where you expect to find the main affected or impacted entity. For example, a query might return sender (`SenderFromAddress` or `SenderMailFromAddress`) and recipient (`RecipientEmailAddress`) addresses. Identifying which of these columns represent the main impacted entity helps the service aggregate relevant alerts, correlate incidents, and target response actions.

You can select only one column for each entity type (mailbox, user, or device). Columns that aren't returned by your query can't be selected.

### 4. Specify actions

Your custom detection rule can automatically take actions on devices, files, users, or emails that are returned by the query.

:::image type="content" source="/defender/media/ah-custom-actions.png" alt-text="Screenshot that shows actions for custom detections in the Microsoft Defender portal." lightbox="/defender/media/ah-custom-actions.png":::

#### Actions on devices

These actions are applied to devices in the `DeviceId` column of the query results:

- **Isolate device** - Uses Microsoft Defender for Endpoint to apply full network isolation, preventing the device from connecting to any application or service. [Learn more about Microsoft Defender for Endpoint machine isolation](/windows/security/threat-protection/microsoft-defender-atp/respond-machine-alerts#isolate-devices-from-the-network).
- **Collect investigation package** - Collects device information in a ZIP file. [Learn more about the Microsoft Defender for Endpoint investigation package](/windows/security/threat-protection/microsoft-defender-atp/respond-machine-alerts#collect-investigation-package-from-devices).
- **Run antivirus scan** - Performs a full Microsoft Defender Antivirus scan on the device.
- **Initiate investigation** - Initiates an [automated investigation](m365d-autoir.md) on the device.
- **Restrict app execution** - Sets restrictions on device to allow only files that are signed with a Microsoft-issued certificate to run. [Learn more about app restrictions with Microsoft Defender for Endpoint](/defender-endpoint/respond-machine-alerts#restrict-app-execution).

#### Actions on files

- When selected, the **Allow/Block** action can be applied to the file. Blocking files are only allowed if you have *Remediate* permissions for files and if the query results have identified a file ID, such as an SHA1. Once a file is blocked, other instances of the same file in all devices are also blocked. You can control which device group the blocking is applied to, but not specific devices.

- When selected, the **Quarantine file** action can be applied to files in the `SHA1`, `InitiatingProcessSHA1`, `SHA256`, or `InitiatingProcessSHA256` column of the query results. This action deletes the file from its current location and places a copy in quarantine.

#### Actions on users

- When selected, the **Mark user as compromised** action is taken on users in the `AccountObjectId`, `InitiatingProcessAccountObjectId`, or `RecipientObjectId` column of the query results. This action sets the users risk level to "high" in Microsoft Entra ID, triggering corresponding [identity protection policies](/azure/active-directory/identity-protection/overview-identity-protection).

- Select **Disable user** to temporarily prevent a user from logging in.
- Select **Force password reset** to prompt the user to change their password on the next sign in session.
- Both the `Disable user` and `Force password reset` options require the user SID, which are in the columns `AccountSid`, `InitiatingProcessAccountSid`, `RequestAccountSid`, and `OnPremSid`.

For more details on user actions, read [Remediation actions in Microsoft Defender for Identity](/defender-for-identity/remediation-actions).

#### Actions on emails

- If the custom detection yields email messages, you can select **Move to mailbox folder** to move the email to  a selected folder (any of **Junk**, **Inbox**, or **Deleted items** folders). Specifically, you can move email results from quarantined items (for instance, in the case of false positives) by selecting the **Inbox** option.

   :::image type="content" source="media/advanced-hunting-custom-quarantine-results.png" alt-text="Screenshot of the Inbox option under custom detections in the Microsoft Defender portal." lightbox="media/advanced-hunting-custom-quarantine-results.png":::
  :::image type="content" source="media/advanced-hunting-custom-quarantine-results.png" alt-text="Screenshot of the Inbox option under custom detections in the Microsoft Defender portal." lightbox="media/advanced-hunting-custom-quarantine-results.png":::

- Alternatively, you can select **Delete email** and then choose to either move the emails to Deleted Items (**Soft delete**) or delete the selected emails permanently (**Hard delete**).

The columns `NetworkMessageId` and `RecipientEmailAddress` must be present in the output results of the query to apply actions to email messages.

### 5. Set the rule scope

Set the scope to specify which devices are covered by the rule. The scope influences rules that check devices and doesn't affect rules that check only mailboxes and user accounts or identities.

When setting the scope, you can select:

- All devices
- Specific device groups

Only data from devices in the scope will be queried. Also, actions are taken only on those devices.

> [!NOTE]
> Users are able to create or edit a custom detection rule only if they have the corresponding permissions for the devices included in the scope of the rule. For instance, admins can only create or edit rules that are scoped to all device groups if they have permissions for all device groups. 

### 6. Review and turn on the rule

After reviewing the rule, select **Create** to save it. The custom detection rule immediately runs. It runs again based on configured frequency to check for matches, generate alerts, and take response actions.

> [!IMPORTANT]
> Custom detections should be regularly reviewed for efficiency and effectiveness. For guidance on how to optimize your queries, follow the **[Advanced hunting query best practices](advanced-hunting-best-practices.md)**. To make sure you're creating detections that trigger true alerts, take time to review your existing custom detections by following the steps in **[Manage existing custom detection rules](custom-detection-manage.md)**.
>
> You maintain control over the broadness or specificity of your custom detections so any false alerts generated by custom detections might indicate a need to modify certain parameters of the rules.



## See also

- [Custom detections overview](custom-detections-overview.md)
- [Manage custom detections](custom-detection-manage.md)
- [Advanced hunting overview](advanced-hunting-overview.md)
- [Learn the advanced hunting query language](advanced-hunting-query-language.md)
- [Migrate advanced hunting queries from Microsoft Defender for Endpoint](advanced-hunting-migrate-from-mde.md)
- [Microsoft Graph security API for custom detections](/graph/api/resources/security-api-overview?view=graph-rest-beta&preserve-view=true#custom-detections)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
