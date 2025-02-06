---
title: Use the installer script to deploy Microsoft Defender for Endpoint on Linux
description: Describes how to deploy Microsoft Defender for Endpoint on Linux using an installer script.
ms.service: defender-endpoint
ms.author: ewalsh
author: emmwalshh
ms.reviewer: gopkr; meghapriya
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
ms.date: 02/05/2025
---

# Use the installer script to deploy Microsoft Defender for Endpoint on Linux

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to**:

- Microsoft Defender for Endpoint Server
- [Microsoft Defender for Servers](/azure/defender-for-cloud/integration-defender-for-endpoint)

> Want to experience Defender for Endpoint? [Sign up for a free trial.](https://signup.microsoft.com/create-account/signup?products=7f379fee-c4f9-4278-b0a1-e4c8c2fcdf7e&ru=https://aka.ms/MDEp2OpenTrial?ocid=docs-wdatp-investigateip-abovefoldlink)

> [!TIP]
> Looking for advanced guidance on deploying Microsoft Defender for Endpoint on Linux? See [Advanced deployment guide on Defender for Endpoint on Linux](comprehensive-guidance-on-linux-deployment.md).

This article describes how to deploy Microsoft Defender for Endpoint on Linux using an installer script.

## Introduction

This article describes how to automate the deployment of Microsoft Defender for Endpoint on Linux using an installer script. The script identifies the distribution and version, selects the right repository, pulls the latest agent version, and onboards the device to Defender for Endpoint. This method greatly simplifies the deployment process and is one of the most recommended methods.

:::image type="content" source="media/linux-script-image.png" alt-text="Onboard Linux Server" lightbox="media/linux-script-image.png":::

## Prerequisites and system requirements

Before you get started, see [Microsoft Defender for Endpoint on Linux](microsoft-defender-endpoint-linux.md) for a description of prerequisites and system requirements for the current software version.

## Installer script

1. Download the onboarding package from Microsoft Defender portal by following these steps:

    1. In the [Microsoft Defender portal](https://security.microsoft.com), go to **Settings** > **Endpoints** > **Device management** > **Onboarding**.
    
    2. In the first drop-down menu, select **Linux Server** as the operating system.
    
    3. In the second drop-down menu, select **Local Script** as the deployment method.
    
    4. Select **Download onboarding package**. Save the file as `WindowsDefenderATPOnboardingPackage.zip`.
    
    5. From a command prompt, verify that you have the file, and extract the contents of the archive:

        ```bash
        unzip WindowsDefenderATPOnboardingPackage.zip
        ```

        ```console
        Archive:  WindowsDefenderATPOnboardingPackage.zip
        inflating: MicrosoftDefenderATPOnboardingLinuxServer.py
        ```

       > [!WARNING]
       > Repackaging the Defender for Endpoint installation package isn't a supported scenario. Doing so can negatively affect the integrity of the product and lead to adverse results, including but not limited to triggering tampering alerts and updates failing to apply. 

       > [!IMPORTANT]
       > If you miss this step, any command executed shows a warning message indicating that the product is unlicensed. Also the mdatp health command returns a value of false. 

2. Download the [installer bash script](https://github.com/microsoft/mdatp-xplat/blob/master/linux/installation/mde_installer.sh) provided in our public [GitHub repository](https://github.com/microsoft/mdatp-xplat/).

2. Grant executable permissions to the installer script:
  
   ```bash
   chmod +x mde_installer.sh
   ```

3. Run the installer script with parameters like *onboard*, *channel*, and *real-time protection*, according to your business needs. The following table lists several use cases and sample commands:

   | Use case | Command |
   |---|---|
   | Fresh install | `sudo ~/mde_installer.sh --install --channel prod --onboard ~/MicrosoftDefenderATPOnboardingLinuxServer.py --min_req -y –-mdatp "xx.xx.xx.xx" ` |
   | Upgrading to the latest version | `sudo ~/mde_installer.sh --upgrade -y` |
   | Upgrading to a specific version | `sudo ~/mde_installer.sh --upgrade -y –-mdatp 101.24082.0004` |
   | Downgrading to a specific version | `sudo ~/mde_installer.sh --downgrade -y –-mdatp 101.24082.0004` |
   | Remove `mdatp` | `sudo ~/mde_installer.sh --remove -y` |

   > [!NOTE]
   > Upgrading your operating system to a new major version after the product installation requires the product to be reinstalled. You need to uninstall the existing Defender for Endpoint on Linux, upgrade the operating system, and then reconfigure Defender for Endpoint on Linux.

## Verify deployment status

Run an antivirus detection test to verify that the device is properly onboarded and reporting to the service. Perform the following steps on the newly onboarded device:

1. Ensure that real-time protection is enabled (denoted by a result of `true` from running the following command):

   ```bash
   mdatp health --field real_time_protection_enabled
   ```

   If it isn't enabled, execute the following command:

   ```bash
   mdatp config real-time-protection --value enabled
   ```

2. To run a detection test, open a terminal window, and then run the following command:

   ``` bash
   curl -o /tmp/eicar.com.txt https://secure.eicar.org/eicar.com.txt
   ```
     
   To run more detection tests on zipped files, use either of the following commands:

   ```bash
   curl -o /tmp/eicar_com.zip https://secure.eicar.org/eicar_com.zip
   curl -o /tmp/eicarcom2.zip https://secure.eicar.org/eicarcom2.zip
   ```

   Files should be quarantined by Defender for Endpoint on Linux.

3. To get a list of detected threats, use the following command:

   ```bash
   mdatp threat list
   ```
     
2. To run an EDR detection test and simulate a detection, perform the following steps on a newly onboarded device. This process helps to verify that the device is properly onboarded and reporting to the service. 

   1. Verify that the onboarded Linux server appears in the Microsoft Defender portal. If this is the first onboarding of the machine, it can take up to 20 minutes until it appears.

   2. Download and extract the [script file](https://aka.ms/MDE-Linux-EDR-DIY) to an onboarded Linux server, and then run the following command: `./mde_linux_edr_diy.sh`.

      After a few minutes, a detection should be raised in the Microsoft Defender portal.

   3. Check the alert details, machine timeline, and perform your typical investigation steps.

## Microsoft Defender for Endpoint package external package dependencies

If the Microsoft Defender for Endpoint installation fails due to missing dependencies errors, you can manually download the required dependencies. 

The following external package dependencies exist for the `mdatp` package:

| Package | Dependencies |
|--|--|
| `mdatp RPM` | - `glibc >= 2.17`<br>- `policycoreutils`<br>- `selinux-policy-targeted`<br>- `mde-netfilter` |
| DEBIAN | - `libc6 >= 2.23`<br>- `uuid-runtime`<br>- `mde-netfilter` |
| Mariner | - `attr`<br>- `diffutils`<br>- `libacl`<br>- `libattr`<br>- `libselinux-utils`<br>- `selinux-policy`<br>- `policycoreutils`<br>- `mde-netfilter` |

> [!NOTE]
> Beginning with version `101.24082.0004`, Defender for Endpoint on Linux no longer supports the `Auditd` event provider. We're transitioning completely to the more efficient eBPF technology.
> If `eBPF` isn't supported on your machines, or if there are specific requirements to remain on `Auditd`, and your machines are using Defender for Endpoint on Linux version `101.24072.0001` or older, the following extra dependency package exists for mdatp:
> | Package | Dependencies |
> |--|--|
> | `mdatp RPM` | - `audit`<br>-  `semanage` |
> | DEBIAN | `auditd` |
> | Mariner | `audit`| 

The `mde-netfilter` package also has the following package dependencies:

| Package | Dependencies |
|--|--|
| DEBIAN | - `libnetfilter-queue1`<br/>- `libglib2.0-0` |
| RPM | - `libmnl` <br/>- `libnfnetlink`<br/>- `libnetfilter_queue`<br/>- `glib2` |
| Mariner | - `libnfnetlink`<br/>- `libnetfilter_queue` |

If the Microsoft Defender for Endpoint installation fails due to missing dependencies errors, you can manually download the prerequisite dependencies.

## Troubleshoot installation issues

- For information on how to find the log that's generated automatically when an installation error occurs, see [Log installation issues](/defender-endpoint/linux-resources#log-installation-issues). 

- For information about common installation issues, see [Installation issues](/defender-endpoint/linux-support-install). 

- If the health of the device is false, see [Investigate agent health issues](health-status.md). 

- For product performance issues, see [Troubleshoot performance issues for Microsoft Defender for Endpoint on Linux](linux-support-perf.md). 

- For proxy and connectivity issues, see [Troubleshoot cloud connectivity issues for Microsoft Defender for Endpoint on Linux](linux-support-connectivity.md). 

- To get support from Microsoft, open a support ticket, and provide the log files created by using the [Microsoft Defender for Endpoint client analyzer tool](run-analyzer-linux.md). 

## How to swtich between channels

To switch channels, such as changing from Insiders-Fast to Production, follow these steps:

1. Uninstall the `Insiders-Fast channel` version of Defender for Endpoint on Linux.

   ```bash
   sudo yum remove mdatp
   ```

2. Disable the Defender for Endpoint on Linux Insiders-Fast repo.

   ```bash
   sudo yum repolist
   ```

   > [!NOTE]
   > The output should show `packages-microsoft-com-fast-prod`.

   ```bash
   sudo yum-config-manager --disable packages-microsoft-com-fast-prod
   ```

3. Redeploy Microsoft Defender for Endpoint on Linux using the Production channel.

Defender for Endpoint on Linux can be deployed from one of the following channels (denoted as [channel]): 
- `insiders-fast`
- `insiders-slow`
- `prod` 

Each of these channels corresponds to a Linux software repository. The instructions in this article describe configuring your device to use one of these repositories. 

The choice of the channel determines the type and frequency of updates that are offered to your device. Devices in insiders-fast are the first ones to receive updates and new features, followed later by insiders-slow and lastly by prod. 

In order to preview new features and provide early feedback, it's recommended that you configure some devices in your enterprise to use either `insiders-fast` or `insiders-slow`. 

> [!WARNING]
> Switching the channel after the initial installation requires the product to be reinstalled. To switch the product channel: uninstall the existing package, re-configure your device to use the new channel, and follow the steps in this document to install the package from the new location. 

## See also

- [Investigate agent health issues](health-status.md)

> [!TIP]
> Do you want to learn more? Engage with the Microsoft Security community in our Tech Community: [Microsoft Defender for Endpoint Tech Community](https://techcommunity.microsoft.com/category/microsoft-defender-for-endpoint/discussions/microsoftdefenderatp)
