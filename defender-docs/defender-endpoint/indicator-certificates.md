---
title: Create indicators based on certificates
ms.reviewer:
description: Create indicators based on certificates that define the detection, prevention, and exclusion of entities.
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
ms.date: 03/04/2025
---

# Create indicators based on certificates

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]


**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

You can create indicators for certificates. Some common use cases include:

- Scenarios when you need to deploy blocking technologies, such as [attack surface reduction rules](attack-surface-reduction.md) but need to allow behaviors from signed applications by adding the certificate in the allowlist.
- Blocking the use of a specific signed application across your organization. By creating an indicator to block the certificate of the application, Microsoft Defender Antivirus prevents file executions (block and remediate), and automated investigation and remediation behaves the same.

## Before you begin

It's important to understand the following requirements before creating indicators for certificates:

- This feature is available if your organization uses Microsoft Defender Antivirus (in active mode) and cloud-based protection is enabled. For more information, see [Manage cloud-based protection](/windows/security/threat-protection/microsoft-defender-antivirus/deploy-manage-report-microsoft-defender-antivirus).
- The anti-malware client version must be `4.18.1901.x` or later.
- Supported on machines on Windows 10, version 1703 or later, Windows Server 2025, Windows Server 2022, Windows Server 2019, Windows Server 2016, and Windows Server 2012 R2.

  > [!NOTE]
  > Windows Server 2016 and Windows Server 2012 R2 must be onboarded using the instructions in [Onboard Windows Server 2012 R2 and Windows Server 2016 to Microsoft Defender for Endpoint](onboard-server.md) for this feature to work.

- The virus and threat protection definitions must be up to date.
- This feature currently supports entering .CER or .PEM file extensions.

> [!IMPORTANT]
>
> - A valid leaf certificate is a signing certificate that has a valid certification path and must be chained to the Root Certificate Authority (CA) trusted by Microsoft. Alternatively, a custom (self-signed) certificate can be used as long as it's trusted by the client (Root CA certificate is installed under the Local Machine 'Trusted Root Certification Authorities').
> - The children or parent of the allow/block certificate IOCs aren't included in the allow/block IoC functionality, only leaf certificates are supported.
> - Microsoft signed certificates can't be blocked.

## Create an indicator for certificates from the settings page:

> [!IMPORTANT]
> It can take up to 3 hours to create and remove a certificate IoC.

1. In the navigation pane, select **Settings** \> **Endpoints** \> **Indicators** (under **Rules**).

2. Select **Add indicator**.

3. Specify the following details:

   - **Indicator**: Specify the entity details and define the expiration of the indicator.
   - **Action**: Specify the action to be taken and provide a description.
   - **Scope**: Define the scope of the machine group.

4. Review the details on the **Summary** tab, and then select **Save**.

## Related articles

- [Create indicators](indicators-overview.md)
- [Create indicators for files](indicator-file.md)
- [Create indicators for IPs and URLs/domains](indicator-ip-domain.md)
- [Manage indicators](indicator-manage.md)
- [Exclusions for Microsoft Defender for Endpoint and Microsoft Defender Antivirus](defender-endpoint-antivirus-exclusions.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
