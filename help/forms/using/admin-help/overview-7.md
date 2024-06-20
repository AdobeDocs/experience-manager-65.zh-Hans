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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 配置表单的基础知识 {#basics-of-configuring-forms}

Forms服务使您能够创建交互式数据捕获客户端应用程序，这些应用程序验证、处理、转换并交付通常在Designer中创建的表单。 表单作者开发了一种表单设计，Forms服务会以各种格式呈现该设计：

* 作为Adobe Reader或浏览器中的PDF
* 在各种浏览器环境中作为HTML，包括兼容的XHTML 1.0渲染
* 在支持AdobeFlash Player的各种浏览器环境中作为表单指南。

有关Forms服务的更多信息，请参阅 [服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

使用管理控制台中的Forms页面，您可以配置Forms服务的行为。 这些设置适用于服务的所有调用。 通过AEM Forms SDK发送的任何参数都将覆盖管理控制台中设置的设置；但是，它们仅影响该特定调用。

在管理控制台中更改Forms设置后，单击保存。 您不需要重新启动服务器以使更改生效。 但是，在配置缓存模式设置时，您可能需要停止并重新启动Forms服务。 (请参阅 [启动和停止服务](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
