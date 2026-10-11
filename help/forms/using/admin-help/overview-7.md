---
title: 配置表单的基础知识
description: 了解帮助您创建交互式数据捕获应用程序的各种表单服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 169f3d94-ac00-41c7-853e-ecf0dbee559f
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
source-wordcount: '200'
ht-degree: 4%
---
# 配置表单的基础知识 {#basics-of-configuring-forms}

Forms服务使您能够创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换并交付通常在Designer中创建的表单。 表单作者开发了一种表单设计，Forms服务会以各种格式呈现该设计：

* 在Adobe Reader或浏览器中作为PDF
* 在各种浏览器环境中作为HTML，包括兼容的XHTML 1.0渲染
* 在支持Adobe Flash Player的各种浏览器环境中作为表单指南。

有关Forms服务的更多信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

使用管理控制台中的Forms页面，您可以配置Forms服务的行为。 这些设置适用于服务的所有调用。 通过AEM表单SDK发送的任何参数都将覆盖管理控制台中设置的设置；但是，它们仅影响该特定调用。

在管理控制台中更改Forms设置后，单击保存。 您不需要重新启动服务器以使更改生效。 但是，在配置缓存模式设置时，您可能需要停止并重新启动Forms服务。 （请参阅[启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)。）
