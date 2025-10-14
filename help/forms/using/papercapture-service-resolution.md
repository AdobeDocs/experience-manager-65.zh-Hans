---
title: 解决当纸张捕获服务无法对PDF执行OCR（光学字符识别）操作时问题的文章。
description: 了解解决PaperCapture服务无法对PDF执行OCR（光学字符识别）操作问题的步骤。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: e030a71a0f52e22a803597122369cb111774f49b
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---


# PaperCature服务无法对PDF执行OCR操作

## 问题

升级到AEM Forms Service Pack 6.5.21.0或AEM Forms Service Pack 6.5.22.0后，`PaperCapture`服务无法对PDF执行OCR（光学字符识别）操作。 该服务不会以PDF或日志文件的形式生成输出。

## 应用到

此解决方案适用于：

* 所有(JBoss、Weblogic、Websphere) JEE服务器上的AEM Forms
* OSGi上的AEM Forms

## 解决方案

1. 从软件分发门户下载[修补程序](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0)。
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
1. 停止AEM应用程序服务器。
1. 将`PaperCaptureSvc`文件夹中的现有内容替换为复制的内容。
1. 重新启动AEM应用程序服务器。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java流程）重新启动AEM SDK可能会导致AEM开发环境不一致。
