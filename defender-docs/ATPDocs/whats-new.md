---
title: What's new | Microsoft Defender for Identity
description: This article is updated frequently to let you know what's new in the latest release of Microsoft Defender for Identity.
ms.date: 08/29/2024
ms.topic: overview
#CustomerIntent: As a Defender for Identity customer, I want to know what's new in the latest release of Defender for Identity, so that I can take advantage of new features and functionality. 
ms.reviewer: AbbyMSFT
---

# What's new in Microsoft Defender for Identity

This article is updated frequently to let you know what's new in the latest releases of Microsoft Defender for Identity.

## What's new scope and references

Defender for Identity releases are deployed gradually across customer tenants. If there's a feature documented here that you don't see yet in your tenant, check back later for the update.

For more information, see also:

- [What's new in Microsoft Defender XDR](/microsoft-365/security/defender/whats-new)
- [What's new in Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/whats-new-in-microsoft-defender-endpoint)
- [What's new in Microsoft Defender for Cloud Apps](/cloud-app-security/release-notes)

For updates about versions and features released six months ago or earlier, see the [What's new archive for Microsoft Defender for Identity](whats-new-archive.md).

## August 2025

### Sensor version 2.246

This version includes bug fixes and stability improvements for the Microsoft Defender for Identity sensor.

### Detection update: Suspected Brute Force attack (Kerberos, NTLM)

Improved detection logic to include scenarios where accounts were locked during attacks. As a result, the number of triggered alerts might increase.


## July 2025

### Identity scoping is now available in Governance environments

Scoping is now supported in government (GOV) environments. Organizations can now define and refine the scope of MDI monitoring and gain granular control over which entities and resources are included in security analysis.

For more information, see [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).

### New security posture assessments for unmonitored identity servers

Microsoft Defender for Identity three new security posture assessments detect when Microsoft Entra Connect, Active Directory Federation Services (ADFS), or Active Directory Certificate Services (ADCS) servers are present in your environment but aren't monitored.

Use these assessments to improve monitoring coverage and strengthen your hybrid identity security posture.

For more information, see:

[Security Assessment: Unmonitored ADCS servers](unmonitored-active-directory-certificate-services-server.md)

[Security Assessment: Unmonitored ADFS servers](unmonitored-active-directory-federation-services-servers.md)

[Security Assessment: Unmonitored Microsoft Entra Connect servers](unmonitored-entra-connect-servers.md)



## June 2025

### Scoped access by Active Directory domain now supported (Preview)

MDI scoping is now available as part of XDR User Role-Based Access Control (URBAC). Organizations can now define and refine the scope of MDI monitoring, providing granular control over which entities and resources are included in security analysis.

Scoping by Active Directory domains helps:

- Optimize performance: Focus monitoring on critical assets and reduce noise from non-essential data.

- Enhance visibility control: Tailor MDI coverage to specific domains and user groups.

- Support operational boundaries: Align access for SOC analysts, identity administrators, and regional teams.

For more information, see: [Configure scoped access for Microsoft Defender for Identity](configure-scoped-access.md).


### Okta integration is now available in Microsoft Defender for Identity

Microsoft Defender for Identity now supports integration with Okta, enabling detection of identity-based threats across cloud and on-premises environments. This integration helps identify suspicious sign-ins, risky role assignments, and potential privilege misuse within your Okta environment.

For prerequisites and configuration steps, see [Integrate Okta with Microsoft Defender for Identity](okta-integration.md).


### Service account classification rules now available

You can now create custom classification rules to identify service accounts based on your organization’s specific criteria. This complements automatic discovery, enabling more accurate identification of service accounts.
For more information, see [Service account discovery](service-account-discovery.md)

### Defender For Identity PowerShell module updates (version 1.0.0.4)

New Features and Improvements:
- Added remote domain functionality.
- Added SensorType parameter to Test-MDISensorApiConnection to inform endpoint URL.
- Added ability to Get/Set/Test the Deleted Objects container permissions.
- Added auditing for Delegated Managed Service Accounts (dMSA) in the DomainObjectAuditing configuration.

Bug Fixes:
- Fixed audit verification checks for non-English operating systems.
- Fixed DomainObjectAuditing identity redundant parameter bug.
- Fixed Domain Controller detection logic to confirm AD Web Services is running on the server.
- Fixed issue with Test-MDIDSA not parsing Deleted Object permissions.
- Other reliability fixes.


## May 2025

###  Expanded New Sensor Deployment Support for Domain Controllers (Preview)
Defender for Identity now supports deploying its new sensor on Domain Controllers without requiring Defender for Endpoint onboarding. This simplifies sensor activation and expands deployment flexibility. [Learn more](deploy/activate-sensor.md).


### Improved Visibility into Defender for Identity New Sensor Eligibility in the Activation page
The Activation Page now displays all servers from your device inventory, including those not currently eligible for the new Defender for Identity sensor. This enhancement increases transparency into sensor eligibility, helping you identify noneligible servers and take action to update and onboard them for enhanced identity protection.


### Local administrators collection (using SAM-R queries) feature is disabled
The remote collection of local administrators group members from endpoints using SAM-R queries in Microsoft Defender for Identity will be disabled by mid-May 2025. This data is currently used to build potential lateral movement path maps, which will no longer be updated after this change. An alternative method is being explored. The change occurs automatically by the specified date, and no administrative action is required.

### New Health Issue

New [health issue](health-alerts.md) for cases where sensors running on VMware have network configuration mismatch.

## April 2025

### Privileged Identity Tag Now Visible in Defender for Identity Inventory

Identities listed in the [Identity inventory](identity-inventory.md) in Microsoft Defender portal now include a **“Privileged account”** tag for accounts managed by a **Privileged Identity Management (PIM)** service.
Privileged accounts are prime targets for attackers. Tagging them in the inventory helps you quickly identify high-risk or high-value accounts, prioritize investigation and mitigation efforts, and streamline incident response workflows.

Learn more about [Privileged Identity Management](/entra/id-governance/privileged-identity-management/pim-configure)

### New Defender for Identity and PAM Integration

Microsoft Defender for Identity now supports integration with industry-leading Privileged Access Management (PAM) platforms to enhance detection and response for privileged identities.

**Supported PAM vendors**:

- CyberArk
- Delinea
- BeyondTrust

For more information, see: [Integrations Defender for Identity and PAM services.](Integrate-microsoft-and-pam-services.md)

## March 2025

### New Service Account Discovery page

Microsoft Defender for Identity now includes a Service Account Discovery capability, offering you  centralized visibility into service accounts across your Active Directory environment.

This update provides:

- Automatic identification of Group Managed Service Accounts, Managed Service Accounts, and user accounts operating as service accounts.

- A centralized Service Accounts inventory, displaying key attributes like account type, authentication type, unique connections, last log-on, service class and criticality.

- A Service Account details page, including an overview, a timeline of activities, alerts, and a new connections tab.

For more information, see: [Investigate and protect Service Accounts | Microsoft Defender for Identity](service-account-discovery.md).

### Enhanced Identity Inventory

The Identities page under *Assets* was updated to provide better visibility and management of identities across your environment.  
The updated Identities Inventory page now includes the following tabs:

- Identities: A consolidated view of identities across Active Directory, Entra ID. This Identities tab highlights key details, including identity types, and user's information. 

- Cloud application accounts: Displays a list of cloud application accounts, including those from application connectors and third-party sources (original available in the previous version based on Microsoft Defender for Cloud Apps). 

For more information, see [Identity inventory details](/defender-for-identity/identity-inventory). 

### New LDAP query events added to the IdentityQueryEvents table in Advanced Hunting
New LDAP query events were added to the `IdentityQueryEvents` table in Advanced Hunting to provide more visibility into additional LDAP search queries running in the customer environment.

## February 2025

### DefenderForIdentity PowerShell module updates (version 1.0.0.3)

New Features and Improvements:
- Support for getting, testing, and setting the Active Directory Recycle Bin in Get/Set/Test MDI Configuration.
- Support for getting, testing, and setting the proxy configuration on new MDI sensor.
- The Active Directory Certificate Services registry value for audit filtering now properly sets the type.
- New-MDIConfigurationReport now shows the name of the tested GPO and supports Server and Identity arguments.

Bug Fixes:
- Improved reliability for DeletedObjects container permissions on non-English operating systems.
- Fixed extraneous output for KDS root key creation.
- Other reliability fixes.

### New attack paths tab on the Identity profile page

This tab provides visibility into potential attack paths leading to a critical identity or involving it within the path, helping assess security risks. For more information, see [Overview of attack path within Exposure Management.](/security-exposure-management/work-attack-paths-overview) 

Additional identity page enhancements:

- New side panel with more information for each entry on the user timeline.

- Filtering capabilities on the Devices tab under Observed in organization.

### Updating 'Protect and manage local admin passwords with Microsoft LAPS' posture recommendation

This update aligns the security posture assessment within Secure Score with the latest version of [Windows LAPS](/windows-server/identity/laps/laps-overview), ensuring it reflects current security best practices for managing local administrator passwords.

### New and updated events in the Advanced hunting IdentityDirectoryEvents table

We have added and updated the following events in the `IdentityDirectoryEvents` table in Advanced Hunting:

- User Account control flag has been changed

- Security group creation in Active directory

- Failed attempt to change an account password

- Successful account password change

- Account primary group ID has been changed

Additionally, the **built-in schema reference** for Advanced Hunting in Microsoft Defender XDR has been updated to include detailed information on all supported event types (**`ActionType`** values) in identity-related tables, ensuring complete visibility into available events. For more information, see [Advanced hunting schema details](/defender-xdr/advanced-hunting-schema-tables).

## January 2025

### New Identity guide tour

Explore key MDI features with the new **Identities Tour** in the Microsoft 365 portal. Navigate Incidents, Hunting, and Settings to enhance identity security and threat investigation.

## December 2024

### New security posture assessment: Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)

Defender for Identity has added the new **Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)** recommendation in Microsoft Secure Score.

This recommendation directly addresses the recently published [CVE-2024-49019](https://msrc.microsoft.com/update-guide/en-US/advisory/CVE-2024-49019), which highlights security risks associated with vulnerable AD CS configurations. This security posture assessment lists all vulnerable certificate templates found in customer environments due to unpatched AD CS servers.

The new recommendation is added to other AD CS-related recommendations. Together, these assessments offer security posture reports that surface security issues and severe misconfigurations that post risks to the entire organization, together with related detections.

For more information, see:

- [Security assessment: Prevent Certificate Enrollment with arbitrary Application Policies (ESC15)](https://go.microsoft.com/fwlink/?linkid=2296922)

- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)

## October 2024

### MDI is expanding coverage with new 10 Identity posture recommendations (preview)

The new Identity security posture assessments (ISPMs) can help customers monitor misconfiguration by watching for weak spots and reduce the risk of potential attack on on-premises infrastructure.   
These new identity recommendations, as part of Microsoft Secure Score, are new security posture reports related to Active Directory infrastructure and Group policy Objects:

- [Accounts with nondefault Primary Group ID](/defender-for-identity/accounts-with-non-default-pgid)

- [Change Domain Controller computer account old password](/defender-for-identity/domain-controller-account-password-change)

- [GPO assigns unprivileged identities to local groups with elevated privileges](/defender-for-identity/gpo-assigns-unprivileged-identities)

- [GPO can be modified by unprivileged accounts](/defender-for-identity/modified-unprivileged-accounts-gpo)

- [Reversible passwords found in GPOs](/defender-for-identity/reversible-passwords-group-policy)

- [Built-in Active Directory Guest account is enabled](/defender-for-identity/built-in-active-directory-guest-account-is-enabled)

- [Unsafe permissions on the DnsAdmins group](/defender-for-identity/unsafe-permissions-dns-admins-group)

- [Ensure that all privileged accounts have the configuration flag "this account is sensitive and cannot be delegated”](/defender-for-identity/ensure-privileged-accounts-with-sensitive-flag)

- [Change password of krbtgt account](/defender-for-identity/change-password-krbtgt-account)

- [Change password of built-in domain Administrator account](/defender-for-identity/change-password-domain-administrator-account)

Additionally, we updated the existing recommendation of "Modify unsecure Kerberos delegations to prevent impersonation" to include indication of Kerberos Constrained Delegation with Protocol Transition to a privileged service. 

## August 2024

#### New Microsoft Entra Connect sensor:

As part of our ongoing effort to enhance Microsoft Defender for Identity coverage in hybrid identity environments, we have introduced a new sensor for Microsoft Entra Connect servers. Additionally, we've released new hybrid security detections and new identity posture recommendations specifically for Microsoft Entra Connect, helping customers stay protected and mitigate potential risks.

**New Microsoft Entra Connect Identity posture recommendations:**

* **Rotate password for Microsoft Entra Connect connector account**
   * A compromised Microsoft Entra Connect connector account (AD DS connector account, commonly shown as MSOL_XXXXXXXX) can grant access to high-privilege functions like replication and password resets, allowing attackers to modify synchronization settings and compromise security in both cloud and on-premises environments as well as offering several paths for compromising the entire domain. In this assessment we recommend customers change the password of MSOL accounts with the password last set over 90 days ago. For more information, click [here](rotate-password-microsoft-entra-connect.md).
* **Remove unnecessary replication permissions for Microsoft Entra Connect Account**
   * By default, the Microsoft Entra Connect connector account has extensive permissions to ensure proper synchronization (even if they aren't required). If Password Hash Sync isn't configured, it’s important to remove unnecessary permissions to reduce the potential attack surface. For more information, click [here](remove-replication-permissions-microsoft-entra-connect.md)
* **Change password for Microsoft Entra seamless SSO account configuration**
   * This report lists all [Microsoft Entra seamless SSO](/entra/identity/hybrid/connect/how-to-connect-sso) computer accounts with password last set over 90 days ago. The password for the Azure SSO computer account isn't automatically changed every 30 days. If an attacker compromises this account, they can generate service tickets for the AZUREADSSOACC account on behalf of any user and impersonate any user in the Microsoft Entra tenant that is synchronized from Active Directory. An attacker can use this to move laterally from Active Directory into Microsoft Entra ID. For more information, click [here](change-password-microsoft-entra-seamless-single-sign-on.md).    

**New Microsoft Entra Connect detections:**

* **Suspicious Interactive Logon to the Microsoft Entra Connect Server**
   * Direct logins to Microsoft Entra Connect servers are highly unusual and potentially malicious. Attackers often target these servers to steal credentials for broader network access. Microsoft Defender for Identity can now detect abnormal logins to Microsoft Entra Connect servers, helping you identify and respond to these potential threats faster. It's specifically applicable when the Microsoft Entra Connect server is a standalone server and not operating as a Domain Controller.
* **User Password Reset by Microsoft Entra Connect Account**
   *  The Microsoft Entra Connect connector account often holds high privileges, including the ability to reset user’s passwords. Microsoft Defender for Identity now has visibility into those actions and will detect any usage of those permissions that were identified as malicious and non-legitimate. This alert is triggered only if the [password writeback feature](/entra/identity/authentication/concept-sspr-writeback) is disabled.
*  **Suspicious writeback by Microsoft Entra Connect on a sensitive user**
   * While Microsoft Entra Connect already prevents writeback for users in privileged groups, Microsoft Defender for Identity expands this protection by identifying additional types of sensitive accounts. This enhanced detection helps prevent unauthorized password resets on critical accounts, which can be a crucial step in advanced attacks targeting both cloud and on-premises environments.

**Additional improvements and capabilities:**

* New activity of any **failed password reset on a sensitive account** available in the ‘IdentityDirectoryEvents’ table in Advanced Hunting. This can help customers track failed password reset events and create custom detection based on this data.
* Enhanced accuracy for the **DC sync attack** detection.
* New [health issue](health-alerts.md) for cases where the sensor is unable to retrieve the configuration from the Microsoft Entra Connect service.
* Extended monitoring for security alerts, such as PowerShell Remote Execution Detector, by enabling the new sensor on Microsoft Entra Connect servers.

[Learn more about the new sensor](deploy/active-directory-federation-services.md)

### Updated DefenderForIdentity PowerShell module

The DefenderForIdentity PowerShell module has been updated, incorporating new functionality and addressing several bug fixes. Key improvements include:

- **New `New-MDIDSA` Cmdlet**: Simplifies creation of service accounts, with a default setting for Group Managed Service Accounts (gMSA) and an option to create standard accounts.
- **Automatic PDCe Detection**: Improves Group Policy Object (GPO) creation reliability by automatically targeting the Primary Domain Controller Emulator (PDCe) for most Active Directory operations.
- **Manual Domain Controller Targeting**: New Server parameter for `Get/Set/Test-MDIConfiguration` cmdlets, allowing you to specify a domain controller for targeting instead of the PDCe.

For more information, see:

- [DefenderForIdentity PowerShell module (PowerShell Gallery)](https://www.powershellgallery.com/packages/DefenderForIdentity/)
- [DefenderForIdentity PowerShell reference documentation](/powershell/defenderforidentity/overview-defenderforidentity)


## July 2024

Six New detections are new in public preview:
* **Possible NetSync attack**
    * NetSync is a module in Mimikatz, a post-exploitation tool, that requests the password hash of a target device's password by pretending to be a domain controller. An attacker might be performing malicious activities inside the network using this feature to gain access to the organization's resources.
* **Possible takeover of a Microsoft Entra seamless SSO account**
    * A Microsoft Entra seamless SSO (single sign-on) account object, AZUREADSSOACC, was modified suspiciously. An attacker might be moving laterally from the on-premises environment to the cloud.
* **Suspicious LDAP query**
    * A suspicious Lightweight Directory Access Protocol (LDAP) query associated with a known attack tool was detected. An attacker might be performing reconnaissance for later steps.
* **Suspicious SPN was added to a user**
    * A suspicious service principal name (SPN) was added to a sensitive user. An attacker might be attempting to gain elevated access for lateral movement within the organization
* **Suspicious creation of ESXi group**
    * A suspicious VMWare ESXi group was created in the domain. This might indicate that an attacker is trying to get more permissions for later steps in an attack.
* **Suspicious ADFS authentication**
    * A domain-joined account signed in using Active Directory Federation Services (ADFS) from a suspicious IP address. An attacker might have stolen a user's credentials and is using it to move laterally in the organization.

### Defender for Identity release 2.238

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## June 2024

### Easily Go Hunt For user Information From the ITDR Dashboard

The Shield Widget provides a quick overview of the number of users in hybrid, cloud, and on-premises environments. This feature now includes direct links to the Advanced Hunting platform, offering detailed user information at your fingertips.

### ITDR Deployment Health Widget Now Include Microsoft Entra Conditional Access and Microsoft Entra Private Access 

Now you can view the license availability for Microsoft Entra Workload Conditional Access, Microsoft Entra User Conditional Access, and Microsoft Entra Private Access.

### Defender for Identity release 2.237

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## May 2024

### Defender for Identity release 2.236

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.235

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## April 2024

### Easily detect CVE-2024-21427 Windows Kerberos Security Feature Bypass Vulnerability

To help customers better identify and detect attempts to bypass security protocols according to [this vulnerability](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-21427), we have added a new activity within Advanced Hunting that monitors Kerberos AS authentication.   

With this data, customers can now easily create their own [custom detection rules within Microsoft Defender XDR](https://aka.ms/CustomDetectionsDocs) and automatically trigger alerts for this type of activity.

Access Defender XDR portal -> Hunting -> Advanced Hunting.

Now, you can copy our recommended query as provided below, and click on “Create detection rule”. Be aware that our provided query also tracks failed logon attempts, which may generate information unrelated to a potential attack. Therefore, feel free to customize the query to suit your specific requirements.


```
IdentityLogonEvents
| where Application == "Active Directory"
| where Protocol == "Kerberos"
| where LogonType in("Resource access", "Failed logon")
| extend Error =  AdditionalFields["Error"]
| extend KerberosType = AdditionalFields['KerberosType']
| where KerberosType == "KerberosAs"
| extend Spns = AdditionalFields["Spns"]
| extend DestinationDC = AdditionalFields["TO.DEVICE"]
| where  Spns !contains "krbtgt" and Spns !contains "kadmin"
| project Timestamp, ActionType, LogonType, AccountUpn, AccountSid, IPAddress, DeviceName, KerberosType, Spns, Error, DestinationDC, DestinationIPAddress, ReportId

```

### Defender for Identity release 2.234

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.233

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## March 2024

### New read-only permissions for viewing Defender for Identity settings

Now you can configure Defender for Identity users with read-only permissions to view Defender for Identity settings. 

For more information, see [Required permissions Defender for Identity in Microsoft Defender XDR](role-groups.md#required-permissions-defender-for-identity-in-microsoft-defender-xdr).

### New Graph based API for viewing and managing Health issues

Now you can view and manage Microsoft Defender for Identity health issues through the Graph API

For more information, see [Managing Health issues through Graph API](/graph/api/resources/security-healthissue?view=graph-rest-beta&preserve-view=true).

### Defender for Identity release 2.232

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.231

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## February 2024

### Defender for Identity release 2.230

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### New security posture assessment for insecure AD CS IIS endpoint configuration

Defender for Identity has added the new **Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)** recommendation in Microsoft Secure Score.

Active Directory Certificate Services (AD CS) supports certificate enrollment through various methods and protocols, including enrollment via HTTP using the Certificate Enrollment Service (CES) or the Web Enrollment interface (Certsrv). Insecure configurations of the CES or Certsrv IIS endpoints might create vulnerabilities to relay attacks (ESC8).

The new **Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)** recommendation is added to other AD CS-related recommendations recently released. Together, these assessments offer security posture reports that surface security issues and severe misconfigurations that post risks to the entire organization, together with related detections.

For more information, see:

- [Security assessment: Edit insecure ADCS certificate enrollment IIS endpoints (ESC8)](security-assessment-insecure-adcs-certificate-enrollment.md)
- [Security posture assessments for AD CS sensors](#security-posture-assessments-for-ad-cs-sensors-preview)
- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)

### Defender for Identity release 2.229

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Enhanced user experience for adjusting alert thresholds (Preview)

The Defender for Identity **Advanced Settings** page is now renamed to **Adjust alert thresholds** and provides a refreshed experience with enhanced flexibility for adjusting alert thresholds.

:::image type="content" source="media/whats-new/adjust-alert-thresholds.png" alt-text="Screenshot of the new Adjust alert thresholds page." lightbox="media/whats-new/adjust-alert-thresholds.png":::

Changes include:

- We've removed the previous **Remove learning period** option, and added a new **Recommended test mode** option. Select **Recommended test mode** to set all threshold levels to **Low**, increasing the number of alerts, and sets all other threshold levels to read-only.

- The previous **Sensitivity level** column is now renamed as **Threshold level**, with newly defined values. By default, all alerts are set to a **High** threshold, which represents the default behavior and a standard alert configuration.

The following table lists the mapping between the previous **Sensitivity level** values and the new **Threshold level** values:

|Sensitivity level (previous name) |Threshold level (new name) |
|---------|---------|
|**Normal**     |  **High**       |
|**Medium**      |  **Medium**       |
|**High**      |  **Low**       |

If you had specific values defined on the **Advanced Settings** page, we've transferred them to the new **Adjust alert thresholds** page as follows:

|Advanced settings page configuration  |New Adjust alert thresholds page configuration  |
|---------|---------|
|**Remove learning period** toggled on     |  **Recommended test mode** toggled off. <br><br> Alert threshold configuration settings remain the same.       |
|**Remove learning period** toggled off      |  **Recommended test mode** toggled off. <br><br> Alert threshold configuration settings are all reset to their default values, with a **High** threshold level.   |

Alerts are always triggered immediately if the **Recommended test mode** option is selected, or if a threshold level is set to **Medium** or **Low**, regardless of whether the alert's learning period has already completed.

For more information, see [Adjust alert thresholds](advanced-settings.md).

### Device details pages now include device descriptions (Preview)

Microsoft Defender XDR now includes device descriptions on device details panes and device details pages. The descriptions are populated from the device's Active Directory [Description](/windows/win32/adschema/a-description) attribute.

For example, on the device details side pane:

:::image type="content" source="media/whats-new/device-description.png" alt-text="Screenshot of the new Device description field on a device details pane." lightbox="media/whats-new/device-description.png":::

For more information, see [Investigation steps for suspicious devices](investigate-assets.md#investigation-steps-for-suspicious-devices).

### Defender for Identity release 2.228

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor, and the following new alerts:

- [Account Enumeration reconnaissance (LDAP) (external ID 2437)](reconnaissance-discovery-alerts.md#account-enumeration-reconnaissance-ldap-external-id-2437-preview) (Preview)
- [Directory Services Restore Mode Password Change (external ID 2438)](other-alerts.md#directory-services-restore-mode-password-change-external-id-2438) (Preview)

## January 2024

### Defender for Identity release 2.227

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Timeline tab added for group entities

Now you can view Active Directory group entity-related activities and alerts from the last 180 days in Microsoft Defender XDR, such as group membership changes, LDAP queries and so on.

To access the group timeline page, select **Open timeline** on the group details pane.



For example:

:::image type="content" source="media/whats-new/group-timeline.png" alt-text="Screenshot of the Open timeline button on a group entity details pane." lightbox="media/whats-new/group-timeline.png":::

For more information, see [Investigation steps for suspicious groups](investigate-assets.md#investigation-steps-for-suspicious-groups).

### Configure and validate your Defender for Identity environment via PowerShell

Defender for Identity now supports the new *DefenderForIdentity* PowerShell module, which is designed to help you configure and validate your environment for working with Microsoft Defender for Identity.

Using the PowerShell commands to avoid misconfigurations and save time and avoiding unnecessary load on your system.

We added the following procedures to the Defender for Identity documentation to help you use the new PowerShell commands:

- [Change proxy configuration using PowerShell](configure-proxy.md#change-proxy-configuration-using-powershell)
- [Configure, get, and test audit policies using PowerShell](configure-windows-event-collection.md#configure-get-and-test-audit-policies-using-powershell)
- [Generate a report with current configurations via PowerShell](configure-windows-event-collection.md#generate-a-report-with-current-configurations-via-powershell)
- [Test your DSA permissions and delegations via PowerShell](directory-service-accounts.md#test-your-dsa-permissions-and-delegations-via-powershell)
- [Test service connectivity using PowerShell](deploy/test-connectivity.md#test-service-connectivity-using-powershell)

For more information, see:

- [DefenderForIdentity PowerShell module (PowerShell Gallery)](https://www.powershellgallery.com/packages/DefenderForIdentity/)
- [DefenderForIdentity PowerShell reference documentation](/powershell/defenderforidentity/overview-defenderforidentity)

### Defender for Identity release 2.226

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.225

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## December 2023

> [!NOTE]
> If you're seeing a decreased number of *Remote code execution attempt* alerts, see our updated [September announcements](#september-2023), which include an [update to the Defender for Identity detection logic](#decreased-number-of-alerts-for-remote-code-execution-attempts). Defender for Identity continues to record the remote code execution activities as before.

### New Identities area and dashboard in Microsoft Defender XDR  (Preview)

Defender for Identity customers now have a new **Identities** area in Microsoft Defender XDR for information about identity security with Defender for Identity.

In Microsoft Defender XDR, select **Identities** to see any of the following new pages:

- **Dashboard**: This page shows graphs and widgets to help you monitor identity threat detection and response activities. For example:

   :::image type="content" source="media/dashboard/dashboard.gif" alt-text="An animated GIF showing a sample ITDR Dashboard page.":::

   For more information, see [Work with Defender for Identity's ITDR dashboard](dashboard.md).

- **Health issues**: This page is moved from the **Settings > Identities** area, and lists any current health issues for your general Defender for Identity deployment and specific sensors. For more information, see [Microsoft Defender for Identity sensor health issues](health-alerts.md).

- **Tools**: This page contains links to helpful information and resources when working with Defender for Identity. On this page, find links to documentation, specifically on the [capacity planning tool](capacity-planning.md), and the [*Test-MdiReadiness.ps1*](https://github.com/microsoft/Microsoft-Defender-for-Identity/tree/main/Test-MdiReadiness) script.

### Defender for Identity release 2.224

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Security posture assessments for AD CS sensors (Preview)

Defenders for Identity's security posture assessments proactively detect and recommend actions across your on-premises Active Directory configurations. 

Recommended actions now include the following new security posture assessments, specifically for certificate templates and certificate authorities.

- **Certificate templates recommended actions**:

   - [Prevent users to request a certificate valid for arbitrary users based on the certificate template (ESC1)](security-assessment-prevent-users-request-certificate.md)
   - [Edit overly permissive certificate template with privileged EKU (Any purpose EKU or No EKU) (ESC2)](security-assessment-edit-overly-permissive-template.md)
   - [Misconfigured enrollment agent certificate template (ESC3)](security-assessment-edit-misconfigured-enrollment-agent.md)
   - [Edit misconfigured certificate templates ACL (ESC4)](security-assessment-edit-misconfigured-acl.md)
   - [Edit misconfigured certificate templates owner (ESC4)](security-assessment-edit-misconfigured-owner.md)

- **Certificate authority recommended actions**:

   - [Edit vulnerable Certificate Authority setting (ESC6)](security-assessment-edit-vulnerable-ca-setting.md)
   - [Edit misconfigured Certificate Authority ACL (ESC7)](security-assessment-edit-misconfigured-ca-acl.md)
   - [Enforce encryption for RPC certificate enrollment interface (ESC11)](security-assessment-enforce-encryption-rpc.md)

The new assessments are available in Microsoft Secure Score, surfacing security issues, and severe misconfigurations that pose risks to the entire organization, alongside detections. Your score is updated accordingly.

For example:

:::image type="content" source="media/secure-score/adcs-new-reports.png" alt-text="Screenshot of the new AD CS security posture assessments.":::

For more information, see [Microsoft Defender for Identity's security posture assessments](security-assessment.md).

> [!NOTE]
> While *certificate template* assessments are available to all customers that have AD CS installed on their environment, *certificate authority* assessments are available only to customers who have installed a sensor on an AD CS server. For more information, see [New sensor type for Active Directory Certificate Services (AD CS)](#new-sensor-type-for-active-directory-certificate-services-ad-cs).

### Defender for Identity release 2.223

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.222

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.221

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## November 2023

### Defender for Identity release 2.220

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.219

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Identity timeline includes more than 30 days of data (Preview)

Defender for Identity is gradually rolling out extended data retentions on identity details to more than 30 days. 

The identity details page **Timeline** tab, which includes activities from Defender for Identity, Microsoft Defender for Cloud Apps, and Microsoft Defender for Endpoint, currently includes a minimum of 150 days and is growing. There might be some variation in data retention rates over the next few weeks.

To view activities and alerts on the identity timeline within a specific time frame, select the default **30 Days** and then select **Custom range**. Filtered data from more than 30 days ago is shown for a maximum of seven days at a time.

For example:

:::image type="content" source="media/whats-new/custom-time-frame.png" alt-text="Screenshot of the custom time frame options." lightbox="media/whats-new/custom-time-frame.png":::

For more information, see [Investigate assets](investigate-assets.md) and [Investigate users in Microsoft Defender XDR](/microsoft-365/security/defender/investigate-users).

### Defender for Identity release 2.218

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## October 2023

### Defender for Identity release 2.217

This version includes the following improvements:

- **Summary report**: The summary report is updated to include two new columns in the *Health issues* tab:

    -	Details: Additional information on the issue, such as a list of impacted objects or specific sensors on which the issue occurs.
    -	Recommendations: A list of recommended actions that can be taken to resolve the issue, or how to investigate the issue further.

    For more information, see [Download and schedule Defender for Identity reports in Microsoft Defender XDR (Preview)](reports.md).

- **Health issues**: The 'Remove learning period' toggle was automatically switched off for this tenant* health issue.

This version also includes bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.216

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## September 2023

### Decreased number of alerts for Remote Code Execution Attempts

To better align Defender for Identity and Microsoft Defender for Endpoint alerts, we updated the detection logic for the Defender for Identity [Remote code execution attempt](other-alerts.md#remote-code-execution-attempt-external-id-2019) detections. 

While this change results in a decreased number of *Remote code execution attempt* alerts, Defender for Identity continues to record the remote code execution activities. Customers can continue to build their own [advanced hunting queries](/microsoft-365/security/defender/advanced-hunting-overview) and create [custom detection policies](/microsoft-365/security/defender/custom-detection-rules). 

### Alert sensitivity settings and learning period enhancements

Some Defenders for Identity alerts wait for a *learning period* before alerts are triggered, while building a profile of patterns to use when distinguishing between legitimate and suspicious activities.

Defender for Identity now provides the following enhancements for the learning period experience:

- Administrators can now use the **Remove learning period** setting to configure the sensitivity used for specific alerts. Define the sensitivity as *Normal* to configure the **Remove learning period** setting as *Off* for the selected type of alert. 

- After you deploy a new sensor in a new Defender for Identity workspace, the **Remove learning period** setting is automatically turned *On* for 30 days. When 30 days are complete, the **Remove learning period** setting is automatically turned *Off,* and alert sensitivity levels are returned to their default functionality.

   To have Defender for Identity use standard learning period functionality, where alerts aren't generated until the learning period is done, configure the **Remove learning periods** setting to *Off*.

If you'd previously updated the **Remove learning period** setting, your setting remains as you'd configured it.

For more information, see [Advanced settings](advanced-settings.md).

> [!NOTE]
> The **Advanced Settings** page originally listed the *Account enumeration reconnaissance* alert under the **Remove learning period** options as configurable for sensitivity settings. This alert was removed from the list and is replaced by the *Security principal reconnaissance (LDAP)* alert. This user interface bug was fixed in November 2023.
>

### Defender for Identity release 2.215

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity reports moved to the main Reports area

Now you can access Defender for Identity reports from Microsoft Defender XDR's main **Reports** area instead of the **Settings** area. For example:

:::image type="content" source="media/whats-new/reports-main-area.png" alt-text="Screenshot of the Defender for Identity report access from the main Reports area.":::

For more information, see [Download and schedule Defender for Identity reports in Microsoft Defender XDR (Preview)](reports.md).

### Go hunt button for groups in Microsoft Defender XDR

Defender for Identity added the **Go hunt** button for groups in Microsoft Defender XDR. Users can use the **Go hunt** button to query for group-related activities and alerts during an investigation.

For example:

:::image type="content" source="media/whats-new/go-hunt-groups.png" alt-text="Screenshot of the new Go hunt button on a group details pane.":::

For more information, see [Quickly hunt for entity or event information with go hunt](/microsoft-365/security/defender/advanced-hunting-go-hunt).

### Defender for Identity release 2.214

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Performance enhancements

Defender for Identity made internal improvements for latency, stability, and performance when transferring real-time events from Defender for Identity services to Microsoft Defender XDR. Customers should expect no delays in Defender for Identity data appearing in Microsoft Defender XDR, such as alerts or activities for advanced hunting.


For more information, see:

- [Security alerts in Microsoft Defender for Identity](alerts-overview.md)
- [Microsoft Defender for Identity's security posture assessments](security-assessment.md)
- [Proactively hunt for threats with advanced hunting in Microsoft Defender XDR](/microsoft-365/security/defender/advanced-hunting-overview)

## August 2023

### Defender for Identity release 2.213

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.212

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### Defender for Identity release 2.211

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

### New sensor type for Active Directory Certificate Services (AD CS)

Defender for Identity now supports the new **ADCS** sensor type for a dedicated server with Active Directory Certificate Services (AD CS) configured.

You see the new sensor type identified in the **Settings > Identities > Sensors** page in Microsoft Defender XDR. For more information, see [Manage and update Microsoft Defender for Identity sensors](sensor-settings.md#sensor-details).

Together with the new sensor type, Defender for Identity also now provides related AD CS alerts and Secure Score reports. To view the new alerts and Secure Score reports, make sure that the required events are being collected and logged on your server. For more information, see [Configure auditing for Active Directory Certificate Services (AD CS) events](configure-windows-event-collection.md#configure-auditing-for-active-directory-certificate-services-ad-cs).

AD CS is a Windows Server role that issues and manages public key infrastructure (PKI) certificates in secure communication and authentication protocols. For more information, see [What is Active Directory Certificate Services?](/windows-server/identity/ad-cs/active-directory-certificate-services-overview)

### Defender for Identity release 2.210

This version includes improvements and bug fixes for cloud services and the Defender for Identity sensor.

## Next steps

- [What is Microsoft Defender for Identity?](what-is.md)
- [Frequently asked questions](technical-faq.yml)

- [Defender for Identity prerequisites](prerequisites.md)
- [Defender for Identity capacity planning](capacity-planning.md)
- [Check out the Defender for Identity forum!](<https://aka.ms/MDIcommunity>)
