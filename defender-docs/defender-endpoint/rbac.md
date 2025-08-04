---
title: Use role-based access control to grant fine-grained access to Microsoft Defender portal
description: Create roles and groups within your security operations to grant access to the portal.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection:
- m365-security
- tier2
ms.topic: how-to
search.appverid: met150
ms.date: 01/28/2025
---

# Manage portal access using role-based access control
> [!NOTE]
> If you are running the Microsoft Defender XDR preview program, you can now experience the new Microsoft Defender 365 Unified role-based access control (RBAC) model. For more information, see [Microsoft Defender 365 Unified role-based access control (RBAC)](/defender-xdr/manage-rbac).

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- Microsoft Entra ID
- Office 365

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

> [!IMPORTANT]
> Starting February 16, 2025, new Microsoft Defender for Endpoint customers will only have access to the Unified Role-Based Access Control (URBAC).
> Existing customers keep their current roles and permissions. For more information, see URBAC [Unified Role-Based Access Control (URBAC) for Microsoft Defender for Endpoint](/defender-xdr/manage-rbac)

Using role-based access control (RBAC), you can create roles and groups within your security operations team to grant appropriate access to the  portal. Based on the roles and groups you create, you have fine-grained control over what users with access to the portal can see and do.

> [!VIDEO https://learn-video.azurefd.net/vod/player?id=c9903800-3d26-4b30-bd0b-fed00dfc6a5c]

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

Large geo-distributed security operations teams typically adopt a tier-based model to assign and authorize access to security portals. Typical tiers include the following three levels:

|Tier|Description|
|---|---|
|Tier 1|**Local security operations team / IT team** <br/> This team usually triages and investigates alerts contained within their geolocation and escalates to Tier 2 in cases where an active remediation is required.|
|Tier 2|**Regional security operations team** <br/>This team can see all the devices for their region and perform remediation actions.|
|Tier 3|**Global security operations team** <br/>This team consists of security experts and is authorized to see and perform all actions from the portal.|

> [!NOTE]
> For Tier 0 assets, refer to [Privileged Identity Management](/azure/active-directory/privileged-identity-management/pim-configure) for security admins to provide more granular control of Microsoft Defender for Endpoint and Microsoft Defender XDR.

Defender for Endpoint RBAC is designed to support your tier- or role-based model of choice and gives you granular control over what roles can see, devices they can access, and actions they can take. The RBAC framework is centered around the following controls:

- **Control who can take specific action**
  - Create custom roles and control what Defender for Endpoint capabilities they can access with granularity.
- **Control who can see information on specific device group or groups**
  - [Create device groups](machine-groups.md) by specific criteria such as names, tags, domains, and others, then grant role access to them using a specific  Microsoft Entra user group.

    > [!NOTE]
    > Device group creation is supported in Defender for Endpoint Plan 1 and Plan 2.

To implement role-based access, you need to define admin roles, assign corresponding permissions, and assign Microsoft Entra user groups assigned to the roles.

## Before you begin

Before using RBAC, it's important that you understand the roles that can grant permissions and the consequences of turning on RBAC.

> [!WARNING]
> Before enabling the feature, it's important that you have an appropriate role, such as Security Administrator assigned in Microsoft Entra ID, and that you have your Microsoft Entra groups ready to reduce the risk of being locked out of the portal.

When you first sign in to the Microsoft Defender portal, you're granted either full access or read only access. Full access rights are granted to users with the Security Administrator role in Microsoft Entra ID. Read only access is granted to users with a Security Reader role in Microsoft Entra ID.

Someone with a Defender for Endpoint Global Administrator role has unrestricted access to all devices, regardless of their device group association and the Microsoft Entra user groups assignments.

> [!WARNING]
> Initially, only those with Microsoft Entra Global Administrator or Security Administrator rights can create and assign roles in the Microsoft Defender portal; therefore, having the right groups ready in Microsoft Entra ID is important.
>
> **Turning on role-based access control causes users with read-only permissions (for example, users assigned to Microsoft Entra Security reader role) to lose access until they are assigned to a role.**
>
> Users with administrator permissions are automatically assigned the default built-in Defender for Endpoint Global Administrator role with full permissions. After opting in to use RBAC, you can assign more users who aren't Microsoft Entra Global Administrators or Security Administrators to the Defender for Endpoint Global Administrator role.
>
> After opting in to use RBAC, you can't revert to the initial roles as when you first logged into the portal.

## Related article

- [RBAC roles](/defender-office-365/migrate-to-defender-for-office-365-onboard#rbac-roles)
- [Create and manage device groups in Microsoft Defender for Endpoint](machine-groups.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
