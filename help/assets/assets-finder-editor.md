---
title: 创建和配置资产编辑器页面
description: 了解如何创建自定义资产编辑器页面和同时编辑多个资产。
contentOwner: AG
role: Business Practitioner, Administrator
feature: Developer Tools,Asset Management
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# 创建和配置资产编辑器页面{#creating-and-configuring-asset-editor-pages}

本文档将介绍以下内容：

* 创建自定义资产编辑器页面的原因。
* 如何创建和自定义资产编辑器页面，这些页面是WCM页面，您可以通过它视图和编辑元数据以及对资产执行操作。
* 如何同时编辑多个资产。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>资产共享可用作开放源引用实施。 请参阅[资产共享共享资源](https://adobe-marketing-cloud.github.io/asset-share-commons/)。 不正式支持。

## 为何要创建和配置资产编辑器页面？{#why-create-and-configure-asset-editor-pages}

数字资产管理正在越来越多的场景中使用。 当专业用户从面向小型用户群的专业培训用户（例如摄影师或分类学家）的小型解决方案转向更大、更多样化的用户群（例如商业用户、WCM作者、记者等）时，专业用户的[!DNL Adobe Experience Manager Assets]强大的用户界面可以提供太多信息和利益相关方开始以请求与他们相关的特定用户界面或应用程序访问数字资产。

这些以资产为中心的应用程序可以是内部网中的简单照片库，员工可以从贸易展访问或面向公众的网站的新闻中心上传照片。 以资产为中心的应用程序还可以扩展到包括购物车、结帐和验证过程在内的完整解决方案。

创建以资源为中心的应用程序在很大程度上成为一个配置过程，它不需要编码，只需要了解用户组及其需求以及所使用元数据的知识。 使用[!DNL Assets]创建的以资源为中心的应用程序具有可扩展性：可以创建适中的编码工作、可重用的组件，用于搜索、查看和修改资产。

[!DNL Experience Manager]中以资源为中心的应用程序由“资源编辑器”页面组成，该页面可用于获取特定资源的详细视图。 资产编辑器页面还允许编辑元数据，前提是访问资产的用户具有必要的权限。

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create a new Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create a new Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create a new asset share page via the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes a number of predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example cq:tags) and a content tree to populate the options from (for example the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, e.g. tiff:ImageLength and the user can then enter a value, e.g. 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## 创建并配置资产编辑器页面{#creating-and-configuring-an-asset-editor-page}

您可以自定义资产编辑器，以确定用户如何视图和编辑数字资产。 为此，您需要创建一个新的“资产编辑器”页面，然后自定义视图以及用户可以对该页面执行的操作。

>[!NOTE]
>
>如果要向DAM资产编辑器添加自定义字段，请向`/apps/dam/content/asseteditors.`添加新的`cq:Widget`节点

### 创建“资产编辑器”页面{#creating-the-asset-editor-page}

创建“资产编辑器”页面时，最好在“资产共享”页面的正下方创建该页面。

要创建“资产编辑器”页面，请执行以下操作：

1. 在&#x200B;**[!UICONTROL 网站]**&#x200B;选项卡中，导航到要创建资产编辑器页面的位置，然后单击&#x200B;**新建**。
1. 选择&#x200B;**Geometrixx资产编辑器**，然后单击&#x200B;**创建**。 将创建新页面，该页面将列在&#x200B;**网站**&#x200B;选项卡中。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用Geometrixx资产编辑器模板创建的基本页面如下所示：

![assetshare5](assets/assetshare5.png)

要自定义您的“资产编辑器”页面，请使用Sidekick中的元素。 从&#x200B;**Geometrixx新闻中心**&#x200B;访问的资产编辑器页面是基于此模板的自定义页面版本：

![assetshare6](assets/assetshare6.png)

#### 将资产编辑器设置为从资产共享页面{#setting-which-asset-editor-opens-from-an-asset-share-page}打开

在创建自定义资产编辑器页面后，您需要确保在按住多次单击您创建的自定义资产共享的资产时，该共享会在自定义编辑器页面中打开资产。

要设置“资产编辑器”页面，请执行以下操作：

1. 在“资产共享”页面中，单击查询 Builder旁边的&#x200B;**编辑**。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 如果尚未选择&#x200B;**常规**&#x200B;选项卡，请单击它。

1. 在&#x200B;**资产编辑器的路径**&#x200B;字段中，输入您希望“资产共享”页面在中打开资产的资产编辑器的路径，然后单击&#x200B;**确定**。

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 添加资产编辑器组件{#adding-asset-editor-components}

您可以通过向页面添加组件来确定资产编辑器具有的功能。

要添加资产编辑器组件，请执行以下操作：

1. 在要自定义的“资产编辑器”页面中，选择Sidekick中的&#x200B;**资产编辑器**。 将显示所有可用的资产编辑器组件。

>[!NOTE]
>
>您可以自定义哪些内容取决于可用的组件。 要启用组件，请转到设计模式并选择需要启用的组件。

1. 将组件从Sidekick拖动到资产编辑器中，并在组件对话框中进行任何修改。 下表对这些组件进行了说明，并在随后的详细说明中进行了说明。

>[!NOTE]
>
>在设计资产编辑器页面时，您可以创建只读或可编辑的组件。 用户知道，如果某个铅笔图像出现在该组件中，则可以编辑该字段。 默认情况下，大多数组件都设置为只读。

| 组件 | 描述 |
|---|---|
| **[!UICONTROL 元数] 据格式 [!UICONTROL 和元数据文本字段]** | 允许您向资产添加其他元数据，并对该资产执行操作（如提交）。 |
| **[!UICONTROL 子资产]** | 允许您自定义子资产。 |
| **标记** | 允许用户选择标记并将其添加到资产。 |
| **[!UICONTROL 缩略图]** | 显示资产的缩略图及其文件名，并允许您添加替代文本。 您也可以在此处添加资产编辑器操作。 |
| **[!UICONTROL 标题]** | 显示可自定义的资产标题。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 元数据表单和文本字段 — 配置视图元数据组件{#metadata-form-and-text-field-configuring-the-view-metadata-component}

元数据表单是包含开始和结束操作的表单。 在中间，输入&#x200B;**文本**&#x200B;字段。 有关使用表单的详细信息，请参阅[Forms](/help/sites-authoring/default-components-foundation.md#form-component)。

1. 通过单击表单的开始区域中的&#x200B;**编辑**&#x200B;创建开始操作。 如果需要，您可以输入框标题。 默认情况下，Box标题为&#x200B;**Metadata**。 如果希望生成用于验证的java-script客户端代码，请选中“客户端验证”复选框。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 通过单击表单“结束”区域中的&#x200B;**编辑**，创建“结束”操作。 例如，您可能希望创建一个&#x200B;**[!UICONTROL Submit]**&#x200B;选项，以允许用户提交其元数据更改。 或者，您可以添加&#x200B;**重置**&#x200B;选项，以将元数据重置为其原始状态。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 在&#x200B;**表单开始**&#x200B;和&#x200B;**表单结尾**&#x200B;之间，将元数据文本字段拖动到表单。 用户将元数据填充到这些文本字段中，他们可以提交或完成对其执行的其他操作。

1. 多次单击字段名称，例如&#x200B;**Title**&#x200B;可打开元数据字段并进行更改。 在&#x200B;**编辑组件**&#x200B;窗口的&#x200B;**常规**&#x200B;选项卡中，您定义命名空间和字段标签以及类型，例如`dc:title`。

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

有关修改元数据表单中可用命名空间的信息，请参阅[自定义和扩展资产](/help/assets/extending-assets.md)。

1. 单击&#x200B;**约束**&#x200B;选项卡。 您可以在此处选择字段是否为必填字段以及是否根据需要添加任何约束。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 单击&#x200B;**显示**&#x200B;选项卡。 在此，您可以为元数据字段输入新的宽度和行数。 选中&#x200B;**字段为只读**&#x200B;复选框，以允许用户编辑元数据。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各种字段的元数据表单的示例：

![元数据](assets/chlimage_1-390.png)

在“资产编辑器”页面上，用户随后可以在元数据字段中输入值（如果可编辑）并执行结束操作（例如，提交更改）。

#### 子资产 {#sub-assets}

您可以在子资产组件中视图和选择子资产。 您可以确定[主资产](/help/assets/assets.md#what-are-digital-assets)和子资产下显示的名称。

多次 — 单击子资产组件以打开子资产对话框，您可以在其中更改主资产和任何子资产的标题。 默认值显示在相应字段的下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是已填充子资产组件的示例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您选择了子资产，请注意组件如何显示相应的页面以及框标题从子资产更改为同级。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 标记 {#tags}

标记组件是一个组件，用户可以通过它将现有标记分配给资产，这有助于以后的组织和检索。 您可以将此组件设置为只读，因此用户无法添加标记，而只能视图标记。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

多次 — 单击“标记”组件以打开标记对话框，您可以根据需要从“标记”更改标题，也可以在其中选择已分配的命名空间。 要使此字段可编辑，请清除&#x200B;**[!UICONTROL 隐藏编辑]**&#x200B;复选框。 默认情况下，标记是可编辑的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果用户可以编辑标记，则可以单击铅笔，通过从“标记”下拉菜单中选择标记来添加标记。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是已填充的标记组件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 缩略图 {#thumbnail}

缩略图组件是资产显示选定缩略图的位置（对于许多格式，缩略图会自动提取）。 此外，该组件还显示文件名以及可修改的](/help/assets/assets-finder-editor.md#adding-asset-editor-actions)操作。[

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

多次 — 单击缩览图组件以打开缩览图对话框，您可以在其中更改替代文本。 默认情况下，缩览图alt文本默认为&#x200B;**单击以下载**&#x200B;资产。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是已填充的缩略图组件的示例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 标题 {#title}

标题组件会显示资产的标题和说明。

默认情况下，它处于只读模式，因此用户无法编辑它。 要使其可编辑，请多次单击组件并清除&#x200B;**隐藏编辑按钮**&#x200B;复选框。 此外，为多个资产输入标题。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以编辑标题，则可以通过单击铅笔打开&#x200B;**资产属性**&#x200B;窗口来添加标题和说明。 此外，您还可以通过选择日期和时间来打开和关闭资产。

在编辑[!UICONTROL 标题]时，用户可以更改&#x200B;**标题**、**说明**，并输入&#x200B;**开启**&#x200B;和&#x200B;**关闭时间**&#x200B;以打开和关闭资产。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是已填充标题组件的示例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 添加资产编辑器操作{#adding-asset-editor-actions}

您可以通过一系列预定义操作来确定用户可以对选定数字资产执行的操作。

要向“资产编辑器”页面添加操作，请执行以下操作：

1. 在要自定义的“资产编辑器”页面中，单击Sidekick中的&#x200B;**资产编辑器**。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

可执行以下操作：

| 操作 | 描述 |
|---|---|
| [!UICONTROL 下载] | 允许用户下载选定内容   资源。 |
| [!UICONTROL 编辑者] | 允许用户编辑图像   （交互式编辑） |
| [!UICONTROL Lightbox] | 将资源保存到   “lightbox”，您可以在其中对其执行其他操作。 这个来了   在跨多个页面处理资产时非常方便。 |
| [!UICONTROL 锁定] | 允许用户锁定资产。 此   默认情况下未启用功能，需要在列表中启用   组件。 |
| [!UICONTROL 引用] | 单击此图标可显示哪些页面   正在使用资产。 |
| [!UICONTROL 版本控制] | 允许您创建和恢复   资产的版本。 |

1. 将相应的操作拖至页面上的&#x200B;**Actions**&#x200B;区域。 它创建一个选项，用于执行在页面上拖动的操作。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用“资产编辑器”页面{#multi-editing-assets-with-the-asset-editor-page}进行多次编辑资产

使用[!DNL Experience Manager Assets]，您可以一次更改多个资产。 在选定资产后，您可以同时更改其：

* 标记
* 元数据

要使用“资产编辑器”页面对资产进行多次编辑，请执行以下操作：

1. 打开Geometrixx **按中心**页：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 选择资产：

   * 在Windows上：`Ctrl + click`每个资产。
   * 在Mac上：`Cmd + click`每个资产。

   要选择资产范围，请执行以下操作：单击第一个资产，然后单击最后一个资产。`Shift + click`

1. 在&#x200B;**操作**&#x200B;字段（页面的左侧部分）中单击&#x200B;**编辑元数据**。
1. Geometrixx **按中心资产编辑器**&#x200B;将在新选项卡中打开。 资产的元数据会按如下方式显示：

   * 标记并不适用于所有资产，而只适用于少数资产，它以斜体显示。
   * 应用于所有资产的标记会使用普通字体显示。
   * 除标记之外的元数据：仅当所有选定资产的字段值相同时，才会显示该字段的值。

1. 单击&#x200B;**下载**&#x200B;以下载包含资产原始演绎版的ZIP文件。
1. 单击&#x200B;**Tags**&#x200B;字段旁边的“编辑标记”选项。

   * 并不适用于所有资源，但仅适用于少数资源的标记具有灰色背景。
   * 应用于所有资源的标记具有白色背景。

   您可以：

   * 单击`x`以删除所有资源的标记。
   * 单击`+`以将标记添加到所有资产。
   * 单击&#x200B;**箭头**&#x200B;并选择一个标记以向所有资产添加新标记。

   单击&#x200B;**确定**&#x200B;将更改写入表单。 将自动选中&#x200B;**标记**&#x200B;字段旁边的框。

1. 编辑描述字段。 例如，将其设置为：

   `This is a common description`

   在编辑字段时，其值会在提交表单时覆盖选定资产的现有值。

   注意：编辑字段时，会自动选中该字段旁边的框。

1. 单击&#x200B;**更新元数据**&#x200B;以提交表单并保存对所有资产所做的更改。

   注意：只修改选定的元数据。
