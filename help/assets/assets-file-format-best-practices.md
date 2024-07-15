---
title: 处理支持的文件格式的最佳实践
description: 使用 [!DNL Experience Manager Assets]处理各种支持的文件类型的最佳实践。
contentOwner: AG
role: Admin
feature: Asset Management,Developer Tools
exl-id: da080f12-4cf7-4c26-901b-cd40d9c00bcb
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Assets文件格式最佳实践 {#assets-file-format-best-practices}

[!DNL Adobe Experience Manager Assets]支持许多专有和第三方文件格式库，以满足用户的各种文件支持要求。 支持的Adobe库包括[!DNL Adobe Camera Raw]、Gibson、Adobe PDF光栅器和[!DNL Adobe InDesign Server]。 此外，[!DNL Experience Manager Assets]还支持第三方库，包括[!DNL ImageMagick]、[!DNL TwelveMonkeys]等。

有关支持的文件格式，请参阅[Assets支持的格式](/help/assets/assets-formats.md)。

>[!TIP]
>
>如果您在AdobeManaged Services (AMS)上使用[!DNL Experience Manager]，如果您计划处理大量大型PSD或PSB文件，请联系Adobe客户支持。 与Adobe客户支持代表合作，为您的AMS部署实施这些最佳实践，并为Adobe的专有格式选择最佳工具和模型。 [!DNL Experience Manager]不能处理超过30000 x 23000像素的超高分辨率PSB文件。

## [!DNL Adobe Camera Raw]库 {#adobe-camera-raw-library}

为获得最佳性能，Adobe建议对RAW和DNG文件使用[!DNL Adobe Camera Raw]库。

[!DNL Adobe Camera Raw]库支持将CMYK颜色配置文件作为输入。 但是，它生成RGB颜色空间的输出，并且仅支持JPEG格式的输出。 它不会在缩略图中保留源文件颜色空间（例如CMYK）。

有关详细信息，请参阅[Camera Raw支持](/help/assets/camera-raw.md)。

## Adobe PDF光栅器库 {#adobe-pdf-rasterizer-library}

为获得最佳结果，Adobe建议对以下文件使用Adobe PDF光栅器库：

* 繁重、内容密集的PDF文件
* 没有现成生成带缩略图的AI文件
* 对于具有专色(PMS)颜色的AI文件

与现成的光栅输出相比，使用PDF光栅器生成的缩略图和预览质量更好。 Adobe PDF光栅器库不支持任何色彩空间转换。 无论源PDF文件的颜色空间如何，Adobe PDF光栅器都只生成RGB输出。

## [!DNL Adobe InDesign Server] {#adobe-indesign-server}

Adobe建议使用[!DNL Adobe InDesign Server]提取特定于[!DNL Adobe InDesign]的演绎版，如IDML和HTML。 有关详细信息，请参阅[在Adobe InDesign中将Experience Manager资源添加为引用](/help/assets/managing-linked-subassets.md#refai)。

## [!DNL Dynamic Media] {#dynamic-media}

[!DNL Dynamic Media]通过其全局、可扩展且性能优化的网络实时生成和交付多种丰富内容变体。 它提供交互式观看体验，并简化了数字营销活动管理流程。 有关启用[!DNL Dynamic Media]的详细信息，请参阅[配置Dynamic Media](/help/assets/config-dynamic.md)。

目前，[!DNL Dynamic Media]可以支持每个文件最多15 GB内容的视频。

## ImageMagick库 {#imagemagick-library}

Adobe建议在以下情况下使用ImageMagick库：

* 为EPS文件生成缩略图演绎版。
* 保留图像配置文件信息。
* 保持透明度。
* 处理PSD和PSB文件。

若要了解如何在[!DNL Experience Manager]中设置[!DNL ImageMagick]库，请参阅[使用ImageMagick](/help/assets/media-handlers.md#an-example-using-imagemagick)。 要获得最佳用法，请参阅[配置ImageMagick的最佳实践](/help/assets/best-practices-for-imagemagick.md)。

## 图像转码库 {#image-transcoding-library}

Adobe成像转码库是一种图像处理解决方案，它执行核心图像处理功能，包括图像编码、转码、重新采样、调整大小等。

图像转码库支持以下MIME类型：

* JPG/JPEG
* PNG（8位和16位）
* GIF
* BMP
* TIFF/压缩TIFF（32位Tiff和PTiff除外）。
* 图标
* ICN

有关详细信息，请参阅[图像转码库](/help/assets/imaging-transcoding-library.md)。
