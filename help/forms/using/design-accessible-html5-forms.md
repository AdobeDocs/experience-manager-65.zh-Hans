---
title: 无障碍 HTML5 Forms 设计
description: HTML5表单使用ARIA HTML5辅助功能标准。 这些表单支持选项卡式导航，经认证与常用屏幕阅读器兼容。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
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
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 2%
---
# 无障碍 HTML5 Forms 设计 {#designing-accessible-html-forms}

HTML5表单使用ARIA HTML5辅助功能标准生成无障碍的HTML表单。 这些表单支持选项卡式导航（Mozilla FireFox除外），经认证与常用屏幕阅读器兼容。 要生成具有良好辅助功能的HTML5表单，请根据一些基本设计准则来设计XFA表单模板。 设计准则包括配置正确的制表符顺序并为每个表单控件提供“说文本”内容。 AEM Forms Designer支持设置这些表单控件属性，以生成可访问的PDF和HTML5表单。

*注释:Tabbed导航未涵盖受保护字段，例如显示值总和的计算字段。 要使屏幕阅读器读取受保护字段的值，请在受保护字段的顶部或旁边放置一个空的只读字段。 将受保护字段的值分配给新的只读字段。 屏幕阅读器或选项卡式导航器可以选取此只读字段，并将其作为受保护字段的值发出。*

AEM Forms Designer包含多个可传递给屏幕阅读器的说文本选项。 对于表单中的每个对象，用户可以为屏幕阅读器文本指定以下几种设置之一：

* 自定义屏幕阅读器文本，可以使用“辅助功能”面板进行设置。 作者可以注释按钮和字段的名称及其用途。
* 工具提示，可在“辅助功能”面板中设置这些提示。
* 表单中的字段标题。
* 对象名称，在“绑定”选项卡的“名称”选项中指定。

![辅助功能](assets/accessibility.png)

当表单控件上有工具提示、屏幕Reader文本和标题等多个选项可用时，屏幕Reader仅使用这些属性之一。 默认顺序为“自定义屏幕Reader文本”、“工具提示”、“标题”和“名称”。 您可以使用辅助功能面板中的屏幕Reader **优先顺序**&#x200B;选项覆盖默认顺序。
