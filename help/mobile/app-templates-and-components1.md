---
title: 应用程序模板和组件
seo-title: 应用程序模板和组件
description: 可查看本页以了解应用程序模板和组件。 它提供了有关模板结构的详细信息。
seo-description: 可查看本页以了解应用程序模板和组件。 它提供了有关模板结构的详细信息。
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 1%

---

# 应用程序模板和组件{#app-templates-and-components}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解更多](/help/sites-developing/spa-overview.md)。

模板用于创建页面并定义可在所选范围内使用的组件。 模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。

每个模板都将为您提供一系列可供使用的组件。

* 模板由[组件](/help/sites-developing/components.md)构建；
* 组件使用和允许访问小组件，这些组件用于呈现内容。

>[!NOTE]
>
>要了解如何使用CRXDE Lite开发AEM应用程序，请参阅[使用CRXDE Lite进行开发](/help/sites-developing/developing-with-crxde-lite.md)。

模板是页面的基础。

要创建页面，必须将模板(node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**)复制到站点树中的相应位置：如果使用&#x200B;**网站**&#x200B;选项卡创建页面，则会发生这种情况。

此复制操作还会为页面提供其初始内容（通常仅限顶级内容）和属性sling:resourceType，用于呈现页面的页面组件的路径（子节点jcr:content中的所有内容）。

## 模板的结构{#structure-of-a-template}

需要考虑两个方面：

* 模板本身的结构
* 使用模板时生成的内容的结构

在&#x200B;**cq:Template**&#x200B;类型的节点下创建模板。

可以设置各种属性，特别是：

* **jcr:title**  — 模板的标题；创建页面时，会显示在对话框中。
* **jcr:description**  — 模板的描述；创建页面时，会显示在对话框中。

此节点包含&#x200B;*jcr:content(cq:PageContent)*&#x200B;节点，用作生成页面的内容节点的基础；此引用使用&#x200B;*sling:resourceType*&#x200B;来表示新页面实际内容的组件。

>[!NOTE]
>
>要了解AEM中模板和组件的基础知识，请参阅以下资源：
>
>* [模板](/help/sites-developing/templates.md)
* [组件](/help/sites-developing/components.md)



在您基本了解模板和组件后，请参阅以下资源：

* [创建和添加模板和组件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳实践](/help/mobile/best-practices-aem-mobile.md)
* [开发AEM Mobile内容服务](/help/mobile/developing-content-services.md)

### 其他资源 {#additional-resources}

要了解有关移动设备应用程序的其他主题，请参阅以下链接：

* [具有内容同步的移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [测试移动设备应用程序](/help/mobile/develop-mobile-apps-testing.md)
