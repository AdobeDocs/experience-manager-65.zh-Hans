---
title: 配置远程端点
description: 了解如何配置远程端点。 本文档介绍如何使用AEM Forms Remoting启用使用Flex构建的应用程序，以调用该服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# 配置远程端点 {#configuring-remoting-endpoints}

利用远程端点，使用Flex构建的应用程序可以使用(不推荐用于AEM表单)AEM表单远程处理来调用服务。 将为每个激活的服务自动创建远程端点。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的远程对象，以调用对相关服务的操作。

## 远程端点设置 {#remoting-endpoint-settings}

**Flex客户端身份验证方法：** 确定当所调用的服务启用了安全性、所调用的操作不支持匿名调用，并且客户端传入了无凭据或无效的凭据时，服务器发送回客户端的响应类型。
