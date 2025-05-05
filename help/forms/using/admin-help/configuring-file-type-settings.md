---
title: 配置文件类型设置
description: 了解如何配置文件类型设置。 在PDF Generator中，您可以为支持的文件类型设置应用程序设置，以配置文件类型设置。
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '6200'
ht-degree: 0%

---

# 配置文件类型设置 {#configuring-file-type-settings}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在PDF Generator中，您可以为支持的文件类型设置应用程序设置。 在Windows上，您可以为每个支持的文件类型设置应用程序设置。 在UNIX和Linux上，您可以为HTML到PDF和OpenOffice设置应用程序设置。

在“文件类型设置”页上，可以执行以下任务：

* [创建或编辑“文件类型”设置](#create-or-edit-file-type-settings)
* 指定默认使用的文件类型设置(请参阅[导入和导出PDF Generator配置文件](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [更改默认设置](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [启用PDF/A支持](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [删除文件类型设置](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>后备转换器(例如，用于HTML到PDF转换的Acrobat、Microsoft PowerPoint、Microsoft Word和Microsoft Excel)的文件类型设置不可用。

## 创建或编辑文件类型设置 {#create-or-edit-file-type-settings}

创建或编辑文件类型设置，以指定应用程序处理所支持文件类型转换的方式。 在Windows上，您可以为每个支持的文件类型设置应用程序设置。 在UNIX和Linux上，您可以为HTML到PDF和OpenOffice设置应用程序设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL 文件类型设置]**。
1. 单击新建或单击设置的名称。
1. 在“文件扩展名”框中，键入此应用程序接受的文件类型的文件扩展名（以逗号分隔）。 不要包含扩展之前的句点或扩展之间的空格。 默认为 `bmp,gif,jpeg,jpg,tif,tiff,png`。
1. （可选）要在图形或图像中使用文本的光学代码识别(OCR)，请选择“使用OCR”并设置以下选项：

**主OCR语言：** OCR引擎用于标识字符的语言。 默认为英语（美国）。

**PDF输出样式：**&#x200B;选择“可搜索图像”可在前景中显示页面的位图图像，并在下面不可见的图层中显示扫描的文本。 页面的外观不会发生更改，但文本会变为可选和可读的。 选择“格式化的文本和图形”以使用可识别的文本、字体、图片和其他图形元素重建原始页面。 默认为可搜索图像（精确）。

**缩减像素取样图像：**&#x200B;减少彩色、灰度和单色图像的像素数。 在OCR完成之后对扫描的图像执行缩减像素采样。 缺省值为“最低”(600 dpi)。 如果将“PDF输出样式”设置为“可搜索图像（精确）”，则此选项不可用。

1. 完成以下部分中的必需信息：

[导入和导出PDF Generator配置文件](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Adobe PDF导出设置（仅限Windows）](#adobe-pdf-export-settings-windows-only)

[HTML到PDF设置](#html-to-pdf-settings)

[Flash视频以PDF设置](#flash-videos-to-pdf-settings)

[XPS到PDF设置](#xps-to-pdf-settings)

[PDF优化程序设置](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Microsoft Excel设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Microsoft PowerPoint设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Microsoft项目设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Microsoft Word设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Microsoft Visio设置（仅限Windows）](#visio)

[Microsoft Publisher设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[AutoCAD设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[OpenOffice设置](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[其他应用程序的设置（仅限Windows）](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   若要转到其他分区，请单击其在网页上的链接，或者使用&#x200B;**[!UICONTROL 下一个]**&#x200B;或&#x200B;**[!UICONTROL 上一个]**&#x200B;按钮。

1. 完成所有部分后，单击&#x200B;**[!UICONTROL 保存]**&#x200B;或&#x200B;**[!UICONTROL 另存为]**，并提供设置的名称。

可以自定义对各种文件类型的支持。 (请参阅[使用AEM表单编程](https://www.adobe.com/go/learn_lc_programming_11)中的“添加对其他本机文件格式的支持[&#128279;](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)”。)

## 更改默认设置 {#change-the-default-settings}

您可以更改适用于新创建源的Adobe PDF设置、安全设置和文件类型设置的默认值。 更改默认值不会影响现有源的设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>PDF Generator]**。
1. 在&#x200B;**[!UICONTROL Adobe PDF设置]**、**[!UICONTROL 文件类型设置]**&#x200B;或&#x200B;**[!UICONTROL 安全设置]**&#x200B;页面上，单击&#x200B;**[!UICONTROL 设置默认设置]**。
1. 选择您的首选默认设置。 “设置默认设置”页面提供了以下一个或多个设置：

   **[!UICONTROL Adobe PDF设置]**：原始默认值为“标准(Acrobat 6)”。

   **[!UICONTROL 安全设置]**：原始默认值为“无安全性(Acrobat 5)”。

   **[!UICONTROL 文件类型设置]**：原始默认值为标准。

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 删除文件类型设置 {#delete-a-file-type-setting}

您可以删除不再使用的文件类型设置。

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 服务>PDF Generator>文件类型设置]**。
1. 选中要删除的设置旁边的复选框。 您可以选择多个源。 旁边没有复选框的设置始终包含在PDF Generator中，无法删除。
1. 单击&#x200B;**[!UICONTROL 删除]**，然后在“删除确认”页面上单击&#x200B;**[!UICONTROL 删除]**。

## 图像到PDF设置 {#image-to-pdf-settings}

以下选项确定如何将图像文件转换为PDF。 有关访问这些设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**文件扩展名：**&#x200B;可转换的文件扩展名的逗号分隔列表。

**尝试回退转换器：** PDF Generator可以使用Java™或Acrobat将图像文件转换为PDF。 当选择此选项且转换失败或达到指定的超时限制时，PDF Generator会使用替代方法尝试转换。 如果备用方法失败或达到指定的超时限制，则会将异常写入日志文件。

>[!NOTE]
>
>JPEG2000文件只能使用Acrobat进行转换。

**使用OCR：**&#x200B;指定是否对PDF应用OCR（光学字符识别）。 OCR软件使您能够搜索、更正和复制PDF中的文本。

***注意&#x200B;**：仅在Microsoft Windows上支持OCRPDF(可搜索PDF)功能。*

**主OCR语言：**&#x200B;指定OCR引擎用于标识字符的语言。

**PDF输出样式：**&#x200B;确定要生成的PDF类型。 所有格式都将OCR和字体及页面识别应用于文本图像，并将它们转换为普通文本。

**可搜索图像：**&#x200B;确保文本可搜索且可选择。 此选项会保留原始图像，根据需要对其进行扭曲并将不可见的文本图层置于其上。 缩减像素取样图像选项可确定图像是否缩减像素取样以及缩减像素取样到什么程度。

**可搜索图像（精确）：**&#x200B;确保文本可搜索且可选择。 此选项会保留原始图像并在其上放置不可见的文本图层。 建议用于要求原始图像的最大保真度的情况。

**ClearScan：**&#x200B;合成与原始字体非常接近的新Type 3字体，并使用低分辨率副本保留页面背景。

**缩减像素取样图像：**&#x200B;在OCR完成之后减少彩色、灰度和单色图像的像素数。 选择要应用的缩减取样程度。 编号较高的选项缩减像素采样，从而生成更高分辨率的PDF。

## Adobe PDF导出设置（仅限Windows） {#adobe-pdf-export-settings-windows-only}

Adobe PDF导出设置部分中的“导出文件类型”设置用于将PDF文件转换为另一种格式。 缺省值为HTML4.01，带有层叠样式表(CSS) 1.0 (*.htm， *.html)。

有关访问此设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

## HTML到PDF设置 {#html-to-pdf-settings}

以下选项确定HTML文件转换为PDF的方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**尝试回退转换器：** PDF Generator可以使用Java™或Acrobat将HTML文件转换为PDF。 当选择此选项且转换失败或达到指定的超时限制时，PDF Generator会使用替代方法尝试转换。 如果备用方法失败或达到指定的超时限制，则会将异常写入日志文件。

**默认编码：**&#x200B;从操作系统和字母表的菜单设置文件文本的输入编码。 仅当HTML源文件未指定编码类型时，才使用默认编码选项中显示的选择。

**强制选定的编码：**&#x200B;忽略HTML源文件中指定的任何编码，并使用“默认编码”选项中显示的选择。

### 爬网设置 {#spidering-settings}

*正在爬网*&#x200B;扫描网页以查找指向其他网页的链接。 当遇到指向其他网页的链接时，将获取目标页面并将其包含在生成的PDF文档中。 启用这些选项可设置要获取并转换为PDF的级别数：

**仅获取X级别：**&#x200B;蜘蛛程序，并将页面从基本页面URL转换为指定级别的深度。 值1仅转换提供的URL。

**获取整个站点：**&#x200B;从提供的URL开始转换整个站点。

**保持在同一路径：**&#x200B;指向与基本URL不在同一相对路径上的页面的任何链接在爬网期间不会转换。

**驻留在同一服务器上：**&#x200B;指向不同服务器上的页面的任何链接在爬网期间都不会被转换。 只有指向与指定URL相同的服务器的链接才会被转换。

### 页面转换设置 {#page-conversion-settings}

启用这些选项可指定如何转换HTML页面。 根据页面大小，宽度、高度和边距值会相应地进行调整。

**页面大小：**&#x200B;选择自定义并指定宽度和高度，或选择预定义的维度。

**方向：**&#x200B;为转换后的PDF文档选择纵向或横向。

**边距：**&#x200B;指定生成的PDF文档中的边距（上、下、左和右）。

**将书签添加到PDF：**&#x200B;将书签添加到PDF文档。

**启用已标记PDF：**&#x200B;将标记嵌入到PDF文档中。

**设置初始视图设置：**&#x200B;允许您配置文档选项、窗口选项和用户界面选项。 这些设置确定内容的初始显示方式。

### 文档选项 {#document-options}

启用这些选项以指定如何显示PDF、如何显示内容文档中的页面以及如何指定放大级别：

**显示：**&#x200B;选择打开PDF文档时要在Acrobat中打开的窗格。

**页面布局：**&#x200B;选择PDF文档的页面布局类型。

**缩放比率：**&#x200B;选择用于PDF文档初始视图的预设缩放比率或选择一个自定义值。 选择默认设置表示使用默认的Acrobat放大率。

**打开页码：**&#x200B;指定PDF打开到的页码。

### 窗口选项 {#window-options}

启用这些选项以指定窗口的大小和显示方式。

**将窗口大小调整为初始页面：**&#x200B;将Acrobat窗口的大小调整为初始页面的大小。

**屏幕上的窗口中心：**&#x200B;在屏幕中心打开窗口。

**以全屏模式打开：**&#x200B;以全屏模式打开窗口。

**显示：**&#x200B;在窗口中显示文档标题或文件名。

### 用户界面选项 {#user-interface-options}

启用这些选项以指定窗口外观：

**隐藏菜单栏：**&#x200B;隐藏PDF文档中的菜单栏。

**隐藏工具栏：**&#x200B;隐藏PDF文档中的工具栏。

**隐藏窗口控件：**&#x200B;隐藏PDF文档中的窗口控件。

## Flash视频以PDF设置 {#flash-videos-to-pdf-settings}

PDF Generator支持提交用于AdobeFlash的视频(SWF或FLV文件)并创建PDF文件的功能，其中嵌入用于AdobeFlash的视频。 此转换不需要在Forms服务器上安装AdobeFlash Player。 有关访问此选项的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**文件扩展名：**&#x200B;可转换的文件扩展名的逗号分隔列表。

## XPS到PDF设置 {#xps-to-pdf-settings}

XML纸张规范(XPS)用于Windows打印机。 这是一种Microsoft格式，可从任何Microsoft Office应用程序创建。 AEM Forms提供以PDF转换XPS文件的功能。

**文件扩展名：**&#x200B;可转换的所有XPS文件扩展名的逗号分隔列表。 目前有一种格式： .xps。

## PDF优化程序设置 {#pdf-optimizer-settings}

PDF Generator支持减小PDF文件大小的功能。 是否使用所有这些设置或仅使用少数几个设置取决于您打算如何使用文件以及文件必须具有的基本属性。 在大多数情况下，默认设置适合最大化效率 — 通过删除嵌入字体、压缩图像以及从不再需要的文件中删除项目来节省空间。

>[!NOTE]
>
>优化数字签名文档可删除数字签名并使其失效。

有关访问此设置的说明，请参阅[创建或编辑文件类型设置](configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**目标PDF版本：**&#x200B;指定与PDF兼容的Acrobat版本。

### 字体 {#fonts}

1. 选择&#x200B;**字体。**
1. 选择以下选项之一：

   **取消嵌入所有字体：**&#x200B;取消嵌入所有嵌入的字体。

   **不取消嵌入任何字体：**&#x200B;不取消嵌入任何字体。

   **取消嵌入某些字体：**&#x200B;仅取消嵌入指定的字体。 按照以下步骤指定要取消嵌入的字体：

   * 如有必要，请从&#x200B;**字体源**&#x200B;下拉菜单中选择其他字体目录。 此下拉菜单列出了&#x200B;**主页>设置>核心系统>核心配置**&#x200B;中指定的字体目录。
   * 从&#x200B;**可用字体**&#x200B;列表中选择一种或多种字体，然后单击&#x200B;**添加**。 这些字体已添加到&#x200B;**要取消嵌入的字体**&#x200B;列表中。
   * 如果要取消嵌入Forms服务器上不存在的某些字体，请在&#x200B;**将字体添加到取消嵌入**&#x200B;框中输入这些字体的名称。 单击&#x200B;**添加**。

   >[!NOTE]
   >
   >*如果要取消嵌入其子集已嵌入文档中的某些字体，请在字体名称前面加上+号。 例如，“+Helvetica”。*

1. 如果只嵌入嵌入字体的使用中子集，请选择&#x200B;**所有嵌入字体的子集**。

   >[!NOTE]
   >
   >*如果将此选项与&#x200B;**取消嵌入某些字体**&#x200B;一起使用，则&#x200B;**将字体添加到取消嵌入**&#x200B;列表中的字体仍将被完全取消嵌入。*

   >[!NOTE]
   >
   >*字体子集是仅嵌入字体一部分的技术。 字体子集仅包含文档中使用的字符。*

### 透明度 {#transparency}

如果PDF文档包含包含包含透明度的图稿，可以使用“PDF优化器”设置来拼合透明度并减小文件大小。

>[!NOTE]
>
>如果选择Acrobat 4.0及更高版本作为TargetPDF版本，则会拼合所有透明对象。 对于其他TargetPDF版本，透明度受支持，您可以配置透明度设置。

选择&#x200B;**透明度**&#x200B;以在优化PDF文档时配置透明度设置。

**透明度级别**&#x200B;指定将保留的矢量信息量。 较高的设置可保留更多的矢量对象，而较低的设置可栅格化更多的矢量对象；中间设置可保留矢量形式的简单区域，并栅格化复杂的区域。 选择最低设置以栅格化所有图稿。

>[!NOTE]
>
>栅格化的发生量取决于页面的复杂性和重叠对象的类型。

**线条图和文本**&#x200B;所有对象（包括图像、矢量图稿、文本和渐变）栅格化的分辨率。 支持的值为1像素/英寸(ppi)到9600 ppi。

>[!NOTE]
>
>通常，线条艺术和文本分辨率应设置为600-1200 ppi，以提供高质量的栅格化，尤其是在衬线或小磅尺寸文字上。

**渐变和网格**&#x200B;网格栅格化后的分辨率。 支持的值为1 ppi到1200 ppi。

>[!NOTE]
>
>渐变和网格分辨率通常应设置为150-300 ppi，因为渐变、阴影和羽化的质量不会随着更高分辨率的提高而提高，但打印时间和文件大小会增加。

**将所有文本转换为外框**&#x200B;将所有文字对象（点类型、区域类型和路径类型）转换为外框，并丢弃包含透明度的页面上的所有文字字符信息。 此选项可确保拼合期间文本的宽度保持一致。 请注意，在Acrobat中查看或在低分辨率的桌面打印机上打印时，启用此选项将导致小字体显示得稍微粗一些。 它不会影响高分辨率打印机或照排机打印的类型的质量。

**将所有描边转换为外框**&#x200B;将所有描边转换为包含透明度的页面上的简单填充路径。 此选项可确保拼合期间笔触的宽度保持一致。 请注意，启用此选项会导致细描边显得稍粗一些，并且可能会降低拼合性能。

**剪切复杂区域**&#x200B;确保矢量图稿和栅格化图稿之间的边界沿对象路径排列。 此选项可减少将工件加入日志时产生的拼接工件

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>有些打印驱动程序处理光栅和矢量图的方式不同，有时会导致颜色拼接。 通过禁用某些特定打印驱动程序的色彩管理设置，您可以最大限度地减少拼接问题。 这些设置因每台打印机而异，因此请参阅打印机随附的文档以了解详细信息。

保留叠印：将透明图稿的颜色与背景颜色混合以创建叠印效果。

下表显示了常见的打印机类型及其以dpi测量的分辨率、以每英寸行数(lpi)测量的默认屏幕划线以及以每英寸像素数(ppi)测量的图像的重新取样分辨率。 例如，如果要打印到600 dpi激光打印机，则输入170作为图像重新取样的分辨率。

**图像**&#x200B;选择图像以指定彩色、灰度和单色图像的压缩和重新取样选项。 您可能希望尝试使用这些选项，以在文件大小和图像质量之间找到合适的平衡。彩色和灰度图像的分辨率设置应该为打印文件时线网的1.5到2倍。 单色图像的分辨率应与输出设备相同，但是以高于1500 dpi的分辨率保存单色图像会增加文件大小，但不会显着改善图像质量。 要放大的图像（如地图）可能需要更高的分辨率。

>[!NOTE]
>
>重新取样单色图像可能会产生意外的查看结果，例如没有图像显示。 如果发生这种情况，请关闭重新取样功能，然后再次转换文件。 缺采样时最有可能出现此问题，而双三次缩减采样时最不可能出现此问题。

<table>
 <tbody>
  <tr>
   <th><p><strong>打印机分辨率</strong></p> </th>
   <th><p><strong>默认行屏幕</strong></p> </th>
   <th><p><strong>图像分辨率</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi（激光打印机）</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi（激光打印机）</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi （照排机）</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi （照排机）</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### 放弃对象 {#discard-objects}

* 选择&#x200B;**放弃对象**&#x200B;以指定要从PDF中删除的对象并优化CAD绘图中的曲线。
* **放弃所有表单提交、导入和重置操作**：禁用与提交或导入表单数据相关的所有操作，并重置表单字段。 此选项会保留操作链接到的表单对象。
* **放弃所有JavaScript操作**：从PDF中删除任何使用JavaScript的操作。
* **放弃嵌入的页面缩略图**：删除嵌入的页面缩略图。 此选项适用于大型文档，在您单击“页面”按钮后，此类文档可能需要很长时间才能绘制页面缩略图。
* **将平滑线转换为曲线**：减少用于在CAD绘图中构建曲线的控制点数，从而使PDF文件更小，屏幕渲染速度更快。
* **放弃嵌入的打印设置**：从文档中删除嵌入的打印设置，如页面缩放和双工模式。
* **放弃书签**：从文档中删除所有书签。
* **拼合表单字段**：使表单字段不可用，而不更改其外观。 表单数据与页面合并，成为页面内容。
* **放弃所有备用映像**：删除映像的所有版本，但用于屏幕查看的版本除外。 某些PDF包含同一图像的多个版本以用于不同的目的，例如低分辨率的屏幕查看和高分辨率的打印。
* **放弃文档标记**：从文档中删除标记，这也会删除文本的可访问性和重排功能。
* **检测和合并图像片段**：查找分割为细切片的图像或蒙版，并尝试将切片合并为单个图像或蒙版。
* **放弃嵌入的搜索索引**：删除嵌入的搜索索引，这会减小文件大小。

#### 放弃用户数据 {#discard-user-data}

选择&#x200B;**放弃用户数据**&#x200B;可删除您不想分发或与其他用户共享的任何个人信息。

* **放弃所有备注、Forms和多媒体**：从PDF中删除所有备注、表单、表单字段和多媒体。
* **放弃所有对象数据**：从PDF中删除所有对象。
* **放弃外部交叉引用**：删除指向其他文档的链接。 跳转到PDF内其他位置的链接不会被删除。
* **放弃隐藏图层内容并拼合可见图层**：减小文件大小。 优化文档看起来与原始PDF相似，但不包含图层信息。
* **放弃文档信息和元数据**：删除文档信息字典和所有元数据流中的信息。 (使用“另存为”命令将PDF流还原为元数据副本。)
* **放弃文件附件**：删除所有文件附件，包括作为注释添加到PDF中的附件。 (PDF优化器不优化附加文件。)
* **放弃其他应用程序的私有数据**：从PDF文档中剥离仅对创建该文档的应用程序有用的信息。 此设置不会影响PDF的功能，但会减小文件大小。

### 清理 {#clean-up}

选择&#x200B;**清理**&#x200B;以从文档中删除不必要的项。
这些项目包括已过时或不需要用于文档预期用途的元素。 删除某些元素可能会严重影响PDF的功能。 默认情况下，只会选择不影响功能的元素。 如果不确定删除其他选项的影响，请使用默认选项。

**压缩**

从下拉菜单中选择以下“平滑”压缩选项之一：

* 压缩整个文件
* 压缩文档结构
* 删除压缩
* 保持压缩不变

**使用Flate对未编码的流进行编码**：将Flate压缩应用于所有未编码的流。

**放弃无效的书签**：删除指向文档中已删除页面的书签。

**放弃未引用的命名目标**：从PDF文档中删除未在内部引用的命名目标。 此选项不检查来自其他PDF文件或网站的链接。

**为快速Web视图优化PDF**：重新构建PDF文档，以便从Web服务器逐页下载（提供字节服务）。

**在使用LZW编码的流中，改用Flate**：将Flate压缩应用于使用LZW编码的所有内容流和图像。

**放弃无效链接**：删除跳转到无效目标的链接。

**优化页面内容**：将所有行尾字符转换为空格字符，这改进了平面压缩。

## Microsoft Excel设置（仅限Windows） {#microsoft-excel-settings-windows-only}

这些选项决定如何转换Microsoft Excel文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**尝试将OpenOffice作为回退转换器**：如果选择了此选项，并且使用Microsoft Excel的转换失败或达到指定的超时限制，则PDF Generator将尝试使用OpenOffice进行转换。 如果使用OpenOffice的转换失败或达到指定的超时限制，则会将异常写入日志文件。

**文件扩展名**：指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为`xls,xlsx`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

**创建PDF/A-1a兼容文件**：强制使用PDF/A-1b：2005RGBAdobe PDF设置。

**将书签添加到Adobe PDF**：将Excel工作表名称转换为书签。 默认情况下，该选项处于选中状态。

**使工作表适合单页**：减小文本大小以使工作表适合单页。

**转换整个工作簿**：转换Excel文件中的所有工作表。 如果未选择此选项，则仅转换当前页面。

**自动运行宏**：在转换文档之前运行Excel文档中的任何宏（例如插入当前时间的宏）。

**转换文档信息**：根据源文件中的文档信息添加PDF文档属性。 这包括文档标题、作者、主题和关键字等信息。

**将链接添加到Adobe PDF**：将源文件中的超链接转换为PDF文档中的超链接。

**将Source文件附加到Adobe PDF**：选择此选项时，原始Excel电子表格将作为附件插入到生成的PDF文档中。

**启用辅助功能和Reflow及带有标记的Adobe PDF**：将标记嵌入到PDF文档中，以启用辅助功能并重新流动。

**要加载的Excel加载项列表**：默认情况下（出于安全原因），将Excel文件转换为PDF时，不会运行Excel加载项。 要允许在转换期间运行某些Excel加载项，请提供以逗号分隔的加载项名称列表。

**要转换的工作表列表**：如果此框为空，则Excel电子表格中的所有工作表都将包含在生成的PDF中。 要有选择地转换工作表的子集，请提供以逗号分隔的工作表名称列表。

## Microsoft PowerPoint设置（仅限Windows） {#microsoft-powerpoint-settings-windows-only}

这些选项确定Microsoft PowerPoint文件的转换方式。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**[!UICONTROL 尝试将OpenOffice作为回退转换器]**：如果选中了此选项，并且使用Microsoft PowerPoint的转换失败或达到指定的超时限制，则PDF Generator将尝试使用OpenOffice进行转换。 如果使用OpenOffice的转换失败或达到指定的超时限制，则会将异常写入日志文件。

**[!UICONTROL 文件扩展名]**：指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为ppt，pptx。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**：从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。 默认情况下，该选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**：将PowerPoint标题转换为书签。 默认情况下，该选项处于选中状态。

**[!UICONTROL 将Source文件附加到Adobe PDF]**：将源文件作为附件添加到PDF文件中。 默认情况下，此选项处于取消选中状态。

**[!UICONTROL 启用带有标记的Adobe PDF的辅助功能和Reflow]**：将标记嵌入到PDF文件中。 默认情况下，此选项处于取消选中状态。

**[!UICONTROL 将多媒体转换为PDF多媒体]**：尽可能将多媒体转换为PDF多媒体。 默认情况下，该选项处于选中状态。

**[!UICONTROL 转换演讲者备注]**：将演讲者备注转换为PDF。

**[!UICONTROL 自动运行宏]**：在转换文档之前运行PowerPoint文档中的任何宏（例如插入当前时间的宏）。

**[!UICONTROL 基于PowerPoint打印机设置的PDF布局]**：使用PowerPoint打印机设置来布局PDF文档。

**[!UICONTROL 添加指向Adobe PDF的链接]**：转换文件时保留现有链接。 链接的外观通常保持不变。 仅当还选中了“启用辅助功能”选项时，才能创建链接。 默认情况下，此选项处于取消选中状态。

**[!UICONTROL 在Adobe PDF中保存幻灯片过渡]**：转换幻灯片过渡。 默认情况下，该选项处于选中状态。

**[!UICONTROL 在Adobe PDF中保存动画]**：将转换后的动画保存在PDF文件中。

**[!UICONTROL 将隐藏的幻灯片转换为PDF页]**：转换隐藏的幻灯片。

**[!UICONTROL 创建PDF/A-1a兼容文件]**：强制使用PDF/A-1b：2005RGBAdobe PDF设置。 在生成PDF文件时，一些PowerPoint功能不会转换。 如果PowerPoint过渡在Acrobat中没有等效过渡，则会替换类似的过渡。 如果同一幻灯片中有多个动画效果，则使用单个效果。 转换页面过渡和项目符号飞入。

## Microsoft项目设置（仅限Windows） {#microsoft-project-settings-windows-only}

这些选项决定如何转换Microsoft项目文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

1. **[!UICONTROL 文件扩展名：]**&#x200B;指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为`mpp`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

1. **[!UICONTROL 转换文档信息]**：从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。 默认情况下，该选项处于选中状态。
1. **[!UICONTROL 将Source文件附加到Adobe PDF]**：将源文件作为附件添加到PDF文件中。
1. **[!UICONTROL 创建PDF/A-1a兼容文件]**：强制使用PDF/A-1b：2005RGBAdobe PDF设置。
1. **[!UICONTROL 自动运行宏]**：在转换文档之前运行Microsoft项目文档中的任何宏（例如插入当前时间的宏）。

## Microsoft Word设置（仅限Windows） {#microsoft-word-settings-windows-only}

这些选项决定如何转换Microsoft Word文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**[!UICONTROL 尝试将OpenOffice作为回退转换器]**：如果选中了此选项，并且使用Microsoft Word的转换失败或达到指定的超时限制，则PDF Generator将尝试使用OpenOffice进行转换。 如果使用OpenOffice的转换失败或达到指定的超时限制，则会将异常写入日志文件。

**[!UICONTROL 文件扩展名]**：指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为`doc,docx,rtf,txt`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**：从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。 默认情况下，该选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**：将标题转换为书签。 默认情况下，该选项处于选中状态。

**[!UICONTROL 将Source文件附加到Adobe PDF]**：将源文件作为附件添加到PDF文件中。

**[!UICONTROL 将交叉引用和目录转换为链接]**：将所有交叉引用和目录条目转换为链接。 默认情况下，该选项处于选中状态。

**[!UICONTROL 启用带有标记的Adobe PDF的辅助功能和Reflow]**：将标记嵌入到PDF文件中。 默认情况下，该选项处于选中状态。

**[!UICONTROL 创建PDF/A-1a兼容文件]**：如果选定此选项，将强制使用PDF/A-1b：2005RGBAdobe PDF设置。

**[!UICONTROL 自动运行宏]**：在转换文档之前运行Word文档中的任何宏（例如插入当前时间的宏）。

**[!UICONTROL 在Adobe PDF中保留文档标记]**：将Word文档中的标记转换为PDF文件中的注释。

**[!UICONTROL 将链接添加到Adobe PDF]**：将源文件中的超链接转换为PDF文档中的超链接。

**[!UICONTROL 转换脚注和尾注链接]**：从PDF文档的脚注和尾注引文创建指向笔记的链接。

**[!UICONTROL 在Adobe PDF中将显示的注释转换为注释]**：将Word文档中的注释转换为PDF文档中的文本注释。

**[!UICONTROL 启用高级标记]**：添加高级标记以增强辅助功能。

**[!UICONTROL 将所有样式转换为书签]**：将Word文档中的所有样式转换为PDF文档中的书签。

**[!UICONTROL 将指定的样式转换为书签]**：将您在&#x200B;**[!UICONTROL 具有级别]**&#x200B;的样式字段中定义的样式转换为PDF文档中的书签。

**[!UICONTROL 具有级别]**&#x200B;的样式：指定Word文档中的哪些样式将转换为PDF文档中的书签。 还指定书签的级别。 若要使用此功能，请取消选择&#x200B;**[!UICONTROL 将所有样式转换为书签]**&#x200B;选项，并以下列格式指定样式名称：

**styleName1=level1[，styleName2=level2...]**

如果Microsoft Word样式名称包含逗号(，)或等号(=)，则在特殊字符之前使用转义字符(&quot;\_)。 例如，指定名为“标题，1”的样式作为“标题\，1”。

**Acrobat PDFMaker编码：**&#x200B;指定Acrobat PDFMaker的输入纯文本文件的编码类型。 例如，如果您使用的是UTF-8编码文件，请选择UTF-8以获得最佳结果。

## Microsoft Visio设置（仅限Windows） {#visio}

**转换文档信息**：从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。 默认情况下，该选项处于选中状态。 此选项默认处于启用状态。

**添加指向Adobe PDF的链接**：保留所有链接。 默认情况下，该选项处于选中状态。

**将书签添加到Adobe PDF**：将标题转换为书签。 默认情况下，该选项处于选中状态。

**将Source文件附加到Adobe PDF**：将源文件作为附件添加到PDF文件中。

**在Adobe PDF中始终拼合图层**：拼合所有Visio图层。

**转换所有页面**：转换Visio文件的所有页面。

**在Adobe Acrobat中查看时打开图层面板**：如果Visio图层未拼合，将打开一个窗口，您可以在其中指定使用Acrobat打开时保留在PDF文件中的图层。 默认情况下，该选项处于选中状态。

**创建PDF/A-1b兼容文件**：强制使用Adobe PDF设置PDF/A-1b：2005(RGB)。

**将注释转换为Adobe PDF注释**：将Visio注释转换为PDF注释。

## Microsoft Publisher设置（仅限Windows） {#microsoft-publisher-settings-windows-only}

这些选项决定如何转换Microsoft Publisher文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](#create-or-edit-file-type-settings)。

**[!UICONTROL 文件扩展名]**：指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为`pub`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

## AutoCAD设置（仅限Windows） {#autocad-settings-windows-only}

这些选项决定如何转换AutoCAD文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**[!UICONTROL 文件扩展名]**：指定此应用程序可接受的以逗号分隔的文件类型的文件扩展名。 默认值为`dwg`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

**[!UICONTROL 转换文档信息]**：从源文件的“属性”对话框添加文档信息，包括标题、主题、作者、关键字、经理、公司、类别和注释。 默认情况下，该选项处于选中状态。

**[!UICONTROL 将书签添加到Adobe PDF]**：将标题转换为书签。

**[!UICONTROL 在Adobe PDF中始终拼合图层]**：拼合所有AutoCAD图层。

**[!UICONTROL 在Adobe Acrobat中查看时打开图层窗格]**：在Acrobat中打开PDF时显示图层结构。

**[!UICONTROL 转换所有布局]**：包括PDF中的所有布局。

**[!UICONTROL 将模型空间转换为3D]**：在选中时，模型空间布局将转换为PDF中的3D批注。

**[!UICONTROL 添加指向Adobe PDF的链接]**：如果选定此选项，将保留所有链接。

**[!UICONTROL 将Source文件附加到Adobe PDF]**：将源文件作为附件添加到PDF文件中。

**[!UICONTROL 创建PDF/A-1b兼容文件]**：强制使用PDF/A-1b Adobe PDF设置。

**[!UICONTROL 转换所有图层]**：默认情况下，PDF Generator仅将AutoCAD文件的默认图层转换为PDF，而不是文件中的所有图层。 选择此选项可转换文件的所有层。

**[!UICONTROL 嵌入比例信息]**：保留绘图比例信息。

**[!UICONTROL 转换当前布局]**：仅包括PDF中的当前布局。

**[!UICONTROL 要转换的AutoCAD布局列表]**： AutoCAD绘图可以有多个布局。 如果此框为空，则AutoCAD绘图中的所有布局都将包含在生成的PDF文档中。 要选择性地转换布局的子集，请提供以逗号分隔的布局名称列表。

## OpenOffice设置 {#openoffice-settings}

这些选项决定如何转换OpenOffice文件。 有关访问这些选项的说明，请参阅[创建或编辑文件类型设置](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings)。

**尝试将PDFMaker作为回退转换器**：如果选中了此选项，并且使用OpenOffice的转换失败或达到指定的超时限制，则PDF Generator将尝试使用PDFMaker进行转换。 如果使用PDFMaker的转换失败或达到指定的超时限制，则会将异常写入日志文件。

**文件扩展名**：为此应用程序接受的文件类型指定文件扩展名（以逗号分隔）。 默认值为`odt,odp,ods,odg,odf,sxw,sxi,sxd`。 不要在扩展之前添加句点，也不要在扩展之间添加空格。

**范围**：转换所有页面，或指定特定页面或页面范围。 如果未定义页面范围，则会转换所有页面。 要导出一定范围的页面，请使用格式3-6。 要导出单个页面，请使用格式7；9；11。 您可以使用格式（如3-6；8；10；12）导出页面范围和单个页面的组合。

**页面方向**：仅对于纯文本文件，请为转换的PDF文档选择纵向或横向。

**图像**：配置图像的转换方式。 包含嵌入预览的EPS图像仅导出为预览。 没有嵌入预览的EPS图像将导出为空占位符。 通过对图像进行无损压缩，可以保留所有像素。 由于图像的JPEG压缩和高质量级别，因此几乎所有的像素都被保留。 在低质量级别，某些像素会丢失并引入伪像，但文件大小会减小。

**常规**：启用转换带标签的PDF、导出Writer和FormCalc文档注释、Impress幻灯片过渡效果或空白页到PDF的选项。 导出标记时，文件大小可能会大幅增加。 有些导出的标记是目录、超链接和控件。

您还可以指定提交表单的方式。 选项有XML、FDF、PDF或HTML。 此设置将覆盖您在文档中设置的控件的URL属性。 只能为PDF文档选择一个通用设置：

* PDF（发送整个文档）
* FDF（发送控制内容）
* HTML
* XML

**标记PDF**：允许从OpenOffice文档创建标记PDF。 已标记的PDF包含有关文档内容结构的信息。 当在具有不同屏幕的设备上显示文档时，以及使用屏幕阅读器软件时，此功能会有所帮助。 它还有助于辅助功能软件对PDF文档执行各种有用的操作，例如大声阅读PDF文档的内容。

**导出注释**：将OpenOffice文档中的注释转换为生成的PDF文档中的注释。

**使用过渡效果**：将OpenOffice演示文稿中的幻灯片过渡效果转换为相应的PDF过渡效果。

**以格式提交Forms**：创建一个PDF表单，该表单可由PDF文档的用户填写和打印。

**导出自动插入的空白页**：选中此选项时，生成的PDF文档中包含自动插入的空白页。 如果要双面打印PDF文档，则此功能非常有用。 例如，可以配置一本书籍，使章节的第一页始终从奇数页开始。 如果上一章以奇数页结尾，则OpenOffice会插入空白的偶数页。 此选项控制是否在生成的PDF中包含该偶数页。

## 其他应用程序设置（仅限Windows） {#other-applications-settings-windows-only}

您不能通过管理控制台更改其他应用程序的设置；它们显示所支持文件类型的文件扩展名。 有关访问这些设置的说明，请参阅[创建或编辑文件类型设置](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)。

* Corel WordPerfect： `wpd`
* AdobePageMaker： `pmd, pm6, p65, pm`
* Adobe FrameMaker： `fm`
* Adobe Photoshop： `psd`

可能需要自定义对这些文件类型的支持。 有关详细信息，请参阅[使用AEM Forms编程](https://www.adobe.com/go/learn_aemforms_programming_62)中的“添加对其他本机文件格式的支持”。

有关配置PDFG网络打印机的帮助，请参阅[设置PDFG网络打印机（仅限Windows）](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md)。
