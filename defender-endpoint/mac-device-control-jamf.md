---
title: Deploy and manage device control using JAMF 
description: Learn how to use device control policies using JAMF.
ms.service: defender-endpoint
author: emmwalshh
ms.author: ewalsh
ms.reviewer: joshbregman
manager: deniseb
ms.localizationpriority: medium
audience: ITPro
ms.collection: 
- m365-security
- tier3
- mde-macos
ms.topic: conceptual
ms.subservice: macos
search.appverid: met150
ms.date: 04/30/2024
---

# Deploy and manage Device Control using JAMF

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 1](microsoft-defender-endpoint.md)
- [Microsoft Defender for Endpoint Plan 2](microsoft-defender-endpoint.md)
- [Microsoft Defender XDR](/defender-xdr)
- [Microsoft Defender for Business](/defender-business)

> Want to experience Microsoft Defender for Endpoint? [Sign up for a free trial.](https://signup.microsoft.com/create-account/signup?products=7f379fee-c4f9-4278-b0a1-e4c8c2fcdf7e&ru=https://aka.ms/MDEp2OpenTrial?ocid=docs-wdatp-exposedapis-abovefoldlink)

Microsoft Defender for Endpoint Device Control feature enables you to audit, allow, or prevent the read, write, or execute access to removable storage, and allows you to manage iOS and Portable device and Bluetooth media with or without exclusions.

## Licensing requirements

Before you get started with Removable Storage Access Control, you must confirm your [Microsoft 365 subscription](https://www.microsoft.com/microsoft-365/compare-microsoft-365-enterprise-plans?rtc=3). To access and use Removable Storage Access Control, you must have Microsoft 365 E3.

[!INCLUDE [Microsoft Defender for Endpoint third-party tool support](../includes/support.md)]

## Deploy policy by using JAMF

### Step 1: Creating a JSON policy

Device Control on MacOS is defined through a JSON policy. This policy should have the appropriate groups, rules, and settings defined to tailor specific customer conditions. For example some enterprises might need to block all removable media devices entirely while others might have specific exceptions for a vendor or serial number. Microsoft has a [local Github repository](https://github.com/microsoft/mdatp-devicecontrol/tree/main/macOS/policy/samples"https://github.com/microsoft/mdatp-devicecontrol/tree/main/macos/policy/samples") that can be utilized as building blocks to assist enterprises in building their policies.

See [Device Control for macOS](mac-device-control-overview.md) for information about settings, rules, and groups.

### Step 2: Validating a JSON policy

Enterprises need to validate their JSON policies after it has been created to ensure there are no syntax or configuration errors. The schema for device control policies that is used can be [located here](https://github.com/microsoft/mdatp-devicecontrol/blob/main/macOS/policy/device_control_policy_schema.json"https://github.com/microsoft/mdatp-devicecontrol/blob/main/macos/policy/device_control_policy_schema.json"). The Defender application has a built in functionality to compare provided JSON to the defined schema. 

- Save your configuration on a local device as a .json file

- Ensure you have access to "mdatp" commands. If your device is already onboarded then you will have this functionality.

- Run **mdatp device-control policy validate --path <pathtojson>**

### Step 3: Update MDE Preferences Schema

The [MDE Preferences schema](https://github.com/microsoft/mdatp-xplat/blob/master/macos/schema/schema.json) is updated to include the new `deviceControl/policy` key. The existing MDE Preferences configuration profile should be updated to use the new schema file's content.

:::image type="content" source="media/macos-device-control-jamf-mde-preferences-schema.png" alt-text="Shows where to edit the Microsoft Defender for Endpoint Preferences Schema to update." lightbox="media/macos-device-control-jamf-mde-preferences-schema.png":::

### Step 4: Add Device Control Policy to MDE Preferences

A new 'Device Control' property is now available to add to the UX.  

1. Select the topmost **Add/Remove properties** button, then select **Device Control** and press **Apply**.

:::image type="content" source="media/macos-device-control-jamf-device-control-property.png" alt-text="Shows how to add Device Control in Microsoft Defender for Endpoint" lightbox="media/macos-device-control-jamf-device-control-property.png":::

2. Next, scroll down until you see the **Device Control** property (it's the bottommost entry), and select **Add/Remove properties** directly underneath it.

3. Select **Device Control Policy**, and then select **Apply**.  

:::image type="content" source="media/macos-device-control-jamf-device-control-add-remove-property.png" alt-text="Shows how to apply Device Control Policy in Microsoft Defender for Endpoint." lightbox="media/macos-device-control-jamf-device-control-add-remove-property.png":::

4. To finish, copy and paste the Device Control policy JSON into the text box, and save your changes to the configuration profile.

:::image type="content" source="media/macos-device-control-jamf-device-control-policy-json.png" alt-text="Shows where to add the Device Control policy JSON in Microsoft Defender for Endpoint." lightbox="media/macos-device-control-jamf-device-control-policy-json.png":::

## See also

- [Device Control for macOS](mac-device-control-overview.md)
- [Deploy and manage Device Control using Intune](mac-device-control-intune.md)
- [macOS Device Control frequently asked questions (FAQ)](mac-device-control-faq.md)
[!INCLUDE [Microsoft Defender for Endpoint Tech Community](../includes/defender-mde-techcommunity.md)]
