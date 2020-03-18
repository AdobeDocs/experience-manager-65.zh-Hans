---
title: 资产支持的格式
description: AEM资产支持的文件格式列表以及每种格式支持的功能。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 08ea08fc2f8c36d509509f761a76a428d6df7e6a

---


# Assets supported formats {#assets-supported-formats}

AEM资产支持各种文件格式，并且每种功能都对不同MIME类型提供不同的支持。

要将AEM资产与其他符合标准的数字资产管理(DAM)解决方案和桌面软件相集成，请使用Adobe的可扩展元数据平台(XMP)。

使用图例了解支持级别。

| 支持级别 | 描述 |
|:---:|---|
| ✓ | 支持 |
| * | 受支持，但需要附加功能 |
| - | 不适用 |

## Supported Raster image formats {#supported-raster-image-formats}

资产管理功能支持的栅格图像格式如下：

| 格式 | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | 交互式编辑 | 元数据写回 | 分析 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PNM | ✓ | ✓ |  |  |  |  | ✓ |
| PGM | ✓ | ✓ |  |  |  |  | ✓ |
| PBM | ✓ | ✓ |  |  |  |  | ✓ |
| PPM | ✓ | ✓ |  |  |  |  | ✓ |
| PSD* | ✓ | ✓ | ✓ | ✓ |  |  | ✓ |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ |  | ✓ |  |
| PICT |  |  |  |  |  |  | ✓ |
| PSB | ✓ | ✓ | ✓ | ✓ |  |  |  |

Dynamic Media功能支持的栅格图像格式如下：

| 格式 | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| PNG | ✓ | ✓ | ✓ | ✓ | ✓ |
| GIF | ✓ | ✓ | ✓ | ✓ | ✓ |
| TIFF | ✓ | ✓ | ✓ | ✓ | ✓ |
| JPEG | ✓ | ✓ | ✓ | ✓ | ✓ |
| BMP | ✓ |  |  |  |  |
| PSD* | ✓ |  |  |  |  |
| [EPS](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| PICT | ✓ |  |  |  |  |

&amp;ast;合并的图像从PSD文件中提取。 它是由Adobe Photoshop生成并包含在PSD文件中的图像。 根据设置，合并的图像可能是实际图像，也可能不是实际图像。

除了上述信息外，请考虑以下事项：

* 对EPS文件的支持仅适用于栅格图像。 例如，默认不支持为 EPS 矢量图像生成缩略图。要添加支持，请 [配置ImageMagick](best-practices-for-imagemagick.md)。 要集成第三方工具以启用其他功能，请参阅基 [于命令行的媒体处理程序](media-handlers.md#command-line-based-media-handler)。

* 将元数据写回添加到处理函数时，它适用于PSB文件格 `NComm` 式。

* 要使用Dynamic Media预览和生成EPS文件的动态演绎版，请参阅 [Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 对于EPS文件，PostScript文档结构约定(PS-Adobe)版本3.0或更高版本支持元数据写回。

## 支持的PDF栅格化器库 {#supported-pdf-rasterizer-library}

Adobe PDF Rasterizer库可为大型和内容密集型Adobe Illustrator和PDF文件生成高质量的缩览图和预览。 Adobe建议对以下内容使用PDF栅格化器库：

* 需要大量处理的内容密集型AI/PDF文件。
* AI/PDF文件，默认情况下不生成缩略图。
* 具有Pantone Matching System(PMS)颜色的AI文件。

See [Using PDF Rasterizer](aem-pdf-rasterizer.md).

## 支持的图像转码库 {#supported-image-transcoding-library}

Adobe Imaging Tronding库是一款图像处理解决方案，可执行核心图像处理功能，如编码、转码、重新取样和调整大小。

成像转码库支持JPG/JPEG、PNG（8位和16位）、GIF、BMP、TIFF/压缩TIFF（除32位TIFF文件和PTIFF文件外）、ICO和ICN MIME类型。

请参阅 [图像转码库](imaging-transcoding-library.md)。

## 支持的相机原始数据 {#supported-camera-raw}

Adobe Camera Raw库使AEM资产能够摄取原始图像。 See [Camera Raw support](camera-raw.md).

## Supported document formats {#supported-document-formats}

资产管理功能支持的文档格式如下：

| 格式 | 存储 | Metadata<br> management | Metadata<br> extraction | Thumbnail<br> generation | Interactive<br> editing | Metadata<br> writeback | [分析](touch-ui-asset-insights.md) | [连接的资产](use-assets-across-connected-assets-instances.md) |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| DOC | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| DOCX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| RTF | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| TXT | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLS | ✓ | ✓ | ✓ |  |  |  |  | ✓ |
| XLSX | ✓ | ✓ | ✓ | ✓ |  |  |  | ✓ |
| ODS | ✓ | ✓ | ✓ |  |  |  |  |  |
| PPT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| PPTX | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| ODP | ✓ | ✓ | ✓ |  |  |  |  |  |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ | ✓ |  | ✓ | ✓ | ✓ | ✓ |  |
| PS | ✓ | ✓ |  |  |  |  |  |  |
| QXP | ✓ | ✓ |  |  |  |  |  |  |
| EPUB | ✓ | ✓ |  | ✓ | ✓ |  |  |  |

Dynamic Media功能支持的文档格式如下：

| 格式 | Upload<br> (Input format) | Create<br> image<br> preset<br> (Output format) | Preview<br> dynamic<br> rendition | Deliver<br> dynamic<br> rendition | Download<br> dynamic<br> rendition |
|---|:---:|:---:|:---:|:---:|:---:|
| [AI](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ |  |  |  |  |
| [PDF](managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats) | ✓ | ✓ | ✓ | ✓ | ✓ |
| [INDD](managing-image-presets.md#indesign-indd-file-format) | ✓ |  |  |  |  |

除了上述功能外，还要考虑以下几点：

* 要使用Dynamic Media为PDF文件生成动态演绎版，请参阅 [Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media预览和生成AI文件的动态演绎版，请参阅 [Adobe Illustrator(AI)、Postscript(EPS)和PDF文件格式。](../assets/managing-image-presets.md#adobe-illustrator-ai-postscript-eps-and-pdf-file-formats)

* 要使用Dynamic Media为INDD文件生成动态演绎版，请参阅 [InDesign(INDD)文件格式](../assets/managing-image-presets.md#indesign-indd-file-format)。

## 支持的多媒体格式 {#supported-multimedia-formats}

|  | 存储 | 元数据管理 | 元数据提取 | 缩略图生成 | FFMPEG转码 |
|:---|:---:|:---:|:---:|:---:|:---:|
| AAC | ✓ | ✓ |  | - | * |
| MIDI | ✓ | ✓ |  | - | * |
| 3GP | ✓ | ✓ |  | - | * |
| MP3 | ✓ | ✓ | ✓ | - | * |
| MPG | ✓ | ✓ |  | - | * |
| OGA | ✓ | ✓ |  | - | * |
| OGG | ✓ | ✓ |  | - | * |
| RA | ✓ | ✓ |  | - | * |
| WAV | ✓ | ✓ |  | - | * |
| WMA | ✓ | ✓ |  | - | * |
| DVI | ✓ | ✓ |  | * | * |
| FLV | ✓ | ✓ |  | * | * |
| M4V | ✓ | ✓ |  | * | * |
| MPEG | ✓ | ✓ |  | * | * |
| OGV | ✓ | ✓ |  | * | * |
| MOV | ✓ | ✓ |  | * | * |
| WMV | ✓ | ✓ |  | * | * |
| SWF | ✓ | ✓ |  |  |  |

## Supported input video formats for Dynamic Media Transcoding {#supported-input-video-formats-for-dynamic-media-transcoding}

| 视频文件扩展名 | 容器 | 推荐的视频编解码器 | 不支持的视频编解码器 |
|---|---|---|---|
| MP4 | MPEG-4 | H264/AVC（所有配置文件） |  |
| MOV、QT | Apple QuickTime | H264/AVC、Apple ProRes422 &amp; HQ、Sony XDCAM、Sony DVCAM、HDV、Panasonic DVCPro、Apple DV (DV25)、Apple PhotoJPEG、Sorenson、Avid DNxHD、Avid AVR | Apple Intermediate、Apple Animation |
| FLV、F4V | Adobe Flash | H264/AVC、Flix VP6、H263、Sorenson | SWF（矢量动画文件） |
| WMV | Windows Media 9 | WMV3 (v9)、WMV2 (v8)、WMV1 (v7)、GoToMeeting（G2M2、G2M3、G2M4） | Microsoft Screen (MSS2)、Microsoft Photo Story (WVP2) |
| MPG、VOB、M2V、MP2 | MPEG-2 | MPEG-2 |  |
| M4V | Apple iTunes | H264/AVC |  |
| AVI | A/V Interleave | XVID、DIVX、HDV、MiniDV (DV25)、Techsmith Camtasia、Huffyuv、Fraps、Panasonic DVCPro | Indeo3 (IV30)、MJPEG、Microsoft Video 1 (MS-CRAM) |
| WebM | WebM | Google VP8 |  |
| OGV, OGG | Ogg | Theora、VP3、Dirac |  |
| MXF | MXF | Sony XDCAM、MPEG-2、MPEG-4、Panasonic DVCPro |  |
| MTS | AVCHD | H264/AVC |  |
| MKV | Matroska | H264/AVC |  |
| R3D, RM | Red Raw Video | MJPEG 2000 |  |
| RAM, RM | RealVideo | 不支持 | Real G2 (RV20)、Real 8 (RV30)、Real 10 (RV40) |
| FLAC | Native Flac | 免费的无损音频编解码器 |  |
| MJ2 | Motion JPEG2000 | Motion JPEG 2000编解码器 |  |

## Supported archive formats {#supported-archive-formats}

下表介绍了支持的存档格式和常见DAM工作流的适用性。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 动态媒体交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| TGZ | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| JAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| RAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| TAR | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| ZIP | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

## Other supported formats {#other-supported-formats}

下表介绍了几种其他文件格式的通用DAM工作流的适用性。 所有文件均支持常见的DAM功能（Dynamic Media Delivery除外）。

| 格式 | 存储 | 版本控制 | 工作流 | 发布 | 访问控制 | 动态媒体交付 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| SVG | ✓ | ✓ | ✓ | ✓ | ✓ |  |
| CSS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| VTT | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| XML | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| JavaScript（当配置有自己的交付域时） |  |  |  |  |  | ✓ |

**&amp;ast;** DAM中支持其他格式，用于存储、版本控制、ACL、工作流、发布和元数据管理。

## Supported MIME types {#supported-mime-types}

默认情况下，AEM会使用文件扩展名检测文件类型。 AEM可以从文件内容中检测到它。 对于后者，在AEM Web [!UICONTROL 控制台的Day CQ DAM Mime类型服务中] ，选 [!UICONTROL 择“从内容检测MIME] ”选项。

在CRXDE Lite中，提供了支持的MIME类型列表 `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`。

请参 [阅配置基于MIME类型的上传作业参数支持](config-dynamic.md)。

另请参 [阅启用基于MIME类型的资产/Scene7上传作业参数支持](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。

| 文件扩展名 | MIME类型/Internet媒体类型 | 默认jobParam值 | 允许的jobParam值 |
|---|---|---|---|
| 图像 | image/s7asset | `usmAmount=1.75&usmRadius=0.2`<br>`&usmThreshold=2&usmMonochrome=0&` | 默认jobParam适用于所有图像mime类型资产。<ul><li>[knockoutBackgroundOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_knockout_background_options.html)</li><li>manualCropOptions</li><li>[autoColorCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_auto_color_crop_options)</li><li>[autoTransparentCropOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_auto_transparent_crop_options)</li><li>[colorManagementOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_color_management_options.html)</li><li>[autoSetCreationOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_auto_set_creation_options.html)</li><li>[emailSetting](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/string_constants/index.html?f=r_email_settings)</li><li>[xmpKeywords](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_xmp_keywords)</li><li>[usmarpMaskOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_unsharp_mask_options.html)</li></ul> |
| 3G2 | video/3gpp2 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| 3GP | video/3gpp |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_exclude_master_video_from_avs) |
| AAC | audio/x-aac |  |  |
| AFM | application/x-font-type1 |  |  |
| AI | application/postscript | `aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_post_script_options.html)</li><li> [illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_illustrator_options.html)</li></ul> |
| AIFF | audio/x-aiff |  |  |
| AVI | video/x-msvideo |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| BMP | image/bmp |  |  |
| CSS | 文本/css |  |  |
| DOC | application/msword |  |  |
| EPS | <ul><li>application/postscript</li><li>application/eps</li><li>application/x-eps</li><li>image/eps</li><li>image/x-eps</li></ul> |  |  |
| F4V | video/x-f4v |  | ExcludeMasterVideoFromAVS |
| FLA | application/x-shockwave-flash |  |  |
| FLV | video/x-flv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| FPX | image/vnd.fpx |  |  |
| GIF | image/gif |  |  |
| ICC | application/vnd.iccprofile |  |  |
| ICM | application/vnd.iccprofile |  |  |
| INDD | application/x-indesign |  |  |
| JPEG | image/jpeg |  |  |
| JPG | image/jpeg |  |  |
| M2V | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| M4V | video/x-m4v |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MOV | video/quicktime |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MP3 | audio/mpeg |  |  |
| MP4 | video/mp4 |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPEG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MPG | video/mpeg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| MTS | model/vnd.mts |  |  |
| OGV | video/ogg |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| OTF | application/x-font-otf |  |  |
| PDF | application/pdf | `pdfprocess=Rasterize&resolution=150`<br>`&colorspace=Auto&pdfbrochure=false`<br>`&keywords=false&links=false` | [pdf选项](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_pdf_options) |
| PFB | application/x-font-type1 |  |  |
| PFM | application/x-font-type1 |  |  |
| PICT | image/x-pict |  |  |
| PNG | image/png |  |  |
| PPT | application/vnd.ms-powerpoint |  |  |
| PS | application/postscript | `psprocess=Rasterize&psresolution=150`<br>`&pscolorspace=Auto&psalpha=false`<br>`&psextractsearchwords=false`<br>`&aiprocess=Rasterize&airesolution=150`<br>`&aicolorspace=Auto&aialpha=false` | <ul><li>[postScriptOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_post_script_options)</li><li>[illustratorOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/index.html?f=r_illustrator_options)</li></ul> |
| PSD | image/vnd.adobe.photoshop | `process=None&layerNaming=Layername`<br>`&anchor=Center&createTemplate=false`<br>`&extractText=false&extendLayers=false` | <ul><li>[photoshopOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/?f=r_photoshop_options)</li><li>[photoshopLayerOptions](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_photoshop_layer_options.html)</li></ul> |
| RTF | application/rtf |  |  |
| SVG | image/svg+xml |  |  |
| SWF | application/x-shockwave-flash |  |  |
| TAR | application/x-tar |  |  |
| TIF / TIFF | image/tiff |  |  |
| TTC | application/x-font-ttf |  |  |
| TTF | application/x-font-ttf |  |  |
| VOB | video/dvd |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| VTT | text/vtt |  |  |
| WAV | audio/x-wav |  |  |
| WEBM | video/webm |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| WMA | audio/x-ms-wma |  |  |
| WMV | video/x-ms-wmv |  | [ExcludeMasterVideoFromAVS](https://marketing.adobe.com/resources/help/en_US/s7/ips_api/types/r_exclude_master_video_from_avs.html) |
| XLS | application/vnd.ms-excel |  |  |
| ZIP | application/zip |  |  |

>[!MORELIKETHIS]
>
>* [支持基于MIME类型的资产/Scene7上传作业参数](../sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support)。

