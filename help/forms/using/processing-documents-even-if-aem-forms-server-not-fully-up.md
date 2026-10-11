---
title: AEM Forms服务器甚至在所有服务启动并运行之前就开始处理文档。
description: 在所有服务都启动并在JEE服务器和OSGi服务器上运行之前，AEM Forms服务器就开始处理文档。
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 3%
---
# AEM Forms服务器甚至在所有服务启动并运行之前就开始处理文档{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 问题 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

在AEM Forms服务器完全启动并且所有应用程序都启动并运行之前，AEM Forms服务器将开始处理文档。


## 应用到 {#applies-to}

该解决方案适用于JEE服务器上的AEM Forms和OSGi服务器上的AEM Forms 。

## 解决办法 {#solution}

要解决此问题，请在服务器启动期间向[批处理文件](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html?lang=zh-Hans#windows-platform-start-bat-script-example)添加参数`Dcom.adobe.livecycle.dsc.deferServiceStart=true`。
