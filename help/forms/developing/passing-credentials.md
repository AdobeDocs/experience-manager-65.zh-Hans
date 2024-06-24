---
title: 使用WS-security标头传递凭据
description: 了解如何使用WS-security标头传递凭据
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 使用WS-Security标头传递凭据 {#using-execute-script-service-aem-forms-jee-workbench}

使用Web服务在JEE服务上调用AEM Forms时，您可以使用WS-Security标头传递AEM Forms on JEE所需的客户端身份验证信息。 WS-Security定义SOAP扩展以实现客户端身份验证、消息机密性和消息完整性。 因此，当JEE上的AEM Forms部署为独立服务器或群集环境时，您可以调用JEE上的AEM Forms 。

如何在JEE上将WS-Security标头传递到AEM Forms，取决于您使用的是轴生成的Java类，还是使用服务的本机SOAP栈栈的.NET客户端程序集。

>[!NOTE]
>
>作为使用WS-Security标头调用服务的示例，本主题通过调用Encryption服务使用口令对PDF文档进行加密。

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
