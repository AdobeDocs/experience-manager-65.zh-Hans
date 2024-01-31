---
title: PDF生成无法使用WorkBench打印大量PDF
description: 当客户通过通过WorkBench实施的服务生成大量PDF时，打印服务将失败。
source-git-commit: 9cdf22918f08fe505c3efd0ce43235e3442165d5
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# PDF生成无法通过WorkBench打印大量PDF {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## 问题 {#issue}

当客户通过通过WorkBench实施的服务生成大量PDF时。 服务因内存不足而失败。 错误显示为：

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

这是因为在Windows上，打印请求中的最大页数限制为大约1000页。 当生成打印输出时，模板和数据需要加载到内存中，并且生成的布局构建在内存中。 这意味着最终输出的大小存在限制。 生成打印输出的过程是一个32位任务，这意味着在Windows上它最多只能有2 GB的RAM <!--and 4 GB on UNIX-->.

## 应用到 {#applies-to}

该解决方案适用于AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> 用于x86_win32 XMLFM。

## 解决方案 {#solution}

影响内存使用率的最大因素是表单上的数据量。 但是，在形状设计中存在其它因素，它们对内存使用的影响较小。 当您意识到这些因素时，可以设计一个表单以获得更大的打印输出。 以下部分按优先级顺序指示影响内存占用空间的因素：

### 影响因子 {#impact-factor}

**高**

1. **选择子表单**  — 选择子表单集是子表单集对象的变体，允许您使用条件语句从集中自定义特定子表单的显示。
1. **使用静态文本代替字幕**  — 几乎每个字段内都提供标题，用户应使用它而不是额外的静态文本作为标题。
1. 使用 **富文本格式(RTF)** 尽可能。

**Average**

设计表单模板时，为帮助提高内存使用率，应考虑其他因素：

1. 避免使用静态文本标记字段。 请改用文本字段中的标题。
2. 不要过度使用矩形、线条、对象和表格。
3. 如果可能，请避免使用RichText和Choice子表单。
4. 避免过度使用子表单和嵌套子表单。

### 数据大小限制 {#data-size-limitations}

由于受到最大进程内存的限制，进程所消耗的内存不仅取决于数据文件的大小。 它与表单设计有着非常密切的关系，在某种程度上也与表单中合并的实际数据量有着密切的关系。

如果表单有许多小节点，但数据很小，那么该过程将消耗更多内存（因此内存耗尽速度更快），而不是具有更少节点（即使）的表单具有大数据。

阅读 [以下附录](#appendix) 有关更多信息，测试结果基于打印表单(无标记PDF)。 使用标记的PDF进程内存需求增加。 它还取决于表单中的字段数 — 大约流程内存需求是未标记PDF的1.5倍多。

### 交互式Forms {#interactive-forms}

由于交互字段再次呈现，因此交互式表单占用的内存将多于打印Forms 。 在执行的测试中，与打印表单相比，内存消耗增加了约1.5倍，这些表单是静态交互表单。

### 图像格式 {#image-formats}

Adobe不推荐任何特定的图像格式。 但是，最好是让图像更小，例如PNG（可移植网络图形）。 也不建议使用大小为数百MB的高分辨率图像。 此外，不建议使用压缩图像，因为解压缩后压缩图像的大小会扩展到数百MB的数据。

### 附录 {#appendix}

**表示例**

下面显示了表的不同变量，这些变量显示简单表和复杂表的渲染页数与数据大小。

1. 带有单列的表，其中生成了5000页PDF，数据文件大小为24 MB和30-K记录。

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. 一个有许多小列的表，其中生成了800页PDF，数据文件大小为4.6 MB，记录为20-K。
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. 具有许多小列的表，但由于使用了较大的xmlTag名称，数据文件较大。
此处，所有内容与上一个相同，但xml标记名称已变大（以便数据文件大小增加而不增加实际有效数据），最终结果（上限）几乎相同。 数据文件大小从4.6 MB增加到44.6 MB。 此处生成的PDF为800页，数据文件大小为44.6 MB，记录为20-K。

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

因此，很难对数据文件大小设置一般的上限。 每个表单都是唯一的，因此内存消耗会因表单而异。