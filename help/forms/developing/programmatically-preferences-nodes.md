---
title: 以编程方式管理PreferencesNodes
description: 使用首选项管理器服务API (Java)以编程方式管理首选项节点。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%
---
# 以编程方式管理首选项节点 {#programmatically-managing-the-preferencesnodes}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

本主题介绍如何使用首选项管理器服务API (Java)以编程方式管理首选项节点。

您可以从管理员UI手动更改配置设置。 要更改选项，请导航到`Home>Settings>User Management> Configuration>Manual Configuration`。 进行更改后导入`config.xml`，您会注意到除了在节点`/Adobe/Adobe Experience Manager Forms/Config/UM persist`进行的更改之外的所有更改都将丢失。 用户管理导入和导出预览不支持更改其他组件的配置设置。 现在，可以使用`PreferencesManagerServiceClient` API进行这些更改。

**步骤摘要**&#x200B;要以编程方式管理首选项节点，请执行以下步骤：

1. 包括项目文件。
1. 创建PreferencesManagerService客户端
1. 调用相应的角色或权限操作

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建PreferencesManagerService客户端**

必须先创建PreferencesManagerService客户端，然后才能以编程方式执行用户管理PreferencesManagerService操作。 使用Java API可通过创建PreferencesManagerServiceClient对象来实现这一点。

**调用适当的角色或权限操作**

创建服务客户端后，可以调用Preferences Manager操作。 服务客户端允许您读取和设置权限。
