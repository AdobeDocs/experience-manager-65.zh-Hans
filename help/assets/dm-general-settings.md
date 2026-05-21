---
title: 配置Dynamic Media常规设置
description: 了解如何在Dynamic Media中管理常规设置。 您可以在此处设置发布服务器名称和原始服务器名称，并设置图像覆盖选项。 此外，还有用于图像钝化蒙版的默认上传选项，以及用于了解如何处理PostScript、Adobe Photoshop、PDF和Adobe Illustrator文件的上传选项。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:43.326Z'
TQID: 'https://experienceleague.adobe.com/MXCLWQOBsCl3DPKVPn-WjnPeu-NGnQtUn6EYueH7OfE'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2:
  - id: a01bfd36-4ab8-4bf8-9dc0-5b45b890552e
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
source-git-commit: 9c96b6744c7af2f061b4dfbf403560047485f9b5
workflow-type: tm+mt
source-wordcount: 2537
ht-degree: 0%

---

# 配置Dynamic Media常规设置

配置&#x200B;**[!UICONTROL Dynamic Media常规设置]**&#x200B;仅适用于以下情况：

* 您正在以Scene7模式运行Dynamic Media。 请参阅[在Scene7模式下启用Dynamic Media](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode)。
* 您在Adobe Experience Manager 6.5.11或更高版本中具有&#x200B;*现有* **[!UICONTROL Dynamic Media配置]** （位于&#x200B;**[!UICONTROL Cloud Services]**）。 请参阅[在云服务中创建Dynamic Media配置](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services)。
* 您是具有管理员权限的Experience Manager系统管理员。

Dynamic Media常规设置旨在供经验丰富的网站开发人员和程序员使用。 Adobe Dynamic Media建议更改这些发布设置的用户熟悉Adobe Experience Manager上的Dynamic Media以及基础图像技术。

在创建帐户时，Adobe Dynamic Media会自动为贵公司提供分配的服务器。 这些服务器用于构建网站和应用程序的URL字符串。 这些URL调用特定于您的帐户。

“Dynamic Media发布设置”页面建立了默认设置，用于确定如何将资源从Adobe Dynamic Media服务器传递到网站或应用程序。 如果未指定设置，则Adobe Dynamic Media服务器将根据“Dynamic Media发布设置”页面上配置的默认设置交付资源。

另请参阅[可选 — Dynamic Media - Scene7模式设置的设置和配置](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)，了解更多可选配置任务。

>[!NOTE]
>
>在Adobe Experience Manager上从Dynamic Media Classic升级到Dynamic Media？ Dynamic Media中的“常规设置”页面和[发布设置](/help/assets/dm-publish-settings.md)页面已预填充从您的Dynamic Media Classic帐户中获取的值。 例外情况是“常规设置”页面的&#x200B;**[!UICONTROL 默认上载选项]**&#x200B;区域下列出的所有值。 这些值已在Experience Manager中。 因此，您通过Experience Manager用户界面在&#x200B;**[!UICONTROL 默认上传选项]**&#x200B;下对五个选项卡中的任何选项卡所做的任何更改都会反映在Dynamic Media中，而不是Dynamic Media Classic中。 在Dynamic Media Classic和Experience Manager上的Dynamic Media之间会维护“常规设置”页面和[发布设置](/help/assets/dm-publish-settings.md)页面中的所有其他设置和值。

**配置Dynamic Media常规设置：**

1. 在Experience Manager创作模式下，选择Experience Manager徽标以访问全局导航控制台。
1. 在左边栏中，选择工具图标，然后转到&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media常规设置]**。
1. 在“服务器”页面中，设置您的&#x200B;**[!UICONTROL 已发布的服务器名称]**&#x200B;和&#x200B;**[!UICONTROL 原始服务器名称]**，然后使用这五个选项卡配置用于图像编辑以及Postscript、Photoshop、PDF和Illustrator文件的默认上载选项。

   * [服务器](#server-general-setting)
   * [上载到应用程序](#upload-to-application)
   * [图像编辑](#image-editing-tab)选项卡
   * [PostScript](#postscript-tab)选项卡
   * [Photoshop](#photoshop-tab)选项卡
   * [PDF](#pdf-tab)选项卡
   * [Illustrator](#illustrator-tab)选项卡

   ![Dynamic Media常规设置页面](/help/assets/assets-dm/dm-general-settings.png)
   *Dynamic Media常规设置页面，已选择&#x200B;**[!UICONTROL 图像编辑]**&#x200B;选项卡。*<br><br>

1. 完成后，在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**。

## 服务器 {#server-general-setting}

在创建帐户时，Adobe Dynamic Media会自动为贵公司提供分配的服务器。 这些服务器用于构建网站和应用程序的URL字符串。 这些URL调用特定于您的帐户。

| 选项 | 描述 |
| --- | --- |
| **[!UICONTROL 已发布的服务器名称]** | 必需。<br>该名称必须在路径中使用`https://`。<br>此服务器是在所有特定于您帐户的系统生成URL调用中使用的实时CDN（内容分发网络）服务器。 请勿更改此服务器名称，除非Adobe技术支持指示您执行此操作。 |
| **[!UICONTROL 原始服务器名称]** | 必需。<br>此服务器仅用于质量保证测试。 除非得到Adobe技术支持的指示，否则请勿更改此服务器名称。 |

## 上载到应用程序 {#upload-to-application}

* **[!UICONTROL 覆盖图像]**

  Adobe Dynamic Media不允许两个文件具有相同的名称。 每个项目的Adobe Dynamic Media ID（图像名称减去文件扩展名）必须是唯一的。 由于此规则，**[!UICONTROL 上载到应用程序]**&#x200B;时发生了覆盖。 此选项的确切效果取决于您选择的指定覆盖图像选项。 这些选项指定如何上载替换图像：替换原始图像还是成为重复图像。 使用`-1`重命名重复图像。 例如，`chair.tif`被重命名为`chair-1.tif`。 这些选项会影响上载到与原始文件不同的文件夹的图像，或者文件扩展名与原始文件扩展名不同的图像，例如JPG、TIF或PNG。

  >[!NOTE]
  >
  >要保持与Experience Manager的一致性，请选择“覆盖图像”选项&#x200B;**[!UICONTROL 在当前文件夹中覆盖相同的基本名称/扩展名]**。

  | “覆盖图像”选项 | 描述 |
  | --- | --- |
  | **[!UICONTROL 在当前文件夹内，使用相同的基本名称/扩展名进行覆盖]** | *仅新Dynamic Media帐户的默认值*。<br>此选项是最严格的替换规则。 它要求您将替换图像上传到与原始图像相同的文件夹，并且替换图像具有与原始图像相同的文件扩展名。 如果不满足这些要求，则会创建副本。<br>*要与Experience Manager保持一致，请选择此选项*。 |
  | **[!UICONTROL 在当前文件夹内，使用相同的基本名称（不论扩展名是什么）进行覆盖]** | 要求您将替换图像上传到与原始图像相同的文件夹，但文件扩展名可能与原始图像不同。 例如，chair.tif将取代chair.jpg。 |
  | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称/扩展名进行覆盖]** | 要求替换图像具有与原始图像相同的文件扩展名（例如，chair.jpg必须替换chair.jpg，而不是chair.tif）。 但是，您可以将替换图像上传到与原始图像不同的文件夹。 更新的图像驻留在新文件夹中；无法再在其原始位置找到该文件。 |
  | **[!UICONTROL 在任意文件夹内，使用相同的基本资源名称（不论扩展名是什么）进行覆盖]** | 此选项是最具包容性的替换规则。 您可以将替换图像上载到与原始图像不同的文件夹，上载文件扩展名不同的文件，然后替换原始文件。 如果原始文件位于其他文件夹中，则替换图像将位于上载到的新文件夹中。 |

* **[!UICONTROL 保留裁切]**

  控制任何现有手动裁切定义的保留。

  另请参阅Dynamic Media查看器参考指南中的[UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html)和[ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html)中的`preserveCrop`。

## 默认上载选项 {#default-upload-options}

### “图像编辑”选项卡 {#image-editing-tab}

此滤镜允许您对最终取样缩小的图像微调锐化滤镜效果。 它有助于控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。

“钝化蒙版”效果使用与Photoshop的“钝化蒙版”滤镜相同的选项。 与名称所暗示的相反，“钝化蒙版”是一种锐化滤镜。

| “USM锐化”选项 | 描述 |
| --- | --- |
| **[!UICONTROL 金额]** | 必需。<br>控制应用于边缘像素的对比度大小。<br>将其视为效果的强度。 Adobe Dynamic Media中钝化蒙版的量值与Adobe Photoshop中的量值的主要区别在于Photoshop的量范围为1%到500%。 而在Adobe Dynamic Media中，值范围为`0.0`到`5.0`。 Adobe Dynamic Media中的5.0值大致相当于Photoshop中的500%；0.9值相当于90%，依此类推。 |
| **[!UICONTROL 半径]** | 必需。<br>控制效果的半径。<br>值范围为`0`到`250`。 该效果在图像中的所有像素上运行，并从所有像素向各个方向辐射。 半径以像素为单位测量。 例如，要对2000 x 2000像素图像和500 x 500像素图像获得类似的锐化效果，应将2000 x 2000像素图像上的半径设置为2像素。 然后在500 x 500像素图像上设置一个像素的半径值。 较大的值适用于像素较多的图像。 |
| **[!UICONTROL 阈值]** | 必需。<br>阈值是在应用钝化蒙版滤镜时忽略的对比度范围。 这种效果非常重要，因此使用此滤波器时，图像不会引入“杂色”。 值范围为`0` - `255`，这是灰度图像中的亮度阶数。 `0`=黑色，`128`=50%灰色和`255`=白色。<br>阈值为`12`将忽略肤色亮度的细微变化，以避免添加杂色，但仍会为相差的区域（如睫毛与皮肤相遇的区域）添加边缘对比度。<br>如果您有某人的面部照片，则“钝化蒙版”会影响图像的对比度部分。 例如，睫毛和皮肤相遇可产生明显对比区域，而皮肤本身光滑。 即使最光滑的皮肤也会表现出亮度值的细微变化。 如果不使用阈值，则滤镜会强调外观像素中的这些细微变化。 反过来，在增加睫毛上的对比度的同时，产生噪音和不希望的效果，增强锐利度。<br>为了避免此问题，引入了一个阈值，该阈值告知滤镜忽略对比度没有显着变化的像素，如平滑外观。<br>在前面显示的拉链图形中，请注意拉链旁边的纹理。 由于阈值过低，图像噪声难以抑制。 |
| **[!UICONTROL 单色]** | 选择此项可取消锐化蒙版图像亮度（强度）。<br>取消选择此项可单独取消锐化蒙版每个颜色组件。 |

另请参阅[在Adobe Dynamic Media和图像服务器](/help/assets/assets/sharpening_images.pdf)上锐化图像。

### PostScript选项卡 {#postscript-tab}

可以栅格化®文件、保持透明背景、选择分辨率以及选择颜色空间。

您可以在Adobe Dynamic Media中使用Adobe PostScript® (EPS)文件。 Adobe Dynamic Media提供上传这些文件时用于配置这些文件的命令。

上传PostScript (EPS)图像文件时，可以采用各种方式设置其格式。 您可以栅格化文件、保持透明背景、选择分辨率以及选择颜色空间。

| PostScript选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”以将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]** — 保留文件的色彩空间。<br>· **[!UICONTROL 强制为RGB]** — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]** — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制为灰度]** — 转换为灰度色彩空间。 |

### Photoshop选项卡 {#photoshop-tab}

您可以从® Photoshop®文件创建模板、维护图层、指定图层的命名方式、提取文本以及指定如何将图像锚定到模板中。

| Photoshop选项 | 描述 |
| --- | --- |
| **[!UICONTROL 保留图层]** | 将PSD中的图层（如果有）拆分为单独的资源。 资源层仍与PSD相关联。 您可以通过在“详细信息视图”中打开PSD文件并选择图层面板来查看这些内容。 请参阅在PSD文件中查看和编辑图层。 |
| **[!UICONTROL 创建模板]** | 从PSD文件中的图层创建模板。 |
| **[!UICONTROL 提取文本]** | 提取文本，以便用户能够在查看器中搜索文本。 |
| **[!UICONTROL 将图层扩展至背景大小]** | 将已翻录图像图层的大小扩展到背景图层的大小。 |
| **[!UICONTROL 图层命名]** | 将翻录图像图层的大小扩展到背景图层的大小。<br>· **[!UICONTROL 图层名称]** — 在PSD文件中将图像命名为图层名称后面的名称。 例如，原始PSD文件中名为“Price Tag”的图层会变成名为“Price Tag”的图像。 但是，如果PSD文件中的图层名称是默认的Photoshop图层名称（背景、第1层、第2层等），则图像将根据PSD文件中的图层编号进行命名。 <br>· **[!UICONTROL Photoshop和图层编号]** — 将图像命名为PSD文件中的图层编号，忽略原始图层名称。 使用Photoshop文件名和附加的图层编号来命名图像。 例如，名为`Spring Ad.psd`的文件的第二层名为`Spring Ad_2`，即使它在Photoshop中具有非默认名称。<br>· **[!UICONTROL Photoshop和图层名称]** — 将图像命名为PSD文件后跟图层名称或图层编号。 如果PSD文件中的图层名称是默认的Photoshop图层名称，则使用图层编号。 例如，名为`SpringAd`的PSD文件中名为`Price Tag`的图层名为`Spring Ad_Price Tag`。 默认名称为Layer 2的层称为`Spring Ad_2`。 |
| **[!UICONTROL 锚点]** | 指定如何在模板中定位图像，这些模板是从PSD文件生成的分层组合生成的。 默认情况下，锚点是中心。 中心锚点允许替换图像以最佳方式填充相同的空间，而不管替换图像的长宽比如何。 当引用模板并使用参数替换时，替换此图像的不同方面的图像有效地占用了相同的空间。 如果您的应用程序要求替换图像填充模板中分配的空间，请更改为其他设置。 |

### PDF选项卡 {#pdf-tab}

您可以选择栅格化文件、提取搜索词和链接、设置分辨率以及选择颜色空间。

| PDF选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | · **[!UICONTROL 无]** — 未对PDF进行任何处理。<br>· **[!UICONTROL 缩略图]** — 跳过PDF文件中的每个页面，并将其转换为缩略图图像。<br> · **[!UICONTROL 栅格化]** — 撕裂PDF文件中的页面，并将矢量图形转换为位图图像。 要创建eCatalog，请选择此选项。 |
| **[!UICONTROL 提取]** | · **[!UICONTROL 无]** — 未从PDF中提取任何搜索词或链接。<br>· **[!UICONTROL 搜索词]** — 从PDF文件中提取搜索词，以便在eCatalog查看器中按关键字搜索该文件。<br>· **[!UICONTROL 链接]** — 从PDF文件中提取链接，并将其转换为在eCatalog查看器中使用的图像映射。<br>· **[!UICONTROL 搜索词和链接]** — 提取搜索词和链接以在eCatalog查看器中使用。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定PDF文件中每英寸显示的像素数。 默认值为150。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]** — 保留PDF文件的色彩空间。<br>· **[!UICONTROL 强制作为RGB]** — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制作为CMYK]** — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制作为灰度]** — 转换为灰度色彩空间。 |

### Illustrator选项卡 {#illustrator-tab}

可以栅格化®文件、保持透明背景、选择分辨率以及选择颜色空间。

您可以在Adobe Dynamic Media中使用Adobe® Illustrator® (AI)文件。 Adobe Dynamic Media提供上传这些文件时用于配置这些文件的命令。

上传Illustrator (AI)图像文件时，可以采用各种方式设置其格式。 您可以栅格化文件、保持透明背景、选择分辨率以及选择颜色空间。 用于格式化PostScript和Illustrator文件的选项位于“上载作业选项”框中的“PostScript选项”和“Illustrator选项”下的上载屏幕上。


| Illustrator选项 | 描述 |
| --- | --- |
| **[!UICONTROL 正在处理]** | 选择“栅格化”以将文件中的矢量图形转换为位图格式。 |
| **[!UICONTROL 在渲染的图像中保持透明背景]** | 保留文件的背景透明度。 |
| **[!UICONTROL 分辨率（像素/英寸）]** | 确定分辨率设置。 此设置确定文件中每英寸显示的像素数。 |
| **[!UICONTROL 色彩空间]** | · **[!UICONTROL 自动检测]** — 保留文件的色彩空间。<br>· **[!UICONTROL 强制为RGB]** — 转换为RGB色彩空间。<br>· **[!UICONTROL 强制为CMYK]** — 转换为CMYK色彩空间。<br>· **[!UICONTROL 强制为灰度]** — 转换为灰度色彩空间。 |
