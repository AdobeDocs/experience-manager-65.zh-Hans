---
title: 将Dynamic Media Classic (Scene7)功能添加到您的页面
description: Adobe Dynamic Media Classic (Scene7)是一款托管解决方案，用于管理、增强和发布富媒体资产，并将其交付给Web、移动设备、电子邮件和连接到Internet的显示和打印。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 0%

---

# 将Dynamic Media Classic (Scene7)功能添加到您的页面{#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html)是一个托管解决方案，用于管理、增强、发布富媒体资源并将其交付给Web、移动设备、电子邮件和连接到Internet的显示和打印。

您可以在多种查看器中查看在Dynamic Media Classic (Scene7)中发布的Experience Manager资源：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资源直接从Experience Manager发布到Dynamic Media Classic (Scene7)，也可以将数字资源从Dynamic Media Classic (Scene7)发布到Experience Manager。

本文档介绍如何将数字资源从Experience Manager发布到Dynamic Media Classic (Scene7)，反之亦然。 还详细介绍了查看器。 有关为Dynamic Media Classic (Scene7)配置Experience Manager的信息，请参阅[将Dynamic Media Classic (Scene7)与Experience Manager集成](/help/sites-administering/scene7.md)。

另请参阅[添加图像映射](/help/assets/image-maps.md)。

有关在Experience Manager中使用视频组件的更多信息，请参阅以下内容：

* [视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>如果Dynamic Media Classic (Scene7)资源显示不正确，请确保Dynamic Media已[禁用](/help/assets/config-dynamic.md#disabling-dynamic-media)，然后刷新页面。

## 从Assets手动发布到Dynamic Media Classic (Scene7) {#manually-publishing-to-scene-from-assets}

您可以在经典UI中从Dynamic Media Classic控制台将数字资源发布到Assets (Scene7)，也可以直接从资源发布数字资源。

>[!NOTE]
>
>Experience Manager以异步方式发布到Dynamic Media Classic (Scene7)。 选择&#x200B;**[!UICONTROL Publish]**&#x200B;后，可能需要几秒钟才能将资源发布到Dynamic Media Classic (Scene7)。
>

### 从Assets控制台中发布 {#publishing-from-the-assets-console}

如果资产位于Dynamic Media Classic (Scene7)目标文件夹中，您可以从Assets控制台发布到Dynamic Media Classic (Scene7)。

1. 在Experience Manager Classic UI中，选择&#x200B;**[!UICONTROL Digital Assets]**&#x200B;以访问数字资产管理器。

1. 从目标文件夹中选择要发布到Dynamic Media Classic (Scene7)的资源（或资源）或文件夹，右键单击并选择&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**。 或者，您也可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中选择&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**。

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. 转到Dynamic Media Classic (Scene7)并确认资源可用。

   >[!NOTE]
   >
   >如果资源不在Dynamic Media Classic (Scene7)同步文件夹中，则两个菜单中的&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**&#x200B;均可见但处于禁用状态。

### 从资源访问Publish {#publishing-from-an-asset}

您可以手动发布资源，只要该资源位于已同步的Dynamic Media Classic (Scene7)文件夹内。

>[!NOTE]
>
>如果资产不在Dynamic Media Classic (Scene7)同步文件夹中，则不会显示指向&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**&#x200B;的链接。

要直接从数字资源发布到Dynamic Media Classic (Scene7)，请执行以下操作：

1. 在Experience Manager中，选择&#x200B;**[!UICONTROL 数字Assets]**&#x200B;以访问数字资产管理器。

1. 双击可打开资产。

1. 在资源详细信息窗格中，选择&#x200B;**[!UICONTROL Publish to Dynamic Media Classic (Scene7)]**。

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. 链接更改为&#x200B;**[!UICONTROL 发布……]**，然后更改为&#x200B;**[!UICONTROL 发布]**。 转到Dynamic Media Classic (Scene7)并确认资源可用。

   >[!NOTE]
   >
   >如果资产未正确发布到Dynamic Media Classic (Scene7)，则链接将更改为&#x200B;**[!UICONTROL 发布失败]**。 如果资产已发布到Dynamic Media Classic (Scene7)，则链接显示为&#x200B;**[!UICONTROL Re-Publish to Dynamic Media Classic (Scene7)]**。 重新发布允许您更改Experience Manager中的资产并重新发布它们。

### CQ目标文件夹外部的Publish资源 {#publishing-assets-from-outside-the-cq-target-folder}

Adobe建议仅从Dynamic Media Classic (Scene7)目标文件夹中的资源将资源发布到Dynamic Media Classic (Scene7)。 但是，如果必须从目标文件夹以外的文件夹上传资源，您仍然可以通过将其上传到Dynamic Media Classic (Scene7)上的按需文件夹来执行此操作。 首先，为要显示资产的页面配置云配置。 然后，将Dynamic Media Classic (Scene7)组件添加到页面中，并将资产拖放到组件上。 为该页面设置页面属性后，在选定触发器上传到Dynamic Media Classic (Scene7)时，将显示&#x200B;**[!UICONTROL Publish到Dynamic Media Classic (Scene7)]**&#x200B;链接。

>[!NOTE]
>
>按需文件夹中的Assets不会显示在Dynamic Media Classic (Scene7)内容浏览器中。

**要从CQ目标文件夹外部发布资源，请执行以下操作：**

1. 在经典UI中的Experience Manager中，选择&#x200B;**[!UICONTROL 网站]**，然后导航到要将数字资产添加到且尚未发布到Dynamic Media Classic (Scene7)的网页。 （适用普通页面继承规则。）

1. 在Sidekick中，选择&#x200B;**[!UICONTROL 页面]**&#x200B;图标，然后选择&#x200B;**[!UICONTROL 页面属性]**。

1. 选择&#x200B;**[!UICONTROL Cloud Service]**。
1. 选择&#x200B;**[!UICONTROL 添加服务]**。
1. 选择&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**。
1. 在&#x200B;**[!UICONTROL Adobe Dynamic Media Classic (Scene7)]**&#x200B;下拉列表中，选择所需的配置并选择&#x200B;**[!UICONTROL 确定]**。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 在网页上，将Dynamic Media Classic (Scene7)组件添加到页面上所需的位置。
1. 从内容查找器中，将数字资产拖动到组件。 您看到指向&#x200B;**[!UICONTROL 检查Dynamic Media Classic (Scene7)发布状态]**&#x200B;的链接。

   >[!NOTE]
   >
   >如果数字资产在CQ目标文件夹中，则不会显示指向&#x200B;**[!UICONTROL 检查Dynamic Media Classic (Scene7)发布状态]**&#x200B;的链接。 资产放置在组件中。

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. 选择&#x200B;**[!UICONTROL 检查Dynamic Media Classic (Scene7)发布状态]**。 如果资源未发布，则Experience Manager会将资源发布到Dynamic Media Classic (Scene7)。 上传资产后，即可在按需文件夹中找到该资产。 默认情况下，按需文件夹位于&#x200B;**[!UICONTROL name_of_the_company/CQ5_adhoc]**&#x200B;中。 如果需要，您可以[配置按需文件夹](#configuringtheadhocfolder)。

   >[!NOTE]
   >
   >如果资产不在Dynamic Media Classic (Scene7)同步文件夹中，并且没有与当前页面关联的Dynamic Media Classic (Scene7)云配置，则上传失败。

## Dynamic Media Classic (Scene7)组件 {#scene-components}

以下Dynamic Media Classic (Scene7)组件在Experience Manager中可用：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>默认情况下，这些组件不可用，必须在使用之前在设计模式中进行选择。

在设计模式下提供组件后，您可以将组件像任何其他Experience Manager组件一样添加到页面。 如果在同步文件夹中或在页面上，或者使用Dynamic Media Classic (Scene7)云配置，则尚未发布到Dynamic Media Classic (Scene7)的Assets将发布到Dynamic Media Classic (Scene7)。

>[!NOTE]
>
>如果您正在创建和开发自定义S7查看器并使用内容查找器，则必须显式添加`allowfullscreen`参数。

### Flash查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic (Scene7)正式终止对Flash查看器平台的支持。

### 将Dynamic Media Classic (Scene7)组件添加到页面 {#adding-a-scene-component-to-a-page}

将Dynamic Media Classic (Scene7)组件添加到页面与将组件添加到任何页面相同。 以下部分详细介绍了Dynamic Media Classic (Scene7)组件。

要将Dynamic Media Classic (Scene7)组件/查看器添加到经典UI中的页面，请执行以下操作：

1. 在Experience Manager中，打开要添加Dynamic Media Classic (Scene7)组件的页面。

1. 如果没有可用的Dynamic Media Classic (Scene7)组件，请选择Sidekick中的标尺以进入&#x200B;**设计**&#x200B;模式，选择&#x200B;**[!UICONTROL 编辑]** parsys，然后选择所有&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;组件以使其可用。

1. 通过在Sidekick中选择铅笔返回到&#x200B;**编辑**&#x200B;模式。

1. 将sidekick中&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;组中的组件拖动到所需位置的页面上。

1. 选择***[!UICONTROL 编辑]**，以便打开该组件。

1. 根据需要编辑该组件并选择&#x200B;**[!UICONTROL 确定]**&#x200B;以保存更改。

### 向响应式网站添加交互式查看体验 {#adding-interactive-viewing-experiences-to-a-responsive-website}

资产的响应式设计意味着您的资产会根据显示的位置进行调整。 通过响应式设计，可以在多个设备上有效地显示相同的资产。

要在经典UI中为响应式网站添加交互式查看体验，请执行以下操作：

1. 登录Experience Manager，并确保您已[配置Adobe Dynamic Media Classic (Scene7)Cloud Service](/help/sites-administering/scene7.md#configuring-scene-integration)，并且Dynamic Media Classic (Scene7)组件可用。

   >[!NOTE]
   >
   >如果Dynamic Media Classic (Scene7) WCM组件不可用，请确保通过设计模式启用它们。

1. 在启用了Dynamic Media Classic (Scene7)组件的网站中，将&#x200B;**[!UICONTROL Image]**&#x200B;查看器拖动到页面。
1. 在&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)设置]**&#x200B;选项卡中编辑组件并调整断点。

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. 确认查看者正在响应式地调整大小，并且所有交互都已针对桌面、平板电脑和移动设备进行了优化。

### 所有Dynamic Media Classic (Scene7)组件通用的设置 {#settings-common-to-all-scene-components}

尽管配置选项有所不同，但以下内容是所有Dynamic Media Classic (Scene7)组件共有的：

* **文件引用** — 浏览到要引用的文件。 文件引用显示资源URL，不一定是完整的Dynamic Media Classic (Scene7) URL，包括URL命令和参数。 您无法在此字段中添加Dynamic Media Classic (Scene7) URL命令和参数。 相反，必须通过组件中的相应功能添加这些变量。
* **宽度** — 允许您设置宽度。
* **高度** — 允许您设置高度。

您可以通过打开（双击）Dynamic Media Classic (Scene7)组件来设置这些配置选项，例如，在打开&#x200B;**Zoom**&#x200B;组件时：

![chlimage_1-52](assets/chlimage_1-52.png)

### 缩放 {#zoom}

按+按钮时，HTML5缩放组件显示较大的图像。

资产底部有缩放工具。 选择要放大的&#x200B;**[!UICONTROL +]**。 选择要减少的&#x200B;**[!UICONTROL -]**。 选择&#x200B;**[!UICONTROL x]**&#x200B;或重置缩放箭头可使图像恢复到导入图像的原始大小。 选择对角线箭头，以便全屏显示。 选择&#x200B;**[!UICONTROL 编辑]**，以便配置该组件。 通过此组件，您可以配置所有Dynamic Media Classic (Scene7)组件通用的[设置](#settings-common-to-all-scene-components)。

![HTML5缩放组件中的郁金香花的图像。](do-not-localize/chlimage_1-3.png)

### 弹出 {#flyout}

在HTML5弹出组件中，资源显示为分屏；左侧的资源使用指定大小；右侧的缩放部分显示。 选择&#x200B;**[!UICONTROL 编辑]**，以便配置该组件。 通过此组件，您可以配置所有Dynamic Media Classic (Scene7)组件通用的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>如果您的弹出组件使用自定义大小，则会使用该自定义大小并禁用该组件的响应式设置。
>
>如果弹出组件使用在“设计”视图中设置的缺省大小，则使用缺省大小。 组件会在启用组件的响应式设置的情况下进行扩展以适应页面布局大小。 但是，请注意，组件的响应式设置存在限制。 在响应设置中使用弹出组件时，不应将其用于全页拉伸。 否则，弹出部分可能会超出页面的右边框。

![chlimage_1-53](assets/chlimage_1-53.png)

### 图像 {#image}

Dynamic Media Classic (Scene7)图像组件允许您将Dynamic Media Classic (Scene7)功能添加到图像，例如Dynamic Media Classic (Scene7)修饰符、图像或查看器预设以及锐化。 Dynamic Media Classic (Scene7)图像组件与Experience Manager中的其他图像组件类似，具有特殊的Dynamic Media Classic (Scene7)功能。 在此示例中，图像应用了Dynamic Media Classic (Scene7) URL修饰符`&op_invert=1`。

Dynamic Media Classic (Scene 7)图像组件](do-not-localize/chlimage_1-4.png)中的球体图像![

**标题，替换文本** — 在“高级”选项卡中，为已关闭图形的用户添加标题和替换文本。

**URL，在**&#x200B;中打开 — 您可以从中设置资产以打开链接。 在的“打开”中设置URL并指示您是要在同一窗口中打开还是要在新窗口中打开。

![chlimage_1-54](assets/chlimage_1-54.png)

**查看器预设** — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 请参阅管理查看器预设。 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

**Dynamic Media Classic (Scene7)配置** — 选择要用于从SPS获取活动图像预设的Dynamic Media Classic (Scene7)配置。

**图像预设** — 从下拉菜单中选择现有的图像预设。 如果您要查找的图像预设不可见，则必须使其可见。 请参阅管理图像预设。 如果您使用的是图像预设，则无法选择查看器预设，反之亦然。

**输出格式** — 选择图像的输出格式，例如jpeg。 根据您选择的输出格式，可能还有其他配置选项。 请参阅图像预设最佳实践。

**锐化** — 选择要如何锐化图像。 图像预设最佳实践和锐化最佳实践中对锐化进行了详细解释。

**URL修饰符** — 您可以通过提供其他S7图像命令来更改图像效果。 这些命令在“图像预设”和“命令”参考中介绍。

**断点** — 如果您的网站有响应，则要调整断点。 断点必须以逗号(，)分隔。

### 图像模板 {#image-template}

Dynamic Media Classic (Scene7)图像模板是导入Dynamic Media Classic (Scene7)的分层Photoshop内容，其中内容和属性进行了参数化以实现可变性。 通过&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件，您可以导入图像并在Experience Manager中动态更改文本。 此外，您可以将&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件配置为使用来自客户端上下文的值，以便每个用户以个性化的方式体验图像。

选择&#x200B;**[!UICONTROL 编辑]** — 以配置该组件。 您可以配置所有Dynamic Media Classic (Scene7)组件通用的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)以及此部分描述的其他设置。

![chlimage_1-55](assets/chlimage_1-55.png)

**文件引用、宽度、高度** — 查看所有Dynamic Media Classic (Scene7)组件共有的[设置](/help/sites-administering/scene7.md#settingscommontoallscene7components)。

>[!NOTE]
>
>Dynamic Media Classic (Scene7) URL命令和参数无法直接添加到文件引用URL。 它们只能在&#x200B;**[!UICONTROL 参数]**&#x200B;面板的组件UI中定义。

**标题，替换文本** — 在Dynamic Media Classic (Scene7)的“图像模板”选项卡中，为已关闭图形的用户添加标题和替换文本。

**URL，在**&#x200B;中打开 — 您可以从中设置资产以打开链接。 在的“打开”中设置URL并指示您是要在同一窗口中打开还是要在新窗口中打开。

![chlimage_1-56](assets/chlimage_1-56.png)

**参数面板** — 导入图像时，使用图像中的信息预填充参数。 如果没有可动态更改的内容，则此窗口为空。

![chlimage_1-57](assets/chlimage_1-57.png)

#### 动态更改文本 {#changing-text-dynamically}

若要动态更改文本，请在字段中输入新文本并选择&#x200B;**[!UICONTROL 确定]**。 在此示例中，**价格**&#x200B;现在为$50，运费为99美分。

![chlimage_1-58](assets/chlimage_1-58.png)

图像中的文本会更改。 通过选择字段旁边的&#x200B;**[!UICONTROL 重置]**，可以将文本重置回原始值。

![chlimage_1-59](assets/chlimage_1-59.png)

#### 更改文本以反映客户端上下文值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要将字段链接到客户端上下文值，请选择&#x200B;**[!UICONTROL 选择]**&#x200B;以打开客户端上下文菜单，选择客户端上下文，然后选择&#x200B;**[!UICONTROL 确定]**。 在此示例中，根据将名称与配置文件中的格式化名称之间的链接，名称会发生更改。

![chlimage_1-60](assets/chlimage_1-60.png)

该文本反映当前登录用户的名称。 通过选择字段旁边的&#x200B;**[!UICONTROL 重置]**，可以将文本重置回原始值。

![chlimage_1-61](assets/chlimage_1-61.png)

#### 将Dynamic Media Classic (Scene7)图像模板设为链接 {#making-the-scene-image-template-a-link}

您可以将Dynamic Media Classic (Scene7)图像模板组件设为一个可单击的链接。

1. 在包含Dynamic Media Classic (Scene7)图像模板组件的页面上，选择&#x200B;**[!UICONTROL 编辑]**。
1. 在&#x200B;**[!UICONTROL URL]**&#x200B;字段中，输入用户在单击图像时转到的URL。 在&#x200B;**[!UICONTROL 在]**&#x200B;中打开字段中，选择要打开目标（新窗口还是同一窗口）。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 选择&#x200B;**[!UICONTROL 确定]**。

### 视频组件 {#video-component}

Dynamic Media Classic (Scene7) **[!UICONTROL Video]**&#x200B;组件(可从Sidekick的Dynamic Media Classic (Scene7)部分获得)使用设备和带宽检测将正确的视频提供给每个屏幕。 此组件是一个HTML5视频播放器；它是一个可用于跨渠道的单个查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

有关视频如何与Dynamic Media Classic (Scene7)集成结合使用的更多信息，请参阅[视频](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)。 此外，请查看[Dynamic Media Classic (Scene7) video **组件与foundation** video **组件](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)的比较。**

![chlimage_1-63](assets/chlimage_1-63.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM会显示是否上传了主源视频。 它们不显示这些代理资源：

* Dynamic Media Classic (Scene7)编码呈现版本
* Dynamic Media Classic (Scene7)自适应视频集

在将自适应视频集与Dynamic Media Classic (Scene7)视频组件结合使用时，必须调整组件大小以适合视频的尺寸。

## Dynamic Media Classic (Scene7)内容浏览器 {#scene-content-browser}

Dynamic Media Classic (Scene7)内容浏览器允许您直接在Experience Manager中查看Dynamic Media Classic (Scene7)中的内容。 要访问内容浏览器，请在内容查找器中，选择触控优化用户界面中的&#x200B;**Dynamic Media Classic (Scene7)**&#x200B;或传统用户界面中的&#x200B;**S7**&#x200B;图标。 两个用户界面之间的功能相同。

如果您有多个配置，默认情况下Experience Manager会显示[默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration)。 您可以直接在Dynamic Media Classic (Scene7)内容浏览器的下拉菜单中选择其他配置。

>[!NOTE]
>
>* 按需文件夹中的Assets不会出现在Dynamic Media Classic (Scene7)内容浏览器中。
>* 启用[安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)后，Dynamic Media Classic (Scene7)上已发布和未发布的资源都会显示在Dynamic Media Classic (Scene7)内容浏览器中。
>* 如果您在内容浏览器中未看到&#x200B;**[!UICONTROL Dynamic Media Classic (Scene7)]**&#x200B;或&#x200B;**[!UICONTROL S7]**&#x200B;图标，则必须[配置Dynamic Media Classic (Scene7)以使用Experience Manager](/help/sites-administering/scene7.md)。
>* 对于视频，Dynamic Media Classic (Scene7)内容浏览器支持：
>   * 自适应视频集：包含跨多个屏幕无缝播放所需的所有视频演绎版的容器
>   * 单个MP4视频
>   * 单个F4V视频

### 浏览内容 {#browsing-content-in-the-classic-ui}

通过选择&#x200B;**[!UICONTROL S7]**&#x200B;选项卡，浏览Dynamic Media Classic (Scene7)中的内容。

您可以通过选择配置来更改正在访问的配置。 文件夹会根据所选配置而发生更改。

![chlimage_1-64](assets/chlimage_1-64.png)

与Assets的内容查找器一样，您可以搜索资源和筛选结果。 但是，与Assets查找器不同，在&#x200B;**S7**&#x200B;选项卡中输入关键字时，文件名&#x200B;**以您输入的字符串**&#x200B;开头，而不是&#x200B;**在文件名中包含**&#x200B;关键字。

默认情况下，资源按文件名显示。 但是，您还可以按资源类型筛选结果。

>[!NOTE]
>
>对于视频，WCM的Dynamic Media Classic (Scene7)内容浏览器支持：
>
>* 自适应视频集：包含跨多个屏幕无缝播放所需的所有视频演绎版的容器
>* 单个MP4视频
>* 单个F4V视频
>

### 使用内容浏览器搜索Dynamic Media Classic (Scene7)资源 {#searching-for-scene-assets-with-the-content-browser}

搜索Dynamic Media Classic (Scene7)资源与搜索Experience Manager资源类似。 唯一例外是，当您搜索时，您实际上会看到Dynamic Media Classic (Scene7)系统中资源的远程视图，而不是直接将其导入Experience Manager。

您可以使用经典UI或触屏优化UI来查看和搜索资产。 根据界面，您的搜索方式会略有不同。

在任一UI中搜索时，您可以按以下条件进行筛选（如触屏优化UI中所示）：

**输入关键字** — 您可以按名称搜索资源。 在搜索关键字时，您输入的是文件名以开头的。 例如，键入“swimming”将查找任何以相应顺序的字母开头的资产文件名。 键入搜索词以查找资产后，请确保选择`Enter`。

![chlimage_1-65](assets/chlimage_1-65.png)

**文件夹/路径** — 文件夹的名称基于您选择的配置。 通过选择文件夹图标并选择子文件夹，然后选择复选标记以将其选中，您可以向下钻取到更低级别。

如果输入关键字并选择文件夹，则Experience Manager将搜索该文件夹及其所有子文件夹。 但是，如果在搜索时未输入任何关键字，则选择该文件夹只会显示该文件夹中的资源，不包括任何子文件夹。

默认情况下，Experience Manager会搜索选定的文件夹和所有子文件夹。

![chlimage_1-66](assets/chlimage_1-66.png)

**资源类型** — 选择Dynamic Media Classic (Scene7)以浏览Dynamic Media Classic (Scene7)内容。 此选项仅在配置Dynamic Media Classic (Scene7)后可用。

![chlimage_1-67](assets/chlimage_1-67.png)

**配置** — 如果您在Cloud Service中定义了多个Dynamic Media Classic (Scene7)配置，则可以在此处选择它。 因此，文件夹会根据您选择的配置进行更改。

![chlimage_1-68](assets/chlimage_1-68.png)

**资源类型** — 在Dynamic Media Classic (Scene7)浏览器中，您可以筛选结果以包含以下任一项：图像、模板、视频和自适应视频集。 如果不选择任何资源类型，默认情况下，Experience Manager将搜索所有资源类型。

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* 在经典UI中，您还可以搜索&#x200B;**Flash**&#x200B;和&#x200B;**FXG**。 不支持在触屏优化UI中过滤这两个术语。
>
>* 搜索视频时，您将搜索单个演绎版。 结果返回原始演绎版（仅&#42;.mp4）和编码的演绎版。
* 搜索自适应视频集时，您将搜索文件夹及其所有子文件夹，但前提是已向搜索添加了关键词。 如果尚未添加关键字，则Experience Manager不会搜索子文件夹。
>

**Publish状态** — 您可以根据发布状态筛选资源：已取消发布或已发布。 如果您未选择任何Publish状态，默认情况下，Experience Manager将搜索所有发布状态。

![chlimage_1-70](assets/chlimage_1-70.png)
