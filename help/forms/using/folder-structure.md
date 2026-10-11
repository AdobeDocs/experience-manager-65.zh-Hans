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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 5%
---
# 了解文件夹结构 {#understanding-the-folder-structure}

AEM Forms工作区组件使用骨干在MVC架构上设计。 每个组件都有一个文件，用于：

* 模型，其中包含业务逻辑。
* 模板，即包含接口控件的HTML文件。
* 视图，充当模板的Controller类。

所有组件的资产都放置在如下所述的文件夹结构中。 要访问资源，请登录CRXDE Lite并浏览至`/libs/ws/js/runtime/`。

**个模型**&#x200B;包含主干模型。

**个视图**&#x200B;包含主干视图。

**模板**&#x200B;仅包含组件的HTML模板。

**路由**&#x200B;包含通用路由。 路由中的Templates文件夹包含HTML代码和对组件的引用。

**服务**&#x200B;包含用于调用REST端点上的Adobe Experience Manager服务器API的服务接口。

**util**&#x200B;包含可由多个组件使用的通用实用程序。
