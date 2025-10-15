---
title: 如何在Firefox和Chrome上打开基于XFA的PDF forms
description: 如何在Firefox和Chrome上打开基于XFA的PDF forms
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# 如何在Firefox和Chrome上打开基于XFA的PDF forms

## 问题

随Mozilla Firefox和Google Chrome一起引入的内置PDF查看器不支持基于XFA的PDF forms。 因此，基于XFA的PDF forms不会在Firefox和Chrome的更高版本中打开。

## 解决方案

要在Firefox和Chrome上使用基于XFA的PDF forms，请执行以下步骤，将Firefox和Chrome配置为使用Adobe Reader或Adobe Acrobat打开PDF。

>[!NOTE]
> 
> 确保您的计算机上安装了Adobe Reader或Adobe Acrobat。

### 配置Firefox

1. 在Firefox中，选择&#x200B;**工具>选项**。

1. 在“选项”对话框中，单击&#x200B;**应用程序**。

1. 在“应用程序”选项卡的搜索字段中键入PDF。

1. 对于搜索结果中的可移植文档格式(PDF)内容类型，请从“操作”下拉列表中选择&#x200B;**使用Adobe Acrobat（在Firefox中）**。
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. 单击“确定”。

1. 重新启动Firefox。

### 配置Chrome

1. 在Chrome中，转到chrome://plugins/ 。

1. 单击Chrome PDF Viewer下的禁用，然后单击Adobe PDF Plug-In下的启用。
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
有关详细信息，请参阅Google提供的[Adobe PDF插件](https://support.google.com/chrome/?hl=en&visit_id=638803785294106945-2276548125&rd=4&topic=3421431#topic=7439538)文档。

>[!NOTE]
> 
> LiveCycle ES4支持将基于XFA的表单渲染到HTML5，以便这些表单可以在支持HTML5的浏览器中打开，包括那些在iPad等移动设备上运行的表单。 表单的HTML5演绎版维护表单设计的布局，并支持嵌入到XFA表单模板中的大多数表单逻辑(如JavaScript、表单计算和表单验证)。 这样，您对XFA表单的技术投资就可以轻松转移到无法运行Adobe Reader插件的设备上。
>有关详细信息，请参阅[LiveCycle产品文档](https://business.adobe.com/cn/products/experience-manager/forms/aem-forms.html)。

[法律声明](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [联机隐私策略](https://www.adobe.com/cn/privacy.html)