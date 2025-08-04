---
title: Allow or block files using the Tenant Allow/Block List
f1.keywords:
  - NOCSH
ms.author: chrisda
author: chrisda
manager: deniseb
audience: ITPro
ms.topic: how-to
ms.localizationpriority: medium
search.appverid:
  - MET150
ms.collection:
  - m365-security
  - tier1
description: Admins can learn how to allow or block files in the Tenant Allow/Block List.
ms.service: defender-office-365
ms.date: 07/08/2025
appliesto:
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/eop-about" target="_blank">Default email protections for cloud mailboxes</a>
  - ✅ <a href="https://learn.microsoft.com/defender-office-365/mdo-about#defender-for-office-365-plan-1-vs-plan-2-cheat-sheet" target="_blank">Microsoft Defender for Office 365 Plan 1 and Plan 2</a>
  - ✅ <a href="https://learn.microsoft.com/defender-xdr/microsoft-365-defender" target="_blank">Microsoft Defender XDR</a>
---

# Allow or block files using the Tenant Allow/Block List

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

In all organizations with cloud mailboxes, admins can create and manage entries for files in the Tenant Allow/Block List. For more information about the Tenant Allow/Block List, see [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about.md).

This article describes how admins can manage entries for files in the Microsoft Defender portal and in Exchange Online PowerShell.

## What do you need to know before you begin?

- You open the Microsoft Defender portal at <https://security.microsoft.com>. To go directly to the **Tenant Allow/Block Lists** page, use <https://security.microsoft.com/tenantAllowBlockList>. To go directly to the **Submissions** page, use <https://security.microsoft.com/reportsubmission>.

- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- You specify files by using the SHA256 hash value of the file. To find the SHA256 hash value of a file in Windows, run the following command in PowerShell:

  ```powershell
  Get-FileHash -Path "<Path>\<Filename>" -Algorithm SHA256
  ```

  An example value is `768a813668695ef2483b2bde7cf5d1b2db0423a0d3e63e498f3ab6f2eb13ea3a`. Perceptual hash (pHash) values aren't supported.

- Entry limits for files:
  - **Microsoft 365 organizations without Defender for Office 365**: A maximum of 1000 total file entries:
    - Allow entries: 500 maximum.
    - Block entries: 500 maximum
  - **Microsoft 365 organizations with Defender for Office 365 Plan 1 (included or in an add-on subscription)**: A maximum of 2000 total file entries:
    - Allow entries: 1000 maximum.
    - Block entries: 1000 maximum.
  - **Microsoft 365 organizations with Defender for Office 365 Plan 2 (included or in an add-on subscription)**: A maximum of 15000 total file entries:
    - Allow entries: 5000 maximum.
    - Block entries: 10000 maximum.

- You can enter a maximum of 64 characters in a file entry.

- An entry should be active within 5 minutes.

- You need to be assigned permissions before you can do the procedures in this article. You have the following options:
  - [Microsoft Defender XDR Unified role based access control (RBAC)](/defender-xdr/manage-rbac) (If **Email & collaboration** \> **Defender for Office 365** permissions is :::image type="icon" source="media/scc-toggle-on.png" border="false"::: **Active**. Affects the Defender portal only, not PowerShell): 
    - *Add and remove entries from the Tenant Allow/Block List*: Membership assigned with the following permissions:
      - **Authorization and settings/Security settings/Detection tuning (manage)**
    - *Read-only access to the Tenant Allow/Block List*: 
      - **Authorization and settings/Security settings/Read-only**.
      - **Authorization and settings/Security settings/Core Security settings (read)**.
  - [Exchange Online permissions](/exchange/permissions-exo/permissions-exo):
    - _Add and remove entries from the Tenant Allow/Block List_: Membership in one of the following role groups:
      - **Organization Management** or **Security Administrator** (Security admin role).
      - **Security Operator** (Tenant AllowBlockList Manager role): This permission works only when assigned directly in the **Exchange admin center** at <https://admin.exchange.microsoft.com> \> **Roles** \> **Admin Roles**.
    - _Read-only access to the Tenant Allow/Block List_: Membership in one of the following role groups:
      - **Global Reader**
      - **Security Reader**
      - **View-Only Configuration**
      - **View-Only Organization Management**
  - [Microsoft Entra permissions](/entra/identity/role-based-access-control/manage-roles-portal): Membership in the **Global Administrator**<sup>\*</sup>, **Security Administrator**, **Global Reader**, or **Security Reader** roles gives users the required permissions _and_ permissions for other features in Microsoft 365.

    > [!IMPORTANT]
    > <sup>\*</sup> Microsoft recommends that you use roles with the fewest permissions. Using lower permissioned accounts helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

- A **Files** tab is available on the **Submissions** page only in organizations with Microsoft Defender XDR or Microsoft Defender for Endpoint Plan 2. For information and instructions to submit files from the **Files** tab, see [Submit files in Microsoft Defender for Endpoint](/defender-endpoint/admin-submissions-mde).

## Create allow entries for files

You can't create allow entries for files directly in the Tenant Allow/Block List. Unnecessary allow entries expose your organization to malicious email that the system would otherwise filter.

Instead, you use the **Email attachments** tab on the **Submissions** page at <https://security.microsoft.com/reportsubmission?viewid=emailAttachment>. When you submit a blocked file as **I've confirmed it's clean**, you can select **Allow this file** to add an allow entry for the file on the **Files** tab on the **Tenant Allow/Block Lists** page. For instructions, see [Submit good email attachments to Microsoft](submissions-admin.md#report-good-email-attachments-to-microsoft).

[!INCLUDE [Allow entry facts](../includes/allow-entry-facts.md)]
>
> During time of click, the file allow entry overrides all filters associated with the file entity, which allows users to access the file.

## Create block entries for files

Email messages that contain these blocked files are blocked as *malware*. Messages that contain the blocked files are quarantined.

To create block entries for files, use either of the following methods:

- From the **Email attachments** tab on the **Submissions** page at <https://security.microsoft.com/reportsubmission?viewid=emailAttachment>. When you submit a file as **I've confirmed it's a threat**, you can select **Block this file** to add a block entry to the **Files** tab on the **Tenant Allow/Block Lists** page. For instructions, see [Report questionable email attachments to Microsoft](submissions-admin.md#report-questionable-email-attachments-to-microsoft).

- From the **Files** tab on the **Tenant Allow/Block Lists** page or in PowerShell as described in this section.

### Use the Microsoft Defender portal to create block entries for files in the Tenant Allow/Block List

1. In the Microsoft Defender portal at <https://security.microsoft.com>, go to **Policies & rules** \> **Threat Policies** \> **Rules** section \> **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use <https://security.microsoft.com/tenantAllowBlockList>.

2. On the **Tenant Allow/Block Lists** page, select the **Files** tab.

3. On the **Files** tab, select :::image type="icon" source="media/m365-cc-sc-create-icon.png" border="false"::: **Add**, and then select **Block**.

4. In the **Block files** flyout that opens, configure the following settings:

   - **Add file hashes**: Enter one SHA256 hash value per line, up to a maximum of 20.

   - **Remove block entry after**: Select from the following values:
     - **1 day**
     - **7 days**
     - **30 days** (default)
     - **Never expire**
     - **Specific date**: The maximum value is 90 days from today.

   - **Optional note**: Enter descriptive text for why you're blocking the files.

   When you're finished in the **Block files** flyout, select **Add**.

Back on the **Files** tab, the entry is listed.

#### Use PowerShell to create block entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
New-TenantAllowBlockListItems -ListType FileHash -Block -Entries "HashValue1","HashValue2",..."HashValueN" <-ExpirationDate Date | -NoExpiration> [-Notes <String>]
```

This example adds a block entry for the specified files that never expires.

```powershell
New-TenantAllowBlockListItems -ListType FileHash -Block -Entries "768a813668695ef2483b2bde7cf5d1b2db0423a0d3e63e498f3ab6f2eb13ea3","2c0a35409ff0873cfa28b70b8224e9aca2362241c1f0ed6f622fef8d4722fd9a" -NoExpiration
```

For detailed syntax and parameter information, see [New-TenantAllowBlockListItems](/powershell/module/exchange/new-tenantallowblocklistitems).

## Use the Microsoft Defender portal to view entries for files in the Tenant Allow/Block List

In the Microsoft Defender portal at <https://security.microsoft.com>, go to **Policies & rules** \> **Threat Policies** \> **Tenant Allow/Block Lists** in the **Rules** section. Or, to go directly to the **Tenant Allow/Block Lists** page, use <https://security.microsoft.com/tenantAllowBlockList>.

Select the **Files** tab.

On the **Files** tab, you can sort the entries by clicking on an available column header. The following columns are available:

- **Value**: The file hash.
- **Action**: The available values are  **Allow** or **Block**.
- **Override verdicts**: The available values are **Up to malware** for both block and allow entries.
- **Modified by**
- **Last updated**
- **Last used date**: The date the entry was last used in the filtering system to override the verdict.
- **Remove on**: The expiration date.
- **Notes**

To filter the entries, select :::image type="icon" source="media/m365-cc-sc-filter-icon.png" border="false"::: **Filter**. The following filters are available in the **Filter** flyout that opens:

- **Action**: The available values are **Allow** and **Block**.
- **Never expire**: :::image type="icon" source="media/scc-toggle-on.png" border="false"::: or :::image type="icon" source="media/scc-toggle-off.png" border="false":::
- **Last updated**: Select **From** and **To** dates.
- **Last used date**: Select **From** and **To** dates.
- **Remove on**: Select **From** and **To** dates.
- **Modified by**: Provide an incomplete or complete email address to search by it. 

When you're finished in the **Filter** flyout, select **Apply**. To clear the filters, select :::image type="icon" source="media/m365-cc-sc-clear-filters-icon.png" border="false"::: **Clear filters**.

Use the :::image type="icon" source="media/m365-cc-sc-search-icon.png" border="false"::: **Search** box and a corresponding value to find specific entries.

To group the entries, select :::image type="icon" source="media/m365-cc-sc-group-icon.png" border="false"::: **Group** and then select **Action**. To ungroup the entries, select **None**.

### Use PowerShell to view entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Get-TenantAllowBlockListItems -ListType FileHash [-Allow] [-Block] [-Entry <FileHashValue>] [<-ExpirationDate Date | -NoExpiration>]
```

This example returns all allowed and blocked files.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash
```

This example returns information for the specified file hash value.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash -Entry "9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08"
```

This example filters the results by blocked files.

```powershell
Get-TenantAllowBlockListItems -ListType FileHash -Block
```

For detailed syntax and parameter information, see [Get-TenantAllowBlockListItems](/powershell/module/exchange/get-tenantallowblocklistitems).

## Use the Microsoft Defender portal to modify entries for files in the Tenant Allow/Block List

In existing file entries, you can change the expiration date and note.

1. In the Microsoft Defender portal at <https://security.microsoft.com>, go to **Policies & rules** \> **Threat Policies** \> **Rules** section \> **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use <https://security.microsoft.com/tenantAllowBlockList>.

2. Select the **Files** tab

3. On the **Files** tab, select the entry from the list by selecting the check box next to the first column, and then select the :::image type="icon" source="media/m365-cc-sc-edit-icon.png" border="false"::: **Edit** action that appears.

4. In the **Edit file** flyout that opens, the following settings are available:
   - **Block entries**:
     - **Remove block entry after**: Select from the following values:
       - **1 day**
       - **7 days**
       - **30 days**
       - **Never expire**
       - **Specific date**: The maximum value is 90 days from today.
     - **Optional note**
   - **Allow entries**:
     - **Remove allow entry after**: Select from the following values:
       - **1 day**
       - **7 days**
       - **30 days**
       - **45 days after last used date**
       - **Specific date**: The maximum value is 30 days from today.
     - **Optional note**

   When you're finished in the **Edit file** flyout, select **Save**.

> [!TIP]
> In the details flyout of an entry on the **Files** tab, use :::image type="icon" source="media/m365-cc-sc-view-submission-icon.png" border="false"::: **View submission** at the top of the flyout to go to the details of the corresponding entry on the **Submissions** page. This action is available if a submission was responsible for creating the entry in the Tenant Allow/Block List.

### Use PowerShell to modify existing allow or block entries for files in the Tenant Allow/Block List

In [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Set-TenantAllowBlockListItems -ListType FileHash <-Ids <Identity value> | -Entries <Value>> [<-ExpirationDate Date | -NoExpiration>] [-Notes <String>]
```

This example changes the expiration date of the specified file block entry.

```powershell
Set-TenantAllowBlockListItems -ListType FileHash -Entries "27c5973b2451db9deeb01114a0f39e2cbcd2f868d08cedb3e210ab3ece102214" -ExpirationDate "9/1/2022"
```

For detailed syntax and parameter information, see [Set-TenantAllowBlockListItems](/powershell/module/exchange/set-tenantallowblocklistitems).

## Use the Microsoft Defender portal to remove entries for files from the Tenant Allow/Block List

1. In the Microsoft Defender portal at <https://security.microsoft.com>, go to **Policies & rules** \> **Threat Policies** \> **Rules** section \> **Tenant Allow/Block Lists**. Or, to go directly to the **Tenant Allow/Block Lists** page, use <https://security.microsoft.com/tenantAllowBlockList>.

2. Select the **Files** tab.

3. On the **Files** tab, do one of the following steps:

   - Select the entry from the list by selecting the check box next to the first column, and then select the :::image type="icon" source="media/m365-cc-sc-delete-icon.png" border="false"::: **Delete** action that appears.
   - Select the entry from the list by clicking anywhere in the row other than the check box. In the details flyout that opens, select :::image type="icon" source="media/m365-cc-sc-delete-icon.png" border="false"::: **Delete** at the top of the flyout.

     > [!TIP]
     > To see details about other entries without leaving the details flyout, use :::image type="icon" source="media/updownarrows.png" border="false"::: **Previous item** and **Next item** at the top of the flyout.

4. In the warning dialog that opens, select **Delete**.

Back on the **Files** tab, the entry is no longer listed.

> [!TIP]
> You can select multiple entries by selecting each check box, or select all entries by selecting the check box next to the **Value** column header.

### Use PowerShell to remove entries for files from the Tenant Allow/Block List

In [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell), use the following syntax:

```powershell
Remove-TenantAllowBlockListItems -ListType FileHash <-Ids <Identity value> | -Entries <Value>>
```

This example removes the specified file block from the Tenant Allow/Block List.

```powershell
Remove-TenantAllowBlockListItems -ListType FileHash -Entries "27c5973b2451db9deeb01114a0f39e2cbcd2f868d08cedb3e210ab3ece102214"
```

For detailed syntax and parameter information, see [Remove-TenantAllowBlockListItems](/powershell/module/exchange/remove-tenantallowblocklistitems).

## Related articles

- [Use the Submissions page to submit suspected spam, phish, URLs, legitimate email getting blocked, and email attachments to Microsoft](submissions-admin.md)
- [Report false positives and false negatives](submissions-outlook-report-messages.md)
- [Manage allows and blocks in the Tenant Allow/Block List](tenant-allow-block-list-about.md)
- [Allow or block emails in the Tenant Allow/Block List](tenant-allow-block-list-email-spoof-configure.md)
- [Allow or block URLs in the Tenant Allow/Block List](tenant-allow-block-list-urls-configure.md)
- [Allow or block IPv6 addresses in the Tenant Allow/Block List](tenant-allow-block-list-ip-addresses-configure.md)
