---
title: 配置Adobe PDF设置
seo-title: 配置Adobe PDF设置
description: 了解如何配置Adobe PDF设置。
seo-description: 了解如何配置Adobe PDF设置。
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: PDF 生成器
exl-id: 1bcb8429-c06e-4bd3-b422-4c512084dd09
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '7278'
ht-degree: 0%

---

# 配置Adobe PDF设置{#configuring-adobe-pdf-settings}

“Adobe PDF设置”页面显示可为源指定的转换设置。 您可以使用任何预定义的PDF设置，也可以创建您自己的PDF设置。 PDF设置可准确确定文件的转换方式及其生成的PDF结构和功能。 Adobe PDF设置以前称为Distiller®参数或作业选项。

在Adobe PDF设置页面上，您可以执行以下任务：

* 查看预定义的PDF设置。 （请参阅[关于预定义的PDF设置](configuring-pdf-settings.md#about-the-predefined-pdf-settings)。）
* 创建PDF设置或编辑您之前创建的设置。 （请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。）
* 指定默认PDF设置。 （请参阅[更改默认设置](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)）
* 将PDF设置文件上传到服务器。 （请参阅[上传PDF设置](configuring-pdf-settings.md#upload-pdf-settings)。）
* 删除自定义PDF设置。 （请参阅[删除PDF设置](configuring-pdf-settings.md#delete-pdf-settings)。）
* 上传和下载原版和尾文件。 （请参阅[上载和下载序列和尾文件](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files)。）

Adobe PDF设置仅适用于基于PDFMaker的转化。 这些转化包括以下转化：

* Microsoft Word文档(DOC、DOCX、RTF、TXT)
* Microsoft Excel文档(XLS、XLSX)
* Microsoft PowerPoint文档(PPT、PPTX)
* Microsoft Project文档(MPP)
* Microsoft Visio文档(VSD)

>[!NOTE]
>
>使用OpenOffice转换上述格式时，不会应用Adobe PDF设置。

## 关于预定义的PDF设置{#about-the-predefined-pdf-settings}

PDF生成器提供了一些预定义的PDF设置供您使用。 您无法修改这些预定义设置；但是，您可以通过编辑设置并使用新名称将其保存来基于现有设置创建设置。

**高质量打印：** 为高质量输出创建PDF文件。此设置：

* 以300 dpi对彩色和灰度图像进行缩减像素采样
* 以1200 dpi对单色图像进行降采样
* 打印到更高的图像分辨率
* 使用其他设置来保留与原始文档有关的最大信息量。

这些PDF文件可在Adobe Acrobat 5和Adobe AcrobatReader® 5或更高版本中打开。

**超大页面：** 创建PDF文档，以便可靠地查看和打印大于200 x 200英寸的工程图。创建的PDF文档可以在Adobe Acrobat Professional和Acrobat Standard、版本7或更高版本以及Adobe Reader 7或更高版本中打开。

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** 检查传入的作业是否符合ISO标准以长期保留（存档）电子文档，并仅在符合时创建PDF/A文件。这些文件主要用于存档。 兼容文件只能包含文本、光栅图像和矢量对象；它们不能包含加密和脚本。 此外，必须嵌入所有字体，才能打开文档并在创建时查看文档。 PDF/A-1b使用PDF 1.4，并根据您选择的标准将所有颜色转换为CMYK或RGB。 可以在Acrobat 5和Acrobat Reader 5及更高版本中打开使用此设置文件创建的PDF文件。 有关PDF/A的更多信息，请参阅Adobe和行业标准。

**PDF/X-1a 2001:** 检查传入的作业是否符合PDF/X-1a规范，并仅在符合规范时创建PDF文件。PDF/X-1a是用于图形内容交换的ISO标准。 PDF/X-1a要求嵌入所有字体，指定相应的PDF框，并且颜色显示为CMYK或专色。 满足PDF/X-1a要求的PDF文件针对特定输出条件，例如根据规范Web Offset Publications进行Web Offset Printing。 有关PDF/X的更多信息，请参阅Adobe和行业标准。

**PDF/X-3 2002:** 检查传入的作业是否符合PDF/X-3规范，并仅在符合规范时创建PDF文件。与PDF/X-1a类似，PDF/X-3是用于图形内容交换的ISO标准。 主要区别在于PDF/X-3支持与设备无关的颜色。

**按质量：** 创建PDF文件以用于高质量打印生产（例如，在照排机或制版机上）。在这种情况下，不考虑文件大小。 其目标是维护PDF文件中商业打印机或印前服务提供商正确打印文档所需的所有信息。 以下选项集：

* 以300 dpi对彩色和灰度图像进行缩减像素采样
* 以1200 dpi对单色图像进行降采样
* 嵌入文档中使用的所有字体的子集
* 打印到更高的图像分辨率，
* 不会根据文本或文档结构约定(DSC)注释的方向自动旋转页面
* 使用其他设置来保留与原始文档有关的最大信息量。

如果打印作业的字体无法嵌入，则打印作业会失败。 这些PDF文件可在Acrobat 5和Acrobat Reader 5及更高版本中打开。

>[!NOTE]
>
>在创建PDF文件以发送给商业打印机或印前服务提供商之前，请确定输出分辨率和其他设置，或使用建议的设置请求.joboptions文件。 您可能需要为特定提供商自定义Adobe PDF设置，然后提供您自己的.joboptions文件。

**最小文件大小：** 创建PDF文件，以在Web或内联网上显示，或通过电子邮件系统分发以便在屏幕上查看。这组选项使用压缩、缩减采样和相对较低的图像分辨率。 它会将所有颜色转换为sRGB，除非必要，否则不会嵌入字体。 它还会优化用于字节提供的文件。 这些PDF文件可在Acrobat 5和Acrobat Reader 5.0及更高版本中打开。

**标准：** 创建PDF文件以打印到桌面打印机或数字复印机、在CD上发布或作为发布校样发送到客户端。这组选项使用压缩和缩减采样来减小文件大小。 它还嵌入文件中使用的所有字体的子集，将所有颜色转换为sRGB，并打印到中等分辨率，以创建原始文档的相当准确的呈现版本。 请注意，默认情况下未嵌入Microsoft Windows字体子集。 这些PDF文件可在Acrobat 5和Acrobat Reader 5.0及更高版本中打开。

## 添加或编辑PDF设置{#add-or-edit-pdf-settings}

PDF设置可准确确定文件的转换方式及其生成的PDF结构和功能。 定义新的PDF设置或编辑您之前创建的设置。 您无法修改预定义的设置，但可以根据现有设置创建设置，方法是编辑该设置并使用新名称保存该设置。

1. 在管理控制台中，单击服务> PDF生成器> Adobe PDF设置。
1. 单击“新建”或单击现有设置的名称。
1. 在新建/编辑Adobe PDF设置页面中，完成以下部分中的必需信息：

[常规选项](configuring-pdf-settings.md#general-options)

[图像选项](configuring-pdf-settings.md#images-options)

[字体选项](configuring-pdf-settings.md#fonts-options)

[颜色选项](configuring-pdf-settings.md#color-options)

[高级选项](configuring-pdf-settings.md#advanced-options)

[标准报告和合规选项](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

[初始视图选项](configuring-pdf-settings.md#initial-view-options)

   要转到其他部分，请单击其网页上的链接，或使用“下一步”和“上一步”按钮。

1. 完成所有部分中的信息后，单击保存或另存为，并提供设置的名称。

## 上传PDF设置{#upload-pdf-settings}

您可以通过从本地计算机或网络位置上传PDF设置，在PDF生成器服务器上提供PDF设置。

1. 在管理控制台中，单击“服务”>“PDF生成器”>“Adobe PDF设置”，然后单击“上传”。
1. 在上传Adobe PDF设置页面上，单击浏览，找到PDF设置文件，然后单击打开。
1. 单击“确定”，然后再次单击“确定”。

## 删除PDF设置{#delete-pdf-settings}

如果不再需要PDF设置，您可以永久删除这些设置。

1. 在管理控制台中，单击服务> PDF生成器> Adobe PDF设置。
1. 选中要删除的设置旁边的复选框。 您可以选择多个设置。
1. 单击删除，然后在“删除确认”页面上再次单击删除。

## 常规选项{#general-options}

使用常规选项指定用于文件兼容性的Acrobat版本以及其他文件和设备选项。 有关访问“常规”选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

### 文件选项{#file-options}

**兼容性：** PDF文件的兼容性级别。对于将广泛分发的文档，请考虑选择Acrobat 4(PDF 1.3)或Acrobat 5(PDF 1.4)，以确保所有用户都可以查看和打印文档。 如果您使用Acrobat 5兼容性或更高版本创建文件，则它们可能与Acrobat的早期版本不兼容。 以下子部分显示了使用不同级别的Acrobat兼容性创建的PDF文件之间的一些差异。

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4(PDF 1.3)</p> </th>
   <th><p>Acrobat 5(PDF 1.4)</p> </th>
   <th><p>Acrobat 6(PDF 1.5)</p> </th>
   <th><p>Acrobat 7(PDF 1.6)和Acrobat 8(PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>可在Acrobat 3.0和Acrobat Reader 3.0及更高版本中打开。</p> </td>
   <td><p>可在Acrobat 3.0和Acrobat Reader 3.0及更高版本中打开。 特定于较新版本的功能可能丢失或不可查看。</p> </td>
   <td><p>大多数内容可在Acrobat 4和Acrobat Reader 4.0及更高版本中打开。 特定于较新版本的功能可能丢失或不可查看。</p> </td>
   <td><p>大多数内容可在Acrobat 4和Acrobat Reader 4.0及更高版本中打开。 特定于较新版本的功能可能丢失或不可查看。</p> </td>
  </tr>
  <tr>
   <td><p>不能包含使用实时透明效果的图稿。 转换为PDF 1.3之前，必须对任何透明度进行扁平化处理。</p> </td>
   <td><p>支持在图稿中使用实时透明度。 (Acrobat Distiller功能拼合透明度。)</p> </td>
   <td><p>支持在图稿中使用实时透明度。 (Acrobat Distiller功能拼合透明度。)</p> </td>
   <td><p>支持在图稿中使用实时透明度。 (Acrobat Distiller功能拼合透明度。)</p> </td>
  </tr>
  <tr>
   <td><p>不支持层。</p> </td>
   <td><p>不支持层。</p> </td>
   <td><p>从支持生成分层PDF文档的应用程序(如Adobe Illustrator® CS或Adobe InDesign® CS及更高版本)创建PDF文件时保留图层。</p> </td>
   <td><p>在从支持生成分层PDF文档的应用程序(如Illustrator CS或InDesignCS及更高版本)创建PDF文件时保留图层。</p> </td>
  </tr>
  <tr>
   <td><p>支持具有8种颜料的DeviceN色彩空间。</p> </td>
   <td><p>支持具有8种颜料的DeviceN色彩空间。</p> </td>
   <td><p>支持最多31种颜色的DeviceN色彩空间。</p> </td>
   <td><p>支持最多31种颜色的DeviceN色彩空间。</p> </td>
  </tr>
  <tr>
   <td><p>可以嵌入多字节字体。 (Distiller在嵌入时转换字体。)</p> </td>
   <td><p>可以嵌入多字节字体。</p> </td>
   <td><p>可以嵌入多字节字体。</p> </td>
   <td><p>可以嵌入多字节字体。</p> </td>
  </tr>
  <tr>
   <td><p>支持40位RC4安全性。</p> </td>
   <td><p>支持128位RC4安全。</p> </td>
   <td><p>支持128位RC4安全。</p> </td>
   <td><p>支持128位RC4和128位AES（高级加密标准）安全性。</p> </td>
  </tr>
 </tbody>
</table>

**对象级别压缩：** 将小对象（每个对象本身不可压缩）合并到流中，之后可以高效压缩这些流。

**关闭：** 不压缩PDF文档中的任何结构信息。如果希望用户使用Acrobat 5及更高版本查看、导航书签和其他结构性信息并与之交互，请选择此选项。

**仅限标记：** 压缩PDF文档中的结构信息。使用此选项可生成一个PDF文件，该文件可使用Acrobat 5打开和打印。 用户无法在Acrobat 5或Acrobat Reader 5.0中查看任何辅助功能、结构或带标签的PDF信息，但他们可以在Acrobat 6和Adobe Reader 6.0中查看此信息。

**自动旋转页面：** 根据文本或DSC注释的方向设置页面的自动旋转。例如，某些页面（例如包含表格的页面）可能要求用户侧翻这些页面来阅读它们。 选择“逐个”以根据该页面上文本的方向旋转每个页面。 选择“按文件集中”，以根据大多数文本的方向旋转文档中的所有页面。

>[!NOTE]
>
>如果在“高级”设置中选择了“处理DSC注释”，并且包含%%查看方向注释，则在确定页面方向时，这些注释优先。

**绑定：** 指定是显示具有左侧绑定还是右侧绑定的PDF文件。此设置会影响面向页面 — 连续布局中页面的显示以及缩略图的并排显示。

**分辨率：** 为输入文件设置打印机分辨率的模拟，这些输入文件根据打印到的打印机的分辨率调整其行为。对于大多数输入文件，分辨率较高的设置会生成较大但质量较高的PDF文件，而设置较低的设置会生成较小但质量较低的PDF文件。 通常，分辨率决定渐变或混合中的步骤数。 您可以输入一个介于72到4000之间的值。 将此设置保留为默认设置，除非您计划将PDF文件打印到特定打印机，并且希望模拟原始输入文件中定义的分辨率。

>[!NOTE]
>
>提高分辨率设置会增加文件大小，并可能会略微增加处理某些文件所需的时间。

**所有页面或页面来源：** 指定要转换的页面。将“收件人”框留空，以创建从您在“发件人”框中输入的页码到文件末尾的范围。

**为快速Web查看而优化：** 重新构建文件，以便从Web服务器进行逐页下载（字节服务）。无论您在“图像”选项卡上选择了什么压缩设置，此选项都会压缩文本和线条图。 从Web或网络下载文件时，压缩可加快访问和查看速度。 默认情况下，此选项处于未启用状态。

### 默认页面大小{#default-page-size}

“默认页面大小”选项指定在原始文件中未指定页面大小时要使用的页面大小。 通常，Adobe PostScript文件会包含此信息，但封装的PostScript(EPS)文件除外，这些文件会给出定界框大小，但不提供页面大小。 允许的最大页面大小在任一方向为15,000,000英寸（31,800,000厘米）。 以下选项配置默认页面大小：

**宽度：** 页面宽度

**高度：** 页面高度

**件数：** 用于宽度和高度设置的件数

## 图像选项{#images-options}

“图像”选项可为图像指定压缩和重新取样。 您可以试用这些选项，在文件大小和图像质量之间找到适当的平衡。 有关访问“图像”设置的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

这些选项可配置颜色、灰度和单色图像：

**缩减采样：** 为每种类型的图像设置一个值。要缩减彩色、灰度或单色图像的采样，PDF生成器会将采样区域中的像素组合在一起，使一个像素变大。 以每英寸点数(dpi)提供输出设备的分辨率，并在“用于上图像”框中输入dpi分辨率。 对于分辨率超过此阈值的图像，PDF生成器会根据需要组合像素，以将图像的分辨率（每英寸像素数）降低到指定的dpi设置。 要关闭缩减采样，请选择“关闭”。 以下是选项：

**平均缩减采样到：** 平均采样区域中的像素数，并以指定分辨率的平均像素颜色替换整个区域。

**双立方缩减采样至：** 使用加权平均来确定像素颜色，并且通常比简单的缩减采样平均方法获得更好的结果。双立方是最慢但最精确的方法，可产生最平滑的色调渐变。

**子采样至：** 选择采样区域中心的像素，并以指定分辨率将整个区域替换为该像素。与缩减采样相比，子采样可显着缩短转换时间，但会导致图像不那么平滑和连续。

颜色和灰度的分辨率设置应是确定文件打印位置的行屏幕的1.5到2倍。 （如果不低于此建议的分辨率设置，则不包含直线、几何或重复图案的图像不会受到较低分辨率的影响。） 单色图像的分辨率应与输出设备相同。 但是，请注意，将单色图像保存为高于1500 dpi的分辨率会增加文件大小，而不会显着提高图像质量。

此外，还应考虑用户是否需要放大页面。 例如，如果您要创建地图的PDF文档，请考虑使用更高的图像分辨率，以便用户能够放大地图。

>[!NOTE]
>
>重新取样单色图像可能会产生意外的查看结果，例如没有图像显示。 如果出现此问题，请关闭重新取样并再次转换文件。 子采样最有可能出现此问题，而双立方缩减采样最不可能出现此问题。

此表显示了打印机的类型及其分辨率（以dpi测量）、默认屏幕规则(以每英寸线数(lpi)测量)以及以每英寸像素数(ppi)测量的图像的重新取样分辨率。 例如，要打印到600 dpi激光打印机，请输入170作为分辨率，以重新采样图像。

<table>
 <tbody>
  <tr>
   <th><p>打印机分辨率</p> </th>
   <th><p>默认行屏幕</p> </th>
   <th><p>图像分辨率</p> </th>
  </tr>
  <tr>
   <td><p>300 dpi（激光打印机）</p> </td>
   <td><p>60lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi（激光打印机）</p> </td>
   <td><p>85lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi（照排机）</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi（照排机）</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

**压缩：** 设置一个值，以应用于彩色、灰度和单色图像。对于彩色和灰度图像，还应设置图像质量：

* 对于彩色或灰度图像，选择ZIP可对具有较大区域的单色或重复图案的图像应用效果良好的压缩。 示例包括屏幕截图、使用绘画程序创建的简单图像以及包含重复模式的单色图像。 选择“JPEG”（质量最小到最大），以应用适合灰度或彩色图像的压缩，例如包含比屏幕或打印中可再现的更多细节的连续色调照片。 选择“自动(JPEG)”以自动确定彩色和灰度图像的最佳质量。
* 对于单色图像，请选择“CCITT组4”、“CCITT组3”、“ZIP”、“JPEG200”、“自动(JPEG2000)”或“运行长度压缩”。

确保将单色图像扫描为单色图像，而不是灰度图像。 默认情况下，扫描的文本有时会另存为灰度图像。 使用JPEG压缩方法压缩的灰度文本不清晰，可能无法读取。

**图像质量：** 配置彩色和灰度图像的图像质量。选项有最小值、低值、中值、高值和最大值。

**消除锯齿为灰色：** 平滑单色图像中的锯齿边缘。选择2位、4位或8位以指定4、16或256级灰色。 （消除锯齿可能会模糊小文字或细线。）

>[!NOTE]
>
>文本和线条图的压缩始终处于打开状态。

**图像策略：** 为彩色、灰度和单色图像设置策略。如果图像分辨率低于指定的分辨率，您仍可以选择继续（忽略）、提供警告消息或取消作业。

## 字体选项{#fonts-options}

“字体”选项指定要嵌入PDF文件的字体，以及是否嵌入PDF文件中使用的字符子集。 有关访问“字体”选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

>[!NOTE]
>
>当您将PDF文件与同一字体子集合并时，PDF生成器会尝试合并字体子集。

**嵌入所有字体：** 嵌入文件中使用的所有字体。要符合PDF/X规范，需要嵌入字体。

**使用的字符百分比小于时，嵌入字体的子集：** 如果选择此选项，请指定一个阈值百分比，以仅嵌入字体的子集。例如，如果阈值为35，而使用的字符数少于35%，则PDF生成器仅嵌入这些字符。 只嵌入具有适当权限位的字体。

**嵌入失败时：** 指定在处理文件时找不到要嵌入的字体时PDF生成器如何响应。您可以让PDF生成器忽略请求并替换字体，警告您并替换字体，或取消当前作业的处理。

**字体源：** PDF生成器使用的字体的位置。

### 指定要嵌入的字体{#specify-which-fonts-to-embed}

1. 在管理控制台中，单击服务> PDF生成器> Adobe PDF设置。
1. 单击“新建”或单击设置的名称。
1. 单击“字体”并取消选择“嵌入所有字体”。
1. 从“字体源”列表中，选择一个字体源，然后单击“开始”以刷新左侧框中的字体列表。
1. 单击左侧框中的字体。 然后，单击相应框旁边的添加，以将其移至始终嵌入列表或从不嵌入列表。 对每种字体重复执行上述步骤。 按住Ctrl键并单击以选择多个要移动的字体。
1. 要从“始终嵌入”或“从不嵌入”列表中删除字体，请选择该字体，然后单击相应框旁边的“删除”。 此操作不会从系统中删除字体；它只会删除列表中对它的引用。
1. 如果您要指定的字体未显示，请在“添加字体”框中键入其名称，然后单击“始终嵌入”或“从不嵌入”。 字体名称不能包含字母数字字符。

>[!NOTE]
>
>TrueType字体可以包含字体设计器添加的设置，该设置可防止字体嵌入PDF文件中。

>[!NOTE]
>
>从Windows系统字体缓存中选取字体，并且需要系统重新启动才能更新缓存。 指定客户字体目录后，请确保重新启动安装AEM表单的系统。

## 颜色选项{#color-options}

“颜色”选项可设置PDF生成器的所有颜色管理信息。 有关访问“颜色”选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

### Adobe Color设置{#adobe-color-settings}

**设置文件：** 此列表包含一个颜色设置列表，这些设置也在主要图形应用程序(如Adobe Photoshop和Adobe Illustrator)中使用。您选择的颜色设置决定了此页面上的其他Adobe颜色设置。 例如，如果选择“无”以外的设置，则除“设备相关数据”选项之外的所有选项都将进行预定义并变暗。 只有在为“设置文件”选择“无”时，才能编辑“色彩管理策略”和“工作空间”设置。

### 色彩管理策略{#color-management-policies}

如果为“设置文件”选择了“无”，则“色彩管理策略”区域会指定PDF生成器如何在PostScript文件中转换非托管颜色。

**保持颜色不变：** 保持与设备相关的颜色不变，并将与设备无关的颜色保留为PDF中最接近的等效颜色。此选项对于打印已校准其所有设备的商店、使用该信息在文件中指定颜色并仅输出到这些设备非常有用。

**为色彩管理添加所有标签：** 在提取文件和校准图像中的颜色时，嵌入国际色彩联盟配置文件，这样在您选择Acrobat 4(PDF 1.3)或更高版本兼容性时，生成的PDF文件中的颜色就与设备无关。但是，文件（RGB、灰度和CMYK）中与设备相关的色彩空间会转换为与设备无关的色彩空间（CalRGB、CalGray和LAB）。

**仅标记用于色彩管理的图像：** 如果您选择了Acrobat 4(PDF 1.3)兼容性，则在提取文件时，ICC配置文件仅嵌入在图像中，而不嵌入文本或图形中。此选项可防止黑色文本发生任何颜色偏移。 但是，图像中与设备相关的色彩空间（RGB、灰度和CMYK）会转换为与设备无关的色彩空间（CalRGB、CalGray和LAB）。 文本和图形不会转换。

**将所有颜色转换为sRGB或将所有颜色转换为CMYK:** 在文件中校准颜色，使颜色设备与颜色设备无关，与“标记色彩管理的所有内容”类似。如果选择Acrobat 4(PDF 1.3)或更高版本的兼容性并转换为sRGB，则CMYK和RGB图像将转换为sRGB。

无论选择何种兼容性选项，灰度图像都保持不变。 这通常会减小PDF文件的大小并提高PDF文件的显示速度，因为描述RGB图像所需的信息比描述CMYK图像所需的信息少。 由于RGB是显示器上使用的本机颜色空间，因此在显示过程中无需进行颜色转换，这有助于快速联机查看。 如果PDF文件用于联机或与低分辨率打印机一起使用，则建议使用此选项。

**文档渲染意图：** 在色彩空间之间映射颜色的方法。任何特定方法的结果取决于色彩空间的配置文件。 例如，某些用户档案会使用不同方法产生相同的结果。 以下选项可用：

>[!NOTE]
>
>在所有情况下，在创建PDF文件后发生的色彩管理操作都可能会忽略意图或覆盖意图。

**保留：** 表示意图是在输出设备中指定，而不是在PDF文件中指定。在许多输出设备中，“相对比色”是缺省目的。

**感知：** 在原始像素映射到目标色域时，维护这些像素之间的相对颜色值。尽管颜色值本身可能会发生更改，但此方法可保留颜色之间的视觉关系。

**饱和度：** 保持原始像素的相对饱和度值。该方法适用于商业图形，其中颜色之间的确切关系不像具有明亮饱和颜色那么重要。

**相对比色：** 将源空间的白点重新映射到目标空间的白点。

**绝对比色：** 在转换颜色时禁用白点和黑点的匹配。除非您必须保留签名颜色（如商标或徽标中使用的颜色），否则不建议使用此方法。

### 工作空间{#working-spaces}

对于“色彩管理策略”下列表中除“保持色彩不变”之外的所有值，从“工作空间”区域的列表中选择，以指定用于定义和校准蒸馏PDF文件中的灰度、RGB和CMYK色彩空间的ICC配置文件。 以下选项可用：

**灰色：** 定义文件中所有灰度图像的颜色空间。仅当您为“颜色管理”选择“标记所有”或为“颜色管理”选择“仅标记图像”时，此选项才可用。 灰度图像的默认ICC配置文件为灰度Gamma 2.2。您还可以选择“无”以阻止灰度图像被转换。

**RGB:** 定义文件中所有RGB图像的颜色空间。默认的sRGB IEC61966-2.1选项通常是一个好选项，因为它正在成为行业标准，许多输出设备都能识别它。 您还可以选择“无”以阻止RGB图像转换。

**CMYK:** 定义文件中所有CMYK图像的色彩空间。默认为US Web Coated(SWOP)v2。 您还可以选择“无”以阻止CMYK图像转换。

>[!NOTE]
>
>为所有三个工作空间选择“无”与选择“保持颜色不变”具有相同的效果。

**为已校准的CMYK色彩空间保留CMYK值：** 选中后，与设备无关的CMYK值将被视为与设备相关的(DeviceCMYK)值，丢弃与设备无关的色彩空间，PDF/X-1a文件使用“将所有颜色转换为CMYK值”。取消选择后，如果颜色管理策略设置为“将所有颜色转换为CMYK”，则与设备无关的色彩空间将转换为CMYK。

### 与设备相关的数据{#device-dependent-data}

如果您使用的是使用高端文档和图形应用程序(如Adobe Illustrator和Adobe InDesign)创建的文档，则这些选项适用。 有关更多信息，请参阅应用程序附带的文档。

传送功能用于艺术效果并根据特定输出装置的规格进行调整。 例如，用于在特定的照排机上输出的文件可以包含补偿该打印机固有的点增益的传输函数。

**在“颜色移除”和“黑色生成”下保留：** 如果这些设置存在于PostScript文件中，则保留这些设置。黑色生成计算您尝试重现特定颜色时要使用的黑色量。 减色(UCR)会减少青色、洋红和黄色成分的量，以补偿黑色层添加的黑色量。 由于UCR使用的油墨较少，因此UCR通常用于新闻纸和无涂层纸。

**找到传输函数时：** 确定找到传输函数时要执行的操作：

**保留：** 保留传统上用于补偿在图像传输到胶片时可能出现的点增益或点损失的传递函数。当构成打印图像的墨点比半色调网中的墨点大（例如，由于在纸上铺展）时，会出现点增益；当点打印较小时，会出现点丢失。 使用此选项，传输函数将作为文件的一部分保留，并在输出文件时应用于文件。

**应用：** 不保留传输函数，但将其应用于文件，从而更改文件中的颜色。此选项对于在文件中创建色彩效果非常有用。 默认情况下，会为新设置选中此选项。

**删除：** 删除所有应用的传输函数。删除已应用的传输函数，除非PDF文件将输出到为其创建源PostScript文件的相同设备。

**保留半色调信息：** 在文件中保留任何半色调信息。半色调信息由控制油墨半色调设备在纸张上特定位置的沉积量的点组成。 更改点大小和密度会产生灰色或连续颜色变化的错觉。 对于CMYK图像，使用四个半色调网屏，每个油墨在打印过程中使用一个。

在传统印刷制作中，半色调是通过将半色调网置于薄膜和图像之间，然后曝光该薄膜来制造的。 电子等效项(如在Adobe Photoshop中)允许用户在生成胶片或纸张输出之前指定半色调网屏属性。 半色调信息用于特定输出设备。

## 高级选项 {#advanced-options}

“高级”选项指定要保留在PDF文件中的文档结构约定(DSC)注释，以及如何设置影响从PostScript转换的其他选项。 在PostScript文件中，DSC注释包含有关该文件的信息（如原始应用程序、创建日期和页面方向）。 它们还为文件中的页面描述提供了结构（如prolog部分的开始和结束语句）。 当您的文档要打印或按时，DSC注释会很有用。 有关访问“高级”选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

使用“高级”选项时，了解PostScript语言及其如何翻译为PDF将会很有帮助。 (请参阅[Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html)。)

**允许PostScript文件覆盖Adobe PDF设置：** 使用存储在PostScript文件中的设置，而不是当前的Adobe PDF设置文件。在处理PostScript文件之前，可以将参数放置在文件中以控制以下方面：

* 文本和图形的压缩
* 采样图像的缩减采样和编码
* 嵌入1类字体和1类多主控字体实例

**允许PostScript XObjects:** PostScript XObjects存储在同一文件的许多页面上显示的信息，如背景图像或页眉和页脚信息。使用PostScript XObjects可加快打印速度，但需要更多打印机内存。 要阻止创建PostScript XObjects，如果创建的PDF文件与Acrobat 5(PDF 1.4)或更高版本兼容，请取消选择此选项。

**将渐变转换为平滑阴影：** 将混合颜色转换为Acrobat 4及更高版本的平滑阴影，从而缩小PDF文件，并可能提高最终输出的质量。PDF生成器可转换来自Adobe Illustrator、Adobe InDesign、Adobe FreeHand MX、CorelDraw、Quark Xpress和Microsoft PowerPoint的渐变。

**将平滑线转换为曲线：** 减少在CAD绘图中构建曲线的控制点数量，这样可减少PDF，并加快屏幕渲染速度。

**保留2级复制页面语义：** 使用在LanguageLevel 2 PostScript中定义的复制页面运算符，而不是在LanguageLevel 3 PostScript中定义的运算符。如果您有一个PostScript文件并选择此选项，则复制页面运算符会复制该页面。 如果未选择此选项，则执行showpage操作的等效操作，但图形状态未重新初始化。

**保留叠印设置：** 保留将转换为PDF的文件中的任何叠印设置。叠印的颜色是彼此顶部印刷的两种或多种油墨。 例如，当青色油墨在黄色油墨上打印时，生成的叠印为绿色。 如果不进行叠印，则不会打印底下的黄色，从而产生青色。

**叠印默认值为非零叠印：** 防止具有零CMYK值的叠印对象击出它们下面的CMYK对象。在PDF文件中插入OPM 1图形状态参数，只要存在Setoverprint运算符，就可以实现此效果。

**将Adobe PDF设置保存在PDF文件中：** 嵌入用于创建PDF文件的设置文件。您可以在Acrobat的“文件附件”对话框中打开并查看设置文件（文件扩展名为.joboptions）。 Adobe PDF设置文件将成为PDF文件内EmbeddedFiles树中的项目。

**尽可能将原始JPEG图像保存在PDF中：** 处理任何压缩的JPEG图像（已使用DCT编码压缩的图像），而不重新压缩它们。如果选择此选项，PDF生成器会解压缩JPEG图像，以确保它们不会损坏。 但是，它不会重新压缩有效图像，因此会处理未触发的原始图像。 选择此选项后，性能会提高，因为只执行解压缩（而不是重新压缩），并且图像数据和元数据会保留。

**在PDF文件中保存可移植的作业票证：** 在PDF文件中保留PostScript作业票证。作业票证包含有关PostScript文件的信息（如页面大小、分辨率和陷印信息），而不是有关内容的信息。 此信息稍后可在工作流中使用或用于打印PDF。

**使用Prolog.ps和Epilog.ps:** 发送每个作业的prolog和epilog文件。这些文件有多种用途。 例如，可以编辑prolog文件以指定封面。 可以编辑尾文件以解析PostScript文件中的一系列过程。 您可以上传或下载文件。 （请参阅上传和下载原版和尾文件。）

**处理DSC注释：** 维护PostScript文件中的DSC信息。以下子选项可用：

**记录DSC警告：** 显示有关处理过程中出现问题的DSC注释的警告消息，并将它们添加到日志文件中。

**保留DSC中的EPS信息：** 保留信息，如EPS文件的原始应用程序和创建日期。如果取消选择此选项，则页面将根据页面上左上角对象的左上角和右下角对象的右下角来调整大小并居中。

**保留OPI注释：** 保留将“仅用于放置(FPO)”图像或注释替换为高分辨率图像(位于支持Open Prepress Interface(OPI)版本1.3和2.0的服务器上)所需的信息。

**保留来自DSC的文档信息：** 保留标题、创建日期和时间等信息。在Acrobat中打开PDF文件时，此信息会显示在“文档属性描述”面板中。

**为EPS文件调整页面大小和将图稿居中：** 将EPS图像居中，并调整页面大小以紧贴图像周围。此选项仅适用于包含单个EPS文件的作业。

## 标准报告和合规选项{#standards-reporting-and-compliance-options}

PDF生成器可以在创建PDF文件之前检查PostScript文件中的文档内容，以确保它们符合标准PDF/X-1a、PDF/X-3或PDF/A标准。 对于符合PDF/X规范的文件，您还可以通过在“标准报告与合规性”下选择其他选项来要求PostScript文件满足其他标准。 选项的可用性取决于您选择的标准。

符合PDF/X规范的文件主要用于交换用于高分辨率打印生产的PDF文件的标准化格式。 除非您为打印生产创建PDF文档，否则可以忽略PDF/X合规标准。

符合PDF/A规范的文件主要用于存档。 由于长期保存是目标，因此文档必须仅包含在文档的整个预期生命周期中打开和查看所需的内容。 例如，PDF/A兼容文件只能包含文本、光栅图像和矢量对象；它们不能包含加密和脚本。 此外，必须嵌入所有字体，才能打开文档并在创建时查看文档。 换言之，PDF/A兼容文档比PDF/X兼容文档&#x200B;*更薄*，后者适用于高端生产。

>[!NOTE]
>
>如果设置监视文件夹以创建PDF/A兼容文件，请确保不向文件夹添加安全性；PDF/A标准不允许加密。

有关访问标准报告和合规性选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

**合规性标准：** 选择一个标准以生成报告，以指示文件是否符合要求，如果不符合，则指明遇到了哪些问题。将“常规设置”页面上的“兼容性”设置为Acrobat 4.0后，将启用以下选项。 将“兼容性”设置为Acrobat 5.0时，只有Acrobat 5.0选项可供选择。 当“兼容性”设置为替代选项时，以下选项将变暗：

* PDF/X-1a(与Acrobat 4.0兼容)
* PDF/X-3(Acrobat 4.0兼容)
* PDF/X-1a(与Acrobat 5.0兼容)
* PDF/X-3(Acrobat 5.0兼容)
* PDF/A-1b(Acrobat 5.0兼容)

### PDF/X标准{#options-for-pdf-x-standards}选项

**不兼容时：** 指定在PostScript文件不符合PDF/X要求时是否创建PDF文件。当“标准报告与合规性”页面上的“合规性标准”设置为“无”以外的选项时，此选项将可用。

**继续：** 创建PDF文件。

**取消作业：** 仅当PostScript文件满足所选报表选项的PDF/X要求并且在其他情况下有效时，才创建PDF文件。如果同时选择了PDF/X报表选项，并且PostScript文件仅满足一组PDF/X标准（例如PDF/X-3），则PDF生成器会创建兼容文件。

**如果未指定TrimBox或ArtBox:** 当“标准报告与合规性”页面上的“符合性标准”设置为“无”以外的选项时，可用。

**报告为错误：** 如果选择了其中一个报告选项，并且任何页面中都缺少一个裁切框或艺术框，则将PostScript文件标记为不兼容。

**设置“裁切框为带偏移的媒体框”：** 如果既未指定裁切框，也未指定艺术框，则根据各页媒体框的偏移计算裁切框的点值。裁切框始终小于或小于封闭的介质框。

**如果未指定出血框：** 当“标准报告与合规性”页上的“符合性标准”设置为“无”以外的选项时，可用。

**将出血框设置为媒体框：** 如果未指定出血框，则使用出血框的媒体框值。

**将出血框设置为带偏移的裁切框：** 如果未指定出血框，则根据各页裁切框的偏移计算出出血框的点值。出血框总是比封闭的裁切框大或大。

**如果未在文档中指定默认值：** 当“标准报告与合规性”页上的Compliance Standard设置为“无”以外的选项时，此选项将可用。

**输出意图配置文件名称：** 指示文档准备的特定打印条件。如果文档未指定输出意图名称，则PDF生成器将使用此菜单中的选定值。 您可以选择提供的名称之一，或在提供的空格中输入名称。 如果工作流要求文档指定输出意图，请选择“无”。 任何不符合要求的文档均未通过合规性检查。

**输出条件标识符：** 指示由输出意图配置文件名称的注册表指定的引用名称。

**输出条件：** 描述预期的打印条件。此条目对PDF文档的目标接收者非常有用。

**注册表名称(URL):** 指示有关注册表的详细信息的网址。自动为ICC注册表名称输入URL。

**陷印：** 指示文档中陷印的状态。PDF/X合规要求值为True或False。 如果文档未指定陷印状态，则使用此处提供的值。 如果工作流要求文档指定陷阱状态，请选择“未定义”。 任何不符合要求的文档均未通过合规性检查。

### PDF/A标准{#options-for-pdf-a-standard}选项

将“兼容性”（在“常规”区域中）设置为Acrobat 4(PDF 1.3)或Acrobat 5(PDF 1.4)时，将启用这些选项。

**不兼容时：** 指定在PostScript文件不符合PDF/A要求时是否创建PDF文件。

**继续：** 即使PostScript文件不符合标准要求，也创建PDF文件。

**取消作业：** 仅当PostScript文件满足PDF/A要求且在其他情况下有效时，才创建PDF文件。

**输出意图配置文件名称：** 指示已为其准备文档且符合PDF/A规范要求的特定打印条件。如果工作流要求文档指定“输出意图”信息，请选择“无”。 如果未提供此信息，文档将无法进行合规性检查。

**输出条件：** 描述预期的打印条件。此条目不是必需的，但可用于向PDF文档的目标接收者提供有用信息。

## 初始视图选项{#initial-view-options}

这些选项分为三个区域：文档选项、窗口选项和用户界面选项。 有关访问初始视图选项的说明，请参阅[添加或编辑PDF设置](configuring-pdf-settings.md#add-or-edit-pdf-settings)。

要使用任何选项，请选择“设置初始视图设置”。

### 文档选项{#document-options}

文档选项控制文档窗口中文档的外观，如放大级别及其滚动方式。

**显示：** 默认情况下，确定在应用程序窗口中显示的窗格和选项卡。“书签”面板和“页面”打开文档窗格并显示“书签”选项卡。

**页面布局：** 确定文档是在单页、对页、连续页面还是连续对页模式下查看。

**放大率：** 设置打开时用于显示文档的缩放级别。默认使用Acrobat或Adobe Reader首选项中用户配置的放大率值。

**打开到页码：** 设置文档在其中打开的页面，通常为第1页。

>[!NOTE]
>
>为放大率和页面布局选项设置“默认”时，会使用Acrobat或Adobe Reader的“页面显示”首选项中的各个用户设置。

### 窗口选项{#window-options}

窗口选项确定用户打开文档时窗口在屏幕区域中的调整方式。 但是，当在Web浏览器中查看PDF文档时，这些选项不起作用。

**调整窗口大小到初始页面：** 根据在“文档选项”下选择的选项，调整文档窗口以适合打开页面周围的情况。

**屏幕上的中心窗口：** 将窗口定位到屏幕区域的中心。

**以全屏模式打开：** 最大化文档窗口，并显示没有菜单栏、工具栏或窗口控件的文档。

**显示：** 文件名在窗口的标题栏中显示文件名。文档标题在窗口的标题栏中显示文档标题。

### 用户界面选项{#user-interface-options}

用户界面选项确定用户打开文档时显示或隐藏的控件。

**隐藏菜单栏：** 如果选中，则隐藏菜单栏

**隐藏工具栏：** 如果选中此选项，则隐藏工具栏

**隐藏窗口控件：** 如果选中此选项，则隐藏窗口控件

>[!NOTE]
>
>如果隐藏菜单栏和工具栏，用户将无法应用命令和选择工具，除非他们在Acrobat中打开文件时知道键盘快捷键。

## 上载和下载程序文件和尾文件{#uploading-and-downloading-prologue-and-epilogue-files}

Prolog文件用于添加在每个正在提取的PostScript作业的开头执行的自定义PostScript代码。 尾部文件用于添加在每个PostScript作业结束时执行的自定义PostScript代码。 您可以从服务器下载程序文件和尾文件，以将它们保存在本地。 您可能希望下载文件以单独配置它们，或将它们上传到其他位置或其他计算机。

这些文件有多种用途。 例如，可以编辑原始文件以指定封面；可以编辑尾文件以解析PostScript文件中的一系列过程。 您还可以选择并上传要随每个作业一起发送的序文件和尾文件。

### 下载序列或尾文件{#download-a-prologue-or-epilogue-file}

1. 在管理控制台中，单击服务> PDF生成器> Adobe PDF设置。
1. 单击“新建”或单击设置的名称。
1. 单击“Advanced（高级）” ，然后在“Use Prolog.ps and Epilog.ps（使用Prolog.ps和Epilog.ps）”选项旁边，单击“Download（下载）”。
1. 在“Download Prolog and Epilog Files（下载原文和外文文件）”页面上，单击Prolog.ps或Epilog.ps ，然后单击“Save（保存）”。

### 上传序录或尾随文件{#upload-a-prologue-or-epilogue-file}

1. 在管理控制台中，单击服务> PDF生成器> Adobe PDF设置。
1. 单击“新建”或单击设置的名称。
1. 单击“Advanced（高级）” ，然后在“Use Prolog.ps And Epilog.ps（使用Prolog.ps和Epilog.ps）”选项旁边，单击“Upload（上传）”。
1. 在“上载原版和尾文件”页面上，单击“浏览”以选择原版或尾文文件。
1. 找到文件，然后单击“打开”。
1. 要使用文件，请确保在“新建/编辑Adobe PDF设置”页面的“高级”区域中选中“使用Prolog.ps和Epliog.ps”。
1. 单击Save

>[!NOTE]
>
>PDF生成器仅支持将PostScript和封装的PostScript文件转换为PDF的前置文件和后置文件。
