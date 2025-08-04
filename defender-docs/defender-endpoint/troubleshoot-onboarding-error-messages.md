---
title: Troubleshoot onboarding issues and error messages
description: Troubleshoot onboarding issues and error message while completing setup of Microsoft Defender for Endpoint.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.topic: troubleshooting
ms.subservice: onboard
search.appverid: met150
ms.date: 07/18/2024
---

# Troubleshoot subscription and portal access issues

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

This page provides detailed steps to troubleshoot issues that might occur when setting up your Microsoft Defender for Endpoint service.

If you receive an error message, Microsoft Defender XDR provides a detailed explanation on what the issue is and relevant links are supplied.

## No subscriptions found

If, while you're accessing Microsoft Defender XDR, you get an error message that says, "No subscriptions found," it means that the Microsoft Entra ID used to sign into the Microsoft Defender portal doesn't have a license for Defender for Endpoint.

Potential reasons:

- The Windows E5 and Office E5 licenses are separate licenses.
- The license was purchased but not provisioned to this Microsoft Entra instance.
  - It could be a license provisioning issue.
  - It could be you inadvertently provisioned the license to a different Microsoft Entra ID than the one used for authentication into the service.

For both cases, you should contact Microsoft support at [General Microsoft Defender for Endpoint Support](https://support.microsoft.com/getsupport?wf=0&tenant=ClassicCommercial&oaspworkflow=start_1.0.0.0&locale=en-us&supportregion=en-us&pesid=16055&ccsid=636419533611396913) or
[Volume license support](https://www.microsoft.com/licensing/servicecenter/Help/Contact.aspx).

:::image type="content" source="media/atp-no-subscriptions-found.png" alt-text="The No subscriptions found page" lightbox="media/atp-no-subscriptions-found.png":::

## Your subscription has expired

If while accessing Microsoft Defender XDR you get a **Your subscription has expired** message, your online service subscription has expired. Microsoft Defender for Endpoint subscription, like any other online service subscription, has an expiration date.

You can choose to renew or extend the license at any point in time. When accessing the portal after the expiration date, a message appears that says, "Your subscription has expired." The message includes an option to download the device offboarding package, just in case you choose to not renew your subscription.

> [!NOTE]
> For security reasons, the package used to Offboard devices will expire seven days after the date it was downloaded. Expired offboarding packages sent to a device are rejected. When downloading an offboarding package, you're notified of the package's expiry date and it is also included in the package name.

:::image type="content" source="media/atp-subscription-expired.png" alt-text="The subscription expired notification message" lightbox="media/atp-subscription-expired.png":::

## You are not authorized to access the portal

If you receive a message that says, "You are not authorized to access the portal," it's most likely because you haven't been granted access to the Microsoft Defender portal. Defender for Endpoint is a security monitoring, incident investigation and response product, and as such, access to it's restricted and controlled by your organization's security team. For more information, see, [**Assign user access to the portal**](/windows/threat-protection/windows-defender-atp/assign-portal-access-windows-defender-advanced-threat-protection).

:::image type="content" source="media/atp-not-authorized-to-access-portal.png" alt-text="The access disallowed notification message" lightbox="media/atp-not-authorized-to-access-portal.png":::

## Data currently isn't available on some sections of the portal

If the portal dashboard and other sections show an error message, such as "Data currently isn't available," you might need to allow subdomains.

:::image type="content" source="media/atp-data-not-available.png" alt-text="The data unavailability notification message" lightbox="media/atp-data-not-available.png":::

You need to allow the `security.windows.com` and all subdomains under it on your web browser. For example, `*.security.windows.com`.

## Portal communication issues

If you encounter issues with accessing the portal, missing data, or restricted access to portions of the portal, you need to verify that the following URLs are accessible through the browser for authorized users:

- `*.blob.core.windows.net`
- `crl.microsoft.com`
- `https://*.microsoftonline-p.com`
- `https://*.security.microsoft.com`
- `https://automatediracs-eus-prd.security.microsoft.com`
- `https://login.microsoftonline.com`
- `https://login.windows.net`
- `https://onboardingpackagescusprd.blob.core.windows.net`
- `https://secure.aadcdn.microsoftonline-p.com`
- `https://security.microsoft.com`
- `https://static2.sharepointonline.com`
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
