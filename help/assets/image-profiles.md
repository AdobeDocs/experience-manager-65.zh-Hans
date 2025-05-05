---
title: Dynamic Media图像配置文件
description: 创建包含钝化蒙版和/或智能裁切或智能色板设置的图像配置文件，然后将配置文件应用到图像资源的文件夹。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
solution: Experience Manager, Experience Manager Assets
source-git-commit: a4c95d604e63c4fd00f17d2fb99a9e46f823ca10
workflow-type: tm+mt
source-wordcount: '3063'
ht-degree: 4%

---

# Dynamic Media图像配置文件 {#image-profiles}

上传图像时，您可以通过将图像配置文件应用到文件夹来在上传时自动裁切图像。

>[!IMPORTANT]
>
>* 智能裁剪仅在Dynamic Media - Scene7模式下可用。
>* 图像配置文件不适用于PDF、动画GIF或INDD (Adobe InDesign)文件。

## 裁切选项 {#crop-options}

对图像实施智能裁剪时，Adobe建议采用以下最佳实践并强制实施以下限制：

| 限制类型 | 最佳实践 | 施加的限制 |
| --- | --- | --- |
| 每个图像的智能裁剪数 | 5 | 100 |

另请参阅[Dynamic Media限制](/help/assets/limitations.md)。

<!-- CQDOC-16069 for paragraph directly below -->

智能裁剪坐标与纵横比相关。 对于图像配置文件中的各种智能裁剪设置，如果图像配置文件中添加的维度的纵横比相同，则会将相同的纵横比发送到Dynamic Media。 Adobe建议您使用相同的裁切区域。 这样做可以确保对图像配置文件中使用的不同尺寸没有影响。

您创建的每个智能裁剪生成都需要额外的处理。 例如，添加五个以上的智能裁切长宽比可能会导致资源摄取速度缓慢。 它还会导致系统负载增加。 由于您可以在文件夹级别应用智能裁切，因此Adobe建议您仅在需要它的文件夹&#x200B;*上*&#x200B;使用它。

**在图像配置文件中定义智能裁剪的准则**
为了控制智能裁切的使用情况，并优化裁切的处理时间和存储，Adobe建议遵循以下准则和提示：

* 要应用智能裁剪的图像资源必须至少为50 x 50像素或更大。
* 理想情况下，每个图像可以有10-15种智能裁剪，以优化屏幕比例和处理时间。
* 根据裁切维度而不是最终用途命名智能裁切。 这样做有助于优化在多个页面上使用单个维度的重复项。
* 为特定文件夹和子文件夹创建基于页面/资源类型的图像配置文件，而不是创建应用于所有文件夹或所有资源的通用智能裁剪配置文件。
* 应用于子文件夹的图像配置文件将覆盖应用于该文件夹的图像配置文件。
* 不允许包含重复的智能裁剪维度的图像配置文件。
* 不允许设置智能裁剪选项的重复命名图像配置文件。

您有两个图像裁切选项可供选择：像素裁切或智能裁切。 您还可以选择自动创建颜色和图像色板。

>[!IMPORTANT]
>
>* Adobe建议您查看任何生成的裁切和色板，以确保它们合适且与您的品牌和价值观相关。
>* 智能裁剪不支持CMYK图像格式。

| 选项 | 何时使用 | 描述 |
| --- | --- | --- |
| 像素裁剪 | 仅根据尺寸批量裁切图像。 | 要使用此选项，请从“裁切选项”下拉列表中选择&#x200B;**[!UICONTROL 像素裁切]**。<br><br>若要从图像侧面裁切，请输入要从图像任何侧面或每侧面裁切的像素数。 裁切图像的数量取决于图像文件中的ppi（每英寸像素数）设置。<br><br>图像配置文件像素裁切按以下方式呈现：<br>·值为“顶部”、“底部”、“左侧”和“右侧”。<br>·左上角被视为`0,0`，像素裁切将从此处计算。<br>·裁切起点：左为X，上为Y<br>·水平计算：原始图像的水平像素维度减去Left，再减去Right。<br>·垂直计算：垂直像素高度减去“顶部”，然后减去“底部”。<br><br>例如，假设您有4000 x 3000像素的图像。 您可以使用以下值：Top=250、Bottom=500、Left=300、Right=700。<br><br>从左上(300,250)裁切，使用填充空间（4000-300-700、3000-250-500或3000,2250）。 |
| 智能裁切 | 根据视觉焦点批量裁切图像。 | 智能裁剪利用Adobe Sensei中的人工智能的强大功能快速批量自动裁剪图像。 智能裁切会自动检测并裁切到任何图像中的焦点，以捕获预期的目标点，而不管屏幕大小如何。</p> <p>要使用智能裁切，请从“裁切选项”下拉列表中选择&#x200B;**[!UICONTROL 智能裁切]**，然后启用（打开）响应式图像裁切的右侧。</p> <p>大型、Medium和小型的默认断点大小通常涵盖大部分图像在移动设备和平板电脑设备、桌面和横幅上使用的完整大小。 如果需要，可以编辑“大”、“Medium”和“小”的默认名称。</p> <p>要添加更多断点，请选择&#x200B;**[!UICONTROL 添加裁切]**&#x200B;以删除裁切，选择“垃圾桶”图标。 |
| 颜色和图像样本 | 批量为每个图像生成图像样本。 | **注意**： Dynamic Media Classic不支持智能色板。<br><br>从显示颜色或纹理的产品图像自动定位并生成高质量色板。<br><br>要使用颜色和图像样本，请从“裁切选项”下拉列表中选择&#x200B;**[!UICONTROL 智能裁切]**，然后在颜色和图像样本的右侧，启用（打开）该功能。 在“宽度”和“高度”文本框中输入一个像素值。<br><br>虽然所有图像裁剪都可以从“呈现版本”边栏中使用，但样本只能通过“复制URL”功能使用。 使用您自己的查看组件渲染网站上的色板。 (此规则的例外是轮播横幅。 Dynamic Media为轮播横幅中使用的样本提供查看组件。)<br><br>**使用图像样本**<br>&#x200B;图像样本的URL简单明了。 它是：<br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>，其中`:Swatch`已附加到资产请求。<br><br>**使用色板**<br>&#x200B;要使用色板，您发出了包含以下内容的`req=userdata`请求：<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br>例如，以下是Dynamic Media Classic中的色板资源：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br>，以下是色板资源对应的`req=userdata` URL：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br>`req=userdata`响应如下：<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>您还可以请求采用XML或JSON格式的`req=userdata`响应，如以下相应的URL示例所示：<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**注意：**&#x200B;创建您自己的WCM组件以请求所表示的色板并解析`SmartSwatchColor`属性，以24位RGB的十六进制值表示。<br><br>另请参阅查看器参考指南[&#128279;](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata)中的`userdata`。 |

## USM 锐化 {#unsharp-mask}

使用&#x200B;**[!UICONTROL 钝化蒙版]**&#x200B;对最终取样缩小的图像微调锐化滤镜效果。 您可以控制效果的强度、效果的半径（以像素为单位）以及被忽略的对比度阈值。 此效果使用与Adobe Photoshop的&#x200B;*钝化蒙版*&#x200B;滤镜相同的选项。

>[!NOTE]
>
>USM只应用于PTIFF（金字塔tiff）内缩减采样率超过50%的缩减格式副本。 这意味着ptiff中最大大小的演绎版不受钝化蒙版的影响，而较小大小的演绎版（例如缩略图）会发生变化（并显示钝化蒙版）。

在&#x200B;**[!UICONTROL USM锐化]**&#x200B;中，具有以下过滤选项：

| 选项 | 描述 |
| --- | --- |
| 数量 | 控制应用于边缘像素的对比度数量。 默认值为1.75。对于高分辨率图像，最高可将其增加到5。 将“量”视为滤镜强度的度量。 范围是0-5。 |
| 半径 | 确定边缘像素周围影响锐化的像素数。对于高分辨率图像，输入1到2。低值仅锐化边缘像素；高值锐化较宽范围的像素。 正确的值取决于图像的大小。 默认值为0.2。范围是0-250。 |
| 阈值 | 确定在应用钝化蒙版滤镜时要忽略的对比度范围。换句话说，此选项确定锐化的像素与周围区域必须有多大的不同，才会被视为边缘像素并进行锐化。 为避免引入噪声，请尝试使用0-255之间的值。 |

在[锐化图像](/help/assets/assets/sharpening_images.pdf)中描述了锐化。

## 创建Dynamic Media图像配置文件 {#creating-image-profiles}

要为其他资源类型定义高级处理参数，请参阅[配置资源处理](config-dms7.md#configuring-asset-processing)。

查看用于处理元数据、图像和视频的[配置文件](processing-profiles.md)。

另请参阅[组织数字Assets以使用处理配置文件的最佳实践](/help/assets/organize-assets.md)。

**创建Dynamic Media图像配置文件：**

1. 选择Adobe Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像配置文件]**。
1. 选择&#x200B;**[!UICONTROL 创建]**，以便添加图像配置文件。
1. 输入配置文件名称，以及钝化蒙版、裁切或色板（或两者）的值。

   使用专用于其目标用途的配置文件名称。 例如，如果要创建仅生成样本的配置文件，即禁用（关闭）智能裁切并启用（打开）颜色和图像样本，请使用配置文件名称“智能样本”。

   另请参阅[智能裁切和智能色板选项](#crop-options)和[钝化蒙版](#unsharp-mask)。

   ![裁切](assets/crop.png)

1. 选择&#x200B;**[!UICONTROL 保存]**。新创建的配置文件将显示在可用配置文件的列表中。

## 编辑或删除Dynamic Media图像配置文件 {#editing-or-deleting-image-profiles}

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像配置文件]**。
1. 选择要编辑或删除的图像配置文件。 要编辑它，请选择&#x200B;**[!UICONTROL 编辑图像配置文件]**。 要删除它，请选择&#x200B;**[!UICONTROL 删除图像配置文件]**。

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. 如果编辑，请保存更改。 如果删除，请确认您要移除配置文件。

## 将Dynamic Media图像配置文件应用到文件夹 {#applying-an-image-profile-to-folders}

将图像配置文件分配给文件夹时，任何子文件夹都会自动从其父文件夹继承配置文件。 此工作流意味着您只能将一个图像配置文件分配给文件夹。 因此，请仔细考虑上传、存储、使用和存档资产的文件夹的结构。

如果为文件夹分配了其他图像配置文件，则新配置文件将覆盖以前的配置文件。 以前存在的文件夹资产保持不变。 新配置文件将应用于稍后添加到该文件夹的资源。

已为其分配配置文件的文件夹在用户界面中使用卡片中显示的配置文件名称指示。

<!-- When you add smart crop to an existing Image Profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

您可以将图像配置文件应用到特定文件夹，或全局应用到所有资源。

如果文件夹已具有您后来更改的现有“图像配置文件”，您可以重新处理该文件夹中的资产。 查看编辑文件夹中用于处理资产的配置文件后[重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

### 将Dynamic Media图像配置文件应用到特定文件夹 {#applying-image-profiles-to-specific-folders}

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中将图像配置文件应用到文件夹，或者如果您在文件夹中，也可以从&#x200B;**[!UICONTROL 属性]**。 本节将介绍这两种将图像配置文件应用到文件夹的方法。

如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

如果文件夹已具有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 查看编辑文件夹中用于处理资产的配置文件后[重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

#### 从“配置文件”用户界面将Dynamic Media图像配置文件应用到文件夹 {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像配置文件]**。
1. 选择要应用于一个或多个文件夹的图像配置文件。

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. 选择&#x200B;**[!UICONTROL 将处理配置文件应用到文件夹]**，然后选择一个或多个要用来接收新上传资源的文件夹，然后选择&#x200B;**[!UICONTROL 应用]**。 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

#### 从“属性”将Dynamic Media图像配置文件应用到文件夹 {#applying-image-profiles-to-folders-from-properties}

1. 选择Experience League徽标并导航到&#x200B;**[!UICONTROL Assets]**。 然后导航到要应用图像配置文件的文件夹的父文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 图像配置文件]**&#x200B;选项卡。 从&#x200B;**[!UICONTROL 配置文件名称]**&#x200B;下拉列表中选择配置文件，然后选择&#x200B;**[!UICONTROL 保存并关闭]**。 如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。

   ![chlimage_1-256](assets/chlimage_1-256.png)

### 全局应用Dynamic Media图像配置文件 {#applying-an-image-profile-globally}

除了将配置文件应用到文件夹外，您还可以全局应用配置文件，以便上传到任何文件夹中Experience Manager资产的任何内容均已应用选定的配置文件。

如果文件夹已具有您后来更改的现有视频配置文件，您可以重新处理该文件夹中的资产。 查看编辑文件夹中用于处理资产的配置文件后[重新处理该文件夹中的资产](processing-profiles.md#reprocessing-assets)。

**要全局应用Dynamic Media图像配置文件：**

1. 执行下列操作之一：

   * 导航到`https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam`并应用相应的配置文件，然后选择&#x200B;**[!UICONTROL 保存]**。

     ![chlimage_1-257](assets/chlimage_1-257.png)

   * 导航到CRXDE Lite到以下节点： `/content/dam/jcr:content`。

     添加属性`imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>`并选择&#x200B;**[!UICONTROL 全部保存]**。

     ![配置_图像_配置文件](assets/configure_image_profiles.png)

## 编辑单个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!IMPORTANT]
>
>* 智能裁剪仅在Dynamic Media - Scene7模式下可用。

您可以手动重新对齐图像的智能裁切窗口或调整其大小，以进一步优化其焦点。

在编辑智能裁切并保存之后，所做的更改将传播到您对特定图像使用该裁切的任何位置。

如有必要，重新运行智能裁剪以再次生成其他裁剪。

另请参阅[编辑多个图像的智能裁剪或智能色板](#editing-the-smart-crop-or-smart-swatch-of-multiple-images)。

**要编辑单个图像的智能裁剪或智能色板：**

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL Assets]**，然后导航到应用了智能裁剪或智能色板图像配置文件的文件夹。
1. 选择文件夹以打开其内容。
1. 选择要调整其智能裁剪或智能色板的图像。
1. 在工具栏中，选择&#x200B;**[!UICONTROL 智能裁剪]**。

   >[!TIP]
   >
   >使用热键`s`编辑智能裁剪或智能色板。

1. 执行以下任一操作：

   * 在页面的右上角附近，向左或向右拖动滑块可分别增加或减少图像显示。
   * 在图像上，拖动角手柄以调整裁切或色板的可查看区域的大小。
   * 在图像上，将框/样本拖动到新位置。 您只能编辑图像样本；颜色样本是静态的。
   * 在图像上方，选择&#x200B;**[!UICONTROL 还原]**&#x200B;以撤消所有编辑并恢复原始裁切或色板。

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到资源文件夹。

## 编辑多个图像的智能裁剪或智能色板 {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

>[!IMPORTANT]
>
>* 智能裁剪仅在Dynamic Media - Scene7模式下可用。

将包含智能裁切的图像配置文件应用到文件夹后，该文件夹中的所有图像都会应用裁切。 如果需要，您可以&#x200B;*手动*&#x200B;在多个图像中重新对齐智能裁剪窗口或调整其大小，以进一步优化其焦点。

在编辑智能裁切并保存之后，所做的更改将传播到您对特定图像使用该裁切的任何位置。

如有必要，重新运行智能裁剪以再次生成其他裁剪。

**要编辑多个图像的智能裁剪或智能色板：**

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL Assets]**，然后导航到应用了智能裁剪或智能色板图像配置文件的文件夹。
1. 在文件夹中，选择&#x200B;**[!UICONTROL 更多操作]** (...)图标，然后选择&#x200B;**[!UICONTROL 智能裁切]**。

1. 在&#x200B;**[!UICONTROL 编辑智能裁剪]**&#x200B;页面上，执行以下任一操作：

   * 调整页面上图像的查看大小。

     在断点名称下拉列表的右侧，向左或向右拖动滑块栏以更改可视图像显示的大小。

     ![edit_smart_ranks-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * 根据断点名称筛选可见图像的列表。 在下面的示例中，图像是按断点名称“Medium”过滤的。

     在页面的右上角附近，从下拉列表中选择一个断点名称，以筛选您看到的图像。 （请参阅上图。）

     ![edit_smart_rances-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * 调整智能裁剪框的大小。 执行以下任一操作：

      * 如果图像仅具有智能裁切或智能色板，请在图像上拖动裁切框的角手柄以调整裁切可视区域的大小。
      * 如果图像同时具有智能裁切和智能色板，请在图像上拖动裁切框的角手柄以调整裁切可视区域的大小。 或者，选择图像下方的智能色板（颜色色板为静态），然后拖动裁切框的角手柄以调整色板的可查看区域大小。

     ![调整图像的智能裁剪大小](assets/edit_smart_crops-resize.png)

   * 移动智能裁剪框。 执行以下任一操作：

      * 如果图像具有智能裁切或仅具有智能色板，请在图像上将裁切框拖动到新位置。
      * 如果图像同时具有智能裁切和智能色板，请在图像上将智能裁切框拖动到新位置。 或者，选择图像下方的智能色板（颜色色板是静态的），然后将智能色板裁切框拖动到新位置。

     ![edit_smart_ranks-move](assets/edit_smart_crops-move.png)

   * 撤消所有编辑并恢复原始智能裁剪或智能色板（仅适用于当前编辑会话）。

     选择图像上方的&#x200B;**[!UICONTROL 还原]**。

     ![edit_smart_comps-revert](assets/edit_smart_crops-revert.png)

1. 在页面的右上角附近，选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 关闭]**&#x200B;以返回到资源文件夹。

## 从文件夹中删除Dynamic Media图像配置文件 {#removing-an-image-profile-from-folders}

当您从文件夹中删除图像配置文件时，任何子文件夹都会自动从其父文件夹中删除配置文件。 但是，在文件夹中进行的任何文件处理操作将保持不变。

您可以从&#x200B;**[!UICONTROL 工具]**&#x200B;菜单中的文件夹删除图像配置文件，或者如果您在文件夹中，也可以从&#x200B;**[!UICONTROL 属性]**&#x200B;中删除。 本节将介绍这两种将图像配置文件从文件夹删除的方法。

### 通过“配置文件”用户界面从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. 选择Experience Manager徽标并导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 图像配置文件]**。
1. 选择要从一个或多个文件夹中删除的图像配置文件。
1. 选择&#x200B;**[!UICONTROL 从文件夹中删除处理配置文件]**，然后选择要从中删除配置文件的文件夹或多个文件夹，并选择&#x200B;**[!UICONTROL 删除]**。

   您可以确认图像配置文件不再应用于文件夹，因为文件夹名称下方不再显示该名称。

### 通过属性从文件夹中删除Dynamic Media图像配置文件 {#removing-image-profiles-from-folders-via-properties}

1. 选择Experience Manager徽标并导航&#x200B;**[!UICONTROL Assets]**，然后转到要删除图像配置文件的文件夹。
1. 在文件夹上，选中复选标记以将其选中，然后选择&#x200B;**[!UICONTROL 属性]**。
1. 选择&#x200B;**[!UICONTROL 图像配置文件]**&#x200B;选项卡。
1. 从&#x200B;**[!UICONTROL 配置文件名称]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 无]**，然后选择&#x200B;**[!UICONTROL 保存并关闭]**。

   如果文件夹已经分配了配置文件，则文件夹名称正下方会显示配置文件的名称。
