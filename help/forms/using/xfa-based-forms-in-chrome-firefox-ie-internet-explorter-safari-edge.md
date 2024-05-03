---
title: 无法在Google Chrome、Firefox、Microsoft&reg； Edge、Microsoft&reg； Internet Explorer或Apple Safari中打开基于XFA的PDF forms
description: 无法在Google Chrome、Firefox、Microsoft&reg； Edge、Microsoft&reg； Internet Explorer或Apple Safari中打开基于XFA的PDF forms
feature: Adaptive Forms
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 无法在Google Chrome、Firefox、Microsoft、Edge®Microsoft®Internet Explorer或Apple Safari中打开基于XFA的PDF forms{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

许多最新浏览器版本都包含自身对基于XFA的PDF forms的有限支持。 虽然这些浏览器可以打开基于XFA的PDF forms，但提供的功能有限。 如果您无法在新式浏览器中打开或提交基于XFA的PDF表单，请使用以下方法之一：

* 使用 [Adobe®Acrobat®](https://www.adobe.com/acrobat.html) 或 [Adobe®Adobe®Reader®](https://get.adobe.com/reader/)，版本8或更高版本，用于打开和提交基于XFA的PDF forms。
* 在Microsoft® Windows®上，Acrobat和Reader允许您配置以在“受保护的视图”模式下打开PDF，从而阻止打开基于XFA的PDF forms。 确保Acrobat或Reader中的“受保护的视图”模式已禁用。 有关更多信息，请参阅 [受保护的视图（仅限Windows）](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (对于Forms开发人员) Adobe Experience Manager Forms还支持执行以下操作：

   * [将基于XFA的表单渲染到HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) 以便可以在支持HTML5的浏览器中打开表单，包括在iPad等移动设备上运行的浏览器。 表单的HTML5演绎版维护表单设计的布局，并支持嵌入到XFA表单模板中的大多数表单逻辑（如JavaScript、表单计算和表单验证）。
   * [将基于XFA的表单转换为移动响应式自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). 这些表单提供响应式布局、个性化功能，并根据需要添加或删除字段或部分以动态适应用户响应。 此外，它们还为各种数据源提供现成的连接器、记录文档功能，并轻松连接到Adobe Analytics以进行性能评估。 有关更多信息，请参阅 [主要特性和功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)
这样，您在XFA表单中的技术投资就能得到保护，并继续为最终用户提供最佳体验。 有关更多信息，请参阅 [Adobe Experience Manager Forms产品文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
