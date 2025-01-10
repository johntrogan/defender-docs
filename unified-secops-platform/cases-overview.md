---
title: Manage cases natively with the Case Management Starter Kit (Preview)
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

The Case Management Starter Kit (CMSK) is the beginning of an end-to-end solution that provides seamless management of security alerts, incidents, and investigations. This first step builds rich collaboration, customization, evidence collection, and reporting within Microsoft's unified SecOps platform. SOC analysts maintain security context, work more efficiently and respond faster to attacks when they manage case work without leaving the Defender portal.

## Plan for cases

The CMSK is available in the Defender portal for all Microsoft Sentinel customers that have onboarded to the unified SecOps platform. For more information on connecting a Microsoft Sentinel workspace, see [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal).

| Cases feature | Minimum permissions required |
|---|---|
| View only</br>- case queue</br>- case details</br>- tasks</br>- comments</br>- case audits | Microsoft Defender XDR Unified RBAC</br>Security operations > Security data basics (read)|
| Create and Manage</br>- cases and case tasks</br>- assign</br>- update status</br>- link and unlink incidents | Microsoft Defender XDR Unified RBAC</br>Security operations > Alerts (manage)|
| Customize case status options | Microsoft Defender XDR Unified RBAC</br>Authorization and setting > Core Security settings (manage)|

Bring the best processes from your non-Microsoft ticketing system to the CMSK. SecOps teams 

Here are some of the priorities that are important to us as we work towards a robust case management experience:

- Automation
- Rich text with images
- ?

## Case queue

View and filter cases from **Cases** in the Defender portal.

:::image type="content" source="media/cases-overview/cases-queue-view.png" alt-text="Screenshot of case queue.":::

Each case on the page

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

:::image type="content" source="media/cases-overview/add-task-small.png" alt-text="Screenshot showing the task pane with tasks populated for the case and statuses available." lightbox="media/cases-overview/add-task-small.png":::

## Activity log

Create comments and review the audit events in the activity log.

## Related content

[Case Management Starter Kit blog announcement](https://techcommunity.microsoft.com/category/microsoft-sentinel/blog/MicrosoftSentinelBlog)
[Microsoft Defender Experts for Hunting](../defender-xdr/defender-experts-for-hunting.md)
[Hunts for Microsoft Sentinel]