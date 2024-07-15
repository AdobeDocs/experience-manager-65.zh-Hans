---
title: AEM Forms Workspace架构
description: LiveCycleAEM Forms工作区的架构的概念信息和概述。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# AEM Forms Workspace架构 {#aem-forms-workspace-architecture}

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
