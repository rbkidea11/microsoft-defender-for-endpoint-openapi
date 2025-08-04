---
title: Access the Microsoft Defender XDR MSSP customer portal
description: Access the Microsoft Defender XDR MSSP customer portal
ms.service: defender-endpoint
ms.subservice: onboard
ms.author: ewalsh
author: emmwalshh
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.topic: how-to
search.appverid: met150
ms.date: 03/21/2025
---

# Access the Microsoft Defender XDR MSSP customer portal

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

> [!IMPORTANT]
> Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

> [!NOTE]
> These set of steps are directed towards the MSSP.

By default, MSSP customers access their Microsoft Defender XDR tenant through the following URL: `https://security.microsoft.com/`.

MSSPs however, will need to use a tenant-specific URL in the following format: `https://security.microsoft.com?tid=customer_tenant_id` to access the MSSP customer portal.

In general, MSSPs will need to be added to each of the MSSP customer's Microsoft Entra ID that they intend to manage.

Use the following steps to obtain the MSSP customer tenant ID and then use the ID to access the tenant-specific URL:

1. As an MSSP, log in to Microsoft Entra ID with your credentials.
2. Switch directory to the MSSP customer's tenant.
3. Select **Microsoft Entra ID > Properties**. You'll find the tenant ID in the Tenant ID field.
4. Access the MSSP customer portal by replacing the `customer_tenant_id` value in the following URL: `https://security.microsoft.com/?tid=customer_tenant_id`.
5. Access a Unified View for MSSP (Preview) in `https://mto.security.microsoft.com/`

## Related topics

- [Grant MSSP access to the portal](grant-mssp-access.md)
- [Configure alert notifications](configure-mssp-notifications.md)
- [Fetch alerts from customer tenant](api/fetch-alerts-mssp.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
