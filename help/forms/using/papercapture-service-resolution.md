---
title: 解决当纸张捕获服务无法对PDF执行OCR（光学字符识别）操作时的问题。
description: 了解解决PaperCapture服务无法对PDF执行OCR（光学字符识别）操作问题的步骤。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# PaperCature服务无法对PDF执行OCR

## 问题

升级到AEM Forms Service Pack 6.5.21.0后， `PaperCapture` 服务无法对PDF执行OCR（光学字符识别）操作。 该服务不会以PDF或日志文件的形式生成输出。

## 解决方案

1. 下载 [修补程序](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) 从软件分发门户访问。
1. 提取并复制下载文件夹的内容。
1. 导航到以下相应应用程序服务器的路径：
   * **jboss**：
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**：
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**：\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **OSGi设置**：\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. 替换现有内容 `PaperCaptureSvc` 包含复制内容的文件夹。
1. [重新启动AEM实例](/help/forms/using/restart-aem-sdk.md).


