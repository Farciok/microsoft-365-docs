---
title: Microsoft Defender for Endpoint Device Control Removable Storage frequently asked questions
description: Answers frequently asked questions on MDE device control removable storage. 
ms.service: microsoft-365-security
ms.subservice: mde
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: security
ms.author: dansimp
author: dansimp
ms.localizationpriority: medium
manager: dansimp
audience: ITPro
ms.collection: 
- m365-security
- tier3
ms.custom: admindeeplinkDEFENDER
ms.topic: conceptual
ms.date: 08/25/2022
ms.reviewer: tewchen
search.appverid: met150
---

# Microsoft Defender for Endpoint Device Control Removable Storage frequently asked questions

**Applies to:**
- [Microsoft Defender for Endpoint Plan 2](https://go.microsoft.com/fwlink/p/?linkid=2154037)

## How do I generate GUID for Group ID/PolicyRule ID/Entry ID?

You can generate the GUID through online open source, or through PowerShell. For more information, see [How to generate GUID through PowerShell](/powershell/module/microsoft.powershell.utility/new-guid).

![Screenshot of GUID in PowerShell.](https://user-images.githubusercontent.com/81826151/159046476-26ea0a21-8087-4f01-b8ae-5aa73b392d8f.png)

## What are the removable storage media and policy limitations?

The backend call is done through OMA-URI (GET to read or PATCH to update) either from the Microsoft Endpoint Manager admin center (Intune), or through Microsoft Graph API. The limitation is the same as any OMA-URI custom configuration profile at Microsoft, which is officially 350,000 characters for XML files.

For example, if you need two blocks of entries per user SID to "Allow" / "Audit allowed" specific users, and then two blocks of entries at the end to "Deny" all, you'll be able to manage 2,276 users.

## Why doesn't the policy work?

1. The most common reason is there's no required [anti-malware client version](/microsoft-365/security/defender-endpoint/device-control-removable-storage-access-control#prepare-your-endpoints).

2. Another reason could be that the XML file isn't correctly formatted. For example, not using the correct markdown formatting for the "&" character in the XML file or the text editor might add a byte order mark (BOM) 0xEF 0xBB 0xBF at the beginning of the files causing the XML parsing not to work. One simple solution is to download the [sample file](https://github.com/microsoft/mdatp-devicecontrol/tree/main/Removable%20Storage%20Access%20Control%20Samples) (select **Raw** and then **Save as**), and then update.

3. If you're deploying and managing the policy by using Group Policy, make sure to combine all PolicyRule into one XML file within a parent node called PolicyRules. Also combine all Group into one XML file within a parent node called Groups. If you manage through Intune, keep one PolicyRule one XML file, and one Group one XML file.

If it still doesn't work, contact support, and share your support cab. To get that file, use Command Prompt as an administrator: 

`"%programfiles%\Windows Defender\MpCmdRun.exe" -GetFiles`

## Why is there no configuration UX for some policy groups? 

There is no configuration UX for **Define device control policy groups** and **Define device control policy rules** on your Group Policy. But, you can still get the related .adml and .admx files by selecting **Raw** and **Save as** at the [WindowsDefender.adml](https://github.com/microsoft/mdatp-devicecontrol/blob/main/Removable%20Storage%20Access%20Control%20Samples/WindowsDefender.adml) and [WindowsDefender.admx](https://github.com/microsoft/mdatp-devicecontrol/blob/main/Removable%20Storage%20Access%20Control%20Samples/WindowsDefender.admx) files.

## How do I confirm that the latest policy has been deployed to the target machine?

You can run the PowerShell cmdlet `Get-MpComputerStatus` as an administrator. The following value will show whether the latest policy has been applied to the target machine.

:::image type="icon" source="images/148609885-bea388a9-c07d-47ef-b848-999d794d24b8.png" border="false":::

## How can I know which machine is using out of date anti-malware client version in the organization?

You can use following query to get anti-malware client version on the Microsoft 365 security portal:

```kusto
//check the anti-malware client version
DeviceFileEvents
|where FileName == "MsMpEng.exe"
|where FolderPath contains @"C:\ProgramData\Microsoft\Windows Defender\Platform\"
|extend PlatformVersion=tostring(split(FolderPath, "\\", 5))
//|project DeviceName, PlatformVersion // check which machine is using legacy platformVersion
|summarize dcount(DeviceName) by PlatformVersion // check how many machines are using which platformVersion
|order by PlatformVersion desc
```

## How do I find the media property in the Device Manager?

1. Plug in the media.

2. Open Device Manager. 

   ![Screenshot of Device Manager.](https://user-images.githubusercontent.com/81826151/181859412-affd6aa1-09ad-44bf-9541-330499cc2c87.png)

3. Locate the media in the Device Manager, right-click, and then select **Properties**.

   :::image type="content" alt-text="Screenshot of media in the Device Manager." source="https://user-images.githubusercontent.com/81826151/181859700-62a6f704-b12e-41e3-a048-7d63432654a4.png":::

4. Open **Details**, and select **Properties**.

   :::image type="content" alt-text="Screenshot of device property in Device Manager." source="https://user-images.githubusercontent.com/81826151/181859852-00bc8b11-8ee5-4d46-9770-fa29f894d13f.png":::
    