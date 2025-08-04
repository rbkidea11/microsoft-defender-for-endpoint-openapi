---
title: Manage endpoint security policies in Microsoft Defender for Endpoint
description: Learn how to set windows, mac, and linux endpoint security policies such as antivirus, firewall, endpoint detection and response in Microsoft Defender for Endpoint.
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
ms.date: 05/28/2025
---

# Manage endpoint security policies in Microsoft Defender for Endpoint

[!Include[Prerelease information](../includes/prerelease.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](defender-endpoint-plan-1.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)


Use security policies to manage security settings on devices. As a Security Administrator, you can configure security policy settings in the Microsoft Defender portal. 

> [!IMPORTANT]
> Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. Global Administrator is a highly privileged role that should be limited to emergency scenarios when you can't use an existing role.

You'll find endpoint security policies under **Endpoints** > **Configuration management** > **Endpoint security policies**.

> [!NOTE]
> The **Endpoint Security Policies** page in the Microsoft Defender portal ([https://security.microsoft.com](https://security.microsoft.com)) is available only for users who have access to all devices and possess `Core security settings (manage)` permissions. Any user role without these permissions, such as `Security Reader`, cannot access the portal. When a user has the required permissions to view policies in the Microsoft Defender portal, the data is presented based on Intune permissions. If the user is in scope for Intune role-based access control, it applies to the list of policies presented in the Microsoft Defender portal. We recommend granting security administrators with the [Intune built-in role, "Endpoint Security Manager"](/mem/intune/fundamentals/role-based-access-control#built-in-roles) to effectively align the level of permissions between Intune and the Microsoft Defender portal.

:::image type="content" source="./media/endpoint-security-policies.png" alt-text="Managing Endpoint security policies in the Microsoft Defender portal":::

The following list provides a brief description of each endpoint security policy type:

- **Antivirus** - Antivirus policies help security admins focus on managing the discrete group of antivirus settings for managed devices. 

- **Disk encryption** - Endpoint security disk encryption profiles focus on only the settings that are relevant for a devices built-in encryption method, like FileVault or BitLocker. This focus makes it easy for security admins to manage disk encryption settings without having to navigate a host of unrelated settings.

- **Firewall** - Use the endpoint security Firewall policy in Intune to configure a devices built-in firewall for devices that run macOS and Windows 10/11.

- **Endpoint detection and response** - When you integrate Microsoft Defender for Endpoint with Intune, use the endpoint security policies for endpoint detection and response (EDR) to manage the EDR settings and onboard devices to Microsoft Defender for Endpoint.

- **Attack surface reduction** - When Microsoft Defender Antivirus is in use on your Windows 10/11 devices, use Intune endpoint security policies for attack surface reduction to manage those settings for your devices.


## Create an endpoint security policy

1. Sign in to the [Microsoft Defender portal](https://security.microsoft.com) using at least a Security Administrator role.

2. Select **Endpoints > Configuration management > Endpoint security policies** and then select **Create new Policy**. 

3. Select a platform from the dropdown list.

4. Select a template, then select **Create policy**.


5. On the **Basics** page, enter a name and description for the profile, then choose **Next**.

6. On the **Settings** page, expand each group of settings, and configure the settings you want to manage with this profile.

   When you're done configuring settings, select **Next**.

7. On the **Assignments** page, select the groups that will receive this profile. 

   Select **Next**.

8. On the **Review + create** page, when you're done, select **Save**. The new profile is displayed in the list when you select the policy type for the profile you created.

> [!NOTE]
> To edit the scope tags, you'll need to go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

## To edit an endpoint security policy

1. Select the new policy, and then select **Edit**.
 
2. Select **Settings** to expand a list of the configuration settings in the policy. You can't modify the settings from this view, but you can review how they're configured.

3. To modify the policy, select **Edit** for each category where you want to make a change:
   - Basics
   - Settings
   - Assignments

4. After you've made changes, select **Save** to save your edits.  Edits to one category must be saved before you can introduce edits to additional categories.

## Verify endpoint security policies

To verify that you have successfully created a policy, select a policy name from the list of endpoint security policies.

> [!NOTE]
> It can take up to 90 minutes for a policy to reach a device. To expedite the process, for devices Managed by Defender for Endpoint, you can select **Policy sync** from the actions menu so that it is applied in approximately 10 minutes.
> :::image type="content" source="./media/policy-sync.png" alt-text="Image showing policy sync button":::

The policy page displays details that summarize the status of the policy. You can view a policy's status, which devices it has been applied to, and assigned groups.

During an investigation, you can also view the **Security policies** tab in the device page to view the list of policies that are being applied to a particular device. For more information, see [Investigating devices](investigate-machines.md).

:::image type="content" source="./media/security-policies-list.png" alt-text="Security policies tab with list of policies":::


[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
