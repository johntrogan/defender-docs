---
title: Microsoft Sentinel threat intelligence management in Microsoft Defender XDR
ms.reviewer: 
description: Learn what steps you need to take to get started with Microsoft Sentinel threat intelligence management in Microsoft Defender XDR
search.appverid: met150
ms.service: defender-xdr
ms.author: pauloliveria
author: poliveria
ms.localizationpriority: medium
manager: dolmont
audience: ITPro
ms.collection: 
  - m365-security
  - highpri
  - tier3
ms.custom:
- cx-ti
- cx-ta
ms.topic: conceptual
ms.date: 01/17/2025
---

# Microsoft Sentinel threat intelligence management in Microsoft Defender XDR

[!include[Prerelease information](../includes/prerelease.md)]
**Applies to:**

- [Microsoft Defender XDR](microsoft-365-defender.md)

[Microsoft Sentinel](/azure/sentinel/overview) subscribers can now access and manage threat intelligence from inside the Microsoft Defender portal. 

For security information and event management (SIEM) solutions like Microsoft Sentinel, the most common forms of threat intelligence are threat indicators, which are also known as indicators of compromise (IOCs) or indicators of attack. Threat indicators are data that associate observed artifacts such as URLs, file hashes, or IP addresses with known threat activity such as phishing, botnets, or malware. You can use these indicators and other supported threat intelligence types in Microsoft Sentinel to detect malicious activity observed in your environment and provide context to security investigators to inform response decisions.

In the Defender portal, under **Threat intelligence**, select **Intel management**. From there, you can integrate threat intelligence into Microsoft Sentinel through the following activities:

- [Add indicators](/azure/sentinel/indicators-bulk-file-import) in bulk to Microsoft Sentinel threat intelligence from a CSV or JSON file.
- [View and manage](/azure/sentinel/work-with-threat-indicators) the imported threat intelligence.


[Learn more about threat intelligence in Microsoft Sentinel](/azure/sentinel/understand-threat-intelligence)

[!INCLUDE [Microsoft Defender XDR rebranding](../includes/defender-m3d-techcommunity.md)]
