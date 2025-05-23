---
title: 管理通用电子商务
description: AEM通用解决方案提供了管理存储库中保留的商务信息的方法。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 2%

---

# 管理通用电子商务 {#administering-generic-ecommerce}

Adobe Experience Manager (AEM)通用解决方案提供了管理存储库中保留的商务信息的方法（与使用外部电子商务引擎不同）。 这包括：

* [产品](/help/commerce/cif-classic/administering/concepts.md#products)
* [产品的系列品种](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目录](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促销活动](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [优惠券](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [订单](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [代理页面](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>标准AEM安装包括通用AEM (JCR)电子商务实施。
>
>它旨在用于演示目的，或作为根据您的要求进行自定义实施的基本基础。

## 产品和产品变体 {#products-and-product-variations}

>[!NOTE]
>
>以下过程同时适用于产品和产品变体。

在创建产品之前，请定义[基架](/help/sites-authoring/scaffolding.md)。 这会指定必须定义的字段、产品以及编辑方式。

每种不同的产品类型都需要一个基架。 适当的基架通过以下任一方式与产品相关联：

* 路径
* 产品可以引用基架

>[!NOTE]
>
>Geometrixx-Outdoors商店只有一种产品类型（因此只有一种基架）：
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-Outdoors产品类型在以下位置处于活动状态：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>无需任何其他设置，您便可以在产品定义下的任何位置创建产品定义。

### 正在导入产品 {#importing-products}

#### 导入产品 — 触屏优化UI {#importing-products-touch-optimized-ui}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**产品**&#x200B;控制台导航到所需的位置。
1. 使用&#x200B;**导入产品**&#x200B;图标打开向导。

   ![导入产品图标](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定：

   * **导入程序**

     特定[商务提供程序](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的导入程序，默认为`Geometrixx`。

   * **来源**

     要导入的文件；您可以使用浏览器选择文件。

   * **增量导入**

     指示这是否为增量导入（而不是完全导入）。

   >[!NOTE]
   >
   >增量导入（示例geometrixx-outdoor导入程序的）在产品级别运行。
   >
   >可以定义自定义导入程序以根据需要进行操作。

1. 选择&#x200B;**下一步**&#x200B;以导入产品，此时将显示所采取操作的日志。

   >[!NOTE]
   >
   >产品会导入到当前位置或相对于当前位置。

   >[!NOTE]
   >
   >重复使用&#x200B;**Next**&#x200B;和&#x200B;**Back**&#x200B;重复导入产品定义。 但是，由于它们具有相同的SKU，因此会覆盖存储库中存在的信息。

1. 选择&#x200B;**完成**&#x200B;以关闭向导。

#### 导入产品 — 经典UI {#importing-products-classic-ui}

1. 使用&#x200B;**工具**&#x200B;控制台打开&#x200B;**Commerce**&#x200B;文件夹。
1. 双击以打开&#x200B;**产品导入程序**：

   ![产品导入程序控制台](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定：

   * **存储名称**

     产品将导入到：

     `/etc/commerce/products/<*store name*>/`

   * **Commerce提供程序**

     您的[商务提供程序](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的导入程序；默认为Geometrixx。

   * **Source文件**

     要导入的文件在存储库中的位置。

   * **增量导入**

     指示这是否为增量导入（而不是完全导入）。

1. 单击&#x200B;**导入产品**。

### 创建产品信息 {#creating-product-information}

>[!NOTE]
>
>标准产品管理是基本的，因为Geometrixx-Outdoors产品集是基本的。 复杂性基于产品[基架](/help/sites-authoring/scaffolding.md)，因此使用您自己的产品基架可以实现更复杂的编辑。

#### 创建产品信息 — 触屏优化UI {#creating-product-information-touch-optimized-ui}

1. 使用&#x200B;**产品**&#x200B;控制台(通过&#x200B;**Commerce**)导航到所需的位置。
1. 使用&#x200B;**创建**&#x200B;图标选择以下任一选项（具体取决于结构和位置）：

   * **创建产品**
   * **创建产品变体**

   ![加号形状创建图标](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 将打开向导。 使用&#x200B;**基本**&#x200B;和&#x200B;**产品选项卡**&#x200B;为新产品或产品变型输入[产品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。

   >[!NOTE]
   >
   >**Title**&#x200B;和&#x200B;**SKU**&#x200B;是创建产品或变体所需的最小值。

1. 选择&#x200B;**创建**&#x200B;以保存信息。

>[!NOTE]
>
>许多产品的颜色和/或尺寸各不相同。 有关基本产品和相关产品变体的信息均可从&#x200B;**产品**&#x200B;控制台进行管理。
>
>产品及其变体存储为树结构，产品信息位于顶部，变体位于下方（此结构由UI强制实施）。

### 编辑产品信息 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors中的产品图像可从以下位置提供：
>
>`/etc/commerce/products/...`
>
>这意味着，默认情况下，[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans)会阻止这些服务器，因此请根据需要进行配置。

#### 编辑产品信息 — 触屏优化UI {#editing-product-information-touch-optimized-ui}

1. 使用&#x200B;**产品**&#x200B;控制台(通过&#x200B;**Commerce**)导航到您的产品信息。
1. 使用：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**查看产品数据**&#x200B;图标：

   ![查看产品数据图标 — 信息图标](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 将显示[产品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。 使用&#x200B;**编辑**&#x200B;和&#x200B;**完成**&#x200B;进行任何更改。

### 显示产品引用 {#showing-product-references}

#### 显示产品引用 — 触控优化的UI {#showing-product-references-touch-optimized-ui}

1. 使用&#x200B;**产品**&#x200B;控制台(通过&#x200B;**Commerce**)导航到您的产品信息。
1. 使用图标打开引用的辅助边栏：

   ![双箭头图标](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 选择所需的产品 — 二级边栏更新，其中显示了可用的引用类型：

   引用打开的![产品控制台](/help/sites-administering/assets/chlimage_1-88.png)

1. 单击引用类型（例如，“产品页面”）以展开列表。
1. 选择特定引用，以便显示以下选项：

   * 导航到产品页面
   * 编辑产品页面

   ![产品控制台引用面板](/help/sites-administering/assets/chlimage_1-89.png)

### 搜索产品 {#search-for-products}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用图标打开要搜索的辅助边栏：

   ![放大镜图标](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 您可以使用多个Facet来搜索产品。 搜索只能使用一个或多个Facet。 显示的产品包括：

   产品控制台中的![产品数据](/help/sites-administering/assets/chlimage_1-90.png)

1. 单击/点按产品可将其打开。 您还可以发布或查看产品数据。

#### 扩展搜索 {#extending-search}

您可以使用CRXDE Lite修改现有方面或添加新方面：

1. 导航至：

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以编辑产品搜索页面上显示的大小。 单击`sizegroup`节点。
1. 单击`items`节点，然后单击`propertypredicate`节点。
1. 您可以编辑`propertyValues`。 例如，可以添加XS、XXL或移除大小。
1. 单击&#x200B;**全部保存**，然后导航到产品搜索页面。 此时应会显示您的更改。

### 多个Assets {#multiple-assets}

您可以在产品组件中添加多个资产，然后指定要显示在产品页面上的资产。

>[!NOTE]
>
>与多个资产相关的所有操作均可通过触屏优化UI完成。

#### 添加多个Assets {#adding-multiple-assets}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**产品**&#x200B;控制台，导航到所需的产品。

   >[!NOTE]
   >
   >您必须处于产品级别，而不是变型级别。

1. 选择带有选择模式或快速操作的&#x200B;**查看产品数据**&#x200B;图标。
1. 选择编辑图标。
1. 滚动到&#x200B;**添加**。

   ![正在添加产品数据屏幕快照](/help/sites-administering/assets/chlimage_1-91.png)

1. 选择&#x200B;**添加**。 将出现一个新的资产占位符。
1. 选择&#x200B;**更改**&#x200B;将打开一个对话框，允许您选择资源。
1. 选择要添加的资源。

   >[!NOTE]
   >
   >您可以选择的资源来自[Assets](/help/assets/assets.md)。

1. 选择完成图标。

两个资产现在存储在您的产品组件中。 您可以配置哪个出现在产品页面上。 这适用于类别系统。 首先，必须将类别添加到单个资产：

1. 选择&#x200B;**查看产品数据**。
1. 在资源下键入&#x200B;**资源类别**，例如`cat1`和`cat2`。

   >[!NOTE]
   >
   >您还可以将标记用于类别。

1. 选择完成图标。 您现在必须[转出](#rolling-out-a-catalog)您的更改。

现在，产品组件中的资产具有一个类别。 您可以配置在三个不同级别显示的类别：

* [产品页面](#product-page)
* [目录](#catalog)
* [产品控制台](#products-console)

>[!NOTE]
>
>如果不设置类别，则第一个资产会显示在产品页面上。

选择要显示的图像的机制如下：

1. 验证是否为产品页面设置了类别。
1. 如果没有，请验证是否为目录设置了类别。
1. 如果没有，请验证是否为产品控制台设置了类别。

>[!NOTE]
>
>对于目录级别和产品控制台级别，您必须转出更改以应用修改并在产品页面上查看差异。

#### 产品页面 {#product-page}

1. 导航到您的产品页面。
1. **编辑**&#x200B;产品组件。
1. 键入您选择的&#x200B;**图像类别**（例如`cat1`）。
1. 选择&#x200B;**完成**。 页面将刷新，并且应会显示正确的资产。

#### 目录  {#catalog}

1. 导航到您的目录。
1. 选择&#x200B;**查看属性**。
1. 选择&#x200B;**编辑**。
1. 选择&#x200B;**资源**&#x200B;选项卡。
1. 键入所需的&#x200B;**产品资产类别**。
1. 选择&#x200B;**完成**。
1. [转出](#rolling-out-a-catalog)您的更改。

#### 产品控制台 {#products-console}

1. 使用&#x200B;**产品**&#x200B;控制台，导航到所需的产品。
1. 选择&#x200B;**查看产品数据**。
1. 选择&#x200B;**编辑**。
1. 键入&#x200B;**默认资源类别**。
1. 选择&#x200B;**完成**。
1. [转出](#rolling-out-a-catalog)您的更改。

### 发布/取消发布产品信息 {#publishing-unpublishing-product-information}

#### 发布/取消发布产品信息 — 触屏优化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>通常，产品信息会通过引用它的页面发布。 例如，在发布引用产品Y的页面X时，AEM会询问您是否还想发布产品Y。
>
>对于特殊情况，AEM还支持直接从产品数据发布。

1. 使用&#x200B;**产品**&#x200B;控制台(通过&#x200B;**Commerce**)导航到您的产品信息。
1. 使用：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   根据需要选择&#x200B;**Publish**&#x200B;或&#x200B;**取消发布**&#x200B;图标：

   ![世界图标](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![带有十字符号的世界图标 — 无符号](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   根据需要，发布或取消发布产品信息。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 产品更新的事件处理程序 {#event-handler-for-product-updates}

有一个事件处理程序，可在添加、编辑或删除产品以及添加、编辑或删除产品页面时记录事件。 有以下OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

对于`PRODUCT_*`事件，路径指向`/etc/commerce/products`中的基础产品。 对于`PRODUCT_PAGE_*`事件，路径指向`cq:Page`节点。

您可以在OSGI事件( `/system/console/events`)的Web控制台中查看它们，例如：

![OSGI事件示例](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另请阅读AEM[&#128279;](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)中的事件处理。

### 包含添加到购物车链接的图像 {#image-with-add-to-cart-links}

使用包含添加到购物车链接的图像组件，您可以通过创建与图像上的产品链接的热点来快速将产品添加到购物车。

单击热点将打开一个对话框，您可以在其中选择产品的大小和数量。

1. 导航到要添加该组件的页面。
1. 将组件拖放到页面中。
1. 从[资源浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)将图像拖放到组件中。
1. 您可以：

   * 单击组件，然后单击编辑图标
   * 进行慢速双击

1. 单击全屏图标。

   ![全屏图标](/help/sites-administering/assets/chlimage_1-92.png)

1. 单击启动图图标。

   ![启动地图图标](/help/sites-administering/assets/chlimage_1-93.png)

1. 单击其中一个形状图标。

   ![形状图标](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 根据需要修改和移动形状。
1. 单击形状。
1. 单击浏览图标可打开[资产选取器](/help/assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，您可以直接键入必须在产品级别而非变型级别的产品路径。

   ![类型路径](/help/sites-administering/assets/chlimage_1-94.png)

1. 单击两次确认图标，然后单击退出全屏。
1. 单击页面中组件旁边的某个位置。 页面应刷新，您应该会在图像上看到以下符号：

   ![加号](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切换到[预览](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui)模式。
1. 单击+热点。 将打开一个对话框，您可以在其中选择在&#x200B;**路径**&#x200B;中输入的产品的大小和数量。

   ![产品示例： poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. 输入大小和数量。
1. 单击添加到购物车按钮。 对话框关闭。
1. 导航到购物车。 产品应该在这里。

#### 配置选项 {#configuration-options}

您可以配置在单击热点时对话框的外观：

1. 单击组件，然后单击配置图标。

   ![配置图标](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下滚动。 有一个&#x200B;**添加到购物车**&#x200B;选项卡。

   ![添加到购物车选项卡](/help/sites-administering/assets/chlimage_1-97.png)

1. 单击&#x200B;**添加到购物车**。 有三个配置选项可供您使用。

   ![配置选项](/help/sites-administering/assets/chlimage_1-98.png)

1. 单击完成图标。

## 目录 {#catalogs}

### 生成目录 {#generating-a-catalog}

#### 生成目录 — 触屏优化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目录引用您的产品数据。

要生成目录，请执行以下操作：

1. 打开站点控制台(例如，[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 导航到要创建页面的位置。
1. 要打开选项列表，请使用&#x200B;**创建**&#x200B;图标：

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 从列表中选择&#x200B;**创建目录**。 此时将打开“创建目录”向导。

   ![创建目录向导](/help/sites-administering/assets/chlimage_1-99.png)

1. 导航到所需的目录Blueprint。
1. 选择&#x200B;**选择**&#x200B;按钮并单击所需的目录Blueprint。
1. 选择&#x200B;**下一步**。

   ![目录属性向导](/help/sites-administering/assets/chlimage_1-100.png)

1. 键入&#x200B;**标题**&#x200B;和&#x200B;**名称**。
1. 选择&#x200B;**创建**&#x200B;按钮。 将创建目录并打开一个对话框。

   ![目录已创建对话框](/help/sites-administering/assets/chlimage_1-101.png)

1. 选择&#x200B;**完成**&#x200B;按钮将返回站点控制台，您可以在其中查看目录。

   点按/单击&#x200B;**打开目录**&#x200B;按钮可打开您的目录（例如，`http://localhost:4502/editor.html/content/test-catalog.html`）。

#### 生成目录 — 经典UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目录引用您的[产品数据](#products-and-product-variants)。

1. 使用&#x200B;**网站**&#x200B;控制台，导航到您的&#x200B;**目录Blueprint**，然后导航到基本目录。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用&#x200B;**分区Blueprint**&#x200B;模板创建页面。

   例如：`Swimwear`。

1. 打开新的`Swimwear`页面，然后单击&#x200B;**编辑Blueprint**。 将打开&#x200B;**属性**&#x200B;对话框，您可以设置&#x200B;**产品**&#x200B;选项。

   例如，打开&#x200B;**标记/关键字**&#x200B;字段以选择“活动”，然后从“Geometrixx — 户外”部分选择“游泳”。

1. 单击&#x200B;**确定**&#x200B;以保存您的属性；示例产品显示在Blueprint页面的&#x200B;**产品选择标准**&#x200B;下。
1. 单击&#x200B;**转出更改……**，选择&#x200B;**转出页面和所有子页面**，然后单击&#x200B;**下一步**，再单击&#x200B;**转出**。 成功完成转出后，**状态**&#x200B;指示器显示为绿色。
1. 您现在可以单击&#x200B;**关闭**&#x200B;并检查新目录部分；例如，位于和下：

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 再次从Blueprint页面单击&#x200B;**编辑Blueprint**，然后在&#x200B;**属性**&#x200B;对话框中打开&#x200B;**生成的页面**&#x200B;选项卡。 在“横幅”列表字段中，选择要显示的图像；例如，`summer.jpg`
1. 单击&#x200B;**确定**&#x200B;以保存您的属性；横幅信息显示在Blueprint页面的&#x200B;**产品选择标准**&#x200B;下。
1. 转出这些新更改。

### 转出目录 {#rolling-out-a-catalog}

#### 转出Catalog — 触屏优化UI {#rolling-out-a-catalog-touch-optimized-ui}

要转出目录：

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**目录**&#x200B;控制台。
1. 导航到要转出的目录。
1. 使用：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**转出更改**&#x200B;图标：

   ![转出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在向导中，根据需要设置转出，然后单击&#x200B;**转出更改**。
1. 随即会打开一个对话框。 进程完成后，选择&#x200B;**完成**。

#### 转出目录 — 经典UI {#rolling-out-a-catalog-classic-ui}

要转出目录：

1. 导航到要转出的目录。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 单击&#x200B;**转出更改……**
1. 根据需要设置转出。
1. 单击&#x200B;**转出**。

### Blueprint导入程序 {#blueprint-importer}

#### Blueprint导入器 — 触屏优化UI {#blueprint-importer-touch-optimized-ui}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**目录**&#x200B;控制台。
1. 导航到要导入目录Blueprint的位置。
1. 选择&#x200B;**导入Blueprint**&#x200B;图标。

   ![导入Blueprint图标](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在该向导中，根据需要选择Source并单击&#x200B;**下一步**。

   ![Blueprint向导](/help/sites-administering/assets/chlimage_1-102.png)

1. 导入完成后，选择&#x200B;**完成**。

#### Blueprint导入程序 — 经典UI {#blueprint-importer-classic-ui}

1. 使用&#x200B;**工具**&#x200B;控制台，导航到&#x200B;**Commerce**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 打开&#x200B;**目录Blueprint导入程序**。
1. 根据需要设置导入。
1. 单击&#x200B;**导入目录Blueprint**。

## 促销活动 {#promotions}

### 创建促销活动 {#creating-a-promotion}

#### 创建促销活动 — 经典UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>以下示例涉及直接在[促销活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中举行的促销，这用于优惠券。
>
>促销活动也可以位于[体验](/help/sites-authoring/personalization.md)中。
>
>有关详细信息，请参阅[促销和优惠券](#promotions-and-vouchers)。

1. 打开创作实例的&#x200B;**网站**&#x200B;控制台。
1. 在左侧窗格中，选择所需的&#x200B;**营销活动**。
1. 单击&#x200B;**新建**，选择&#x200B;**促销活动**&#x200B;模板，然后为新优惠券指定一个&#x200B;**标题**（如有必要，指定&#x200B;**名称**）。
1. 单击&#x200B;**创建**。新的促销页面将显示在右侧窗格中。

1. 通过以下任一方式编辑&#x200B;**属性**：

   * 打开页面，然后单击编辑按钮以打开属性对话框
   * 在网站控制台中选择页面，然后使用上下文菜单（通常是鼠标右键）选择&#x200B;**属性……**&#x200B;并打开属性对话框

   根据需要指定&#x200B;**促销活动类型**、**折扣类型**、**折扣值**&#x200B;和任何其他字段。

1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活促销活动，以便购物者可以在发布实例上看到它。

## 优惠券 {#vouchers}

### 创建优惠券 {#creating-a-voucher}

#### 创建优惠券 — 经典UI {#creating-a-voucher-classic-ui}

1. 打开创作实例的&#x200B;**网站**&#x200B;控制台。
1. 在左侧窗格中，选择所需的&#x200B;**营销活动**。
1. 单击&#x200B;**新建**，选择&#x200B;**优惠券**&#x200B;模板，然后为新优惠券指定一个&#x200B;**标题**（如有必要，还指定&#x200B;**名称**）。
1. 单击&#x200B;**创建**。新凭单页面将显示在右侧窗格中。

1. 双击打开您的新优惠券页面，然后单击&#x200B;**编辑**&#x200B;并根据需要配置信息。
1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活优惠券，以便购物者可以在发布实例上的购物车中使用该优惠券。

### 删除优惠券 {#removing-vouchers}

#### 删除优惠券 — 经典UI {#removing-vouchers-classic-ui}

要使优惠券对客户不可用，您可以：

* 停用优惠券 — 它仍然在创作环境中可用，以便您稍后可以重新激活。
* 将其完全删除。

这两项操作都可以从&#x200B;**网站**&#x200B;控制台中完成。

### 修改凭证 {#modifying-vouchers}

#### 修改优惠券 — 经典UI {#modifying-vouchers-classic-ui}

若要更改优惠券或促销活动的属性，请在&#x200B;**网站**&#x200B;控制台上双击该优惠券或促销活动，然后单击&#x200B;**编辑**。 保存后，您应该激活它，以便将更改推送到发布实例。

### 将优惠券添加到购物车 {#adding-vouchers-to-a-cart}

要允许用户将优惠券添加到其购物车，您可以使用内置的&#x200B;**优惠券**&#x200B;组件(Commerce类别)。 将此项添加到显示购物车的同一页面（但这不是强制性的）。 优惠券组件只是用户可以在其中输入优惠券代码的表单，它是实际显示应用优惠券及其折扣列表的购物车组件。

在演示站点(Geometrixx Outdoors语 — 英语)中，您可以在购物车页面上看到实际购物车下的优惠券表单。

## 订单 {#orders}

>[!NOTE]
>
>请记住，开箱即用的AEM没有与订单相关的标准功能所需的操作，例如退回商品、更新订单状态、执行履行、生成装箱单。 它主要用于技术预览。
>
>AEM中的通用Order Management一直保持为基本；向导中可用的字段取决于基架：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果您创建自定义基架，则可以存储更多订单信息。

>[!NOTE]
>
>订单控制台会公开从未发布的供应商订单信息。
>
>客户订单信息保存在其主目录中，并在其账户的订单历史记录中公开。 此信息与其主目录的其余部分一起发布。

### 创建订单信息 {#creating-order-information}

#### 创建订单信息 — 触屏优化UI {#creating-order-information-touch-optimized-ui}

1. 使用&#x200B;**订单**&#x200B;控制台导航到所需的位置。
1. 使用&#x200B;**创建**&#x200B;图标选择&#x200B;**创建订单**。

   ![加号形状创建图标](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 将打开向导。 使用&#x200B;**基本**、**内容**、**付款**&#x200B;和&#x200B;**履行**&#x200B;选项卡输入有关新订单[&#128279;](/help/commerce/cif-classic/administering/concepts.md#order-information)的信息。

1. 选择&#x200B;**创建**&#x200B;以保存信息。

### 编辑订单信息 {#editing-order-information}

#### 编辑订单信息 — 触屏优化UI {#editing-order-information-touch-optimized-ui}

1. 使用&#x200B;**订单**&#x200B;控制台导航到订单。
1. 使用：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**查看订单数据**&#x200B;图标：

   ![信息图标](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 显示[订单信息](/help/commerce/cif-classic/administering/concepts.md#order-information)。 使用&#x200B;**编辑**&#x200B;和&#x200B;**完成**&#x200B;进行任何更改。

