---
title: Manage cases natively
description: Learn about case management features across Microsoft's unified security operations (SecOps) platform.
search.appverid: met150
ms.service: unified-secops-platform
ms.author: austinmc
author: austinmccollum
ms.localizationpriority: medium
ms.date: 01/16/2025
audience: ITPro
ms.collection:
- M365-security-compliance
- tier1
- usx-security
ms.topic: conceptual

# customer intent: As a security operations center business decision maker, I want to learn about the case management tool available in Microsoft's unified SecOps platform so I can unify security tickets and case management tools so I can get visibility into, and disrupt attacks in real time across identities, endpoints, email, cloud apps, data in hybrid and multicloud environments.
---

# Manage cases natively in Microsoft's unified security operations (SecOps) platform

Collaborate and investigate in Microsoft's unified SecOps platform with builtin case management. The Case Management Starter Kit (CMSK) is the end-to-end solution that provides seamless management of security alerts, incidents and investigations. Maintain security context and work all the jobs to be done more efficiently.

## Plan for cases

The CSMK is available in the Defender portal for all Microsoft Sentinel customers that have onboarded to the unified SecOps platform. For more information on connecting a Microsoft Sentinel workspace, see [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal).

| Cases feature | Minimum permissions required |
|---|---|
| View only</br>- case queue</br>- case details</br>- tasks</br>- comments</br>- case audits | Microsoft Defender XDR Unified RBAC</br>Security operations > Security data basics (read)|
| Create and Manage</br>- cases and case tasks</br>- assign</br>- update status</br>- link and unlink incidents | Microsoft Defender XDR Unified RBAC</br>Security operations > Alerts (manage)|
| Customize case status options | Microsoft Defender XDR Unified RBAC</br>Authorization and setting > Core Security settings (manage)|

## Case queue

:::image type="content" source="media/cases-overview/cases-queue-view.png" alt-text="Screenshot of case queue.":::

Key screenshot show - Catch what others miss (run security copilot on incidents), strengthen team expertise (run security copilot for summaries)
investigations, use security copilot to train jr analyst.
TI
DEX
Vuln management

:::image type="content" source="media/cases-overview/case-details.png" alt-text="Screenshot of case details.":::

## Customize status

Architect case management to fit the needs of your security operations center (SOC). Customize the status options available to your analysts to fit the processes you have in place.

:::image type="content" source="media/cases-overview/customize-status.png" alt-text="Screenshot showing default status options and customized statuses.":::

## Link incidents

Link incidents to a case from the case or from the incident.

:::image type="content" source="media/cases-overview/link-incident-from-incident.png" alt-text="Screenshot showing the link incident option from ellipses menu in the incident view.":::

## Tasks

Tasks have the following statuses available

- New
- In progress
- Failed
- Partially completed
- Skipped
- Completed

:::image type="content" source="media/cases-overview/add-task.png" alt-text="Screenshot showing the add task pane with tasks populated for the case and 6 statuses available.":::

## Activity log

Create comments and review the audit events in the activity log.

## Related content

[Case Management Starter Kit blog announcement](https://techcommunity.microsoft.com/category/microsoft-sentinel/blog/MicrosoftSentinelBlog)
[Microsoft Defender Experts for Hunting](/defender-xdr/defender-experts-for-hunting.md)
[Hunts for Microsoft Sentinel]