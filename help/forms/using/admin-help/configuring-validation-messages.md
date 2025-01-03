---
title: 配置验证消息
description: 了解如何指定验证消息的显示方式及其相对于Web浏览器中返回表单的位置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 14314383-5228-4904-98c1-586f48a1142c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# 配置验证消息 {#configuring-validation-messages}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

对于呈现为HTML的表单，将为用户显示出现的表单验证错误。 您可以自定义验证消息的显示方式。 根据显示验证消息的位置，您还可以控制消息在表单中的位置和帧边框的大小。

## 指定验证消息的显示方式 {#specify-how-validation-messages-are-displayed}

1. 在管理控制台中，单击服务>表单。
1. 在“验证输出”下的“报告”列表中，选择以下选项之一：

   **消息框：**&#x200B;在单独的对话框中显示验证消息。

   **帧：**&#x200B;在同一窗口的帧中显示验证消息。

   **无帧：**&#x200B;在同一窗口中显示验证消息。 此值为默认值。

   **通过API（包含数据）：**&#x200B;通过API（包含数据）返回验证消息。 验证消息不显示在屏幕上。

   **通过API（含表单）：**&#x200B;通过API（含表单）返回验证消息。 验证消息不显示在屏幕上。

   **无：**&#x200B;不显示验证消息。

1. 单击“保存”。

## 指定与Web浏览器中返回的表单相关的验证消息的位置 {#specify-the-location-of-validation-messages-relative-to-the-form-returned-in-the-web-browser}

当Reporting设置为Frame或No Frame时，可以指定验证消息的位置。

1. 在“验证输出”下的“位置”列表中，选择以下选项之一：

   **左：**&#x200B;在Web浏览器的左侧显示验证消息。

   **右：**&#x200B;在Web浏览器的右侧显示验证消息。

   **Top**：在Web浏览器的顶部显示验证消息。 此值为默认值。

   **Bottom**：在Web浏览器底部显示验证消息。

1. 单击“保存”。

## 指定框架边框大小 {#specify-the-frame-border-size}

当“报告”设置为“帧”时，可以指定帧边框大小。

1. 在“验证输出”下的“边框大小”框中，键入框架边框的大小（以像素为单位）。

   边框大小必须等于或大于0。 默认值为 1。

1. 单击“保存”。
