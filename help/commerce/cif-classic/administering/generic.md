---
title: 管理通用电子商务
seo-title: 管理通用电子商务
description: AEM通用解决方案提供了管理存储库中保存的商务信息的方法。
seo-description: AEM通用解决方案提供了管理存储库中保存的商务信息的方法。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 812d1a43176a75ff22e3a0bc07bc658cb5070a62
workflow-type: tm+mt
source-wordcount: '3002'
ht-degree: 4%

---

# 管理通用电子商务 {#administering-generic-ecommerce}

AEM通用解决方案提供了管理存储库中保存的商务信息的方法（而不是使用外部电子商务引擎）。 这包括：

* [产品](/help/commerce/cif-classic/administering/concepts.md#products)
* [产品的系列品种](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目录](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促销活动](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [优惠券](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [订单](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [代理页](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>标准AEM安装包括通用AEM(JCR)电子商务实施。
>
>此功能当前用于演示目的，或根据您的要求作为自定义实施的基本基础。

## 产品和产品变量 {#products-and-product-variations}

>[!NOTE]
>
>以下过程适用于产品和产品变体。

在创建产品之前，您需要定义[scaffold](/help/sites-authoring/scaffolding.md)。 这会指定定义产品及其编辑方式所需的字段。

每个不同的产品类型都需要基架。 相应的基架通过以下任一方式与产品关联：

* 路径
* 产品可以引用scaffold

>[!NOTE]
>
>Geometrixx-Outdoors商店具有单个产品类型（因此具有单个基架）：
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-Outdoors产品类型在以下位置处于活动状态：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在下的任意位置创建新的产品定义，而无需进行任何其他设置。

### 正在导入产品 {#importing-products}

#### 导入产品 — 触屏优化UI {#importing-products-touch-optimized-ui}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**Products**&#x200B;控制台导航到所需的位置。
1. 使用&#x200B;**导入产品**&#x200B;图标打开向导。

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定：

   * **导入程序**

      特定[商务提供程序](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的导入器，默认为`Geometrixx`。

   * **源**

      要导入的文件；您可以使用浏览器选择文件。

   * **增量导入**

      指示这是否是增量导入（而不是完全导入）。
   >[!NOTE]
   >
   >示例geometrixx-outdoor导入程序的增量导入在产品级别运行。
   >
   >可定义自定义导入器以根据需要进行操作。

1. 选择&#x200B;**Next**&#x200B;以导入产品，将显示所执行操作的日志。

   >[!NOTE]
   >
   >产品将导入到当前位置，或相对于当前位置。

   >[!NOTE]
   >
   >反复使用&#x200B;**Next**&#x200B;和&#x200B;**Back**&#x200B;将重复导入产品定义。 但是，由于它们具有相同的SKU，因此存储库中现有的信息将会被覆盖。

1. 选择&#x200B;**完成**&#x200B;以关闭向导。

#### 导入产品 — 经典UI {#importing-products-classic-ui}

1. 使用&#x200B;**Tools**&#x200B;控制台打开&#x200B;**Commerce**&#x200B;文件夹。
1. 双击以打开&#x200B;**产品导入程序**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定：

   * **存储名称**

      产品将导入到：

      `/etc/commerce/products/<*store name*>/`

   * **商业提供程序**

      [商务提供程序](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的导入程序；默认Geometrixx。

   * **源文件**

      要导入的文件的存储库中的位置。

   * **增量导入**

      指示这是否是增量导入（而不是完全导入）。

1. 单击&#x200B;**Import Products**。

### 创建产品信息 {#creating-product-information}

>[!NOTE]
>
>标准产品管理是基本的，因为Geometrixx-Outdoors产品集一直是基本的。 复杂性基于产品[基架](/help/sites-authoring/scaffolding.md)，因此使用您自己的产品基架可以实现更复杂的编辑。

#### 创建产品信息 — 触屏优化UI {#creating-product-information-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（通过&#x200B;**Commerce**）导航到所需位置。
1. 使用&#x200B;**创建**&#x200B;图标选择以下任一选项（取决于结构和位置）：

   * **创建产品**
   * **创建产品变量**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 随即会打开向导。 使用&#x200B;**Basic**&#x200B;和&#x200B;**Product Tabs**&#x200B;为新产品或产品变体输入[产品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。

   >[!NOTE]
   >
   >**** 标题和 **** SKU是创建产品或变体所需的最低版本。

1. 选择&#x200B;**创建**&#x200B;以保存信息。

>[!NOTE]
>
>许多产品都提供多种颜色和/或尺寸。 有关基本产品和相关产品变型的信息，可以从&#x200B;**产品**&#x200B;控制台进行管理。
>
>产品及其变体以树结构形式存储，产品信息位于顶部，下面有变体（此结构由UI强制实施）。

### 编辑产品信息 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors中的产品图像来自：
>
>`/etc/commerce/products/...`
>
>这意味着，默认情况下， [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)会阻止它们，因此请根据需要进行配置。

#### 编辑产品信息 — 触屏优化UI {#editing-product-information-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（通过&#x200B;**Commerce**）导航到您的产品信息。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**查看产品数据**&#x200B;图标：

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 将显示[产品属性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。 使用&#x200B;**Edit**&#x200B;和&#x200B;**Done**&#x200B;进行任何更改。

### 显示产品引用 {#showing-product-references}

#### 显示产品引用 — 触屏优化UI {#showing-product-references-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（通过&#x200B;**Commerce**）导航到您的产品信息。
1. 使用图标打开引用的辅助边栏：

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 选择您需要的产品 — 辅助边栏将更新以显示可用的引用类型：

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. 单击/点按引用类型（例如，产品页面）以展开列表。
1. 选择特定引用以显示选项：

   * 导航到产品页面
   * 编辑产品页面

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### 搜索产品 {#search-for-products}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用图标打开“搜索”的辅助边栏：

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 您可以使用多个Facet来搜索产品。 您只能对搜索使用一个或多个Facet。 将显示找到的产品：

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. 单击/点按产品会打开它。 您还可以发布或查看产品数据。

#### 扩展搜索 {#extending-search}

您可以使用以下CRXDE Lite修改现有小平面或添加新小平面：

1. 导航至:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 您可以修改产品搜索页面上显示的大小。 单击`sizegroup`节点。
1. 单击`items`节点，然后单击`propertypredicate`节点。
1. 您可以修改`propertyValues`。 例如，您可以添加XS、XXL或删除大小。
1. 单击&#x200B;**Save All**&#x200B;并导航到产品搜索页面。 此时应会显示您所做的更改。

### 多个资产 {#multiple-assets}

您可以在产品组件中添加多个资产，然后指定将在产品页面上显示的资产。

>[!NOTE]
>
>与多个资产相关的所有操作均可通过触屏优化UI完成。

#### 添加多个资产 {#adding-multiple-assets}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**Products**&#x200B;控制台，导航到所需的产品。

   >[!NOTE]
   >
   >您必须位于产品级别，而不是变体级别。

1. 通过选择模式或快速操作，点按/单击&#x200B;**查看产品数据**&#x200B;图标。
1. 点按/单击编辑图标。
1. 滚动到&#x200B;**Add**。

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. 点按/单击&#x200B;**添加**。 此时会显示新的资产占位符。
1. 点按/单击**更改**会打开一个对话框，通过该对话框可以选择资产。
1. 选择要添加的资产。

   >[!NOTE]
   >
   >您可以选择的资产来自[Assets](/help/assets/assets.md)。

1. 点按/单击完成图标。

现在，两个资产会存储在您的产品组件中。 您可以配置产品页面上将显示哪个页面。 这适用于类别系统。 首先，您需要向单个资产添加类别：

1. 点按/单击&#x200B;**查看产品数据**。
1. 在资产下键入&#x200B;**资产类别**，例如`cat1`和`cat2`。

   >[!NOTE]
   >
   >您还可以对类别使用标记。

1. 点按/单击完成图标。 您现在必须[转出](#rolling-out-a-catalog)您的更改。

现在，您的产品组件中的资产有一个类别。 您可以配置在三个不同级别上显示的类别：

* [产品页面](#product-page)
* [目录](#catalog)
* [产品控制台](#products-console)

>[!NOTE]
>
>如果不设置类别，则第一个资产将显示在产品页面上。

选择要显示的图像的机制如下：

1. 验证是否为产品页面设置了类别。
1. 如果没有，请验证是否为目录设置了类别。
1. 如果未设置，请验证是否为产品控制台设置了类别。

>[!NOTE]
>
>对于目录级别和产品控制台级别，您必须转出更改才能应用修改并在产品页面上查看差异。

#### 产品页面 {#product-page}

1. 导航到您的产品页面。
1. **** 编辑产品组件。
1. 键入您选择的&#x200B;**图像类别**（例如`cat1`）。
1. 点按/单击&#x200B;**完成**。 页面将刷新，并应显示正确的资产。

#### 目录  {#catalog}

1. 导航到您的目录。
1. 点按/单击&#x200B;**查看属性**。
1. 点按/单击&#x200B;**编辑**。
1. 点按/单击&#x200B;**Assets**&#x200B;选项卡。
1. 键入所需的&#x200B;**产品资产类别**。
1. 点按/单击&#x200B;**完成**。
1. [](#rolling-out-a-catalog) 汇总更改。

#### 产品控制台 {#products-console}

1. 使用&#x200B;**Products**&#x200B;控制台，导航到所需的产品。
1. 点按/单击&#x200B;**查看产品数据**。
1. 点按/单击&#x200B;**编辑**。
1. 键入&#x200B;**默认资产类别**。
1. 点按/单击&#x200B;**完成**。
1. [](#rolling-out-a-catalog) 汇总更改。

### 发布/取消发布产品信息 {#publishing-unpublishing-product-information}

#### 发布/取消发布产品信息 — 触屏优化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>产品信息通常通过引用它的页面发布。 例如，在发布引用产品Y的页面X时，AEM将询问您是否还要发布产品Y。
>
>对于特殊情况，AEM还支持直接从产品数据发布。

1. 使用&#x200B;**Products**&#x200B;控制台（通过&#x200B;**Commerce**）导航到您的产品信息。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   根据需要选择&#x200B;**Publish**&#x200B;或&#x200B;**Unpublish**&#x200B;图标：

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   将根据需要发布或取消发布产品信息。

### 产品信息源 {#product-feed}

Search&amp;Promote集成允许您：

* 使用电子商务API，与底层存储库结构和商务平台无关。
* 利用Search&amp;Promote的索引连接器功能以XML格式提供产品馈送。
* 利用Search&amp;Promote的远程控制功能执行产品馈送的按需或计划请求
* 不同Search&amp;Promote帐户的信息源生成，配置为云服务配置。

有关更多信息，请阅读[产品信息源](/help/sites-administering/product-feed.md)。

### 产品更新的事件处理程序 {#event-handler-for-product-updates}

有一个事件处理程序，它会在添加、修改或删除产品以及添加、修改或删除产品页面时记录事件。 以下是OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

对于`PRODUCT_*`事件，路径指向`/etc/commerce/products`中的基本产品。 对于`PRODUCT_PAGE_*`事件，路径指向`cq:Page`节点。

您可以在OSGI事件(`/system/console/events`)的Web控制台中查看这些事件，例如：

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另请阅读AEM](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)中的[事件处理。

### 添加到购物车图像链接 {#image-with-add-to-cart-links}

通过添加到购物车链接的图像组件，您可以通过创建与图像上的产品链接的热点来快速将产品添加到购物车。

单击热点会打开一个对话框，您可以从中选择产品的大小和数量。

1. 导航到要添加组件的页面。
1. 将组件拖放到页面中。
1. 从[资产浏览器](/help/sites-authoring/author-environment-tools.md#assets-browser)将图像拖放到组件中。
1. 您可以：

   * 单击组件，然后单击编辑图标
   * 慢速双击

1. 单击全屏图标。

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. 单击启动映射图标。

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. 单击其中一个形状图标。

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 根据需要修改和移动形状。
1. 单击形状。
1. 单击浏览图标可打开[资产选取器](/help/assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，您也可以直接键入必须位于产品级别而非变体级别的产品路径。

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. 单击确认图标两次，然后单击退出全屏。
1. 单击组件旁边页面上的某个位置。 页面应会刷新，您应会在图像上看到以下符号：

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切换到[preview](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui)模式。
1. 单击+热点。 此时将打开一个对话框，您可以在其中选择在&#x200B;**Path**&#x200B;中输入的产品的大小和数量。

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. 输入大小和数量。
1. 单击添加到购物车按钮。 对话框关闭。
1. 导航到购物车。 产品应该在这里。

#### 配置选项 {#configuration-options}

您可以配置单击热点时对话框的外观：

1. 单击组件，然后单击配置图标。

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下滚动. 有一个&#x200B;**ADD TO CART**&#x200B;选项卡。

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. 单击&#x200B;**添加到购物车**。 您可以使用3个配置选项。

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. 单击完成图标。

## 目录 {#catalogs}

### 生成目录 {#generating-a-catalog}

#### 生成目录 — 触屏优化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目录将引用您的产品数据。

要生成目录，请执行以下操作：

1. 打开“站点”控制台（例如，[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)）。
1. 导航到要创建新页面的位置。
1. 要打开选项列表，请使用“**创建**”图标：

   ![创建图标](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 从列表中选择&#x200B;**创建目录**，此时将打开创建目录向导。

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. 导航到所需的目录Blueprint。
1. 点按/单击&#x200B;**选择**&#x200B;按钮，然后点按/单击所需的目录Blueprint。
1. 点按/单击&#x200B;**下一步**。

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. 键入&#x200B;**标题**&#x200B;和&#x200B;**名称**。
1. 点按/单击&#x200B;**创建**&#x200B;按钮。 随即会创建目录并打开一个对话框。

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. 点按/单击&#x200B;**完成**&#x200B;按钮可返回到站点控制台，您将可以在该控制台中看到目录。

   点按/单击&#x200B;**打开目录**&#x200B;按钮可打开您的目录（例如`http://localhost:4502/editor.html/content/test-catalog.html`）。

#### 生成目录 — 经典UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>该目录将引用您的[产品数据](#products-and-product-variants)。

1. 使用&#x200B;**网站**&#x200B;控制台，导航到&#x200B;**目录Blueprint**，然后导航到基本目录。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用&#x200B;**Section Blueprint**&#x200B;模板创建新页面。

   例如，`Swimwear`。

1. 打开新的`Swimwear`页面，然后单击&#x200B;**编辑Blueprint**&#x200B;以打开&#x200B;**属性**&#x200B;对话框，您可以在其中设置&#x200B;**产品**&#x200B;选择。

   例如，打开&#x200B;**Tags/Keywords**&#x200B;字段以选择“活动”，然后从“Geometrixx — 户外”部分中选择“游泳”。

1. 单击&#x200B;**OK**&#x200B;以保存您的资产；示例产品将显示在Blueprint页面的&#x200B;**产品选择标准**&#x200B;下。
1. 单击&#x200B;**转出更改……**，选择&#x200B;**转出页面和所有子页面**，然后单击&#x200B;**下一步**，然后单击&#x200B;**转出**。 成功完成转出后，**Status**&#x200B;指示器将显示为绿色。
1. 您现在可以单击&#x200B;**关闭**&#x200B;并检查新目录部分；例如，在上和下：

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 在Blueprint页面中，再次单击&#x200B;**编辑Blueprint** ，然后在&#x200B;**属性**&#x200B;对话框中，打开&#x200B;**生成的页面**&#x200B;选项卡。 在横幅列表字段中，选择要显示的图像；例如，`summer.jpg`
1. 单击&#x200B;**OK**&#x200B;以保存您的资产；横幅信息将显示在Blueprint页面的&#x200B;**产品选择标准**&#x200B;下。
1. 转出这些新更改。

### 转出目录 {#rolling-out-a-catalog}

#### 推出目录 — 触屏优化UI {#rolling-out-a-catalog-touch-optimized-ui}

转出目录：

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Catalogs**&#x200B;控制台。
1. 导航到要转出的目录。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**转出更改**&#x200B;图标：

   ![转出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在向导中，根据需要设置转出，然后点按/单击&#x200B;**转出更改**。
1. 将打开一个对话框。 完成该过程后，点按/单击&#x200B;**完成**。

#### 转出目录 — 经典UI {#rolling-out-a-catalog-classic-ui}

转出目录：

1. 导航到要转出的目录。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 单击&#x200B;**转出更改……**
1. 根据需要设置转出。
1. 单击&#x200B;**转出**。

### Blueprint导入程序 {#blueprint-importer}

#### Blueprint导入器 — 触屏优化UI {#blueprint-importer-touch-optimized-ui}

1. 通过&#x200B;**Commerce**&#x200B;导航到&#x200B;**Catalogs**&#x200B;控制台。
1. 导航到要导入目录Blueprint的位置。
1. 点按/单击&#x200B;**导入Blueprint**&#x200B;图标。

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在向导中，根据需要选择源，然后点按/单击&#x200B;**下一步**。

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. 完成导入后，点按/单击&#x200B;**完成**。

#### Blueprint导入器 — 经典UI {#blueprint-importer-classic-ui}

1. 使用&#x200B;**Tools**&#x200B;控制台，导航到&#x200B;**Commerce**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 打开&#x200B;**Catalog Bluprint Importer**。
1. 根据需要设置导入。
1. 单击&#x200B;**Import Catalog Blueprints**。

## 促销活动 {#promotions}

### 创建促销活动 {#creating-a-promotion}

#### 创建促销活动 — 经典UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>以下示例处理直接在[campaign](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中举行的促销活动，该促销活动用于凭单。
>
>促销活动也可以位于促销活动的[体验](/help/sites-authoring/personalization.md)中。
>
>有关详细信息，请参阅[促销活动和凭单](#promotions-and-vouchers)。

1. 打开创作实例的&#x200B;**网站**&#x200B;控制台。
1. 在左窗格中，选择您需要的&#x200B;**Campaign**。
1. 单击&#x200B;**New**，选择&#x200B;**Promotion**&#x200B;模板，然后为新凭证指定&#x200B;**Title**(和&#x200B;**Name**（如果需要）)。
1. 单击&#x200B;**创建**。新的促销活动页面将显示在右侧窗格中。

1. 通过以下任一方式编辑&#x200B;**Properties**:

   * 打开页面，然后单击编辑按钮以打开属性对话框
   * 在“网站”控制台中选择页面，然后使用上下文菜单（通常是鼠标右键）选择&#x200B;**属性……**&#x200B;并打开“属性”对话框

   根据需要指定&#x200B;**促销活动类型**、**折扣类型**、**折扣值**&#x200B;和任何其他字段。

1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活促销活动，以便购物者在发布实例上看到该促销活动。

## 优惠券 {#vouchers}

### 创建优惠券 {#creating-a-voucher}

#### 创建优惠券 — 经典UI {#creating-a-voucher-classic-ui}

1. 打开创作实例的&#x200B;**网站**&#x200B;控制台。
1. 在左窗格中，选择您需要的&#x200B;**Campaign**。
1. 单击&#x200B;**New**，选择&#x200B;**凭单**&#x200B;模板，然后为新凭单指定&#x200B;**标题**（如果需要，可指定&#x200B;**名称**）。
1. 单击&#x200B;**创建**。新的凭单页面将显示在右侧窗格中。

1. 双击打开新凭证页面，然后单击&#x200B;**Edit**&#x200B;以根据需要配置信息。
1. 单击&#x200B;**确定**&#x200B;进行保存。

1. 您现在可以激活您的优惠券，以便购物者在发布实例上的购物车中使用该优惠券。

### 删除凭单 {#removing-vouchers}

#### 删除凭单 — 经典UI {#removing-vouchers-classic-ui}

要使凭单对客户不可用，您可以：

* 停用凭单 — 凭单将在创作环境中保持可用，以便您稍后可以重新激活它。
* 完全删除。

这两项操作都可以从&#x200B;**网站**&#x200B;控制台中完成。

### 修改凭证 {#modifying-vouchers}

#### 修改凭单 — 经典UI {#modifying-vouchers-classic-ui}

要更改凭证或促销活动的属性，可以在&#x200B;**网站**&#x200B;控制台上双击该凭证或促销活动，然后单击&#x200B;**编辑**。 保存后，应激活该实例，以便将更改推送到发布实例。

### 将优惠券添加到购物车 {#adding-vouchers-to-a-cart}

要允许用户向购物车添加凭单，您可以使用内置的&#x200B;**Vouchers**&#x200B;组件（商务类别）。 您需要将此内容添加到显示购物车的同一页面（但不是强制选项）。 凭单组件只是用户可在其中输入凭证代码的表单，它是实际显示已应用凭证列表及其折扣的购物车组件。

在演示网站(Geometrixx Outdoors — 英语)中，您可以在购物车页面的实际购物车下看到凭证表单。

## 订单 {#orders}

>[!NOTE]
>
>应当记住，现成的AEM没有对与订单相关的标准功能（如退货、更新订单状态、执行完成、生成装箱单）所需的操作。 它主要用作技术预览。
>
>AEM中的通用订单管理一直是基本的；向导中可用的字段取决于基架：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果创建自定义基架，则可以存储更多订单信息。

>[!NOTE]
>
>订单控制台会公开供应商订单信息，该信息从未发布。
>
>客户订单信息保存在其主目录中，并由其帐户的订单历史记录公开。 此信息与其其余的主目录一起发布。

### 创建订单信息 {#creating-order-information}

#### 创建订单信息 — 触屏优化UI {#creating-order-information-touch-optimized-ui}

1. 使用&#x200B;**Orders**&#x200B;控制台导航到所需位置。
1. 使用&#x200B;**创建**&#x200B;图标选择&#x200B;**创建顺序**。

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 随即会打开向导。 使用&#x200B;**基本**、**内容**、**付款**&#x200B;和&#x200B;**履行**&#x200B;选项卡，输入有关新订单](/help/commerce/cif-classic/administering/concepts.md#order-information)的[信息。

1. 选择&#x200B;**创建**&#x200B;以保存信息。

### 编辑订单信息 {#editing-order-information}

#### 编辑订单信息 — 触屏优化UI {#editing-order-information-touch-optimized-ui}

1. 使用&#x200B;**Orders**&#x200B;控制台导航到订单。
1. 使用以下任何一种方式：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   选择&#x200B;**查看订单数据**&#x200B;图标：

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 将显示[订单信息](/help/commerce/cif-classic/administering/concepts.md#order-information)。 使用&#x200B;**Edit**&#x200B;和&#x200B;**Done**&#x200B;进行任何更改。

