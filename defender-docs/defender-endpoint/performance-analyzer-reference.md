---
title: Microsoft Defender Antivirus Performance Analyzer reference
description: Microsoft Defender Antivirus Performance Analyzer reference
author: emmwalshh
ms.author: ewalsh
ms.reviewer: yongrhee
ms.service: defender-endpoint
ms.topic: troubleshooting
ms.date: 11/22/2024
ms.subservice: ngp
manager: deniseb
ms.localizationpriority: medium
audience: ITPro
ms.collection: 
- m365-security
- tier2
- mde-ngp 
ms.custom: 
- partner-contribution
f1.keywords: NOCSH 
ai-usage: human-only
---

# Microsoft Defender Antivirus Performance Analyzer reference

## PowerShell reference

You can use the following new PowerShell cmdlets to tune the performance of Microsoft Defender Antivirus:

- [New-MpPerformanceRecording](#new-mpperformancerecording)
- [Get-MpPerformanceReport](#get-mpperformancereport)

### New-MpPerformanceRecording

The following section describes the reference for the new PowerShell cmdlet `New-MpPerformanceRecording`. This cmdlet Collects a performance recording of Microsoft Defender Antivirus scans.

#### Syntax: New-MpPerformanceRecording

```powershell
New-MpPerformanceRecording -RecordTo <String>
```

#### Description: New-MpPerformanceRecording

The `New-MpPerformanceRecording` cmdlet collects a performance recording of Microsoft Defender Antivirus scans. These performance recordings contain Microsoft-Antimalware-Engine and NT kernel process events and can be analyzed after collection using the [Get-MpPerformanceReport](#get-mpperformancereport) cmdlet.

This `New-MpPerformanceRecording` cmdlet provides an insight into problematic files that could cause a degradation in the performance of Microsoft Defender Antivirus. This tool is provided as is, and isn't intended to provide suggestions on [exclusions](navigate-defender-endpoint-antivirus-exclusions.md). Exclusions can reduce the level of protection on your endpoints. Exclusions, if any, should be defined with caution.

For more information on the performance analyzer, see [Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer) docs.

> [!IMPORTANT]
> This cmdlet requires elevated administrator privileges.


#### Examples: New-MpPerformanceRecording

##### Example 1: Collect a performance recording and save it

```powershell
New-MpPerformanceRecording -RecordTo .\Defender-scans.etl
```

The command collects a performance recording and saves it to the specified path: `.\Defender-scans.etl`.

##### Example 2: Collect a performance recording for remote PowerShell session

```powershell
$s = New-PSSession -ComputerName Server02 -Credential Domain01\User01
New-MpPerformanceRecording -RecordTo C:\LocalPathOnServer02\trace.etl -Session $s
```

The command collects a performance recording on `Server02` (as specified by argument $s of parameter Session) and saves it to the specified path: `C:\LocalPathOnServer02\trace.etl` on `Server02`.


#### Parameters: New-MpPerformanceRecording

##### -RecordTo

Specifies the location in which to save the Microsoft Defender Antimalware performance recording.

```yaml
Type: String
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -Session

Specifies the `PSSession` object in which to create and save the Microsoft Defender Antivirus performance recording. When you use this command, the `RecordTo` parameter refers to the local path on the remote machine. Available with Defender platform version `4.18.2201.10` and later.

```yaml
Type: PSSession[]
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### Get-MpPerformanceReport

The following section describes the `Get-MpPerformanceReport` PowerShell cmdlet. Analyzes and reports on Microsoft Defender Antivirus performance recording.

#### Syntax: Get-MpPerformanceReport

```output
    Get-MpPerformanceReport [-Path] <String> [-TopFiles <Int32>] [-TopScansPerFile <Int32>] [-TopProcessesPerFile 
<Int32>] [-TopScansPerProcessPerFile <Int32>] [-TopPaths <Int32>] [-TopPathsDepth <Int32>] [-TopScansPerPath 
<Int32>] [-TopFilesPerPath <Int32>] [-TopScansPerFilePerPath <Int32>] [-TopExtensionsPerPath <Int32>] 
    [-TopScansPerExtensionPerPath <Int32>] [-TopProcessesPerPath <Int32>] [-TopScansPerProcessPerPath <Int32>] 
    [-TopExtensions <Int32>] [-TopScansPerExtension <Int32>] [-TopPathsPerExtension <Int32>] 
    [-TopScansPerPathPerExtension <Int32>] [-TopFilesPerExtension <Int32>] [-TopScansPerFilePerExtension <Int32>] 
    [-TopProcessesPerExtension <Int32>] [-TopScansPerProcessPerExtension <Int32>] [-TopProcesses <Int32>] 
    [-TopScansPerProcess <Int32>] [-TopFilesPerProcess <Int32>] [-TopScansPerFilePerProcess <Int32>] 
    [-TopExtensionsPerProcess <Int32>] [-TopScansPerExtensionPerProcess <Int32>] [-TopPathsPerProcess <Int32>] 
    [-TopScansPerPathPerProcess <Int32>] [-TopScans <Int32>] [-MinDuration <String>] [-MinStartTime <DateTime>] 
    [-MinEndTime <DateTime>] [-MaxStartTime <DateTime>] [-MaxEndTime <DateTime>] [-Overview] [-Raw] 
    [<CommonParameters>]
```

#### Description: Get-MpPerformanceReport

The `Get-MpPerformanceReport` cmdlet analyzes a previously collected Microsoft Defender Antivirus performance recording ([New-MpPerformanceRecording](#new-mpperformancerecording)) and reports the file paths, file extensions, and processes that cause the highest impact to Microsoft Defender Antivirus scans.

The performance analyzer provides an insight into problematic files that could cause a degradation in the performance of Microsoft Defender Antivirus. This tool is provided "as is" and isn't intended to provide suggestions on exclusions. Exclusions can reduce the level of protection on your endpoints. Exclusions, if any, should be defined with caution.

For more information on the performance analyzer, see [Performance Analyzer](/windows-hardware/test/wpt/windows-performance-analyzer) docs.

**Supported OS versions**:

Windows Version 10 and later.

> [!NOTE]
> This feature is available starting with platform version `4.18.2108.X` and later.

#### Examples: Get-MpPerformanceReport

##### Example 1: Single query

```powershell
Get-MpPerformanceReport -Path .\Defender-scans.etl -TopScans 20
```

##### Example 2: Multiple queries

```powershell
Get-MpPerformanceReport -Path .\Defender-scans.etl -TopFiles 10 -TopExtensions 10 -TopProcesses 10 -TopScans 10
```

##### Example 3: Nested queries

```powershell
Get-MpPerformanceReport -Path .\Defender-scans.etl -TopProcesses 10 -TopExtensionsPerProcess 3 -TopScansPerExtensionPerProcess 3
```

##### Example 4: Using -MinDuration parameter

```powershell
Get-MpPerformanceReport -Path .\Defender-scans.etl -TopScans 100 -MinDuration 100ms
```

##### Example 5: Using -Raw parameter

```powershell
Get-MpPerformanceReport -Path .\Defender-scans.etl -TopFiles 10 -TopExtensions 10 -TopProcesses 10 -TopScans 10 -Raw | ConvertTo-Json
```

Using `-Raw` in the command specifies that the output should be machine readable and readily convertible to serialization formats like JSON.

#### Parameters: Get-MpPerformanceReport

##### -TopPaths

Requests a top-paths report and specifies how many top paths to output, sorted by duration. Aggregates the scans based on their path and directory. User can specify how many directories should be displayed on each level and the depth of the selection.

```yaml
- Type: Int32
- Position: Named
- Default value: None
- Accept pipeline input: False
- Accept wildcard characters: False
```

##### -TopPathsDepth

Specifies recursive depth that is used to group and display aggregated path results. For example `C:\` corresponds to a depth of 1, and `C:\Users\Foo` corresponds to a depth of 3.

This flag can accompany all other Top Path options. If missing, a default value of 3 is assumed. The value can't be 0.

```yaml
- Type: Int32
- Position: Named
- Default value: 3
- Accept pipeline input: False
- Accept wildcard characters: False
```

| flag | definition |
|---|---|  
|  `-TopScansPerPath` | Specifies how many top scans to specify for each top path. |
|  `-TopFilesPerPath` | Specifies how many top files to specify for each top path. |
|  `-TopScansPerFilePerPath` | Specifies how many top scans to output for each top file for each top path, sorted by "Duration" |
|  `-TopExtensionsPerPath` | Specifies how many top extensions to output for each top path |
|  `-TopScansPerExtensionPerPath` | Specifies how many top scans to output for each top extension for each top path |
|  `-TopProcessesPerPath` | Specifies how many top processes to output for each top path |
|  `-TopScansPerProcessPerPath` | Specifies how many top scans to output for each top process for each top path |
|  `-TopPathsPerExtension` | Specifies how many top paths to output for each top extension |
|  `-TopScansPerPathPerExtension` | Specifies how many top scans to output for each top path for each top extension |
|  `-TopPathsPerProcess` | Specifies how many top paths to output for each top process |
|  `-TopScansPerPathPerProcess` | Specifies how many top scans to output for each top path for each top process |

##### -MinDuration

Specifies the minimum duration of any scan or total scan durations of files, extensions, and processes included in the report; accepts values like  `0.1234567sec`, `0.1234ms`, `0.1us`, or a valid TimeSpan.

```yaml
Type: String
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -Path

Specifies the path or paths to one or more locations.

```yaml
Type: String
Position: 0
Default value: None
Accept pipeline input: True
Accept wildcard characters: False
```

##### -Raw

Specifies that output of performance recording should be machine readable and readily convertible to serialization formats like JSON (for example, via Convert-to-JSON command). This configuration is recommended for users interested in batch processing with other data processing systems.

```yaml
Type: <SwitchParameter>
Position: Named
Default value: False
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopExtensions

Specifies how many top extensions to output, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopExtensionsPerProcess

Specifies how many top extensions to output for each top process, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopFiles

Requests a top-files report and specifies how many top files to output, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopFilesPerExtension

Specifies how many top files to output for each top extension, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopFilesPerProcess

Specifies how many top files to output for each top process, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopProcesses

Requests a top-processes report and specifies how many of the top processes to output, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopProcessesPerExtension

Specifies how many top processes to output for each top extension, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopProcessesPerFile

Specifies how many top processes to output for each top file, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScans

Requests a top-scans report and specifies how many top scans to output, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerExtension

Specifies how many top scans to output for each top extension, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerExtensionPerProcess

Specifies how many top scans to output for each top extension for each top process, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerFile

Specifies how many top scans to output for each top file, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerFilePerExtension

Specifies how many top scans to output for each top file for each top extension, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerFilePerProcess

Specifies how many top scans for output for each top file for each top process, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerProcess

Specifies how many top scans to output for each top process in the Top Processes report, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerProcessPerExtension

Specifies how many top scans for output for each top process for each top extension, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

##### -TopScansPerProcessPerFile

Specifies how many top scans for output for each top process for each top file, sorted by duration.

```yaml
Type: Int32
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]