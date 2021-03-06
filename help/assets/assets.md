---
title: ' [!DNL Adobe Experience Manager Assets] 简介'
description: 了解数字资产管理、其用例和 [!DNL Adobe Experience Manager Asset] 产品。
contentOwner: AG
feature: 资产管理
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 38%

---

# 关于[!DNL Adobe Experience Manager Assets]作为DAM解决方案 {#administering-assets}

[!DNL Assets] 是一款数字资产管理(DAM)工具，是该平台必不可少的一 [!DNL Experience Manager] 部分，可让您的企业管理和分发数字资产。组织内的用户可以管理、存储和访问多种类型的数字资产，如图像、视频、文档、音频剪辑、3D文件和富媒体，以在Web上使用、在打印中使用和用于数字分发。

## 什么是数字资产管理？ {#what-is-digital-asset-management}

[!DNL Assets] 允许在整个企业范围内共享和分发某组织的关键数字资产。组织内的用户可以通过 Web 界面（或者 CIFS 或 WebDAV 文件夹）存储、管理和访问数字资产，例如图像、图表、音频、视频和文档。

[!DNL Assets] 的功能 [!DNL Experience Manager] 允许您执行以下操作：

* 添加和共享多种文件格式的图像、文档、音频文件和视频文件。
* 通过按标记、灯箱或星形（您的收藏夹）对资产进行分组来管理资产。 可以在资产中添加批注。
* 通过搜索文件名、完整的文档文本、日期、文档类型和标记来查找资产。
* 添加或编辑资产的元数据信息。元数据会与相应的资产一起自动进行版本控制。您可以导入或导出资产元数据。
* 执行图像编辑功能，例如缩放和添加图像筛选器。使用 WebDAV 或 CIFS 文件夹同时导入和导出多个数字资产。
* 使用工作流和通知联合处理和下载任意资产集并管理资产的访问权限。

### [!DNL Experience Manager Assets] 与  [!DNL Experience Manager Sites] {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets] 与完全集成， [!DNL Sites] 并可在所有用例中无缝工作。例如，在创作网页时，[!DNL Sites]作者可以通过内容查找器查找和使用数字资产。 [!DNL Assets]的用户界面与[!DNL Sites]的用户界面相同。 有关完整的详细信息，请参阅[Sites](/help/sites-authoring/page-authoring.md)概述。

基本用户界面与[!DNL Sites]的用户界面相同。 有关完整的详细信息，请参阅[Sites](/help/sites-authoring/page-authoring.md)概述。

### 数字资产管理与图像组件 {#digital-asset-management-versus-image-component}

在确定是将图像放入DAM存储库还是使用图像组件时，请考虑图像生命周期：

* 如果图像的生命周期与页面相同，请使用图像组件。
* 如果图像具有单独的生命周期，例如，如果您使用图像两次或在 WCM 之外使用图像，则使用 [!DNL Assets].

## 什么是数字资产？ {#what-are-digital-assets}

资产是指数字文档、图像、视频或音频（或其中任一部分），它们可以具有多个演绎版，并且可以具有子资产（例如，photoshop文件中的图层、PowerPoint文件中的幻灯片、PDF中的页面、ZIP中的文件）。

资产本质上是一个具有元数据、演绎版和子资产的二进制文件。有关详细信息，请参阅 [DAM 性能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>上传和/或编辑大量资产（特别是图像）可能会影响[!DNL Experience Manager]部署的性能。

### [!DNL Experience Manager Assets] 术语 {#aem-assets-terminology}

在[!DNL Experience Manager]中使用数字资产时，您需要了解以下术语：

* **收藏集**:资产集合，基于物理位置（文件夹）、常用属性（保存的搜索文件夹）或用户选择（灯箱文件夹）。

* **** [!DNL Assets] 元数据；例如，作者、到期日期、DRM信息(Digital Rights Management)等。元数据受访问控制。[!DNL Assets] 支持以下各种常见的现成元数据架构：

   * Dublin Core：包括作者、描述、日期、主题等。
   * IPTC：包括事件、模型、位置等。
   * WCM:包括页面属性、[!UICONTROL 开机时间]和[!UICONTROL 关机时间]等。

* **标记**: [!DNL Assets] 标记和分类。请参阅[组织资产](/help/assets/organize-assets.md)。

* **演绎版**:演绎版是资产的二进制表示形式。[!DNL Assets] 始终具有主要表示形式 — 已上传文件的表示形式。它们可以采用创建的任何数量的其他表示形式，例如定制工作流程步骤或资产上传时创建的表示形式。演绎版可能大小不同、分辨率不同、添加了水印，或者更改了其他一些特性。

* **版本**:版本控制可创建数字资产在特定时间点的快照。您可以将资产恢复至以前的版本。请参阅 [!DNL Assets]](manage-assets.md#asset-versioning)中的[版本控制。

* **子资产**:子资产是构成资产的资产，例如，PDF文件中 [!DNL Adobe Photoshop] 的文件或页面中的层。在[!DNL Assets]中，您可以像管理资产一样管理子资产。

### 如何处理数字资产 {#how-to-work-with-assets}

您可以对资产或收藏集执行操作。这些操作包括创建或修改资产、收藏集和演绎版。您对资产执行的许多基本操作（上传、删除、更新、保存子资产）都会触发预配置的工作流。 这些操作将在[!DNL Assets]中自动打开，并在[!DNL Assets]媒体处理程序中详细描述。

您可以使用这些预配置工作流执行的任务：

* 在存储库中保存或删除资产。
* 提取并保存资产的元数据；单个元数据项将另存为XMP。
* 生成资产的演绎版和缩略图；包括根据需要自动调整大小和裁剪。
* 在必要时对资产进行转码。 例如，供移动设备和 Web 使用的视频将以 24 帧/秒的速率转码，供下载的视频将以 30 帧/秒的速率转码。对于移动设备和Web使用的音频采用128 Kbps的转码，对于下载的音频采用192 Kbps的转码。

当然，您也可以手动应用工作流。请参阅 [ Assets 媒体处理程序](media-handlers.md)，以获取默认工作流的列表。

## [!DNL Experience Manager Assets] 和 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

有关差异的信息，请参阅[资产和Media Library](medialibrary.md)。

>[!MORELIKETHIS]
>
>* [视频简介 — 将资产Experience Manager为现代DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [了解元数据概念](/help/assets/metadata-concepts.md)

