---
title: AEM Forms Workspace 架构
description: LiveCycle AEM Forms Workspace架构的概念信息和概述。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
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
source-wordcount: '220'
ht-degree: 3%
---
# AEM Forms Workspace 架构 {#aem-forms-workspace-architecture}

AEM Forms工作区是托管在CRX™上的Web应用程序。 在浏览器中打开工作区时，将访问CRX资源，并且应用程序将在浏览器中呈现为HTML页面。

该应用程序访问REST端点上的AEM Forms服务器以执行以下操作：

* 获取用户任务、进程起点、进程历史记录和用户信息
* 对任务执行操作
* 数据库中的查询任务
* 更新用户偏好设置等

AEM Forms服务器通过JDBC访问AEM Forms数据库。 数据库保存任务、进程及其实例、用户和相关信息。

AEM Forms工作区设计为模块化JavaScript™组件，可以单独自定义这些组件，并在其他Web应用程序中重复使用。 这些组件基于BackBone，它是一个JavaScript库，为Web应用程序提供结构。 描述组件与BackBone交互的详细文章是[此处](/help/forms/using/backbone-interaction.md)。 [此](/help/forms/using/folder-structure.md)文章中讨论了CRX文件夹结构中组件的组织。

为AEM Forms工作区提供的包：

* `adobe-lc-workspace-pkg-<version>.zip`：它是CRX包，也就是说，可以使用包管理器在CRX中部署它。
* `adobe-lc-workspace-<version>-src.zip`：它是一个存档，其中包含用于创建部署软件包的AEM Forms工作区的完整代码和脚本，即Ship、Debug和Dev软件包。
