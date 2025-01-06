---
title: Troubleshoot performance issues for Microsoft Defender for Endpoint on Linux
description: Troubleshoot performance issues in Microsoft Defender for Endpoint on Linux.
ms.service: defender-endpoint
ms.author: deniseb
author: deniseb
ms.reviewer: gopkr
ms.localizationpriority: medium
ms.date: 12/04/2024
manager: deniseb
audience: ITPro
ms.collection:
- m365-security
- tier3
- mde-linux
ms.topic: conceptual
ms.subservice: linux
search.appverid: met150
---

# Troubleshoot performance issues for Microsoft Defender for Endpoint on Linux

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to**:

- Microsoft Defender for Endpoint Server
- [Microsoft Defender for Servers](/azure/defender-for-cloud/integration-defender-for-endpoint)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://signup.microsoft.com/create-account/signup?products=7f379fee-c4f9-4278-b0a1-e4c8c2fcdf7e&ru=https://aka.ms/MDEp2OpenTrial?ocid=docs-wdatp-investigateip-abovefoldlink)

This document provides instructions on how to narrow down performance issues related to Defender for Endpoint on Linux using the available diagnostic tools to be able to understand and mitigate the existing resource shortages and the processes that are making the system into such situations. Performance problems are mainly caused by bottlenecks in one or more hardware subsystems, depending on the profile of resource utilization on the system. Sometimes applications are sensitive to disk I/O resources and may need more CPU capacity, and sometimes some configurations are not sustainable, and may trigger too many new processes, and open too many file descriptors.

Depending on the applications that you are running and your device characteristics, you may experience suboptimal performance when running Defender for Endpoint on Linux. In particular, applications or system processes that access many resources such as CPU, Disk, and Memory over a short timespan can lead to performance issues in Defender for Endpoint on Linux.

> [!WARNING]
> Before starting, **please make sure that other security products are not currently running on the device**. Multiple security products may conflict and impact the host performance.

## Troubleshoot performance issues using Real-time Protection Statistics

**Applies to:**
- Only performance issues related to antivirus

Real-time protection (RTP) is a feature of Defender for Endpoint on Linux that continuously monitors and protects your device against threats. It consists of file and process monitoring and other heuristics.

The following steps can be used to troubleshoot and mitigate these issues:

1. Disable real-time protection using one of the following methods and observe whether the performance improves. This approach helps narrow down whether Defender for Endpoint on Linux is contributing to the performance issues. If your device is not managed by your organization, real-time protection can be disabled from the command line:

   ```bash
   mdatp config real-time-protection --value disabled
   ```

   ```console
   Configuration property updated
   ```

   If your device is managed by your organization, real-time protection can be disabled by your administrator using the instructions in [Set preferences for Defender for Endpoint on Linux](linux-preferences.md).

   > [!NOTE]
   > If the performance problem persists while real-time protection is off, the origin of the problem could be the endpoint detection and response (EDR) component. In this case please follow the steps from the **Troubleshoot performance issues using Microsoft Defender for Endpoint Client Analyzer** section of this article.

2. To find the applications that are triggering the most scans, you can use real-time statistics gathered by Defender for Endpoint on Linux.

   > [!NOTE]
   > This feature is available in version 100.90.70 or newer.

   This feature is enabled by default on the `Dogfood` and `InsiderFast` channels. If you're using a different update channel, this feature can be enabled from the command line:

   ```bash
   mdatp config real-time-protection-statistics --value enabled
   ```

   This feature requires real-time protection to be enabled. To check the status of real-time protection, run the following command:

   ```bash
   mdatp health --field real_time_protection_enabled
   ```

   Verify that the `real_time_protection_enabled` entry is `true`. Otherwise, run the following command to enable it:

   ```bash
   mdatp config real-time-protection --value enabled
   ```

   ```console
   Configuration property updated
   ```

   To collect current statistics, run:

   ```bash
   mdatp diagnostic real-time-protection-statistics --output json
   ```

   > [!NOTE]
   > Using `--output json` (note the double dash) ensures that the output format is ready for parsing.

   The output of this command shows all processes and their associated scan activity.

3. On your Linux system, download the sample Python parser **high_cpu_parser.py** using the command:

   ```bash
   wget -c https://raw.githubusercontent.com/microsoft/mdatp-xplat/master/linux/diagnostic/high_cpu_parser.py
   ```

   The output of this command should be similar to the following:

   ```console
   --2020-11-14 11:27:27-- https://raw.githubusercontent.com/microsoft.mdatp-xplat/master/linus/diagnostic/high_cpu_parser.py
   Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 151.101.xxx.xxx
   Connecting to raw.githubusercontent.com (raw.githubusercontent.com)| 151.101.xxx.xxx| :443... connected.
   HTTP request sent, awaiting response... 200 OK
   Length: 1020 [text/plain]
   Saving to: 'high_cpu_parser.py'
   100%[===========================================>] 1,020    --.-K/s   in 0s
   ```

4. Type the following commands:

   ```bash
   mdatp diagnostic real-time-protection-statistics --output json | python high_cpu_parser.py
   ```

   The output of the above is a list of the top contributors to performance issues. The first column is the process identifier (PID), the second column is the process name, and the last column is the number of scanned files, sorted by impact. For example, the output of the command will be something like the below:

   ```console
   ... > mdatp diagnostic real-time-protection-statistics --output json | python high_cpu_parser.py | head
   27432 None 76703
   73467 actool    1249
   73914 xcodebuild 1081
   73873 bash 1050
   27475 None 836
   1    launchd     407
   73468 ibtool     344
   549  telemetryd_v1   325
   4764 None 228
   125  CrashPlanService 164
   ```

   To improve the performance of Defender for Endpoint on Linux, locate the one with the highest number under the `Total files scanned` row and add an exclusion for it. For more information, see [Configure and validate exclusions for Defender for Endpoint on Linux](linux-exclusions.md).

   > [!NOTE]
   > The application stores statistics in memory and only keeps track of file activity since it was started and real-time protection was enabled. Processes that were launched before or during periods when real time protection was off are not counted. Additionally, only events which triggered scans are counted.

## Troubleshoot performance issues using Hot Event Sources

**Applies to:**
-  Performance issues in global files and executables.

Hot event sources is a feature that will specifically show the events which have highest count (highest frequency of occurrence) for generating file events.

   > [!NOTE]
   > These commmands require you to have root permissions. Ensure that sudo can be used.

First, check the log level on your machine.

   ```bash
   mdatp health --field log_level
   ```
If it's not on "debug" you need to change it for a detailed report regarding hot files / executables.

   ```bash
   sudo mdatp log level set --level debug
   ```
   ```console
   Log level configured successfully
   ```

To collect current statistics (for files), 

   ```bash
   sudo mdatp diagnostic hot-event-sources files
   ```
The output of which will look similar to the following (JSON);

   ```console
   {
       "startTime": "1729535104539160",
       "endTime": "1729535117570766",
       "totalEvent": "11373",
       "eventSource": [
           {
               "authCount": "2832",
               "csId": "",
               "notifyCount": "0",
               "path": "/mnt/RamDisk/postgres_data/pg_wal/0000000100000014000000A5",
               "pidCount": "1",
               "teamId": ""
           },
           {
               "authCount": "632",
               "csId": "",
               "notifyCount": "0",
               "path": "/mnt/RamDisk/postgres_data/base/635594/2601",
               "pidCount": "1",
               "teamId": ""
           }
       ]
   }
   ```
And similarly output on the console looks like the following (this is just a snippet of the entire output). Here the first row is the count (frequency of occurrence) and the second is the file path.

   ```console
   Total Events: 11179 Time: 12s. Throughput: 75.3333 events/sec. 
   =========== Top 684 Hot Event Sources ===========
   count   file path
   2832    /mnt/RamDisk/postgres_data/pg_wal/0000000100000014000000A5
   632     /mnt/RamDisk/postgres_data/base/635594/2601
   619     /mnt/RamDisk/postgres_data/base/635597/2601
   618     /mnt/RamDisk/postgres_data/base/635596/2601
   618     /mnt/RamDisk/postgres_data/base/635595/2601
   616     /mnt/RamDisk/postgres_data/base/635597/635610
   615     /mnt/RamDisk/postgres_data/base/635596/635602
   614     /mnt/RamDisk/postgres_data/base/635595/635606
   514     /mnt/RamDisk/postgres_data/base/635594/635598_fsm
   496     /mnt/RamDisk/postgres_data/base/635597/635610_fsm
   ```

and similarly for the executables, 

```bash
sudo mdatp diagnostic hot-event-sources executables
```

The output of which will look similar to the following (JSON);

   ```console
   {
       "startTime": "1729534260988396",
       "endTime": "1729534280026883",
       "totalEvent": "48165",
       "eventSource": [
           {
               "authCount": "8126",
               "csId": "",
               "notifyCount": "0",
               "path": "/usr/lib/postgresql/12/bin/psql",
               "pidCount": "2487",
               "teamId": ""
           },
           {
               "authCount": "5127",
               "csId": "",
               "notifyCount": "0",
               "path": "/usr/lib/postgresql/12/bin/postgres (deleted)",
               "pidCount": "2144",
               "teamId": ""
           }
       ]
   }
   ```
Output on the console;

   ```console
   Total Events: 47382 Time: 18s. Throughput: 157 events/sec.
   =========== Top 23 Hot Event Sources ===========
   count    executable path
   8216    /usr/lib/postgresql/12/bin/psql
   5721    /usr/lib/postgresql/12/bin/postgres (deleted)
   3557    /usr/bin/bash
   378     /usr/bin/clamscan
   88      /usr/bin/sudo
   70      /usr/bin/dash
   30      /usr/sbin/zabbix_agent2
   10      /usr/bin/grep
   8       /usr/bin/gawk
   6       /opt/microsoft/mdatp/sbin/wdavdaemonclient
   4       /usr/bin/sleep
   ```
To improve this performance, locate the path with the highest number in `count` row and add a process exclusion (in case of executable) or a file/folder exclusion (in case of file) for it. For more information, see [Configure and validate exclusions for Defender for Endpoint on Linux](linux-exclusions.md).

## Troubleshoot performance issues using eBPF Statistics

**Applies to:**
- All file/ process events, specifically for syscall based performance issues.

eBPF (extended Berkeley Packet Filter) statistics command gives insights into the top event/process that's generating the most file events, along with their syscall ids.

To collect current statistics using eBPF statistics, run:

   ```bash
   mdatp diagnostic ebpf-statistics
   ```

   The output is always on the console and would look similar to the following (this is only a snippet of the entire output):

   ```console
   Top initiator paths:
   /usr/lib/postgresql/12/bin/psql : 902
   /usr/bin/clamscan : 349
   /usr/sbin/zabbix_agent2 : 27
   /usr/lib/postgresql/12/bin/postgres : 10
   
   Top syscall ids:
   80 : 9034
   57 : 8932
   60 : 8929
   59 : 4942
   112 : 4898
   90 : 179
   87 : 170
   119 : 32
   288 : 19
   41 : 15
   ```

To improve this performance, locate the one with the highest `count` in the `Top initiator path` row and add an exclusion for it. For more information, see [Configure and validate exclusions for Defender for Endpoint on Linux](linux-exclusions.md).
   
## Troubleshoot performance issues using Microsoft Defender for Endpoint Client Analyzer

**Applies to:**
- Performance issues of all available Defender for Endpoint components such as AV and EDR

The Microsoft Defender for Endpoint Client Analyzer (MDECA) can collect traces, logs, and diagnostic information in order to troubleshoot performance issues on [onboarded devices](onboard-configure.md) on Linux.

> [!NOTE]
> - The Microsoft Defender for Endpoint Client Analyzer tool is regularly used by Microsoft Customer Support Services (CSS) to collect information such as (but not limited to) IP addresses, PC names that will help troubleshoot issues you may be experiencing with Microsoft Defender for Endpoint. For more information about our privacy statement, see [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement).
> - As a general best practice, it is recommended to update the [Microsoft Defender for Endpoint agent to latest available version](mac-whatsnew.md) and confirming that the issue still persists before investigating further.

To run the client analyzer for troubleshooting performance issues, see [Run the client analyzer on macOS and Linux](run-analyzer-macos-linux.md).

## Configure Global Exclusions for better performance

Configure Microsoft Defender for Endpoint on Linux with exclusions for the processes or disk locations that contribute to the performance issues. For more information, see [Configure and validate exclusions for Microsoft Defender for Endpoint on Linux](linux-exclusions.md). IF you still have performance issues, contact support for further instructions and mitigation.

### Rate Limiter

The XMDEClientAnalyzer support tool contains syntax that can be used to limit the number of events being reported by the auditD plugin. This option will set the rate limit globally for AuditD causing a drop in all the audit events.

> [!NOTE]
> This functionality should be carefully used as limits the number of events being reported by the auditd subsystem as a whole. This could reduces the number of events for other subscribers as well.

The ratelimit option can be used to enable/disable this rate limit.

Enable: `./mde_support_tool.sh ratelimit -e true`

Disable: `./mde_support_tool.sh ratelimit -e false`

When the ratelimit is enabled a rule will be added in AuditD to handle 2500 events/sec.

> [!NOTE]
> Please contact Microsoft support if you need assistance with analyzing and mitigating AuditD related performance issues, or with deploying AuditD exclusions at scale.

## See also

- [Investigate agent health issues](health-status.md)

[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
