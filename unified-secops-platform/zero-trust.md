---
title: Zero Trust with unified security operations | Microsoft Defender
description: Learn how implementing Microsoft's unified security operations platform can help you deploy a Zero Trust architecture.
author: batamig
ms.author: bagol
ms.service: unified-secops-platform
ms.topic: concept-article #Don't change.
ms.date: 01/16/2025
ms.collection:
- usx-security
---

# Zero Trust with Microsoft's unified security operations platform

Zero Trust is a security strategy for designing and implementing the following sets of security principles:

|Verify explicitly  |Use least privilege access  |Assume breach  |
|---------|---------|---------|
|Always authenticate and authorize based on all available data points.     | Limit user access with Just-In-Time and Just-Enough-Access (JIT/JEA), risk-based adaptive policies, and data protection.        | Minimize blast radius and segment access. Verify end-to-end encryption and use analytics to get visibility, drive threat detection, and improve defenses.        |

This article describes how Microsoft's unified security operations (SecOps) platform provides centralized access to the tools and capabilities necessary to implement a comprehensive Zero Trust solution.

## Verify explicitly with unified SecOps

To effectively verify explicitly, Microsoft's unified SecOps platform provides a variety of tools and services to ensure that every access request is authenticated and authorized based on comprehensive data analysis. For example:

- **Microsoft Sentinel** collects data from across the environment and analyzes threats and anomalies so that your organization and any automation implemented, can act based on all available and verified data points.

- **Microsoft Defender XDR** provides extended detection and response across users, identities, devices, apps, and emails. Add **Microsoft Defender for Cloud** to stretch that threat protection across multi-cloud and hybrid environments, and **Microsoft Entra ID Protection** to help you evaluate risk data from sign-in attempts. **Microsoft Sentinel** automation can then help you use risk-based signals captured across the Defender portal to take action, such as blocking or authorizing traffic based on the level of risk.

- **Microsoft Defender Threat Intelligence** enriches your data with the latest threat updates and indicators of compromise (IoCs). 
- **Microsoft Security Copilot** provides AI-driven insights and recommendations that enhance and automate your security operations. 
- Add **Microsoft Security Exposure Management** to enrich your asset information with extra security context.

## Use least privileged access across unified SecOps

Microsoft's unified SecOps platform also provides a comprehensive set of tools to help you implement least privilege access across your environment. For example:

- Implement **Microsoft Defender XDR** unified role-based access control (RBAC) to assign permissions based on roles, ensuring users have only the access they need to perform their tasks.

-  Provide just-in-time activations for privileged role assignments by using **Microsoft Entra ID Protection's** Privileged Identity Management (PIM).

- Implement **Microsoft Defender for Cloud Apps** conditional access policies to enforce adaptive access policies based on user, location, device, and risk signals to ensure secure access to resources.

- Configure **Microsoft Defender for Cloud** threat protection to automatically block and flag risky behavior, and employ hardening mechanisms to implement least privilege access and JIT VM access.

**Microsoft Security Copilot** also authenticates users with on-behalf-of (OBO) authentication, ensuring that users have access only to the resources they need.

## Assume breach across unified SecOps

Assuming breach helps organizations prepare for and respond to security incidents more effectively. For example, with the unified SecOps platform:

- Configure **Microsoft Defender XDR** automatic attack disruption to contain attacks in progress, limiting lateral movement and reducing impact with high-fidelity signals and continuous investigation insights.

- Automatically respond to security threats across the enterprise by using **Microsoft Sentinel's** automation rules and playbooks.

- Implement **Microsoft Defender for Cloud's** recommendations to automatically block and flag risky or suspicious behavior, and automate responses across coverage areas with Azure Logic Apps.

- Enable **Microsoft Entra ID Protection** notifications so that you can respond appropriately when a user is flagged as at risk.

## Next step

[Microsoft's unified security operations platform planning overview](overview-plan.md)
