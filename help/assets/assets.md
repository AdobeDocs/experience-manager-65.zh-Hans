---
title: 简介 [!DNL Adobe Experience Manager Assets]
description: 在 Experience Manager 中创建、管理、处理和分发数字资产。这些指南介绍了最佳实践、辅助功能以及如何使用 AEM 6.5 资源。
hide: true
feature: Asset Management
role: Leader, Architect, User
exl-id: 68239634-a2e8-414e-a866-cd8082641ee8
solution: Experience Manager, Experience Manager Assets
source-git-commit: 347828d5bf3da01685f19fb43609505b24126c63
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 4%

---


# 关于[!DNL Adobe Experience Manager Assets]作为DAM解决方案 {#administering-assets}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/assets/overview) |
| AEM 6.5 | 本文 |

AEM [!DNL Assets]是一种数字资源管理(DAM)工具，它是[!DNL Experience Manager]平台的一部分，使您的企业能够管理和分发数字资源。 组织内的用户可以管理、存储和访问多种类型的数字资产，如图像、视频、文档、音频剪辑、3D文件和富媒体，以便在Web上、在印刷品中和使用数字分发功能。

## 什么是数字资产管理？ {#what-is-digital-asset-management}

[!DNL Assets]提供组织关键数字资产的企业范围共享和分发。 组织内的用户可以通过Web界面（或CIFS或WebDAV文件夹）存储、管理和访问数字资产，如图像、图形、音频、视频和文档。

[!DNL Assets]的[!DNL Experience Manager]功能允许您执行以下操作：

* 添加和共享各种文件格式的图像、文档、音频文件和视频文件。
* 通过按标记、灯箱或星星（您的收藏夹）对资源进行分组来管理资源。 向资产添加注释。
* 通过搜索文件名、文档全文以及搜索日期、文档类型和标记来查找资源。
* 添加或编辑资源的元数据信息。 元数据会自动与相应的资源一起进行版本控制。 您可以导入或导出资源元数据。
* 执行图像编辑功能，例如缩放和添加图像滤镜。 使用WebDAV或CIFS文件夹同时导入和导出多个数字资源。
* 使用工作流和通知允许联合处理和下载任何资产集并管理对资产的访问权限。

### [!DNL Experience Manager Assets]已与[!DNL Experience Manager Sites]集成 {#aem-assets-fully-integrated-in-cq-wcm}

[!DNL Assets]与[!DNL Sites]完全集成，可无缝地用于所有用例。 例如，在创作网页时，[!DNL Sites]作者可以通过内容查找器查找和使用数字资产。 [!DNL Assets]的用户界面与[!DNL Sites]的用户界面相同。 有关完整详细信息，请参阅[网站](/help/sites-authoring/page-authoring.md)概述。

基本用户界面与[!DNL Sites]的相同。 有关完整详细信息，请参阅[网站概述](/help/sites-authoring/page-authoring.md)。

### 数字资产管理与图像组件 {#digital-asset-management-versus-image-component}

在决定是将图像放入DAM存储库还是使用图像组件时，请考虑图像生命周期：

* 如果图像的生命周期与页面相同，则使用图像组件。
* 如果图像具有单独的生命周期，例如，如果您在WCM之外使用两次图像，则使用[!DNL Assets]。

## 什么是数字资产？ {#what-are-digital-assets}

资产是可以具有多个演绎版的数字文档、图像、视频或音频（或其中任一部分）。 它还可以具有子资产，例如，Photoshop文件中的图层、PowerPoint文件中的幻灯片、pdf中的页面、ZIP包中的文件。

资产本质上是二进制文件加元数据加演绎版加子资产。 有关详细信息，请参阅[DAM性能指南](/help/sites-deploying/assets-performance-sizing.md)。

>[!CAUTION]
>
>上传和/或编辑大量资产（特别是图像）可能会影响[!DNL Experience Manager]部署的性能。

### [!DNL Experience Manager Assets]术语 {#aem-assets-terminology}

在[!DNL Experience Manager]中使用数字资产时，如果您了解以下术语，则会很有帮助：

* **收藏集**：资产收藏集，基于物理位置（文件夹）、公共属性（保存的搜索文件夹）或用户选择（灯箱文件夹）。

* **元数据** [!DNL Assets]包含元数据；例如，作者、到期日期和DRM信息(Digital Rights Management)。 元数据受访问控制。 [!DNL Assets]支持以下各种现成的通用元数据架构：

   * 都柏林核心：包括作者、描述、日期、主题等。
   * IPTC：包括事件、模型、位置等。
   * WCM：包括页面属性、[!UICONTROL 开启时间]和[!UICONTROL 关闭时间]等。

* **标记**： [!DNL Assets]可以被标记和分类。 请参阅[组织资产](/help/assets/organize-assets.md)。

* **演绎版**：演绎版是资产的二进制表示形式。 [!DNL Assets]始终具有主要表示形式 — 已上传文件的表示形式。 它们可以具有任意数量的其他表示法，这些表示法是例如通过自定义工作流步骤在上传资产时创建的。 演绎版可以具有不同的尺寸、不同的分辨率、添加的水印或某些其他变化的特征。

* **版本**：版本控制功能在特定时间点创建数字资源的快照。 您可以将资源还原到以前的版本。 查看[中的 [!DNL Assets]](manage-assets.md#asset-versioning)版本控制。

* **子资产**：子资产是构成资产的资产，例如[!DNL Adobe Photoshop]文件中的图层或PDF文件中的页面。 在[!DNL Assets]中，您可以像管理资产一样管理子资产。

### 如何使用数字资产 {#how-to-work-with-assets}

您对资产或收藏集执行操作。 操作可以创建或修改资源、收藏集和演绎版。 您在资产上执行的许多基本操作（上传、删除、更新、保存子资产）都会触发预配置的工作流。 这些在[!DNL Assets]中自动打开，在[!DNL Assets]媒体处理程序中详细描述。

您可以使用这些预配置的工作流执行的任务：

* 在存储库中保存或删除资源。
* 提取并保存资源的元数据；各个元数据项将另存为XMP。
* 为资产生成演绎版和缩略图；包括根据需要自动调整大小和裁切。
* 如有必要，请对资产进行转码。 例如，用于移动和Web的视频以每秒24帧的速度进行转码，下载的视频以每秒30帧的速度进行。 用于移动和Web的音频使用128 Kbps进行转码，用于下载的音频使用192 Kbps。

您也可以手动应用工作流。 有关默认工作流的列表，请参阅[Assets媒体处理程序](media-handlers.md)。

## [!DNL Experience Manager Assets] 和 [!DNL Media Library] {#cq-dam-vs-cq-medialibrary}

有关差异的信息，请参阅[Assets和媒体库](medialibrary.md)。

>[!MORELIKETHIS]
>
>* [视频介绍 — Experience Manager Assets作为现代DAM](https://www.youtube.com/watch?v=PBwQqZgC-yo)
>* [了解元数据概念](/help/assets/metadata-concepts.md)
