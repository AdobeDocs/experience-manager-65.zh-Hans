---
title: 将Dynamic Media Assets添加到页面
description: 如何在Adobe Experience Manager中将Dynamic Media组件添加到页面。
uuid: b5e982f5-fa1c-478a-bcb3-a1ef980df201
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 97a5f018-8255-4b87-9d21-4a0fdf740e4d
docset: aem65
role: User, Admin
exl-id: 62d4a38c-2873-4560-8d58-ad172288764d
feature: Components,Publishing
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '3258'
ht-degree: 21%

---

# 将 Dynamic Media 资源添加到页面{#adding-dynamic-media-assets-to-pages}

要将Dynamic Media功能添加到您在网站上使用的资产中，您可以直接在页面上添加 **Dynamic Media**、 **Interactive Media**、 **Media**&#x200B;或 **** Video 360 Media全景组件。 可通过进入布局模式并启用Dynamic Media组件来添加组件。 然后，您可以将这些组件添加到页面，并将资产添加到该组件。 Dynamic media组件是智能的——它们知道您添加的是图像还是视频，可用的配置选项会相应地发生更改。

如果您使用Dynamic Media作为WCM，则可以直接将Adobe Experience Manager资产添加到页面。 如果您为WCM使用第三方，则 [链接](/help/assets/linking-urls-to-yourwebapplication.md) 或 [嵌入](/help/assets/embed-code.md) 您的资产。 有关响应式第三方网站，请参阅[将优化的图像交付到响应式网站](/help/assets/responsive-site.md)。

>[!NOTE]
>
>在将资产添加到Experience Manager的页面之前，请确保先发布资产。 请参阅 [发布Dynamic Media资产](/help/assets/publishing-dynamicmedia-assets.md).

## 将Dynamic Media组件添加到页面 {#adding-a-dynamic-media-component-to-a-page}

向页面添加3D媒体、Dynamic Media、交互式媒体、全景媒体、智能裁剪视频或视频360媒体组件与向任何页面添加组件相同。 以下部分介绍了Dynamic Media组件。

**要将Dynamic Media组件添加到页面，请执行以下操作：**

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 在页面左侧的面板中（如有必要，可切换侧面板的显示），选择 **[!UICONTROL 组件]** 图标。
1. 在 **[!UICONTROL 组件]** 标题，在下拉列表中，选择 **[!UICONTROL Dynamic Media]**.

   如果没有可用的Dynamic Media组件列表，则必须启用要使用的Dynamic Media组件。 请参阅 [启用Dynamic Media组件](#enabling-dynamic-media-components).

   ![6_5_360video_wcmcomponent](/help/assets/assets/6_5_360video_wcmcomponent.png)

1. 拖动 **[!UICONTROL Dynamic Media]** 组件，并将其拖放到页面上的所需位置。

1. 将鼠标指针直接悬停在组件上。 当组件被蓝色框包围时，选择一次以显示组件的工具栏。 选择 **[!UICONTROL 配置（扳手）]** 图标。

   ![6_5_360video_wcmcomponentconfigure](/help/assets/assets/6_5_360video_wcmcomponentconfigure.png)

1. 根据您拖放到页面上的Dynamic Media组件，将打开一个配置对话框。 [设置组件的选项](/help/assets/adding-dynamic-media-assets-to-pages.md#dynamic-media-components) 视需要。

   以下示例显示了Dynamic Media **[!UICONTROL 视频360媒体]** 组件对话框中，以及“查看器预设”下拉列表中可用的选项。

   ![视频360媒体组件](assets/6_5_360video_wcmcomponentviewerpreset.png)

   Dynamic Media视频360媒体组件。

1. 完成后，在对话框的右上角，选择复选标记以保存更改。

### 启用Dynamic Media组件 {#enabling-dynamic-media-components}

如果没有可添加到页面的Dynamic Media组件，则可能意味着您必须首先启用要使用的组件。

**要启用Dynamic Media组件，请执行以下操作：**

1. 在Experience Manager中，打开要添加Dynamic Media组件的页面。
1. 在工具栏左侧靠近页面顶部的位置，选择页面信息图标，然后选择 **[!UICONTROL 编辑模板]** 从下拉列表中。

   ![edit-template](/help/assets/assets-dm/edit-template.png)

1. 在工具栏右侧页面顶部附近的下拉列表中，选择 **[!UICONTROL 结构]**.

   ![策略](/help/assets/assets-dm/structure-mode.png)

1. 在页面底部附近，选择 **[!UICONTROL 布局容器]** 要打开其工具栏，请选择策略图标。
1. 在 **[!UICONTROL 布局容器]** 页面下 **[!UICONTROL 属性]** 标题，确保 **[!UICONTROL 允许的组件]** 选项卡。

   ![允许的组件](/help/assets/assets-dm/allowed-components.png)

1. 滚动直到您看到 **[!UICONTROL Dynamic Media]**.
1. 选择左侧的>图标 **[!UICONTROL Dynamic Media]** 以展开列表，然后选择要启用的Dynamic Media组件。

   ![Dynamic Media组件列表](/help/assets/assets-dm/dm-components-select.png)

1. 在 **[!UICONTROL 布局容器]** ，选择完成（复选标记）图标。

1. 在工具栏右侧页面顶部附近的下拉列表中，选择 **[!UICONTROL 初始内容]**，则 [将Dynamic Media组件添加到页面](#adding-a-dynamic-media-component-to-a-page) 和往常一样。

## 将Dynamic Media组件本地化 {#localizing-dynamic-media-components}

您可以通过以下两种方式之一将Dynamic Media组件本地化：

* 在“站点”的网页中，打开“属 **[!UICONTROL 性]** ”，然后选择“ **[!UICONTROL 高级]** ”选项卡。 选择所需的本地化语言。

   ![chlimage_1-172](assets/chlimage_1-538.png)

* 从站点选择器中，选择所需的页面或页面群组。 选择 **[!UICONTROL 属性]** ，然后选择 **[!UICONTROL 高级]** 选项卡。 选择所需的本地化语言。

   >[!NOTE]
   >
   >请注意，并非所有语言都在 **[!UICONTROL 语言]** 菜单当前已分配令牌。

## Dynamic Media 组件 {#dynamic-media-components}

当您选择 **[!UICONTROL 组件]** 图标，然后进行筛选 **[!UICONTROL Dynamic Media]**.

可用的Dynamic Media组件包括：

* **[!UICONTROL Dynamic Media]** - 用于图像、视频、电子目录和旋转集等资产。
* **[!UICONTROL 交互式媒体]**  — 用于任何交互式资产，如交互式视频、交互式图像或轮播集。
* **[!UICONTROL 全景媒体]**  — 用于全景图像或全景VR图像资产。
* **[!UICONTROL 视频360媒体]**  — 用于360个视频和360个VR视频资产。

>[!NOTE]
>
>默认情况下，这些组件不可用；在使用模板编辑器之前，必须先通过模板编辑器使用这些模板。 [在它们可用后，](/help/sites-authoring/templates.md#editing-templates-template-authors)在模板编辑器中，您可以像向任何其他Experience Manager组件添加组件一样，将组件添加到页面。

![6_5_dynamicmediawcmcomponents](assets/6_5_dynamicmediawcmcomponents.png)

### Dynamic Media 组件 {#dynamic-media-component}

Dynamic Media组件是智能的。无论您是添加图像还是视频，都有各种不同的选项。 该组件支持图像预设、基于图像的查看器（例如图像集、旋转集、混合媒体集）和视频。此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

>[!NOTE]
>
>如果您的网页具有以下功能：
>
>* 同一页面上使用的Dynamic Media组件的多个实例。
>* 每个实例使用相同的资产类型。

>
>不支持为该页面上的每个Dynamic Media组件分配不同的查看器预设。
>
>但是，您可以对页面中使用相同类型资产的所有Dynamic Media组件使用相同的查看器预设。

添加 Dynamic Media 组件时，如果 **[!UICONTROL Dynamic Media 设置]**&#x200B;为空或无法正常添加资产，请检查以下各项：

* 您已经[启用了 Dynamic Media](/help/assets/config-dynamic.md)。默认情况下，Dynamic Media 处于禁用状态。
* 图像具有金字塔 TIFF 文件。在启用Dynamic Media之前导入的图像没有金字塔tiff文件。

#### 处理图像时 {#when-working-with-images}

Dynamic Media 组件允许您添加动态图像，包括图像集、旋转集和混合媒体集。您可以缩放图像，并在适当的情况下在旋转集内旋转图像，或从其他类型的集合中选择图像。

您还可以直接在组件中配置查看器预设、图像预设或图像格式。要使图像具有响应性，您可以设置断点或应用响应式图像预设。

通过选择 **[!UICONTROL 编辑]** 图标，然后 **[!UICONTROL Dynamic Media设置]**.

![dm-settings-image-preset](assets/dm-settings-image-preset.png)

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

   当您查看图像集、旋转集或混合媒体集时，此选项是唯一可用的选项。 显示的查看器预设是智能的 — 仅显示相关的查看器预设。

* **[!UICONTROL 查看器修饰符]**  — 查看器修饰符采用名称=值对和分隔符的形式，允许您按照《查看器参考指南》中所述更改查看器。 查看器修饰符的示例为 `posterimage=img.jpg&caption=text.vtt,1` 为视频缩略图设置不同的图像，并将隐藏式字幕/子标题文件与视频相关联。

* **[!UICONTROL 图像预设]**  — 从下拉菜单中选择现有的图像预设。 如果您要查找的图像预设不可见，则必须使其可见。 请参阅管理图像预设。如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 图像修饰符]**  — 您可以通过提供其他图像命令来应用图像效果。 图像预设和图像提供命令参考中介绍了这些效果。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 断点]**  — 如果您在响应式网站上使用此资产，则必须添加图像断点。 图像断点之间用逗号分隔(,)。 当图像预设中未定义高度或宽度时，可以使用此选项。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

   您可以通过选择 **[!UICONTROL 编辑]** 中。

* **[!UICONTROL 优化分辨率更高的设备]**  — 选中（默认）复选框以允许DPR（设备像素比）优化。

   的 **[!UICONTROL 优化分辨率更高的设备]** 选项仅在以下情况下才显示：

   * 在“预设类型”下， **[!UICONTROL 图像预设]** ，并且 **[!UICONTROL RESS_IP]** 从 **[!UICONTROL 图像预设]** 下拉列表。

   ![图像预设中的设备像素比率设置](/help/assets/assets-dm/dpr-ress-ip.png)

   另请参阅 [关于设备像素比例优化](/help/assets/imaging-faq.md#dpr). 任何Adobe Experience Manager Dynamic Media智能成像DPR值都将被忽略。

* **[!UICONTROL 标题]**  — 更改图像的标题。

* **[!UICONTROL 替换文本]**  — 为已关闭图形的用户在图像中添加标题。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL URL，在中打开]**  — 您可以设置资产以打开链接。 设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 宽度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

* **[!UICONTROL 高度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

#### 处理视频时 {#when-working-with-video}

使用Dynamic Media组件将动态视频添加到您的网页。 编辑组件时，您可以选择使用预定义的视频查看器预设来在页面上播放视频。

![chlimage_1-173](assets/chlimage_1-540.png)

通过选择 **[!UICONTROL 编辑]** 中。

>[!NOTE]
>
>默认情况下，Dynamic Media 视频组件为自适应组件。如果要使其变为固定大小，请在组件中使用 **[!UICONTROL 宽度]** 和 **[!UICONTROL 高度]** 在 **[!UICONTROL 高级]** 选项卡。

* **[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的视频查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md).

* **[!UICONTROL 查看器修饰符]**  — 查看器修饰符采用名称=值对和分隔符的形式，允许您按照《Adobe查看器参考指南》中所述更改查看器。 查看器修饰符的示例为 `posterimage=img.jpg&caption=text.vtt,1`

   例如，通过查看器修饰符，您可以执行以下操作：

   * 将字幕文件与视频关联： [字幕][https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-caption.html)
   * 将导航文件与视频关联： [导航][https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/command-reference-url-video/r-html5-video-viewer-url-navigation.html)

      您可以通过选择 **[!UICONTROL 编辑]** 中。

* **[!UICONTROL 标题]**  — 更改视频的标题。

* **[!UICONTROL 宽度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

* **[!UICONTROL 高度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

#### 使用智能裁剪时 {#when-working-with-smart-crop}

使用Dynamic Media组件将智能裁剪图像资产添加到您的网页。 编辑组件时，您可以选择使用预定义的视频查看器预设来在页面上播放视频。

另请参阅 [图像配置文件](/help/assets/image-profiles.md).

![dm-settings-smart-crop](assets/dm-settings-smart-crop.png)

通过选择 **[!UICONTROL 编辑]** 中。

>[!NOTE]
>
>默认情况下，Dynamic media图像组件是自适应的。 如果要使其变为固定大小，请在“高级”选项卡的组件中设置 **[!UICONTROL 它]** ，并使用“宽度”和“高 **** 度” ****。

* **[!UICONTROL 图像修饰符]**  — 您可以通过提供其他图像命令来应用图像效果。 图像预设和图像提供命令参考中介绍了这些效果。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

   您可以通过选择 **[!UICONTROL 编辑]** 中。

* **[!UICONTROL 启用宽高比匹配]**  — 要让Dynamic Media选取宽高比与原始图像的宽高比最匹配的智能裁剪呈现，请选择此选项。

* **[!UICONTROL 优化分辨率更高的设备]**  — 选中（默认）复选框以允许DPR（设备像素比）优化。

   的 **[!UICONTROL 优化分辨率更高的设备]** 选项仅在以下情况下才显示：

   * 在“预设类型”下， **[!UICONTROL 智能裁剪]** 选项。

   ![用于智能裁剪的设备像素比设置](/help/assets/assets-dm/dpr-smartcrop.png)

   另请参阅 [关于设备像素比例优化](/help/assets/imaging-faq.md#dpr). 任何Adobe Experience Manager Dynamic Media智能成像DPR值都将被忽略。

* **[!UICONTROL 标题]**  — 更改智能裁剪图像的标题。

* **[!UICONTROL 替换文本]**  — 为关闭了图形的用户添加智能裁剪图像的标题。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL URL，在中打开]**  — 您可以设置资产以打开链接。 设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

   如果您查看的是图像集、旋转集或混合媒体集，则此选项不可用。

* **[!UICONTROL 宽度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

* **[!UICONTROL 高度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

### 交互式媒体组件 {#interactive-media-component}

交互式媒体组件适用于具有交互功能的资产，例如热点或图像映射。如果您具有交互式图像、交互式视频或传送横幅，请使用&#x200B;**[!UICONTROL 交互式媒体]**&#x200B;组件。

交互式媒体组件是智能的。无论您是添加图像还是视频，都有各种不同的选项。 此外，查看器是响应式的 — 屏幕大小会根据屏幕大小自动更改。 所有查看器都是 HTML5 查看器。

>[!NOTE]
>
>如果您的网页具有以下功能：
>
>* 在同一页面上使用的交互式媒体组件的多个实例。
>* 每个实例使用相同的资产类型。

>
>不支持为该页面上的每个交互式媒体组件分配不同的查看器预设。
>
>但是，您可以在页面中为使用相同类型资产的所有交互式媒体组件使用相同的查看器预设。

![chlimage_1-174](assets/chlimage_1-541.png)

您可以编辑以下内容 **[!UICONTROL 常规]** 设置 **[!UICONTROL 编辑]** 中。

* **[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 查看器预设必须先发布，然后才能使用。请参阅管理查看器预设。

* **[!UICONTROL 标题]**  — 更改视频的标题。

* **[!UICONTROL 宽度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

* **[!UICONTROL 高度]**  — 如果希望图像具有固定大小，请输入值（以像素为单位）。 将此值留空会使资产具有自适应性。

   您可以编辑以下内容 **[!UICONTROL 添加到购物车]** 设置 **[!UICONTROL 编辑]** 中。

* **[!UICONTROL 显示产品资产]**  — 默认情况下，此值处于选中状态。 产品资产会按“商务”模块中的定义显示产品的图像。清除复选标记不会显示产品资产。

* **[!UICONTROL 显示产品价格]**  — 默认情况下，此值处于选中状态。 产品价格会按“商务”模块中的定义显示项目的价格。清除复选标记不会显示产品价格。

* **[!UICONTROL 显示产品表单]**  — 默认情况下，未选择此值。 产品表单包含所有产品变量，例如大小和颜色。清除复选标记不会显示产品变量。

### 全景媒体组件 {#panoramic-media-component}

全景媒体组件适用于那些球面全景图像的资产。 此类图像可提供360°的房间、属性、位置或景观观看体验。 要使图像符合球面全景，它必须具有以下任一或两者：

* 宽高比为2:1。
* 使用关键词标记 `equirectangular` 或(`spherical` + `panorama`)或(`spherical` + `panoramic`)。 请参阅 [使用标记](/help/sites-authoring/tags.md).

纵横比和关键字条件都适用于资产详细信息页面和&#x200B;**[!UICONTROL 全景媒体]** WCM 组件的全景资产。

>[!NOTE]
>
>如果您的网页具有以下功能：
>
>* 的多个实例 **[!UICONTROL 全景媒体]** 组件。
>* 每个实例使用相同的资产类型。

>
>为每个查看器预设分配不同的查看器预设 **[!UICONTROL 全景媒体]** 不支持该页面上的组件。
>
>但是，您可以在页面中对使用相同类型资产的所有全景媒体组件使用相同的查看器预设。

![panoramic-media-viewer-preset](assets/panoramic-media-viewer-preset.png)

您可以通过选择 **[!UICONTROL 配置]** 中。

* **[!UICONTROL 查看器预设]**  — 从“查看器预设”下拉菜单中选择一个现有的查看器。

如果您要查找的查看器预设不可见，请勾选以确保该查看器预设已发布。 在使用查看器预设之前，先发布查看器预设。 请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

### 视频360媒体组件 {#video-media-component}

使用 **[!UICONTROL 视频360媒体]** 组件，用于在网页上呈现等矩形视频，以体验房间、属性、位置、景观或医疗过程的沉浸式查看体验。

在平面显示器上播放时，用户可以控制观看角度；移动设备上的播放通常使用其内置的陀螺仪控件。

查看器包含对交付360个视频资产的本机支持。 默认情况下，查看或播放不需要任何其他配置。 您使用标准视频扩展名(如.mp4、.mkv和.mov)来交付360视频。 最常见的编解码器是H.264。

![6_5_360video_wcmcomponent-1](assets/6_5_360video_wcmcomponent-1.png)

您可以通过选择 **[!UICONTROL 配置]** 中。

* **[!UICONTROL 查看器预设]**  — 从“查看器预设”下拉菜单中选择一个现有的查看器。 使用Video360VR的最终用户使用虚拟现实眼镜。 包括基本的视频播放控件和社交媒体功能。 使用Video360_social，其中包含基本的视频播放控件。 视频渲染在立体声模式下完成。 手动视点控制关闭，但陀螺仪控制打开。 没有社交媒体功能。

如果您要查找的查看器预设不可见，请勾选以确保该查看器预设已发布。 请确保在使用查看器预设之前先发布查看器预设。 请参阅[管理查看器预设](/help/assets/managing-viewer-presets.md)。

### 使用HTTP/2交付Dynamic Media资产 {#using-http-to-delivery-dynamic-media-assets}

HTTP/2是经过更新的新Web协议，可改进浏览器和服务器的通信方式。 它提供了更快的信息传输，并降低了所需的处理能力。 现在，Dynamic Media资产的交付可以通过HTTP/2进行，从而提供更好的响应和加载时间。

请参阅 [HTTP2内容交付](/help/assets/http2.md) 有关开始使用HTTP/2与您的Dynamic Media帐户的完整详细信息。

>[!MORELIKETHIS]
>
>* [在Experience ManagerDynamic Media中使用视频播放器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-player-feature-video-use.html)
>* [将交互式视频与Experience ManagerDynamic Media结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-interactive-video-feature-video-use.html)
>* [了解具有Experience ManagerDynamic Media的资产查看器](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-viewer-feature-video-understand.html)
>* [将自定义视频缩略图与Experience ManagerDynamic Media结合使用](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-video-thumbnails-feature-video-use.html)
>* [了解使用Experience ManagerDynamic Media的色彩管理](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-color-management-technical-video-setup.html)
>* [在Experience ManagerDynamic Media中使用图像锐化](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-image-sharpening-feature-video-use.html)

