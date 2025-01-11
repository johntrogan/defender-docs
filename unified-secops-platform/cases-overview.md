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

The Case management starter kit (CMSK) is the beginning of an end-to-end solution that provides seamless management of security alerts, incidents, and investigations. This first step builds rich collaboration, customization, evidence collection, and reporting within Microsoft's unified SecOps platform. SOC analysts maintain security context, work more efficiently, and respond faster to attacks when they manage case work without leaving the Defender portal.

> [!IMPORTANT]
> Some information in this article relates to a prereleased product which may be substantially modified before it's commercially released. Microsoft makes no warranties, expressed or implied, with respect to the information provided here.

## Plan for cases

The CMSK is available in the Defender portal for all Microsoft Sentinel customers that have onboarded to the unified SecOps platform. For more information on connecting a Microsoft Sentinel workspace, see [Microsoft Sentinel in the Defender portal](/azure/sentinel/microsoft-sentinel-defender-portal).

Bring the best processes from your non-Microsoft ticketing system to the CMSK. Consider these foundational features to make case maanagement fit your needs.

- Define your own case workflow with custom status values
- Decide how to assign tasks and configure due dates
- Handle escalations and complex cases by linking multiple incidents to a case
- Link an incident to multiple cases to spread the work out and track service level agreements
- Manage access to your cases using RBAC

Use this table to plan your roles for case management:

| Cases feature | Minimum permissions required in Microsoft Defender XDR Unified RBAC |
|---|---|
| View only</br>- case queue</br>- case details</br>- tasks</br>- comments</br>- case audits | Security operations > Security data basics (read)|
| Create and Manage</br>- cases and case tasks</br>- assign</br>- update status</br>- link and unlink incidents | Security operations > Alerts (manage)|
| Customize case status options | Authorization and setting > Core Security settings (manage)|

Here are some of the priorities important to us as we work towards a robust case management experience:

- Automation
- Rich text with images
- ?

## Case queue

Select **Cases** in the Defender portal to access the CMSK. Filter your cases view to fit what you need to focus on.

:::image type="content" source="media/cases-overview/cases-queue-view.png" alt-text="Screenshot of case queue.":::

Each case has a page which allows analysts to manage the case and displays the following features:

| Displayed case feature | Manage case options | Default value |
|:---|:---|:---|
| Priority| `Very low`, `Low`, `Medium`, `High`, `Critical` | none |
| [Status](#customize-status) | Set by analysts, customizable by admins | `New`|
| Assigned to | A single user or group in the tenant | none |
| Description | Plain text | none |
| Case details | Case ID | Case IDs start at 1000 and aren't deleted. Use custom statuses and filters to archive cases. Case numbers are automatically set.|
| | Created by </br>Created on</br>Last updated by</br>Last updated on | automatically set |
| | Due on</br>Linked incidents | none |
| [Activity log](#activity-log) | Add and edit your own comments in plain text | none |
| | View audit events | events are added automatically |
| [Tasks](#tasks) | Add, edit, and delete tasks | none |
| [Linked incidents](#link-incidents) | Link and unlink one or more incidents | none |

In the following example, a threat hunter is investigating a hypothetical "Burrowing" attack that consists of multiple MITRE ATT&CK techniques and IoCs.

:::image type="content" source="media/cases-overview/case-details.png" alt-text="Screenshot of case details." lightbox="media/cases-overview/case-details.png":::

## Customize status

Architect case management to fit the needs of your security operations center (SOC). Customize the status options available to your analysts to fit the processes you have in place.

Following the previous example, the SOC admins configured statuses enabling threat hunters to keep a backlog of threats for triage on a weekly basis. Custom statuses such as *Research phase* and *Generating hypothesis* match this threat hunting team's established process.

:::image type="content" source="media/cases-overview/customize-status.png" alt-text="Screenshot showing default status options and customized statuses.":::

## Tasks

Add tasks to manage granular components of your cases. Each task comes with its own name, status, priority, owner, and due date. With this information, you always know who is accountable to complete which task and by what time, ensuring all necessary steps are completed.

:::image type="content" source="media/cases-overview/add-task-small.png" alt-text="Screenshot showing the task pane with tasks populated for the case and statuses available." lightbox="media/cases-overview/add-task.png":::
</br>*Image shows the following task statuses available: New, In progress, Failed, Partially completed, Skipped, Completed*

## Link incidents

Linking a case and an incident helps your SOC teams collaborate in the method that works best for them. For example, a threat hunter who finds malicious activity and created an incident for the incident response(IR) team. That threat hunter links the incident to a case so it's clear they're related. Now the IR team understands the context of hunt that found the activity.

:::image type="content" source="media/cases-overview/link-incidents.png" alt-text="Screenshot showing linked incidents for the hypothetical burrowing attack case.":::

Alternatively, if the IR team needs to escalate one or more incidents to the hunting team, they can create a case and link the incidents there. Create and link a case from incident management, **Investigation & response > Incidents & alerts > Incidents**.

:::image type="content" source="media/cases-overview/link-incident-from-incident.png" alt-text="Screenshot showing the link incident option from ellipses menu in the incident view.":::

## Activity log

Create comments and review the audit events in the activity log. Need to write down temporary notes, or that key detection logic to pass along? Comments are a great place to quickly add information to a case without creating an another task.

:::image type="content" source="media/cases-overview/informal-comments.png" alt-text="Screenshot showing informal comments between analysts.":::

Audit activity shows the latest events at the top. Change the filter if you need to focus on comments or audit history.

## Related content

[Case Management Starter Kit blog announcement](https://techcommunity.microsoft.com/category/microsoft-sentinel/blog/MicrosoftSentinelBlog)
[Microsoft Defender Experts for Hunting](/defender-xdr/defender-experts-for-hunting)
[Hunts for Microsoft Sentinel](/azure/sentinel/hunts)