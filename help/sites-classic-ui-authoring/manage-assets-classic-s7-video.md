---
title: 视频
seo-title: Video
description: 资产提供了集中式视频资产管理功能，您可以在该功能中直接将视频上传到Assets以自动编码到Dynamic Media Classic，并直接从Assets中访问Dy视频以进行页面创作。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: b5cf18d8e83786a23005aadf8aafe43d006a2e67
workflow-type: tm+mt
source-wordcount: '1678'
ht-degree: 28%

---

# 视频{#video}

资产提供了集中式视频资产管理功能，您可以在该功能中直接将视频上传到Assets，以自动编码到Dynamic Media Classic，并直接从Assets中访问Dynamic Media Classic视频，以进行页面创作。

Dynamic Media Classic视频集成将优化视频的覆盖范围扩展到所有屏幕（自动设备和带宽检测）。

* Dynamic Media Classic视频组件可自动执行设备和带宽检测，以在台式机、平板电脑和移动设备上播放正确的格式和质量的视频。
* Assets - 您可以包含自适应视频集，而不只是单个视频资产。自适应视频集是一个容器，用于容纳在多个屏幕上无缝播放视频时需要的所有视频演绎版。 自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。您可以使用自适应视频集和S7视频组件，在多个屏幕(包括桌面、iOS、Android™、BlackBerry®和Windows移动设备)上实现自适应视频流播放。 有关更多信息，请参阅[Dynamic Media Classic自适应视频集文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video)。

## 关于FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

默认的视频编码流程以使用基于 FFMPEG 的视频配置文件集成为基础。因此，现成的[!UICONTROL DAM更新资产]工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG 缩略图
* FFMPEG 编码

启用和配置Dynamic Media Classic集成不会从即装即用的[!UICONTROL DAM更新资产]摄取工作流中自动删除或停用这两个工作流步骤。 如果您已在Adobe Experience Manager中使用基于FFMPEG的视频编码，则可能已在创作环境中安装FFMPEG。 在这种情况下，使用Experience Manager资产摄取的新视频会进行两次编码：一次从FFMPEG编码器获取，一次从Dynamic Media Classic集成获取。

如果您在Experience Manager中配置了基于FFMPEG的视频编码，并安装了FFMPEG，则Adobe建议您从[!UICONTROL DAM更新资产]工作流中删除两个FFMPEG工作流。

### 支持的格式 {#supported-formats}

Dynamic Media Classic视频组件支持以下格式：

* F4V H.264
* MP4 H.264

### 确定上传视频的位置 {#deciding-where-to-upload-your-video}

确定要将视频资产上传到的位置取决于以下因素：

* 您是否需要对视频资产使用工作流？
* 您是否需要对视频资产进行版本控制？

如果上述任一问题的答案为“是”或两个问题的答案都为“是”，请将您的视频直接上传到 Adobe DAM。如果两个问题的答案都为“否”，请将您的视频直接上传到Dynamic Media Classic。 以下部分介绍了针对每种情景的工作流。

#### 如果您要将视频直接上传到 Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

如果您需要对资产使用工作流或进行版本控制，应首先将资产上传到 Adobe Assets。下面是建议的工作流：

1. 将视频资产上传到Adobe资产，并自动对视频资产进行编码和发布到Dynamic Media Classic。
1. 在Experience Manager中，在内容查找器的&#x200B;**[!UICONTROL Movies]**&#x200B;选项卡的WCM中访问视频资产。
1. 使用Dynamic Media Classic视频或基础视频组件进行创作。

#### 如果您要将视频上传到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要为资产提供工作流或版本控制，则应将资产上传到Dynamic Media Classic。 下面是建议的工作流：

1. 在Dynamic Media Classic桌面应用程序中， [设置一个计划的FTP上传和编码到Dynamic Media Classic（系统自动）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options)。
1. 在Experience Manager中，在内容查找器的&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;选项卡的WCM中访问视频资产。
1. 使用Dynamic Media Classic视频组件进行创作。

### 配置与Dynamic Media Classic视频的集成 {#configuring-integration-with-scene-video}

1. 在&#x200B;**[!UICONTROL Cloud Services]**&#x200B;中，导航到您的&#x200B;**[!UICONTROL Dynamic Media Classic]**&#x200B;配置，然后选择&#x200B;**[!UICONTROL 编辑]**。
1. 选择&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

   >[!NOTE]
   >
   >如果页面中没有云配置，则不会显示&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。请参阅[为WCM启用Dynamic Media Classic](#enablingscene7forwcm)。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件，或自定义视频编码配置文件。

   >[!NOTE]
   >
   >有关视频预设含义的更多信息，请参阅[用于编码视频文件的视频预设](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)。
   >
   >Adobe 建议您在配置通用预设时选择两个自适应视频集，或选择&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;选项。

1. 选定的编码配置文件会自动应用于上传到您为此Dynamic Media Classic云配置设置的CQ DAM目标文件夹的所有视频。 您可以使用不同的目标文件夹设置多个Dynamic Media Classic云配置，以根据需要应用不同的编码配置文件。

### 更新查看器和编码预设 {#updating-viewer-and-encoding-presets}

如果在Dynamic Media Classic中更新了Experience Manager中的视频的预设，请更新查看器和编码预设。 在这种情况下，导航到云配置中的Dynamic Media Classic配置，然后选择&#x200B;**更新查看器和编码预设**。

![chlimage_1-131](assets/chlimage_1-131.png)

### 上传主源视频 {#uploading-your-master-video}

要从AdobeDAM将主源视频上传到Dynamic Media Classic，请执行以下操作：

1. 导航到CQ DAM目标文件夹，您已在该文件夹中使用Dynamic Media Classic编码配置文件设置云配置。
1. 选择&#x200B;**[!UICONTROL Upload]**&#x200B;以上传主源视频。 在[!UICONTROL DAM更新资产]工作流完成后，视频上传和编码即会完成，并且&#x200B;**[!UICONTROL 发布到Dynamic Media Classic]**&#x200B;带有复选标记。

   >[!NOTE]
   >
   >可能需要一些时间才能生成视频缩略图。

   将DAM主源视频拖动到视频组件上时，它将访问&#x200B;*所有* Dynamic Media Classic编码的代理演绎版以进行交付。

### 基础视频组件与Dynamic Media Classic视频组件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager时，您可以同时访问站点中提供的视频组件和Dynamic Media Classic视频组件。 这些组件不能交换使用。

Dynamic Media Classic视频组件仅适用于Dynamic Media Classic视频。 基础组件可处理从Experience Manager（使用ffmpeg）和Dynamic Media Classic视频存储的视频。

下表说明了何时应使用何种组件：

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Dynamic Media Classic视频组件开箱即用地使用通用视频配置文件。 但是，您可以获取基于HTML5的视频播放器以供Experience Manager使用。 在Dynamic Media Classic中，复制现成HTML5视频播放器的嵌入代码，并将其放入Experience Manager页面。

## Experience Manager视频组件 {#aem-video-component}

即使建议使用Dynamic Media Classic视频组件来查看Dynamic Media Classic视频，本节仍将介绍如何在Experience Manager中将Dynamic Media Classic视频与[!UICONTROL Foundation视频组件]结合使用，以实现完整性。

### Experience Manager视频与Dynamic Media Classic视频比较 {#aem-video-and-scene-video-comparison}

下表简要比较了Experience Manager基础视频组件与Dynamic Media Classic视频组件之间支持的功能：

|  | Experience Manager基础视频 | Dynamic Media Classic视频 |
|---|---|---|
| 方法 | HTML5 为首选方法。Flash 仅用作不可使用 HTML5 时的回退方法。 | 在大多数台式机上使用 Flash。在移动设备和平板电脑上使用 HTML5。 |
| 交付 | 渐进式 | 自适应流式传输 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 设置 {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

根据在Dynamic Media Classic云配置中选择的Dynamic Media Classic编码预设，创建各种视频编码。 要使基础视频组件能够使用这些视频组件，您必须为选定的每个Dynamic Media Classic编码预设创建视频配置文件。 它允许视频组件相应地选择DAM演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对其所做的更改，才能进行发布。

1. 在Experience Manager中，转到&#x200B;**[!UICONTROL 工具]**，然后选择&#x200B;**[!UICONTROL 配置控制台]**。
1. 在配置控制台中，导航到导航树中的&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 资产]** > **[!UICONTROL 视频配置文件]**。
1. 创建Dynamic Media Classic视频配置文件。 在&#x200B;**[!UICONTROL New]**&#x200B;菜单中，选择&#x200B;**[!UICONTROL Create Page]**。
1. 选择Dynamic Media Classic视频配置文件模板。 为新的视频配置文件页面指定一个名称，然后选择&#x200B;**[!UICONTROL 创建]**。

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. 编辑新的视频配置文件。首先选择云配置。然后，选择在云配置中选定的相同编码预设。

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | 属性 | 描述 |
   |---|---|
   | Dynamic Media Classic Cloud配置 | 用于编码预设的云配置。 |
   | Dynamic Media Classic编码预设 | 要将此视频配置文件映射到的编码预设。 |
   | HTML5 视频类型 | 利用此属性，可设置HTML5视频源元素的type属性值。 Dynamic Media Classic编码预设未提供此信息，但使用HTML5视频元素正确渲染视频时需要此信息。 提供了通用格式列表，但是通用格式可被其他格式覆盖。 |

   对要在视频组件中使用的云配置中选定的所有编码预设重复此步骤。

#### 配置设计 {#configuring-design}

基础视频组件必须知晓要使用哪些视频配置文件，才能构建视频源列表。打开视频组件设计对话框，并配置组件设计以使用新的视频配置文件。

>[!NOTE]
>
>如果您在移动设备页面上使用基础视频组件，请在移动设备页面的设计中重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开基础视频组件的设计对话框，并切换到&#x200B;**[!UICONTROL 配置文件]**&#x200B;选项卡。然后，删除现成的配置文件，并添加新的Dynamic Media Classic视频配置文件。 设计对话框中用户档案列表的顺序还定义视频源元素在渲染时的顺序。
1. 对于不支持HTML5的浏览器，视频组件允许您配置Flash回退。 打开视频组件的设计对话框，并切换到 **[!UICONTROL Flash]** 选项卡。配置 Flash Player 设置，并指定 Flash Player 的回退配置文件。

#### 核对清单 {#checklist}

1. 创建Dynamic Media Classic云配置。 确保已设置视频编码预设并且导入器正在运行。
1. 为在云配置中选择的每个视频编码预设创建Dynamic Media Classic视频配置文件。
1. 必须激活视频配置文件。
1. 配置页面上基础视频组件的设计。
1. 完成对设计的更改后，激活设计。
