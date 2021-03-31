---
title: 处理支持的文件格式的最佳实践
description: 使用 [!DNL Experience Manager Assets]处理各种受支持文件类型的最佳实践。
contentOwner: AG
role: 管理员
feature: 资源管理，开发人员工具
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 资产文件格式最佳实践{#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支持许多专有和第三方文件格式库，以满足用户的各种文件支持需求。支持的Adobe库包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF Rasterizer和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]支持第三方库，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

有关支持的文件格式，请参阅[资产支持的格式](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您正在Adobe Managed Services(AMS)上使用[!DNL Experience Manager]，则如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户服务中心。 与Adobe客户服务代表合作，为您的AMS部署实施这些最佳做法，并为Adobe的专有格式选择尽可能最好的工具和模型。 [!DNL Experience Manager] 可能无法处理超30000 x 23000像素的高分辨率PSB文件。

## [!DNL Adobe Camera Raw] 库  {#adobe-camera-raw-library}

为获得最佳性能，Adobe建议对RAW和DNG文件使用[!DNL Adobe Camera Raw]库。

[!DNL Adobe Camera Raw] 库支持CMYK颜色用户档案作为输入。但是，它以RGB色彩空间生成输出，并仅支持JPEG格式的输出。 它不会在缩览图中保留源文件色彩空间（例如CMYK）。

有关详细信息，请参阅[Camera Raw支持](/help/assets/camera-raw.md)。

## Adobe PDF光栅器库{#adobe-pdf-rasterizer-library}

为获得最佳效果，Adobe建议对以下文件使用Adobe PDF栅格化库：

* 内容密集型PDF文件
* 未开箱生成缩览图的AI文件
* 对于具有专色(PMS)颜色的AI文件

与开箱即用的栅格输出相比，使用PDF栅格化工具生成的缩览图和预览的质量更高。 Adobe PDF Rasterizer库不支持任何色彩空间转换。 无论源PDF文件的色彩空间如何，Adobe PDF光栅器只生成RGB输出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建议您使用[!DNL Adobe InDesign Server]提取特定于[!DNL Adobe InDesign]的演绎版，如IDML和HTML。 有关详细信息，请参阅[在Adobe InDesign](/help/assets/managing-linked-subassets.md#refai)中将Experience Manager资产添加为引用。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 通过其全球、可扩展、性能优化的网络实时生成和交付多种形式的丰富内容。它提供交互式观看体验并简化数字活动管理流程。 有关启用[!DNL Dynamic Media]的详细信息，请参阅[配置Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]可支持每个文件最多15 GB内容的视频。

## ImageMagick库{#imagemagick-library}

Adobe建议在以下情况下使用ImageMagick库：

* 为EPS文件生成缩览图再现。
* 保留图像用户档案信息。
* 保持透明度。
* 处理PSD和PSB文件。

要了解如何在[!DNL Experience Manager]中设置[!DNL ImageMagick]库，请参阅[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 有关最佳用法，请参阅[配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)的最佳实践。

## 图像转码库{#image-transcoding-library}

Adobe成像转码库是一款图像处理解决方案，可执行核心图像处理功能，包括图像编码、转码、重新采样、调整大小等。

映像转码库支持以下MIME类型：

* JPG/JPEG
* PNG（8位和16位）
* GIF
* BMP
* TIFF/压缩TIFF（除32位Tiff和PTiff外）。
* ICO
* ICN

有关详细信息，请参阅[成像转码库](/help/assets/imaging-transcoding-library.md)。
