---
title: 处理支持的文件格式的最佳实践
description: 使用 [!DNL Experience Manager Assets]处理各种受支持文件类型的最佳实践。
contentOwner: AG
role: Admin
feature: 资产管理，开发人员工具
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# 资产文件格式最佳实践 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets] 支持许多专有和第三方文件格式库，以满足用户的各种文件支持要求。支持的Adobe库包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF光栅器和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]还支持第三方库，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

有关支持的文件格式，请参阅[资产支持的格式](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在Adobe Managed Services(AMS)上使用[!DNL Experience Manager]，请联系Adobe客户关怀团队，如果您计划处理大量大型PSD或PSB文件。 与Adobe客户关怀代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择尽可能最好的工具和模型。 [!DNL Experience Manager] 可能无法处理超过30000 x 23000像素的高分辨率PSB文件。

## [!DNL Adobe Camera Raw] 库 {#adobe-camera-raw-library}

为获得最佳性能，Adobe建议对RAW和DNG文件使用[!DNL Adobe Camera Raw]库。

[!DNL Adobe Camera Raw] 库支持将CMYK颜色配置文件作为输入。但是，它以RGB色彩空间生成输出，并且仅支持JPEG格式的输出。 缩略图中不保留源文件色彩空间（例如CMYK）。

有关更多信息，请参阅[Camera Raw支持](/help/assets/camera-raw.md)。

## Adobe PDF光栅器库 {#adobe-pdf-rasterizer-library}

为获得最佳结果，Adobe建议对以下文件使用Adobe PDF光栅器库：

* 内容密集型的PDF文件
* 未开箱生成缩略图的AI文件
* 对于具有专色(PMS)颜色的AI文件

与开箱即用的光栅输出相比，使用PDF光栅化器生成的缩略图和预览的质量更高。 Adobe PDF光栅器库不支持任何色彩空间转换。 无论源PDF文件的色彩空间如何，Adobe PDF光栅器仅生成RGB输出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建议您使用[!DNL Adobe InDesign Server]提取特定于[!DNL Adobe InDesign]的呈现版本，如IDML和HTML。 有关更多信息，请参阅[将Experience Manager资产添加为Adobe InDesign](/help/assets/managing-linked-subassets.md#refai)中的引用。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media] 通过其全球、可扩展且性能优化的网络，实时生成和传送多种丰富内容变体。它提供交互式查看体验并简化数字营销活动管理流程。 有关启用[!DNL Dynamic Media]的详细信息，请参阅[配置Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]每个文件最多可支持15 GB的内容。

## ImageMagick库 {#imagemagick-library}

Adobe建议在以下情况下使用ImageMagick库：

* 为EPS文件生成缩略图呈现。
* 用于保留图像配置文件信息。
* 保持透明度。
* 处理PSD和PSB文件。

要了解如何在[!DNL Experience Manager]中设置[!DNL ImageMagick]库，请参阅[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 有关最佳用法，请参阅[配置ImageMagick](/help/assets/best-practices-for-imagemagick.md)的最佳实践。

## 图像转码库 {#image-transcoding-library}

Adobe图像转码库是一款图像处理解决方案，可执行核心的图像处理功能，包括图像编码、转码、重新采样、调整大小等。

映像转码库支持以下MIME类型：

* JPG/JPEG
* PNG（8位和16位）
* GIF
* BMP
* TIFF/压缩TIFF（除32位Tiff和PTiff外）。
* ICO
* ICN

有关详细信息，请参阅[成像转码库](/help/assets/imaging-transcoding-library.md)。
