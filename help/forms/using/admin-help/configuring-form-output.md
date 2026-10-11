---
title: 配置表单输出
description: 了解如何配置表单输出。 要配置表单输出并启用该功能，请在提交表单之前使用自定义脚本。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d739806c-ce72-40fd-b304-3262a0988d96
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
source-wordcount: '257'
ht-degree: 3%
---
# 配置表单输出{#configuring-form-output}

## 指定返回到Web浏览器的HTML输出的类型 {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. 在管理控制台中，单击服务>表单。
1. 在“表单输出”下的“输出类型”列表中，选择以下选项之一：

   **完整HTML：**&#x200B;渲染完整HTML标记中的表单（完整的HTML页面）。 此值为默认值。

   **表单正文：**&#x200B;在`<BODY>`标记内呈现表单（不是完整的HTML页面）。

1. 单击“保存”。

## 指定PDF内容的呈现位置 {#specify-the-location-where-pdf-content-is-rendered}

1. 在“表单输出”下的“渲染位置”列表中，选择以下选项之一：

   **客户端：**&#x200B;用于在Adobe Acrobat或Adobe Reader中呈现PDF forms。 客户端渲染可提高AEM表单的性能，并且仅适用于PDFForm转换。

   **服务器：**&#x200B;在应用程序服务器上呈现PDF forms。

   **自动：**&#x200B;在XDP文件的`dynamicRender`配置值指定的位置渲染PDF表单。 此值为默认值。

1. 单击“保存”。

## 配置表单提交前自定义脚本的调用 {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

执行以下步骤以启用该功能：

1. 登录到管理控制台。
1. 转到&#x200B;**服务** > **表单**。
1. 将输出类型指定为表单主体。
1. 保存设置。
1. 在JavaScript代码的头部分中声明HTML变量__CUSTOM_SCRIPTS_VERSION，并将其值设置为1。

   >[!NOTE]
   >
   >*要禁用该功能，可以删除JavaScript变量或将其值设置为0。*
