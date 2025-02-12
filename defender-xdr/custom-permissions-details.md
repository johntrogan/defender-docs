---
title: Details of custom permissions in Microsoft Defender XDR Unified role-based access control (RBAC)
description: Learn about the custom permissions available in Microsoft Defender XDR Security role-based access control (RBAC)
ms.service: defender-xdr
ms.author: deniseb
author: denisebmsft
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection:
- m365-security
- tier3
ms.custom:
ms.topic: how-to
ms.date: 11/17/2024
ms.reviewer:
search.appverid: met150
---

# Permissions in Microsoft Defender XDR Unified role-based access control (RBAC)

In Microsoft Defender XDR Unified role-based access control (RBAC) you can select permissions from each permission group to customize a role.

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/microsoft-defender.md)]

**Applies to:**

- [Microsoft Defender for Endpoint Plan 2](/defender-endpoint/microsoft-defender-endpoint)
- [Microsoft Defender XDR](microsoft-365-defender.md)
- [Microsoft Defender for Identity](https://go.microsoft.com/fwlink/?LinkID=2198108)
- [Microsoft Defender for Office 365 P2](https://go.microsoft.com/fwlink/?LinkID=2158212)
- [Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management)
- [Microsoft Defender for Cloud](/azure/defender-for-cloud/defender-for-cloud-introduction)
- [Microsoft Security Exposure Management](/security-exposure-management/)
- [Microsoft Defender for Cloud Apps](/defender-cloud-apps/what-is-defender-for-cloud-apps)

<a name='microsoft-365-defender-unified-rbac-permission-details'></a>

## Microsoft Defender XDR Unified RBAC permission details

The following table lists the permissions available to configure for your users based on the tasks they need to do:

> [!NOTE]
> Unless otherwise stated, all permissions are applicable to all supported workloads and will be applied to the data scope selected during the data source and assignment stage.

### Security operations – Security data

Permissions for managing day-to-day operations and responding to incidents and advisories.

|Permission name|Level|Description|
|---|---|---|
|Security data basics|Read|View info about incidents, alerts, investigations, advanced hunting, devices, submissions, evaluation lab, and reports.|
|Alerts|Manage|Manage alerts, start automated investigations, run scans, collect investigation packages, and manage device tags.|
|Response|Manage|Take response actions, approve or dismiss pending remediation actions, and manage blocked and allowed lists for automation.|
|Basic live response|Manage|Initiate a live response session, download files, and perform read-only actions on devices remotely.|
|Advanced live response|Manage|Create live response sessions and perform advanced actions, including uploading files and running scripts on devices remotely.|
|File collection|Manage|Collect or download relevant files for analysis, including executable files.|
|Email & collaboration quarantine|Manage|View and release email from quarantine.|
|Email & collaboration advanced actions|Manage|Move or Delete email to the junk email folder, deleted items or inbox, including soft and hard delete of email.|

### Security operations – Raw data (Email & collaboration)

|Permission name|Level|Description|
|---|---|---|---|
|Email & collaboration metadata|Read|View email and collaboration data in a hunting scenarios, including advanced hunting, threat explorer, campaigns, and email entity.|
|Email & collaboration content|Read|View and download email content and attachments.|

### Security posture – Posture management

Permissions for managing the organization's security posture and performing vulnerability management.

|Permission name|Level|Description|
|---|---|---|
|Vulnerability management|Read|View Defender Vulnerability Management data for the following: software and software inventory, weaknesses, missing KBs, advanced hunting, security baselines assessment, and devices.|
|Exception handling|Manage|Create security recommendation exceptions and manage active exceptions in Defender Vulnerability Management.|
|Remediation handling|Manage|Create remediation tickets, submit new requests, and manage remediation activities in Defender Vulnerability Management.|
|Application handling|Manage|Manage vulnerable applications and software, including blocking and unblocking them in Defender Vulnerability Management.|
|Security baseline assessment|Manage|Create and manage profiles so you can assess if your devices comply to security industry baselines.|
|Exposure Management|Read / Manage|View or manage Exposure Management insights, including Microsoft Secure Score recommendations from all products that are covered by Secure Score.|

### Authorization and settings

Permissions to manages the security and system settings and to create and assign roles.

|Permission name|Level|Description|
|---|---|---|
|Authorization|Read / Manage|View or manage device groups, and custom and built-in roles.|
|Core security settings|Read / Manage|View or manage core security settings for the Microsoft Defender portal.|
|Detection tuning| Manage |Manage tasks related to detections in the Microsoft Defender portal including Custom detections, Alerts Tuning and Threat Indicators of compromise.|
|System settings|Read / Manage|View or manage general systems settings for the Microsoft Defender portal.|

## Next steps

- [Create custom roles](create-custom-rbac-roles.md)
- [Activate Microsoft Defender XDR Unified RBAC](activate-defender-rbac.md)
[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
