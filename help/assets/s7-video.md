---
title: 视频
description: 了解集中式视频资产管理AEM Assets，您可以在其中将视频上传到Dynamic Media Classic以进行自动编码，并直接从AEM Assets访问Dynamic Media Classic视频。 Dynamic Media Classic视频集成将优化视频的范围扩展到所有屏幕。
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
role: Business Practitioner, Administrator
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: 视频
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1589'
ht-degree: 49%

---

# 视频 {#video}

Assets提供了集中式视频资产管理功能，您可以在该功能中直接将视频上传到Assets，以便自动编码到Dynamic Media Classic，并直接从Assets中访问Dynamic Media Classic视频以进行页面创作。

Dynamic Media Classic视频集成将优化视频的覆盖范围扩展到所有屏幕（自动设备和带宽检测）。

* **[!UICONTROL Scene7视频]**&#x200B;组件会自动执行设备和带宽检测，以在台式机、平板电脑和移动设备上播放正确的格式和正确质量的视频。
* Assets - 您可以包含自适应视频集，而不只是单个视频资产。自适应视频集是一个容器，其中包含在多种屏幕上无缝播放视频所需的所有视频演绎版。自适应视频集是同一个视频的一组版本，这些版本以不同的比特率和格式进行编码，例如 400 kbps、800 kbps 和 1000 kbps。使用自适应视频集以及 S7 视频组件，可在多种屏幕（包括台式机、iOS、Android、Blackberry 和 Windows 移动设备）上实现自适应视频流式传输。
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## 关于FFMPEG和Dynamic Media Classic {#about-ffmpeg-and-scene}

默认的视频编码流程以使用基于 FFMPEG 的视频配置文件集成为基础。因此，现成的DAM摄取工作流包含以下两个基于ffmpeg的工作流步骤：

* FFMPEG 缩略图
* FFMPEG 编码

请注意，启用和配置Dynamic Media Classic集成不会从即装即用的DAM摄取工作流中自动删除或停用这两个工作流步骤。 如果您已经在 AEM 中使用基于 FFMPEG 的视频编码，则您很可能已经在创作环境中安装了 FFMPEG。在这种情况下，使用DAM摄取的新视频将进行两次编码：一次从FFMPEG编码器获取，一次从Dynamic Media Classic集成获取。

如果您在AEM中配置了基于FFMPEG的视频编码，并安装了FFMPEG，则Adobe建议您从DAM摄取工作流中删除两个FFMPEG工作流。

## 支持的格式 {#supported-formats}

Scene7 视频组件支持以下格式：

* F4V H.264
* MP4 H.264

## 确定要将视频上传到的位置  {#deciding-where-to-upload-your-video}

确定要将视频资产上传到的位置取决于以下因素：

* 您是否需要对视频资产使用工作流？
* 您是否需要对视频资产进行版本控制？

如果上述任一问题的答案为“是”或两个问题的答案都为“是”，请将您的视频直接上传到 Adobe DAM。如果两个问题的答案都为“否”，请将您的视频直接上传到Dynamic Media Classic。 以下部分介绍了针对每种情景的工作流。

### 如果您要直接将视频上传到AdobeDAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

如果您需要为资产提供工作流或版本控制，则应先上传到AdobeDAM。 下面是建议的工作流：

1. 将视频资产上传到AdobeDAM，并自动对视频资产进行编码和发布到Dynamic Media Classic。
1. 在 AEM 中，从内容查找器的&#x200B;**[!UICONTROL 电影]**&#x200B;选项卡的 WCM 中访问视频资产。
1. 使用&#x200B;**[!UICONTROL Scene7 Video]**&#x200B;或&#x200B;**[!UICONTROL Foundation Video]**&#x200B;组件进行创作。

### 如果您要将视频上传到Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

如果您不需要对资产使用工作流或进行版本控制，应将资产上传到 Scene7。下面是建议的工作流：

1. 在Dynamic Media Classic中，[设置到Scene7的计划FTP上传和编码（系统自动）](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp)。
1. 在 AEM 中，从内容查找器的 **[!UICONTROL Scene7]** 选项卡的 WCM 中访问视频资产。
1. 使用&#x200B;**[!UICONTROL Scene7 Video]**&#x200B;组件进行创作。

## 配置与 Scene7 视频的集成 {#configuring-integration-with-scene-video}

要配置通用预设，请执行以下操作：

1. 在&#x200B;**[!UICONTROL 云服务]**&#x200B;中，导航到 **[!UICONTROL Scene7]** 配置，然后单击&#x200B;**[!UICONTROL 编辑]**。
1. 选择&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >如果页面中没有云配置，则不会显示&#x200B;**[!UICONTROL 视频]**&#x200B;选项卡。

1. 选择自适应视频编码配置文件、现成的单个视频编码配置文件，或自定义视频编码配置文件。

   >[!NOTE]
   >
   >有关视频预设含义的更多信息，请参阅[Dynamic Media Classic文档](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files)。
   >
   >Adobe 建议您在配置通用预设时选择两个自适应视频集，或选择&#x200B;**[!UICONTROL 自适应视频编码]**&#x200B;选项。

1. 选定的编码配置文件会自动应用于上传到您为此 Scene7 云配置设置的 CQ DAM 目标文件夹的所有视频。您可以根据需要设置多个具有不同目标文件夹的 Scene7 云配置，以便应用不同的编码配置文件。

## 更新查看器和编码预设  {#updating-viewer-and-encoding-presets}

如果由于Scene7中的预设已更新，您需要更新Experience Manager中视频的查看器和编码预设，请导航到云配置中的Scene7配置，然后单击&#x200B;**[!UICONTROL 更新查看器和编码预设]**。

![chlimage_1-364](assets/chlimage_1-364.png)

## 从AdobeDAM {#uploading-your-master-video}将主源视频上传到Scene7

1. 导航到在其中为云配置设置了 Scene7 编码配置文件的 CQ DAM 目标文件夹。
1. 单击&#x200B;**[!UICONTROL Upload]**&#x200B;以上传主源视频。 在[!UICONTROL DAM更新资产]工作流完成并且&#x200B;**[!UICONTROL 发布到Scene7]**&#x200B;具有复选标记后，视频上传和编码即已完成。

   >[!NOTE]
   >
   >可能需要一些时间才能生成视频缩略图。

   将DAM主源视频拖到视频组件上，可访问Scene7编码的代理演绎版的&#x200B;*所有*&#x200B;以进行交付。

## 基础视频组件与 Scene7 视频组件 {#foundation-video-component-versus-scene-video-component}

使用Experience Manager时，您可以同时访问站点中可用的视频组件和Scene7视频组件。 这些组件不能交换使用。

Scene7 视频组件仅适用于 Scene7 视频。基础组件可处理从Experience Manager（使用ffmpeg）和Scene7视频存储的视频。

下表说明了何时应使用何种组件：

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>S7 视频组件使用现成的通用视频配置文件。但是，您可以在Scene7中执行以下操作之一，以获取基于HTML5的视频播放器供Experience Manager使用：复制现成HTML5视频播放器的嵌入代码，并将其放入Experience Manager页面。

## AEM 视频组件 {#aem-video-component}

即使建议使用Scene7视频组件来查看Scene7视频，为了内容完整起见，本节仍介绍如何将Scene7视频与Experience Manager中的基础视频组件结合使用。

### AEM 视频与 Scene7 视频的比较 {#aem-video-and-scene-video-comparison}

下表简单地比较了 AEM 基础视频组件与 Scene7 视频组件所支持的功能：

|  | AEM 基础视频 | Scene7 视频 |
|---|---|---|
| 方法 | HTML5 为首选方法。Flash 仅用作不可使用 HTML5 时的回退方法。 | 在大多数台式机上使用 Flash。在移动设备和平板电脑上使用 HTML5。 |
| 交付 | 渐进式 | 自适应流式传输 |
| 跟踪 | 是 | 是 |
| 可扩展性 | 是 | 否 |
| 移动视频 | 是 | 是 |

### 设置  {#setting-up}

#### 创建视频配置文件 {#creating-video-profiles}

各种视频编码是根据在 S7 云配置中选定的 S7 编码预设创建的。要使基础视频组件能够利用这些视频编码，必须为每个选定的 S7 编码预设创建视频配置文件。这会相应地允许视频组件选择 DAM 演绎版。

>[!NOTE]
>
>必须激活新的视频配置文件以及对其所做的更改，才能进行发布。

1. 在AEM中，点按&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 配置控制台]**。
1. 在&#x200B;**[!UICONTROL 配置控制台]**&#x200B;中，导航到导航树中的&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL DAM]** > **[!UICONTROL 视频配置文件]**。
1. 创建一个新的 S7 视频配置文件。在&#x200B;**[!UICONTROL New]**.菜单中，选择&#x200B;**[!UICONTROL 创建页面]**，然后选择Scene7视频配置文件模板。 为新的视频配置文件页面指定一个名称，然后单击&#x200B;**[!UICONTROL 创建]**。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 编辑新的视频配置文件。首先选择云配置。然后，选择在云配置中选定的相同编码预设。

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | 属性 | 描述 |
   |---|---|
   | Scene7 云配置 | 用于编码预设的云配置。 |
   | Scene7 编码预设 | 要将此视频配置文件映射到的编码预设。 |
   | HTML5 视频类型 | 此属性允许设置HTML5视频源元素的type属性的值。 此信息不是由 S7 编码预设提供，但却是使用 HTML5 视频元素正确渲染视频所必需的信息。提供了通用格式列表，但是通用格式可被其他格式覆盖。 |

   对要在视频组件中使用的云配置中选定的所有编码预设重复此步骤。

#### 配置设计{#configuring-design}

**[!UICONTROL 基础视频]**&#x200B;组件必须了解要使用哪些视频配置文件才能构建视频源列表。 您必须打开视频组件设计对话框，并配置组件设计以便使用新的视频配置文件。

>[!NOTE]
>
>如果您在移动设备页面上使用&#x200B;**[!UICONTROL Foundation Video]**&#x200B;组件，则可能需要在移动设备页面的设计中重复这些步骤。

>[!NOTE]
>
>对设计所做的更改需要激活设计，才能在发布时生效。

1. 打开&#x200B;**[!UICONTROL Foundation Video]**&#x200B;组件的设计对话框，并更改为&#x200B;**[!UICONTROL Profiles]**&#x200B;选项卡。 然后，删除现成的用户档案并添加新的S7视频用户档案。 “设计”对话框中配置文件列表的顺序定义视频源元素在渲染时的顺序。
1. 对于不支持HTML5的浏览器，视频组件允许配置Flash回退。 打开视频组件设计对话框，并切换到&#x200B;**[!UICONTROL Flash]**&#x200B;选项卡。 配置Flash播放器设置并为Flash播放器分配备用配置文件。

#### 核对清单 {#checklist}

1. 创建 S7 云配置。确保已设置视频编码预设，且导入程序正在运行。
1. 为云配置中选定的每个视频编码预设创建对应的 S7 视频配置文件。
1. 必须激活视频配置文件。
1. 在页面上配置&#x200B;**[!UICONTROL 基础视频]**&#x200B;组件的设计。
1. 完成对设计的更改后，激活设计。
