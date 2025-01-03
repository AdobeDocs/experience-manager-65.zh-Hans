---
title: 设置国际化选项
description: 了解如何指定用于呈现表单的区域设置，以及如何指定用于编码输出流的字符集。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6cf82c2b-29f0-49d5-a138-99d7801d5a28
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# 设置国际化选项{#setting-internationalization-options}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

## 指定用于呈现表单的区域设置 {#specify-the-locale-used-to-render-forms}

您可以指定呈现PDF表单时使用的区域设置。 PDF表单上的字段使用指定的区域设置来显示数据。 例如，如果区域设置设置为德语，则表单对数值使用德语小数分隔符。 作为HTML转换的一部分，区域设置还用于向客户端设备（如Web浏览器）发送验证消息。

1. 在管理控制台中，单击服务> Forms。
1. 在“国际化”下的“语言”列表中，选择用于呈现表单的区域设置。 默认值为英语（美国）。
1. 单击“保存”。

## 指定用于编码输出流的字符集 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 在“国际化”下的“字符集”列表中，选择一个字符集。 此设置取决于所使用的API，即renderHTMLForm或renderPDFForm。 要指定列出的字符集以外的字符集，请选择自定义，然后在显示的框中指定编码值。

   对于HTML转换，AEM表单支持由`java.nio.charset`包定义的字符编码值。 如果sFormPreference为PDForm，则仅支持特定字符集。 字符集必须是有效的规范名称。 默认值为ISO-8859-1。

1. 单击“保存”。
