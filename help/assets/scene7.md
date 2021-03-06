---
title: 将Dynamic Media Classic功能添加到页面
description: 如何在Adobe Experience Manager中将Dynamic Media Classic功能和组件添加到页面。
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: d947bd98b3a0f6fd79cde5b5b2fca23487077da3
workflow-type: tm+mt
source-wordcount: '2845'
ht-degree: 15%

---

# 将Dynamic Media Classic功能添加到页面 {#adding-scene-features-to-your-page}

[Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) 是一个托管解决方案，用于管理、增强、发布富媒体资产并将其交付到Web、移动设备、电子邮件以及连接Internet的显示屏和打印。

您可以在各种查看器中查看在Dynamic Media Classic中发布的Experience Manager资产：

* 缩放
* 弹出
* 视频
* 图像模板
* 图像

您可以将数字资产从Experience Manager直接发布到Dynamic Media Classic，也可以将数字资产从Dynamic Media Classic发布到Experience Manager。

本文档介绍如何将数字资产从Experience Manager发布到Dynamic Media Classic，反之则介绍。 此外，还详细介绍了各种查看器。有关为Dynamic Media Classic配置Experience Manager的信息，请参阅 [将Dynamic Media Classic与Experience Manager集成](/help/sites-administering/scene7.md).

另请参阅 [添加图像映射](image-maps.md).

有关将视频组件与Experience Manager结合使用的更多信息，请参阅 [视频](video.md).

>[!NOTE]
>
>如果Dynamic Media Classic资产显示不正确，请确保Dynamic Media [已禁用](config-dynamic.md#disabling-dynamic-media) 然后刷新页面。

## 从资产手动发布到Dynamic Media Classic {#manually-publishing-to-scene-from-assets}

您可以按如下方式将数字资产发布到Dynamic Media Classic:

* [在Assets控制台的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [在资产的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [在CQ Target文件夹外部的经典用户界面中](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>Experience Manager会异步发布到Dynamic Media Classic。 在选择 **[!UICONTROL 发布]**，则您的资产需要几秒钟才能发布到Dynamic Media Classic。

## Dynamic Media Classic组件 {#scene-components}

Experience Manager中提供了以下Dynamic Media Classic组件：

* 缩放
* 弹出（缩放）
* 图像模板
* 图像
* 视频

>[!NOTE]
>
>默认情况下，这些组件不可用，必须在 **[!UICONTROL 设计]** 模式。

在 **[!UICONTROL 设计]** 模式下，您可以像向页面添加任何其他Experience Manager组件一样，将组件添加到页面。 如果资产位于同步文件夹、页面或具有Dynamic Media Classic云配置，则尚未发布到Dynamic Media Classic的资产会发布到Dynamic Media Classic。

>[!NOTE]
>
>如果要创建和开发自定义查看器以及使用内容查找器，则必须明确地添加 `allowfullscreen` 参数。

### Flash 查看器生命周期终止通知 {#flash-viewers-end-of-life-notice}

自2017年1月31日起，Adobe Dynamic Media Classic停止支持Flash查看器平台。

### 将Dynamic Media Classic(Scene7)组件添加到页面 {#adding-a-scene-component-to-a-page}

向页面添加Dynamic Media Classic(Scene7)组件与向任何页面添加组件相同。 以下各节详细介绍了Dynamic Media Classic组件。

**要将Dynamic Media Classic(Scene7)组件添加到页面，请执行以下操作：**

1. 在Experience Manager中，打开要在其中添加 **[!UICONTROL Dynamic Media Classic(Scene7)]** 组件。

1. 如果没有可用的Dynamic Media Classic组件，请选择 **[!UICONTROL 设计]** 模式下，选择任何具有蓝色边框的组件，然后选择 **[!UICONTROL 父项]** 图标，然后 **[!UICONTROL 配置]** 图标。 在 **[!UICONTROL Parsys（设计）]**，选择所有Dynamic Media Classic组件以使其可用，然后选择 **[!UICONTROL 确定]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. 选择 **[!UICONTROL 编辑]** 这样，您可以 **[!UICONTROL 编辑]** 模式。

1. 将组件从Sidekick中的Dynamic Media Classic组拖动到页面上所需位置。

1. 选择 **[!UICONTROL 配置]** 图标，以便打开组件。

1. 根据需要编辑组件，然后选择 **[!UICONTROL 确定]** 保存更改。
1. 将图像或视频从内容浏览器拖动到您添加到页面的Dynamic Media Classic组件上。

   >[!NOTE]
   >
   >仅在触屏UI中，必须将图像或视频拖放到您放置在页面上的Dynamic Media Classic组件上。 不支持先选择和编辑Dynamic Media Classic组件，然后再选择资产。

### 向响应式网站添加交互式查看体验 {#adding-interactive-viewing-experiences-to-a-responsive-website}

资产的响应式设计意味着资产会根据资产的显示位置自行调整。 利用响应式设计，可以在多种设备上有效地显示同一资产。

另请参阅 [网页响应式设计](/help/sites-developing/responsive.md).

**要向响应式网站添加交互式查看体验，请执行以下操作：**

1. 登录Experience Manager，并确保您 [已配置Adobe Dynamic Media ClassicCloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) 以及Dynamic Media Classic组件的可用性。

   >[!NOTE]
   >
   >如果Dynamic Media Classic组件不可用，请确保 [以通过设计模式启用它们](/help/sites-authoring/default-components-designmode.md).

1. 在具有 **[!UICONTROL Dynamic Media Classic]** 组件，拖动 **[!UICONTROL 图像]** 组件。
1. 选择组件，然后选择配置图标。
1. 在 **[!UICONTROL Dynamic Media Classic设置]** 选项卡来调整断点。

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. 确认查看器可实现响应式大小调整，并且所有交互已针对台式机、平板电脑和移动设备进行了优化。

### 所有Dynamic Media Classic组件通用的设置 {#settings-common-to-all-scene-components}

尽管配置选项各不相同，但以下各项对所有人都是通用的 [!UICONTROL Dynamic Media Classic] 组件：

* **[!UICONTROL 文件引用]** - 浏览到要引用的文件。文件引用会显示资产URL，但不一定是完整的Dynamic Media Classic URL（包括URL命令和参数）。 您无法在此字段中添加Dynamic Media Classic URL命令和参数。 而是通过组件中的相应功能添加它们。
* **[!UICONTROL 宽度]** - 允许您设置宽度。
* **[!UICONTROL 高度]** - 允许您设置高度。

通过打开（双击）Dynamic Media Classic组件(例如，在您打开 **[!UICONTROL 缩放]** 组件：

![chlimage_1-226](assets/chlimage_1-226.png)

### 缩放 {#zoom}

HTML5缩放组件会在您按 **[!UICONTROL +]** 按钮。

缩放工具位于资产底部。选择 **[!UICONTROL +]** 想扩大的；选择 **[!UICONTROL -]** 如果你想减少的话。 点按 **[!UICONTROL x]** 或者，使用重置缩放箭头可将图像恢复为导入时的原始大小。 选择对角线箭头，使其全屏显示。 选择 **[!UICONTROL 编辑]** 以便配置组件。 通过此组件，您可以配置 [所有通用设置 [!UICONTROL Dynamic Media Classic] 组件](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### 弹出 {#flyout}

在HTML5 **[!UICONTROL 弹出]** ，则资产会显示为分屏；将资产保留在指定的大小；右侧将显示缩放部分。 选择 **[!UICONTROL 编辑]** 以便配置组件。 通过此组件，您可以配置 [所有Dynamic Media Classic组件通用的设置](#settings-common-to-all-scene-components).

>[!NOTE]
>
>如果 **[!UICONTROL 弹出]** 组件使用自定义大小，然后使用该自定义大小并禁用组件的响应设置。
>
>如果 **[!UICONTROL 弹出]** 组件使用默认大小，如 **[!UICONTROL 设计视图]**，则会使用默认大小，组件会延伸以在启用组件响应设置的情况下适应页面布局大小。 组件的响应设置存在限制。 当您使用 **[!UICONTROL 弹出]** 组件进行响应式设置时，请勿将其用于整个页面拉伸。 否则， **[!UICONTROL 弹出]** 超出页面的右边框。

![chlimage_1-228](assets/chlimage_1-228.png)

### 图像 {#image}

Dynamic Media Classic **[!UICONTROL 图像]** 组件允许您在图像中添加Dynamic Media Classic功能，如Dynamic Media Classic修饰符、图像或查看器预设以及锐化。 Dynamic Media Classic **[!UICONTROL 图像]** 组件与Experience Manager中具有特殊Dynamic Media Classic功能的其他图像组件类似。 在此示例中，图像具有Dynamic Media Classic URL修饰符， `&op_invert=1` 应用。

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL 标题，替换文本]**  — 在 **[!UICONTROL 高级]** 选项卡上，为图像添加标题，并为关闭了图形的用户添加替换文本。

**[!UICONTROL URL，在中打开]**  — 您可以设置资产来打开链接。 设置 **[!UICONTROL URL]**，并在&#x200B;**[!UICONTROL 打开方式]**&#x200B;中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL 查看器预设]**  — 从下拉菜单中选择现有的查看器预设。 如果您要查找的查看器预设不可见，则必须使其可见。 请参阅 [管理查看器预设](/help/assets/managing-viewer-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

**[!UICONTROL Dynamic Media Classic配置]**  — 选择要从SPS中获取活动图像预设的Dynamic Media Classic配置。

**[!UICONTROL 图像预设]**  — 从下拉菜单中选择现有的图像预设。 如果您要查找的图像预设不可见，则必须使其可见。 请参阅 [管理图像预设](/help/assets/managing-image-presets.md). 如果您使用的是图像预设，则无法选择查看器预设，反之，则无法选择查看器预设。

**[!UICONTROL 输出格式]**  — 选择图像的输出格式，例如jpeg。 根据您选择的输出格式，还有其他配置选项。 请参阅[图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options)。

**[!UICONTROL 锐化]**  — 选择要锐化图像的方式。 [图像预设最佳实践](/help/assets/managing-image-presets.md#image-preset-options)和[锐化最佳实践](/help/assets/assets/sharpening_images.pdf)中详细介绍了锐化。

**[!UICONTROL URL修饰符]**  — 您可以通过提供其他Dynamic Media Classic图像命令来更改图像效果。 这些命令在 [图像预设](/help/assets/managing-image-presets.md) 和 [命令引用](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL 断点]**  — 如果您的网站是响应式的，您需要调整断点。 断点之间必须使用逗号 (,) 分隔。

### 图像模板 {#image-template}

[Dynamic Media Classic图像模板](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) 是已导入到Dynamic Media Classic的分层Photoshop内容，其中内容和属性已进行参数化，以便进行可变性。 的 **[!UICONTROL 图像模板]** 组件允许您导入图像并在Experience Manager中动态更改文本。 此外，您还可以配置&#x200B;**[!UICONTROL 图像模板]**&#x200B;组件，以使用 Client Context 中的值，从而让每个客户获取个性化的图像体验。

选择 **[!UICONTROL 编辑]** 。 您可以配置 [所有Dynamic Media Classic组件通用的设置](#settings-common-to-all-scene-components) 以及本节中介绍的其他设置。

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL 文件引用、宽度、高度]**  — 请参阅所有ScDynamic Media Classicene7组件通用的设置。

>[!NOTE]
>
>Dynamic Media Classic URL命令和参数不能直接添加到文件引用URL中。 只能在组件 UI 的&#x200B;**[!UICONTROL 参数]**&#x200B;面板中定义这些命令和参数。

**[!UICONTROL 标题，替换文本]**  — 在Dynamic Media Classic图像模板选项卡中，为图像添加标题，并为关闭图形的用户添加替换文本。

**[!UICONTROL URL，在中打开]**  — 您可以设置资产来打开链接。 设置 URL，并在打开方式中指示是要在同一窗口中还是在新窗口中打开该 URL。

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL 参数面板]**  — 导入图像时，参数会预填充图像中的信息。 如果没有可以动态更改的内容，则此窗口将是空的。

![chlimage_1-233](assets/chlimage_1-233.png)

#### 动态更改文本 {#changing-text-dynamically}

要动态更改文本，请在字段中输入新文本，然后选择 **[!UICONTROL 确定]**. 在此示例中，**[!UICONTROL 价格]**&#x200B;现在为 50 美元，运费为 99 美分。

![chlimage_1-234](assets/chlimage_1-234.png)

图像中的文本发生了更改。您可以通过点按将文本重置为原始值 **[!UICONTROL 重置]** 字段旁边。

![chlimage_1-235](assets/chlimage_1-235.png)

#### 更改文本以反映客户端上下文值的值 {#changing-text-to-reflect-the-value-of-a-client-context-value}

要将字段链接到客户端上下文值，请选择 **[!UICONTROL 选择]** 要打开client-context菜单，请选择client context，然后选择 **[!UICONTROL 确定]**. 在此示例中，由于已将名称与个人资料中设置的格式化名称链接在一起，因此名称会相应地发生更改。

![chlimage_1-236](assets/chlimage_1-236.png)

文本反映了当前已登录用户的名称。您可以通过单击相应字段旁边的&#x200B;**[!UICONTROL 重置]**，将文本重置为原始值。

![chlimage_1-237](assets/chlimage_1-237.png)

#### 将Dynamic Media Classic图像模板设为链接 {#making-the-scene-image-template-a-link}

1. 在页面上，Dynamic Media Classic **[!UICONTROL 图像模板]** 组件，选择 **[!UICONTROL 编辑]**.
1. 在 **[!UICONTROL URL]** 字段，输入用户在点按图像时转到的URL。 在&#x200B;**[!UICONTROL 打开方式]**&#x200B;字段中，选择您希望在新窗口中还是在同一窗口中打开目标。

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. 选择 **[!UICONTROL 确定]**.

### 视频组件 {#video-component}

Dynamic Media Classic **[!UICONTROL 视频]** 组件(可从Sidekick的Dynamic Media Classic部分获取)使用设备和带宽检测为每个屏幕提供正确的视频。 此组件是一种 HTML5 视频播放器，它是可以跨渠道使用的单一查看器。

它可用于自适应视频集、单个MP4视频或单个F4V视频。

请参阅 [视频](s7-video.md) 有关视频如何与Dynamic Media Classic集成一起使用的更多信息。 此外，请参阅 [Dynamic Media Classic视频组件与Foundation视频组件](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### 视频组件的已知限制 {#known-limitations-for-the-video-component}

AdobeDAM和WCM显示是否上传了主源视频。 但它们不会显示以下代理资产：

* Dynamic Media Classic编码演绎版
* Dynamic Media Classic自适应视频集

将自适应视频集与Dynamic Media Classic视频组件一起使用时，必须调整组件大小以适合视频的尺寸。

## Dynamic Media Classic内容浏览器 {#scene-content-browser}

通过Dynamic Media Classic内容浏览器，您可以直接在Experience Manager中查看Dynamic Media Classic中的内容。 要访问内容浏览器，请在 **[!UICONTROL 内容查找器]**，选择 **[!UICONTROL Dynamic Media Classic]** 在触屏优化用户界面或 **[!UICONTROL S7]** 图标。 这两种用户界面的功能是相同的。

如果您有多个配置，则默认情况下，Experience Manager会显示 [默认配置](/help/sites-administering/scene7.md#configuring-a-default-configuration). 您可以直接在Dynamic Media Classic内容浏览器的下拉菜单中选择不同的配置。

>[!NOTE]
>
>* 按需文件夹中的资产不会显示在Dynamic Media Classic内容浏览器中。
>* When [已启用安全预览](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)，则Dynamic Media Classic上已发布和未发布的资产都会显示在Dynamic Media Classic内容浏览器中。
>* 如果您没有看到 **[!UICONTROL Dynamic Media Classic]** 或 **[!UICONTROL S7]** 图标作为内容浏览器中的选项，您必须 [配置Dynamic Media Classic以与Experience Manager结合使用](/help/sites-administering/scene7.md).
>* 对于视频，Dynamic Media Classic内容浏览器支持：
   >
   >   * 自适应视频集：一种容器，包含在多种屏幕上实现无缝播放所需的所有视频呈现
   >   * 单个 MP4 视频
   >   * 单个F4V视频


### 在触屏优化UI中浏览内容 {#browsing-content-in-the-touch-optimized-ui}

您可以在触屏优化UI或经典UI中访问内容浏览器。 目前，触屏优化具有以下限制：

* 不支持从Dynamic Media ClassicFlashFXG和资产。

通过选择 **[!UICONTROL Dynamic Media Classic]** 从第三个下拉菜单中。 如果尚未配置Dynamic Media Classic/Experience Manager集成，则Dynamic Media Classic不会显示在列表中。

>[!NOTE]
>
>* Dynamic Media Classic内容浏览器加载了大约100个资产，并按名称对它们进行排序。
>* 如果您设置了安全的预览服务器，则浏览器会使用该预览服务器来渲染缩略图和资产。

>


![chlimage_1-240](assets/chlimage_1-240.png)

此外，您还可以通过将鼠标悬停在浏览器中的资产上，浏览分辨率信息、大小、修改后间隔天数和文件名。

![chlimage_1-241](assets/chlimage_1-241.png)

* 对于自适应视频集和模板，不会为缩略图生成大小信息。
* 对于自适应视频集，不会为缩略图生成分辨率。

### 使用内容浏览器搜索Dynamic Media Classic资产 {#searching-for-scene-assets-with-the-content-browser}

在Dynamic Media Classic中搜索资产与在Experience Manager Assets中搜索资产类似。 但是，在搜索时，您实际上会在Dynamic Media Classic系统中看到资产的远程视图，而不是直接将它们导入Experience Manager。

您可以使用经典 UI 或触屏优化 UI 来查看和搜索资产。根据所用的界面，搜索方式会略有不同。

在任一 UI 中进行搜索时，您都可以按以下条件进行筛选（此处显示的是触屏优化 UI）：

**[!UICONTROL 输入关键词]**  — 您可以按名称搜索资产。 搜索时，您输入的关键词是文件名的开头。 例如，键入“swimming”一词后，将在该文件夹中查找任何以这些字母开头的资产文件名。键入搜索词后，请务必按Enter键以查找资产。

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL 文件夹/路径]**  — 查看的文件夹名称基于您选择的配置。 您可以向下展开到较低级别，方法是点按文件夹图标并选择子文件夹，然后点按复选标记以将其选中。

如果输入关键字并选择文件夹，则Experience Manager会搜索该文件夹及其所有子文件夹。 但是，如果您在搜索时未输入任何关键字，则选择文件夹只会显示该文件夹中的资产，而不包含任何子文件夹。

默认情况下，Experience Manager会搜索选定的文件夹和所有子文件夹。

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL 资产类型]**  — 选择 **[!UICONTROL Dynamic Media Classic]** 浏览Dynamic Media Classic内容。 仅当已配置Dynamic Media Classic时，此选项才可用。

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL 配置]**  — 如果您在 [!UICONTROL Cloud Services]，您可以在此处选择它。 因此，文件夹会根据您选择的配置进行更改。

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL 资产类型]**  — 在Dynamic Media Classic浏览器中，您可以筛选结果以包含以下任一内容：图像、模板、视频和自适应视频集。 如果您未选择任何资产类型，则默认情况下，Experience Manager会搜索所有资产类型。

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* 在经典 UI 中，您还可以搜索 **Flash** 和 **FXG**。不支持在触屏优化UI中过滤这些类型。
>
>* 搜索视频时，您搜索的是单个视频呈现。结果会返回原始呈现版本（仅&amp;ast;.mp4）和编码呈现版本。
>* 搜索自适应视频集时，您会搜索文件夹和所有子文件夹，但前提是您向搜索添加了关键字。 如果您未添加关键词，则Experience Manager不会搜索子文件夹。

>


**[!UICONTROL 发布状态]**  — 您可以根据发布状态筛选资产： **[!UICONTROL 未发布]** 或 **[!UICONTROL 已发布]**. 如果未选择任何 **[!UICONTROL 发布状态]**，则默认情况下Experience Manager会搜索所有发布状态。

![chlimage_1-247](assets/chlimage_1-247.png)
