---
title: AEM Forms服务器甚至在所有服务启动并运行之前就开始处理文档。
description: 在所有服务都启动并在JEE服务器和OSGi服务器上运行之前，AEM Forms服务器就开始处理文档。
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms服务器甚至在所有服务启动并运行之前就开始处理文档{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 问题 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

在AEM Forms服务器完全启动并且所有应用程序都启动并运行之前，AEM Forms服务器将开始处理文档。


## 应用到 {#applies-to}

该解决方案适用于JEE服务器上的AEM Forms和OSGi服务器上的AEM Forms 。

## 解决方案 {#solution}

要解决此问题，请在服务器启动期间向[批处理文件](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html?lang=zh-Hans#windows-platform-start-bat-script-example)添加参数`Dcom.adobe.livecycle.dsc.deferServiceStart=true`。
