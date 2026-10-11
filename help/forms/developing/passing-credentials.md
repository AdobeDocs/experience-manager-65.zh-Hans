---
title: 使用WS-security标头传递凭据
description: 了解如何使用WS-security标头传递凭据
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '228'
ht-degree: 3%
---
# 使用 WS-Security 标头传递凭据 {#using-execute-script-service-aem-forms-jee-workbench}

使用Web服务在JEE服务上调用AEM Forms时，您可以使用WS-Security标头传递AEM Forms on JEE所需的客户端身份验证信息。 WS-Security定义SOAP扩展以实现客户端身份验证、消息机密性和消息完整性。 因此，当JEE上的AEM Forms部署为独立服务器或群集环境时，您可以调用JEE上的AEM Forms 。

如何在JEE上将WS-Security标头传递到AEM Forms，取决于您使用的是轴生成的Java类，还是使用服务的本机SOAP栈栈的.NET客户端程序集。

>[!NOTE]
>
>作为使用WS-Security标头调用服务的示例，本主题通过调用Encryption服务使用密码加密PDF文档。

本文档涵盖以下主题：

* 使用Axis生成的Java类传递客户端身份验证

* 生成调用加密服务所需的Axis库文件

* 使用WS-Security标头调用Encryption服务

* 使用.NET客户端程序集传递客户端身份验证

* 使用WS-Security标头调用Encryption服务


## 要求 {#requirements}

要充分利用本文档，您需要对AEM Forms on JEE软件有一定的了解。

>[!MORELIKETHIS]
>
>* [使用WS-Security标头传递凭据](assets/passing-credentials-using-ws-security-headers.pdf)
