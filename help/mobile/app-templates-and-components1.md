---
title: 应用程序模板和组件
description: 关注此页面，了解应用程序模板和组件。 它提供有关模板结构的详细信息。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 1%

---

# 应用程序模板和组件{#app-templates-and-components}

{{ue-over-mobile}}

模板用于创建页面，并定义可在所选范围内使用的组件。 模板是一种节点层次结构，与要创建页面的结构相同，但没有任何实际内容。

每个模板都会为您提供一系列可供使用的组件。

* 模板由[个组件](/help/sites-developing/components.md)组成；
* 组件使用并允许访问Widget，这些构件用于呈现内容。

>[!NOTE]
>
>要了解如何使用CRXDE Lite开发Adobe Experience Manager (AEM)应用程序，请参阅[使用CRXDE Lite开发](/help/sites-developing/developing-with-crxde-lite.md)。

模板是页面的基础。

要创建页面，必须将模板（节点树&#x200B;**/apps/&lt;myapp>/templates/&lt;mytemplate>**）复制到站点树中的相应位置：如果使用&#x200B;**网站**&#x200B;选项卡创建页面，则会发生这种情况。

此复制操作还会为页面提供其初始内容（通常是仅顶级内容）和属性sling：resourceType，以及用于呈现页面的页面组件的路径（子节点jcr：content中的所有内容）。

## 模板的结构 {#structure-of-a-template}

需要考虑两个方面：

* 模板本身的结构
* 使用模板时生成的内容的结构

模板是在类型为&#x200B;**cq：Template**&#x200B;的节点下创建的。

可以设置各种属性，特别是：

* **jcr：title** — 模板的标题；在创建页面时显示在对话框中。
* **jcr：description** — 模板的描述；在创建页面时显示在对话框中。

此节点包含&#x200B;*jcr：content (cq：PageContent)*&#x200B;节点，该节点用作结果页面的内容节点的基础。 该引用使用&#x200B;*sling：resourceType*&#x200B;来引用用于呈现新页面实际内容的组件。

>[!NOTE]
>
>要了解AEM中模板和组件的基础知识，请参阅以下资源：
>
>* [模板](/help/sites-developing/templates.md)
>* [组件](/help/sites-developing/components.md)
>

在基本了解模板和组件后，请参阅以下资源：

* [创建和添加模板和组件](/help/mobile/mobile-ondemand-app-templates.md)
* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [最佳实践](/help/mobile/best-practices-aem-mobile.md)
* [开发AEM Mobile内容服务](/help/mobile/developing-content-services.md)

### 其他资源 {#additional-resources}

要了解有关移动应用程序的其他主题，请参阅以下链接：

* [通过内容同步处理移动设备](/help/mobile/mobile-ondemand-contentsync.md)
* [测试移动应用程序](/help/mobile/develop-mobile-apps-testing.md)
