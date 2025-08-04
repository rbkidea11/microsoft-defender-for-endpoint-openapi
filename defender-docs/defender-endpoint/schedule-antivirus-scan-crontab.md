---
title: Schedule an antivirus scan using crontab with Microsoft Defender for Endpoint on Linux
description: Learn how to schedule an automatic scanning time for Microsoft Defender for Endpoint (Linux) to better protect your organization's assets.
ms.service: defender-endpoint
ms.author: deniseb
author: denisebmsft
ms.reviewer: gopkr
ms.localizationpriority: medium
manager: deniseb
audience: ITPro
ms.collection: 
- m365-security
- tier3
- mde-linux
ms.topic: conceptual
ms.subservice: linux
search.appverid: met150
ms.date: 03/24/2025
---

# Schedule an antivirus scan using crontab with Microsoft Defender for Endpoint on Linux

**Applies to:**

- Microsoft Defender for Endpoint for servers
- Microsoft Defender for Servers Plan 1 or Plan 2

To run a scan for Linux, see [Supported commands](linux-resources.md#supported-commands).

For Linux (and Unix), you can use a tool called **crontab** (similar to Task Scheduler in Windows) to run scheduled tasks.

## Prerequisite

> [!NOTE]
> To get a list of all the time zones, run the following command:
> `timedatectl list-timezones`<br>
> Examples for timezones:
>
> - `America/Los_Angeles`
> - `America/New_York`
> - `America/Chicago`
> - `America/Denver`

## Set the Cron job

To set the cron job, use the commands in this article.

### Backup crontab entries

```bash
sudo crontab -l > /var/tmp/cron_backup_200919.dat
```

> [!NOTE]
> Where 200919 == YRMMDD

> [!TIP]
> Do this before you edit or remove.

To edit the crontab, and add a new job as a root user:

```bash
sudo crontab -e
```

> [!NOTE]
> The default editor is VIM.

You might see:

```console
0 * * * * /etc/opt/microsoft/mdatp/logrorate.sh
```

Press **Insert**, and then add the following entries:

```bash
CRON_TZ=America/Los_Angeles

0 2 * * sat /usr/bin/mdatp scan quick > ~/mdatp_cron_job.log
```

> [!NOTE]
> In this example, we have  set it to 00 minutes, 2 a.m. (hour in 24 hour format), any day of the month, any month, on Saturdays. Meaning it will run Saturdays at 2:00 a.m. Pacific (UTC -8).

Press **Esc**, and then type "`:wq`" without the double quotes.

> [!NOTE]
> w == write, q == quit

To view your cron jobs, type `sudo crontab -l`

:::image type="content" source="/defender/media/linux-mdatp-1.png" alt-text="Screenshot of the linux mdatp page.":::

#### To inspect cron job runs

```bash
sudo grep mdatp /var/log/cron
```

#### To inspect the mdatp_cron_job.log*

```bash
sudo nano mdatp_cron_job.log
```

## If you're using Ansible, Chef, Puppet, or SaltStack

Use the following commands:

### To set cron jobs in Ansible

```bash
cron - Manage cron.d and crontab entries
```

For more information, see [Ansible documentation](https://docs.ansible.com/ansible/latest).

### To set crontabs in Chef

```bash
cron resource
```

For more information, see [Chef documentation](https://docs.chef.io/resources/cron).

### To set cron jobs in Puppet

```bash
Resource Type: cron
```

For more information, see [Puppet documentation: Resource Type: cron](https://puppet.com/docs/puppet/5.5/types/cron.html). 

**Automating with Puppet: Cron jobs and scheduled tasks**

For more information, see [Puppet documentation about jobs and scheduled tasks](https://puppet.com/blog/automating-puppet-cron-jobs-and-scheduled-tasks/).

### To manage cron jobs in SaltStack

```bash
Resource Type: salt.states.cron
```

**Example:**

```yaml
mdatp scan quick > /tmp/mdatp_scan_log.log:
  cron.present:
    - special: '@hourly'
```

For more information, see the [Salt.States.Cron documentation](https://docs.saltproject.io/en/latest/ref/states/all/salt.states.cron.html).

## Additional information

### To get help with crontab

```bash
man crontab
```

### To get a list of crontab file of the current user

```bash
crontab -l
```

### To get a list of crontab file of another user

```bash
crontab -u username -l
```

### To back up crontab entries

```bash
crontab -l > /var/tmp/cron_backup.dat
```

> [!TIP]
> Do this before you edit or remove.

### To restore crontab entries

```bash
crontab /var/tmp/cron_backup.dat
```

### To edit the crontab and add a new job as a root user

```bash
sudo crontab -e
```

### To edit the crontab and add a new job

```bash
crontab -e
```

### To edit other user's crontab entries

```bash
crontab -u username -e
```

### To remove all crontab entries

```bash
crontab -r
```

### To remove other user's crontab entries

```bash
crontab -u username -r
```

### Explanation

```console
+—————- minute (values: 0 - 59) (special characters: , \- \* /)  <br>
| +————- hour (values: 0 - 23) (special characters: , \- \* /) <br>
| | +———- day of month (values: 1 - 31) (special characters: , \- \* / L W C)  <br>
| | | +——- month (values: 1 - 12) (special characters: , \- \* /)  <br>
| | | | +—- day of week (values: 0 - 6) (Sunday=0 or 7) (special characters: , \- \* / L W C) <br>
| | | | |*****command to be executed
```

## See also

- [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux.md)
- [Prerequisites for Microsoft Defender for Endpoint on Linux](mde-linux-prerequisites.md)
- [Configure security settings and policies for Microsoft Defender for Endpoint on Linux](linux-preferences.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
