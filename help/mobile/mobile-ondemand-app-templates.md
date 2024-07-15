---
title: 创建和添加模板和组件
description: 按照本页面了解如何创建模板和组件并将它们添加到应用程序。 该页面使用Geometrixx Unlimited应用程序作为包含示例应用程序模板和页面模板的应用程序。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 5f050baa-fe10-4acc-ad32-de20793edc13
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 0%

---

# 创建和添加模板和组件 {#creating-and-adding-templates-and-components}

>[!NOTE]
>
>Adobe建议对需要基于单页应用程序框架的客户端渲染（例如React）的项目使用SPA编辑器。 [了解详情](/help/sites-developing/spa-overview.md)。

AEM Mobile On-Demand提供完全配置的应用程序模板、文章模板和文章组件。

We.Unlimited应用程序是一个示例模板，展示了可完全配置且可管理的AEM Mobile On-Demand应用程序的外壳。

创建应用程序时选择此示例模板会提供一个功能丰富的AEM Mobile功能板。

![chlimage_1-70](assets/chlimage_1-70.png)

>[!NOTE]
>
>若要从AEM Mobile应用程序控制中心管理您的应用程序和移动应用程序内容，请参阅[AEM Mobile应用程序仪表板](/help/mobile/mobile-apps-ondemand-application-dashboard.md)。

## 创建应用程序模板 {#creating-app-templates}

应用程序模板用于创建应用程序，并充当页面模板和组件的集合，这些模板和组件表示应用程序的基线或基础。 模板会标记出一些基本属性，以便以适当的方式引导应用程序。 通常，客户不会创建太多应用程序。

应用程序模板提供了一种简单的方式来使用开发人员创建的现有设计，这些设计用于在AEM中创建新的应用程序。

在基于其他应用程序的模板创建应用程序时，您将获得一个应用程序，该应用程序的起点代表创建该应用程序的应用程序。

基于应用程序模板创建应用程序的步骤：

1. 导航到AEM Mobile应用程序目录： *&lt;server-url>/aem/apps.html/content/mobileapps*
1. 选择&#x200B;**创建** > **应用程序**，如下所示

使用此模板创建应用程序后，您可以将文章、横幅和收藏集添加到应用程序。 若要重新访问文章、横幅和收藏集的创建过程，请参阅[内容管理操作](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)。

>[!NOTE]
>
>或者，您也可以选择一个示例应用程序模板，例如AEM开发人员提供的&#x200B;**We.Unlimited**&#x200B;应用程序。 如果您的应用程序使用此示例模板，则会获得一些可处理的示例文章和集合。 您可以选择使用示例模板和组件、自定义现有模板和组件，或为应用程序创建新模板和组件。

>[!CAUTION]
>
>正在设置&#x200B;***redirectTarget***&#x200B;属性
>
>使用某个应用程序模板时，开发人员会定义应用程序的内容。 但是，开发人员必须知道在jcr中创建应用程序的位置以及&#x200B;***redirectTarget***&#x200B;属性的值。
>
>如果应用程序模板中包含redirectTarget属性，且redirectTarget的值定义为相对，则作为创建应用程序操作的一部分计算&#x200B;***redirectTarget***&#x200B;并尝试解析路径。 当创建应用程序进程在应用程序模板中找到redirectTarget的相对值时，该值将被附加到创建应用程序的解析位置。
>
>例如，如果应用程序模板定义了值为“*lanugage-masters/en*”的&#x200B;***redirectTarget***，且应用程序是在“*/content/mobileapps/fooApp*”中创建的，则创建应用程序后redirectTarget的最终值将为“*/content/mobileapps/fooApp/language-masters/en*”。
>

## 创建内容模板 {#creating-content-templates}

每个实体类型都有两个现成的模板。 这四个关键原则分别是：

* **默认模板：**&#x200B;用于创建具有适用默认属性/结构的内容
* **导入的模板：**&#x200B;用于从AEM Mobile导入具有适用的默认属性/结构的内容

### 文章模板 {#article-templates}

Unlimited文章是一个示例模板，表示典型的AEM Mobile On-Demand文章布局。

1. 在&#x200B;**管理文章**&#x200B;中，选择&#x200B;**+**&#x200B;以创建文章。 你可以选择&#x200B;**无限制文章**&#x200B;或&#x200B;**富文本文章**。 下图显示的选项允许您从任意这两个文章模板中进行选择。

1. 单击&#x200B;**下一步**&#x200B;定义文章元数据，如文章名称/标题、描述、作者、摘要、部门、缩略图图像、文章访问权限等。
1. 单击&#x200B;**下一步**&#x200B;填写播发属性。
1. 单击&#x200B;**下一步**&#x200B;以输入文章图像或社交媒体图像
1. 单击&#x200B;**下一步**&#x200B;以选择此新文章的收藏集链接。
1. 单击&#x200B;**下一步**&#x200B;输入社交共享的详细信息。
1. 单击&#x200B;**创建**&#x200B;以完成使用该示例创建文章的过程。 单击&#x200B;**完成**&#x200B;或&#x200B;**编辑文章**&#x200B;以编辑此文章的属性。

![chlimage_1-71](assets/chlimage_1-71.png)

### 将组件添加到文章 {#adding-components-to-article}

创建文章后，作者可以通过添加文本和图像等组件来编辑文章的内容。 文章是AEM页面模板的扩展。

选择要编辑的文章，然后单击&#x200B;**编辑**&#x200B;以向该文章中添加组件。

![chlimage_1-72](assets/chlimage_1-72.png) ![chlimage_1-73](assets/chlimage_1-73.png)

选择左侧面板上的“**+**”将组件添加到您的文章中。

![chlimage_1-74](assets/chlimage_1-74.png)

### 创建现成模板 {#creating-out-of-the-box-templates}

没有现成的文章模板，但存在自定义模板应扩展的默认模板。请参阅Geometrixx Unlimited应用程序的[文章模板示例](http://localhost:4502/crx/de/index.jsp#/apps/geometrixx-unlimited-app/templates/article)。

普通AEM模板所需属性以外的关键属性包括：

***dps-resourceType=&quot;dps：Article&quot;***

此属性可确保将AEM页面识别为AEM Mobile目标文章页面。

根据AEM模板，您可以将任何默认属性或子节点添加到模板的&#x200B;***jcr：content***。

### 横幅和收藏集模板 {#banner-and-collection-templates}

>[!CAUTION]
>
>横幅和收藏集没有内容，因此其创建不支持自定义模板。

## 创建和添加组件 {#creating-and-adding-components}

组件使用并允许访问构件，构件用于呈现内容。

代码存储库中包含一个简单组件，其源可以在AEM中找到。 随后，还可以在CRXDE Lite中本地打开它。

>[!NOTE]
>
>当前没有为AEM Mobile提供现成的组件。
>

您可以将组件添加到页面。 任何组件都可以在AEM Mobile应用程序中使用，但在应用时，可能无法正确呈现。

但是，如果没有在AEM中呈现的自定义导出内容同步处理程序，自定义组件可能无法正确导出并上传到AEM Mobile On-demand Services。

一旦组件已包含在AEM页面中，就可以将另一个组件添加到页面或编辑现有组件，以及一些其他构建基块组件。

**向页面中添加其他组件：**

1. 选择该页面，并通过编辑器标题右上角的下拉菜单确保您处于编辑模式
1. 使用编辑器标题中最左侧的图标切换侧面板
1. 选择&#x200B;**组件**&#x200B;选项卡
1. 将其中一个可用组件拖放到页面上

![chlimage_1-75](assets/chlimage_1-75.png)

**要编辑现有组件：**

1. 选择该页面，并确保您处于&#x200B;**编辑**&#x200B;模式并选择该组件
1. 选择扳手图标以配置组件

>[!NOTE]
>
>您可以在AEM中创建组件，并使用[使用CRXDE Lite开发](/help/sites-developing/developing-with-crxde-lite.md)自定义该组件。 根据要求自定义现有组件后，可以使用&#x200B;**管理文章**&#x200B;下的&#x200B;**编辑**&#x200B;选项将其添加到页面中，如上图所示。

>[!NOTE]
>
>请参阅AEM Mobile中的[模板和组件开发最佳实践](/help/mobile/best-practices-aem-mobile.md)。

### 后续步骤 {#the-next-steps}

* [使用内容属性导出内容](/help/mobile/on-demand-content-properties-exporting.md)
* [通过内容同步处理移动设备](/help/mobile/mobile-ondemand-contentsync.md)
