---
title: Safe Attachments for SharePoint, OneDrive, and Microsoft Teams
f1.keywords: 
  - NOCSH
ms.author: chrisda
author: chrisda
manager: dansimp
audience: Admin
ms.date: 
ms.topic: conceptual

ms.localizationpriority: medium
search.appverid: 
  - MET150
  - MOE150
ms.assetid: 26261670-db33-4c53-b125-af0662c34607
ms.collection: 
  - m365-security
  - SPO_Content
  - m365initiative-defender-office365
ms.custom: 
  - seo-marvel-apr2020
  - seo-marvel-jun2020
description: Learn about Microsoft Defender for Office 365 for files in SharePoint Online, OneDrive for Business, and Microsoft Teams.
ms.subservice: mdo
ms.service: microsoft-365-security
---

# Safe Attachments for SharePoint, OneDrive, and Microsoft Teams

[!INCLUDE [MDO Trial banner](../includes/mdo-trial-banner.md)]

**Applies to**
- [Microsoft Defender for Office 365 plan 1 and plan 2](defender-for-office-365.md)
- [Microsoft 365 Defender](../defender/microsoft-365-defender.md)

Safe Attachments for SharePoint, OneDrive, and Microsoft Teams in [Microsoft Defender for Office 365](whats-new-in-defender-for-office-365.md) provides an additional layer of protection for files that have already been scanned asynchronously by the [common virus detection engine in Microsoft 365](virus-detection-in-spo.md). Safe Attachments for SharePoint, OneDrive, and Microsoft Teams helps detect and block existing files that are identified as malicious in team sites and document libraries.

Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is not enabled by default. To turn it on, see [Turn on Safe Attachments for SharePoint, OneDrive, and Microsoft Teams](turn-on-mdo-for-spo-odb-and-teams.md).

## How Safe Attachments for SharePoint, OneDrive, and Microsoft Teams works

When Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is enabled and identifies a file as malicious, the file is locked using direct integration with the file stores. The following image shows an example of a malicious file detected in a library.

:::image type="content" source="../../media/2bba71cc-7ad1-4799-8b9d-d56f923db3a7.png" alt-text="The files in OneDrive for Business with one detected as malicious" lightbox="../../media/2bba71cc-7ad1-4799-8b9d-d56f923db3a7.png":::

Although the blocked file is still listed in the document library and in web, mobile, or desktop applications, people can't open, copy, move, or share the file. But they can delete the blocked file.

Here's an example of what a blocked file looks like on a mobile device:

:::image type="content" source="../../media/cb1c1705-fd0a-45b8-9a26-c22503011d54.png" alt-text="The option to delete a blocked file from OneDrive for Business from the OneDrive mobile app" lightbox="../../media/cb1c1705-fd0a-45b8-9a26-c22503011d54.png":::

By default, people can download a blocked file. Here's what downloading a blocked file looks like on a mobile device:

:::image type="content" source="../../media/be288a82-bdd8-4371-93d8-1783db3b61bc.png" alt-text="The option to download a blocked file in OneDrive for Business" lightbox="../../media/be288a82-bdd8-4371-93d8-1783db3b61bc.png":::

SharePoint Online admins can prevent people from downloading malicious files. For instructions, see [Use SharePoint Online PowerShell to prevent users from downloading malicious files](turn-on-mdo-for-spo-odb-and-teams.md#step-2-recommended-use-sharepoint-online-powershell-to-prevent-users-from-downloading-malicious-files).

To learn more about the user experience when a file has been detected as malicious, see [What to do when a malicious file is found in SharePoint Online, OneDrive, or Microsoft Teams](https://support.microsoft.com/office/01e902ad-a903-4e0f-b093-1e1ac0c37ad2).

## View information about malicious files detected by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams

Files that are identified as malicious by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams will show up in [reports for Microsoft Defender for Office 365](view-reports-for-mdo.md) and in [Explorer (and real-time detections)](threat-explorer.md).

When a file is identified as malicious by Safe Attachments for SharePoint, OneDrive, and Microsoft Teams, the file is also available in quarantine, but only to admins. For more information, see [Manage quarantined files in Defender for Office 365](manage-quarantined-messages-and-files.md#use-the-microsoft-365-defender-portal-to-manage-quarantined-files-in-defender-for-office-365).

## Keep these points in mind

- Defender for Office 365 will not scan every single file in SharePoint Online, OneDrive for Business, or Microsoft Teams. This is by design. Files are scanned asynchronously. The process uses sharing and guest activity events along with smart heuristics and threat signals to identify malicious files.

- Make sure your SharePoint sites are configured to use the [Modern experience](/sharepoint/guide-to-sharepoint-modern-experience). Defender for Office 365 protection applies whether the Modern experience or the Classic view is used; however, visual indicators that a file is blocked are available only in the Modern experience.

- Safe Attachments for SharePoint, OneDrive, and Microsoft Teams is part of your organization's overall threat protection strategy, which includes anti-spam and anti-malware protection in Exchange Online Protection (EOP), as well as Safe Links and Safe Attachments in Microsoft Defender for Office 365. To learn more, see [Protect against threats in Office 365](protect-against-threats.md).
