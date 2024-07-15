---
title: 了解文件夹结构
description: 如何了解要自定义的AEM Forms工作区源代码的文件夹结构。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# 了解文件夹结构 {#understanding-the-folder-structure}

AEM Forms工作区组件使用骨干在MVC架构上设计。 每个组件都有一个文件，用于：

* 模型，其中包含业务逻辑。
* 模板，即包含接口控件的HTML文件。
* 视图，充当模板的Controller类。

所有组件的资产都放置在如下所述的文件夹结构中。 要访问资源，请登录CRXDE Lite并浏览到`/libs/ws/js/runtime/`。

**个模型**&#x200B;包含主干模型。

**个视图**&#x200B;包含主干视图。

**模板**&#x200B;仅包含组件的HTML模板。

**路由**&#x200B;包含通用路由。 路由中的Templates文件夹包含HTML代码和对组件的引用。

**服务**&#x200B;包含用于调用REST端点上的Adobe Experience Manager服务器API的服务接口。

**util**&#x200B;包含可由多个组件使用的通用实用程序。
