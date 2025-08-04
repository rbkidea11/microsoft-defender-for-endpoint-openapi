---
title: DeviceInfo table in the advanced hunting schema
description: Learn about OS, computer name, and other machine information in the DeviceInfo table of the advanced hunting schema
search.appverid: met150
ms.service: defender-xdr
ms.subservice: adv-hunting
f1.keywords: 
  - NOCSH
ms.author: maccruz
author: schmurky
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- tier3
- m365-security
ms.custom: 
- cx-ti
- cx-ah
appliesto:
    - Microsoft Defender XDR
    - Microsoft Sentinel in the Microsoft Defender portal
ms.topic: reference
ms.date: 03/28/2025
---

# DeviceInfo

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]


The `DeviceInfo` table in the [advanced hunting](advanced-hunting-overview.md) schema contains information about devices in the organization, including OS version, active users, and computer name. Use this reference to construct queries that return information from this table.

> [!IMPORTANT]
> Some information relates to prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.


This advanced hunting table is populated by records from various Microsoft services. If your organization hasn’t deployed the service in Microsoft Defender XDR, queries that use the table aren’t going to work or return any results. For more information about how to deploy a Microsoft service in Defender XDR, read [Deploy supported services](deploy-supported-services.md).


For information on other tables in the advanced hunting schema, [see the advanced hunting reference](advanced-hunting-schema-tables.md).

| Column name | Data type | Description |
|-------------|-----------|-------------|
| `Timestamp` | `datetime` | Last date and time recorded for the device |
| `DeviceId` | `string` | Unique identifier for the device in the service |
| `DeviceName` | `string` | Fully qualified domain name (FQDN) of the device |
| `ClientVersion` | `string` | Version of the endpoint agent or sensor running on the device |
| `PublicIP` | `string` | Public IP address used by the onboarded device to connect to the Microsoft  Defender for Endpoint service. This could be the IP address of the device itself, a NAT device, or a proxy. |
| `OSArchitecture` | `string` | Architecture of the operating system running on the device |
| `OSPlatform` | `string` | Platform of the operating system running on the device. This indicates specific operating systems, including variations within the same family, such as Windows 11, Windows 10 and Windows 7. |
| `OSBuild` | `long` | Build version of the operating system running on the device |
| `IsAzureADJoined` | `boolean` | Boolean indicator of whether device is joined to the Microsoft Entra ID |
| `JoinType` | `string` | The device's Microsoft Entra ID join type |
| `AadDeviceId` | `string` | Unique identifier for the device in Microsoft Entra ID |
| `LoggedOnUsers` | `string` | List of all users that are logged on the device at the time of the event in JSON array format |
| `RegistryDeviceTag` | `string` | Device tag added through the registry |
| `OSVersion` | `string` | Version of the operating system running on the device |
| `MachineGroup` | `string` | Machine group of the device. This group is used by role-based access control to determine access to the device. |
| `ReportId` | `long` | Event identifier based on a repeating counter. To identify unique events, this column must be used in conjunction with the DeviceName and Timestamp columns. |
| `OnboardingStatus` | `string` | Indicates whether the device is currently onboarded or not to  Microsoft Defender For Endpoint or if the device is not supported |
| `AdditionalFields` | `string` | Additional information about the event in JSON array format |
| `DeviceCategory` | `string` | Broader classification that groups certain device types under the following categories: Endpoint, Network device, IoT, Unknown |
| `DeviceType` | `string` | Type of device based on purpose and functionality, such as network device, workstation, server, mobile, gaming console, or printer |
| `DeviceSubtype` | `string` | Additional modifier for certain types of devices, for example, a mobile device can be a tablet or a smartphone; only available if device discovery finds enough information about this attribute |
| `Model` | `string` | Model name or number of the product from the vendor or manufacturer, only available if device discovery finds enough information about this attribute |
| `Vendor` | `string` | Name of the product vendor or manufacturer, only available if device discovery finds enough information about this attribute |
| `OSDistribution` | `string` | Distribution of the OS platform, such as Ubuntu or RedHat for Linux platforms |
| `OSVersionInfo` | `string` | Additional information about the OS version, such as the popular name, code name, or version number |
| `MergedDeviceIds` | `string` | Previous device IDs that have been assigned to the same device |
| `MergedToDeviceId` | `string` | The most recent device ID assigned to a device |
| `IsInternetFacing` | `boolean` | Indicates whether the device is internet-facing |
| `SensorHealthState` | `string` | Indicates health of the device's EDR sensor, if onboarded to Microsoft Defender For Endpoint |
| `IsExcluded`| `bool` | Determines if the device is currently excluded from Microsoft Defender for Vulnerability Management experiences |
| `ExclusionReason` | `string` | Indicates the reason for device exclusion |
| `ExposureLevel` | `string` | The device's level of vulnerability to exploitation based on its exposure score; can be: Low, Medium, High |
| `AssetValue`| `string` | Priority or value assigned to the device in relation to its importance in computing the organization's exposure score; can be: Low, Normal (Default), High |
| `DeviceManualTags` | `string` | Device tags created manually using the portal UI or public API |
| `DeviceDynamicTags` | `string` | Device tags added and removed dynamically based on dynamic rules |
| `ConnectivityType` | `string` | Type of connectivity from the device to the cloud |
| `HostDeviceId` | `string` | Device ID of the device running Windows Subsystem for Linux |
| `AzureResourceId` | `string` | Unique identifier of the Azure resource associated with the device |
| `AwsResourceName` | `string` | Unique identifier specific to Amazon Web Services devices, containing the Amazon resource name |
| `GcpFullResourceName` | `string` | Unique identifier specific to Google Cloud Platform devices, containing a combination of zone and ID for GCP|
| `HardwareUuid` | `string` | Universally Unique Identifier (UUID) of the device's hardware |
| `CloudPlatforms` | `string` | The cloud platforms that the device belongs to. Can be Azure, Amazon Web Services, Google Cloud Platform and Azure Arc. |
| `AzureVmId` | `string` | Unique identifier assigned to the device in Azure |
| `AzureVmSubscriptionId` | `string` | Unique identifier of the Azure subscription associated with the device |
| `IsTransient` | `boolean` | Indicates whether this device is classified as short-lived or transient based on the frequency of appearance of the device on the network |
| `OsBuildRevision` | `string` | Build revision number of the operating system running on the machine |
| `MitigationStatus` | `string` | Indicates the mitigation action applied to a device |
| `Site` | `string` | Represents the physical location where the device is located |
| `DiscoverySources` | `string` | Products or services that have seen or reported the device, including when they last reported it. |

The DeviceInfo table is updated continuously, and all updates contain the full current device data for that device.

You can use the following sample query to get the latest state of a device:

```kusto
// Get latest information on user/device
DeviceInfo
| extend IngestionTime = ingestion_time()
| where DeviceName == "example" and isnotempty(OSPlatform)
| summarize arg_max(IngestionTime, *) by DeviceId
```

## Related topics
- [Advanced hunting overview](advanced-hunting-overview.md)
- [Learn the query language](advanced-hunting-query-language.md)
- [Use shared queries](advanced-hunting-shared-queries.md)
- [Hunt across devices, emails, apps, and identities](advanced-hunting-query-emails-devices.md)
- [Understand the schema](advanced-hunting-schema-tables.md)
- [Apply query best practices](advanced-hunting-best-practices.md)
[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
