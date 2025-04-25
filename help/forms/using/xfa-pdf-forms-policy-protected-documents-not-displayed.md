---
title: 显示基于XFA的PDF forms和受策略保护文档的问题
description: 显示基于XFA的PDF forms和受策略保护文档的问题
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 显示基于XFA的PDF forms和受策略保护文档的问题

如果您无法使用Adobe LiveCycle Rights Management打开基于XFA的PDF表单或受策略保护的文档，请检查以下原因：

* 基于XFA的PDF forms和受策略保护的文档需要Adobe® Acrobat®或Adobe® Reader®，版本8及更高版本。 请参阅[Adobe下载](https://www.adobe.com/downloads.html)，了解如何下载最新的Reader或Acrobat。
* Mozilla Firefox和Google Chrome等浏览器提供了不支持基于XFA的PDF forms的内置PDF查看器。 要在这些浏览器中查看基于XFA的PDF forms，您必须配置以使用Acrobat或Reader打开PDF。 有关更多信息，请参阅在Mozilla Firefox和Google Chrome上基于XFA的PDF forms 。
* Microsoft® Windows®上的Acrobat和Reader允许您配置以在“受保护的视图”模式下打开PDF，这将阻止打开基于XFA的PDF forms和受策略保护的文档。 确保已禁用Acrobat或Reader中的受保护视图模式。 有关详细信息，请参阅[受保护的视图（仅限Windows）](https://helpx.adobe.com/acrobat/kb/end-of-support-acrobat-x-reader-x.html)。
* 如果您尝试在移动设备上访问基于XFA的PDF forms或受策略保护的文档，请考虑以下事项：

   * 在移动设备上打开受策略保护的文档需要Adobe Reader for mobile。 有关详细信息，请参阅[Adobe Reader移动应用程序](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html)。
   * iOS、Android以及Blackberry移动设备和智能手机不支持带有XFA表单的Adobe Reader插件。 LiveCycle ES4提供的服务面向使用HTML5的移动设备；表单创建者必须使用该服务允许在这些设备上使用表单。
   * 如果您在Windows 8移动设备上使用Metro样式，请更改为Classic视图或将HTML5与LiveCycle ES4结合使用。

>[!NOTE]
>
>LiveCycle ES4支持将基于XFA的表单渲染到HTML5，以便这些表单可以在支持HTML5的浏览器中打开，包括那些在iPad等移动设备上运行的表单。 表单的HTML5演绎版维护表单设计的布局，并支持嵌入到XFA表单模板中的大多数表单逻辑(如JavaScript、表单计算和表单验证)。 这样，您对XFA表单的技术投资就可以轻松转移到无法运行Adobe Reader插件的设备上。
>有关详细信息，请参阅升级到[LiveCycle产品文档](https://business.adobe.com/products/experience-manager/forms/aem-forms.html)。

[法律声明](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [联机隐私策略](https://www.adobe.com/cn/privacy.html)