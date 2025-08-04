---
title: What's new in Microsoft Defender for Endpoint on Android
description: Learn about the major changes for previous versions of Microsoft Defender for Endpoint on Android.
ms.service: defender-endpoint
ms.author: ewalsh
author: emmwalshh
ms.localizationpriority: medium
manager: deniseb
ms.reviewer: denishdonga
audience: ITPro
ms.collection:
- m365-security
- tier3
- mde-android
ms.topic: reference
ms.subservice: android
search.appverid: met150
ms.date: 05/15/2025
---

# What's new in Microsoft Defender for Endpoint on Android

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**
- [Microsoft Defender for Endpoint](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)

Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://go.microsoft.com/fwlink/p/?linkid=2225630)

### Releases for Defender for Endpoint on Android

#### July 2025

|Build|1.0.7901.0101|
| -------- | -------- |
|Release Date|July 10, 2025|

**What's New**

UX Improvement for home page and tiles screens, for more details please visit this link - [Android UX Enhancement](/defender-endpoint/android-new-ux)

#### Alerts for activities related to open wireless connection and certificates are now detected as events

May 2025

Starting May 19, 2025, security operations center (SOC) analysts can now view the following as events instead of alerts:

- Connecting or disconnecting to open wireless networks
- Download/installation/removal of self-signed certificates

These events can be viewed in the Timeline tab of a device page. For more information, see [Network protection](android-configure.md#network-protection).

#### Deploy Defender for Endpoint prerelease builds on Android devices using Google Play preproduction tracks

April 2025

**Setup a secure environment to test prerelease builds of Defender for Endpoint on Android**. Learn the steps on how to set up your environment for prerelease testing of Defender for Endpoint on Android. These steps are for Android devices that are onboarded to Microsoft Defender for Endpoint through the following methods:

- Android Enterprise scenarios
- Mobile Application Mangement (MAM) enrollment scenarios

For more information, see [Deploy Defender for Endpoint prerelease builds on Android devices using Google Play preproduction tracks](mobile-pretest-android.md).

#### Defender for Endpoint on Android now supports Android 10 as the minimum version

February 2025

**Defender for Endpoint is ending support for Android 8, 8.1, and 9 on April 30, 2025**. Moving forward, only devices running Android 10 and later are supported.

**How does this change affect your organization's users?**

**New Users**: The application will no longer be available for new installations on devices running below Android 10. When users with Android versions below 10 attempt to download the Microsoft Defender app, Google Play store will notify them that the device is incompatible.

**Existing users**: The Microsoft Defender app continues to function for existing users on Android 8, 8.1, and 9 versions, but they don't receive updates from the Google Play store as they don't meet the minimum SDK version requirements. Therefore, any new updates on the app aren't available to users running an Android version prior to version 10.

After discontinuing support for deprecated versions, Microsoft no longer addresses bugs or provides maintenance for unsupported operating system versions. Any issues occurring on devices running Android version prior to version 10 won't be investigated.

This change is planned to go live on April 30, 2025. No explicit admin or end-user action is required.

#### Microsoft Defender for Mobile: Open Wi-Fi Detection Update

**February 2025:**

As part of our Microsoft Defender for Mobile application, we offer Open Wi-Fi detection within our Network Protection feature set. When enabled, this feature generates an alert in the Security portal. Currently, the alert is informational and doesn't require any action from the SOC analyst or admin. It provides valuable information that aids in triaging incidents involving mobile devices.

**Current Behavior:**

- Every time the end user connects to an open Wi-Fi network, an alert is raised.

- If the user goes out of the open Wi-Fi range and reconnects to the same network, another alert is raised.

Based on our research insights and inputs from Microsoft and other SOC teams, we're implementing a caching behavior to ensure the value of the alerts remains and also doesn't cause fatigue to SOC teams due to sheer volume.

**New behavior:**

- Every time the end user connects to an open Wi-Fi network, an alert is raised.

- If a user reconnects to the same open wi-fi in the next seven days, another alert won't be raised.

Please note that if a user connects to a different open Wi-Fi network, an alert is immediately generated, and there's no change to that behavior.

## Upgrading your experience: Upcoming enhancements you should know about

**January 2025**:

**Key changes**:

We're pleased to introduce the new dashboard for our enterprise users, which has been designed to be more user-friendly and accessible. The updated dashboard structure now includes recommendation cards for alerts and feature tiles.

Recommendation cards prominently display any active alerts, ensuring you stay informed. Additionally, features are now presented in the form of tiles, enhancing ease of use and navigation.

The following screenshot is an example of what the user sees in their dashboard:

:::image type="content" source="media/android-whatsnew/android-dashboard-screen.png" alt-text="Screenshot showing the user's dashboard in the Microsoft Defender app.":::

**Recommendation cards for alerts**:

The structure of the dashboard has been updated to include a recommendation card that contains active alerts (if any). In case there are multiple alerts, resolving the top alert brings forward the next one. Recommendation cards have been implemented to provide a more cohesive user experience. These cards are designed to display important alerts and notifications prominently on the dashboard, as shown in the following table:

| Card | Description |
|---|---|
| :::image type="content" source="media/android-whatsnew/android-connection-unsecured.png" alt-text="Screenshot of recommendation to connect to a secure network."::: | **Network protection** <br/>The user is advised to switch to a secure network. |
| :::image type="content" source="media/android-whatsnew/android-allow-vpn.png" alt-text="Screenshot showing a recommendation to set up a VPN connection."::: | **VPN option** <br/>The user is prompted to set up a VPN connection on their device. |
| :::image type="content" source="media/android-whatsnew/android-threat-found.png" alt-text="Screenshot showing a recommendation to take action on a detected threat."::: | **Malware detection** <br/>The user is prompted to take action on a detected threat. |

**Feature tiles**:

The current enterprise dashboard experience now features a tile view for your security team. The following table describes tiles your security team might see.

| Tile | Description |
|---|---|
| :::image type="content" source="media/android-whatsnew/android-tile-networkprotection.png" alt-text="Screenshot showing the network protection tile for security administrators."::: | **Network protection** <br/>The user can see whether a connection is secured or unsecured. |
| :::image type="content" source="media/android-whatsnew/android-tile-webprotection.png" alt-text="Screenshot of a tile that shows whether web protection is enabled on a device."::: | **Web protection** <br/>The user can see whether web protection is enabled on a user's device. |
| :::image type="content" source="media/android-whatsnew/android-tile-appsecurity.png" alt-text="Screenshot showing the app security tile."::: | **App security** <br/>The user can see whether any threats were found in apps installed on a user's device. |
| :::image type="content" source="media/android-whatsnew/android-tile-globalsecureaccess.png" alt-text="Screenshot showing Global Secure Access status."::: | **Global secure access** <br/>The user can see current connection status. |

## Android low-touch onboarding is now GA

**December 2024**:

**Key benefits**:

1. **Faster setup on Android devices** – Simplified Android onboarding supports silent sign-on and autogranting of certain permissions on a user's device. As such, users are required to grant only the necessary permissions to onboard to Defender for Endpoint.

2. **Intuitive guidance** - A clear and intuitive flow to guide users through each step.

3. **Broad coverage with support across multiple Android profiles** – Android enterprise BYOD, COPE, and fully managed.

**Configuring low-touch onboarding**:

Although low-touch onboarding is disabled by default, security administrators can enable it through app configuration policies in Intune. See [Android low-touch onboarding](/defender-endpoint/android-intune).

> [!IMPORTANT]
> **Ending support for device administrator enrolled devices**:
>
> Microsoft Intune and Defender for Endpoint are ending support for device administrator enrolled devices with access to [Google Mobile Services](/mem/intune/apps/manage-without-gms) (GMS), beginning December 31, 2024.
>
> **For devices with access to GMS**:
>
> After support ends for device administrator enrolled devices, devices with access to GMS will be affected in the following ways:
>
> - Intune and Defender for Endpoint won't make changes or updates to Android device administrator management, such as bug fixes, security fixes, or fixes to address changes in new Android versions.
> - Intune and Defender for Endpoint technical support will no longer support devices with access to GMS.
>
> For more information, see [Tech Community blog: Intune ending support for Android device administrator on devices with GMS in December 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-ending-support-for-android-device-administrator-on-devices-with-gms-in-de/3915443).

## Network protection

**Aug-2024 (version: 1.0.6812.0101)**:

- Network Protection feature is enabled by default for all users

Network protection on Microsoft Defender for Endpoint is now generally available. Network protection provides protection against rogue Wi-Fi related threats, rogue hardware like pineapple devices, and rogue certificates. It notifies the user if a related threat is detected. Users also see a guided experience to connect to secure networks and change networks when they're connected to an insecure connection.

> [!IMPORTANT]
> **This feature is now enabled by default for all users.** As a result, users are able to see a network protection card in the Defender for Endpoint app, along with App Protection and Web Protection. Users are also required to provide location permission to complete the setup. Administrators can change the default value for network protection if they decide not to use it via the Intune App Configuration policies. 
There are also several administrator controls to offer flexibility, including privacy controls to configure the data that's sent by Defender for Endpoint from Android devices. For more information, see [network protection](android-configure.md).

## Device tagging

Mobile Device Tagging is now generally available. This feature enables bulk tagging the mobile devices by allowing the administrators to set up tags via Intune. Administrators can configure the device tags through Intune via configuration policies and push them to user's devices. Once the user installs and activates Defender, the client app passes the device tags to the Security Portal. The Device tags appear against the devices in the Device Inventory.

This configuration is available for both the enrolled (MDM) devices and unenrolled (MAM) devices. For more information, see [Device Tagging (MDM)](android-configure.md#device-tagging) and [Device Tagging (MAM)](android-configure-mam.md#device-tagging).

## Microsoft Defender for Endpoint on company-owned personally enabled devices

Defender for Endpoint is now generally available on AE COPE devices. Enterprises can onboard devices on COPE mode and push Defender for Endpoint to user's devices through the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). With this support, Android Enterprise COPE devices get the full capabilities of our offering on Android, including:

- Phishing and web protection.
- Malware scanning.
- Network protection (preview).
- More breach prevention through integration with Microsoft Intune and Conditional Access.

Read the announcement [Tech Community Blog: Defender for Endpoint is now available on Android corporate-owned personally enabled devices](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/microsoft-defender-for-endpoint-is-now-available-on-android/ba-p/3626100).

## Privacy controls

Microsoft Defender for Endpoint on Android enables privacy controls for both administrators and end users, and includes controls for enrolled (MDM) and unenrolled (MAM) devices. Administrators can configure the privacy in the alert report while End Users can configure the information shared to their organization. For more information, see [privacy controls (MDM)](android-configure.md#privacy-controls) and [privacy controls (MAM)](android-configure-mam.md#configure-privacy-controls).

## Optional permissions and the ability to disable web protection

Microsoft Defender for Endpoint on Android enables **optional permissions** in the onboarding flow. Currently the permissions required by Defender for Endpoint are mandatory in the onboarding flow. With this feature, administrators can deploy Defender for Endpoint on devices without enforcing the mandatory **VPN** and **Accessibility** permissions during onboarding. End Users can onboard the app without the mandatory permissions and can later review these permissions. This feature is currently present only for unenrolled devices (MAM). For more information, see [optional permissions](android-configure-mam.md#optional-permissions).

## Microsoft Defender on Android enterprise BYOD personal profile

Microsoft Defender for Endpoint is now supported on Android Enterprise personal profile (BYOD only) with all the key features including malware scanning, protection from phishing links, network protection, and vulnerability management. This support is coupled with [privacy controls](android-configure.md#privacy-controls) to ensure user privacy on personal profile. For more information, read the [announcement](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/announcing-the-public-preview-of-defender-for-endpoint-personal/ba-p/3370979) and the [deployment guide](android-intune.md#set-up-microsoft-defender-in-personal-profile-on-android-enterprise-in-byod-mode).

## Microsoft Defender on Android app updates

Microsoft Defender is no longer supported for versions 1.0.3011.0302 or earlier. Users are requested to upgrade to latest versions to keep their devices secure.

To update, users can use the following steps:

1. On your work profile, go to Managed Play Store.

2. Tap on the profile icon on the top right corner and select **Manage apps and device**.

3. Locate Defender for Endpoint under updates available and select **Update**.

If you encounter any issues, [submit in-app feedback](android-support-signin.md#send-in-app-feedback).

## The Microsoft Defender for Endpoint app is now Microsoft Defender in the Play store

Microsoft Defender for Endpoint is now available as **Microsoft Defender** in the play store. With this update, the app is available as preview for **Consumers in the US region**. Based on how you log into the app with your work or personal account, you have access to features for Microsoft Defender for Endpoint or for Microsoft Defender for individuals. For more information, see [this blog](https://www.microsoft.com/microsoft-365/microsoft-defender-for-individuals?msockid=0f1c3b9963366db31ba02e78621b6c1e#Overview).

## Vulnerability management

On January 25, 2022, we announced the general availability of Vulnerability management on Android and iOS. For more information, see [the techcommunity post here](https://techcommunity.microsoft.com/t5/microsoft-defender-for-endpoint/announcing-general-availability-of-vulnerability-management/ba-p/3071663).

## Upcoming permission changes for Microsoft Defender for Endpoint running Android 11 or later (Nov 2021)

Release Build: `1.0.3501.0301`
Release month: Nov 2021
Microsoft Defender for Endpoint has released this update required by [Google](https://developer.android.com/distribute/play-policies#APILevel30) to upgrade to Android API 30. This change prompts users seeking access to [new storage permission](https://developer.android.com/training/data-storage/manage-all-files#all-files-access-google-play), for devices running Android 11 or later. Users need to accept this new storage permission once they update Defender app with the release build 1.0.3501.0301 or later. This update ensures that Defender for Endpoint's app security feature to function without any disruption. For more information, review the following sections.

**How this affects your organization**: These changes take effect if you're using Microsoft Defender for Endpoint on devices running Android 11 or later and updated Defender for Endpoint to release build 1.0.3501.0301 or later.

> [!NOTE]
> The new storage permissions can't be configured by administrators to auto approve through Microsoft Intune. Users must take action to provide access to this permission.

**User experience**: Users receive a notification indicating a missing permission for app security. If the user denies this permission, app security functionality is turned off on the device. If user doesn't accept or deny permission, they continue to receive the prompt when unlocking their device or opening the app, until it's approved.

> [!NOTE]
> If your organization is previewing the tamper protection feature and if the new storage permissions aren't granted by the user within seven days of updating to the latest version, the user might lose access to corporate resources.

**What you need to do to prepare**:

Notify your users and help desk (as applicable) that end users must accept the new permissions when prompted after they update Defender for Endpoint to build `1.0.3501.0301` or later. To accept the permissions, users should follow these steps:

1. Tap on the Defender for Endpoint in-app notification or open the Defender for Endpoint app. Users see a screen that lists the permissions needed. A green check mark is missing next to **Storage permission**.

2. Tap **Begin**.

3. Tap the toggle for **Allow access to manage all files**.

   The device is now protected.

   > [!NOTE]
   > This permission allows Microsoft Defender for Endpoint to access storage on user's device, which helps detect and remove malicious and unwanted apps. Microsoft Defender for Endpoint accesses/scans Android app package file (.apk) only. On devices with a Work Profile, Defender for Endpoint only scans work-related files.

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]

## See also

[What's new in Microsoft Defender for Endpoint on iOS](ios-whatsnew.md)
