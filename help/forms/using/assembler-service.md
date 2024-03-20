---
title: 使用汇编程序服务
description: Assembler服务允许您组合、重新排列和增加PDF和XDP文档，并获取有关PDF文档的信息。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services
exl-id: 84c8125d-0f16-432a-9567-63b868667537
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 6%

---

# 使用汇编程序服务{#using-assembler-service}

Assembler服务允许您组合、重新排列和增加PDF和XDP文档，并获取有关PDF文档的信息。 提交给Assembler服务的每个作业包括Document Description XML (DDX)文档、源文档和外部资源（字符串和图形）。 有关汇编程序服务的详细信息，请参见 [汇编程序服务概述](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

您可以将Assemble服务用于以下操作：

## 汇编 PDF 文档 {#assemble-pdf-documents}

您可以使用Assembler服务将两个或多个PDF文档组合到单个PDF文档或PDFPortfolio中。 您还可以对PDF文档应用辅助导航或增强安全性的功能。 以下是可用于汇编 PDF 文档的一些方法：

### 汇编一个简单的 PDF 文档 {#assemble-a-simple-pdf-document}

下图显示了将三个源文档合并到单个生成文档中的情况。

![从多个PDF文档组合一个简单的PDF文档](assets/as_document_assembly.png)

从多个PDF文档组合一个简单的PDF文档

以下示例是用于组合文档的简单DDX文档。 它指定用于生成结果文档的源文档的名称，以及结果文档的名称：

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

文档组件生成一个结果文档，其中包含以下内容和\
特征：

* 每个源文档的全部或部分
* 每个源文档的所有或部分书签，针对组合生成文档进行标准化
* 从基础文档(Doc1)采用的其他特征，包括元数据、页面标签和页面大小
* 可选地，产生的文档包括由源文档中的书签构造的目录

### 创建 PDF 文档组合 {#create-a-pdf-portfolio}

Assembler服务可以创建包含文档集合和自含用户界面的PDFPortfolio。 该界面称为“PDFPortfolio布局”或“PDFPortfolio导航器（导航器）”。 PDFPortfolio通过添加导航器、文件夹和欢迎页面来扩展PDF包的功能。 该界面可以通过利用本地化的文本字符串、自定义颜色方案和图形资源来增强用户体验。 PDFPortfolio还可以包含用于组织项目组合中的文件的文件夹。

当Assembler服务解释以下DDX文档时，它会组合一个PDFPortfolio，其中包括一个PDFPortfolio导航器和一个包含两个文件的包。 此服务从myNavigator源指定的位置获取导航器。 它将导航器的默认颜色方案更改为pinkScheme颜色方案。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### 汇编加密的文档 {#assemble-encrypted-documents}

在组合文档时，还可以使用密码对PDF文档进行加密。 使用密码加密PDF文档后，用户必须指定密码才能在Adobe Reader或Acrobat中查看PDF文档。 要使用口令加密PDF文档，DDX文档必须包含加密PDF文档所需的加密元素值。

加密服务不必是LiveCycle安装的一部分，也可以使用密码对PDF文档进行加密。

如果一个或多个输入文档被加密，请提供密码以作为DDX的一部分打开文档。

### 使用 Bates 编号汇编文档 {#assemble-documents-using-bates-numbering}

在组合文档时，可以使用Bates编号为每个页面应用唯一的页面标识符。 当您使用Bates编号时，文档（或文档集）中的每一页都会分配一个唯一标识该页面的编号。 例如，包含物料清单信息并与装配件的生产关联的制造文档可以包含标识符。 Bates编号包含一个按顺序递增的数值，以及可选的前缀和后缀。 前缀+数字值+后缀称为bates模式。

下图显示了一个PDF文档，该文档的标题中包含唯一标识符。

![在文档标题中包含唯一标识符的PDF文档](do-not-localize/as_batesnumber.png)

在文档标题中包含唯一标识符的PDF文档

### 合并和汇编文档 {#flatten-and-assemble-documents}

可以使用Assembler服务将交互式PDF文档（例如表单）转换为非交互式PDF文档。 交互式PDF文档允许用户在PDF文档字段中输入或修改数据。 将交互式PDF文档转换为非交互式PDF文档的过程称为拼合。 将PDF文档平面化后，表单字段会保留其图形外观，但不再具有交互性。 拼合PDF文档的一个原因是确保无法修改数据。 此外，与字段关联的脚本不再起作用。

当创建从交互式PDF文档装配的PDF文档时，Assembler服务会拼合这些表单，然后将它们装配到生成文档中。

>[!NOTE]
>
>Assembler服务使用Output服务来拼合动态XFA表单。 如果Assembler服务处理要求它拼合XFA动态表单的DDX，并且Output服务不可用，则会引发异常。 汇编程序服务可拼合Acrobat表单或静态XFA表单，而无需使用输出服务。

## 汇编XDP文档 {#assemble-xdp-documents}

您可以使用Assembler服务将多个XDP文档组合到单个XDP文档或PDF文档中。 对于包含插入点的源XDP文件，您可以指定要插入的片段。

以下是组合XDP文档的一些方法：

### 汇编简单的XDP文档 {#assemble-a-simple-xdp-document}

下图显示了将三个源XDP文档组合到单个生成XDP文档中的情况。 生成的XDP文档包含三个源XDP文档及其关联数据。 产生的文档从基础文档（第一个源XDP文档）获得基本属性。

![从多个XDP文档组合一个简单的XDP文档](assets/as_assembler_xdpassembly.png)

从多个XDP文档组合一个简单的XDP文档

以下是一份DDX文档，该文档提供了上述结果。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### 在装配期间解析引用 {#resolving-references-during-assembly}

通常，XDP文档可以包含通过绝对或相对引用引用的图像。 默认情况下，汇编程序服务会保留对生成XDP文档中图像的引用。

您可以指定Assembler服务在汇编时如何通过XDP文件中的绝对或相对引用处理源XDP文档中引用的图像。 可选择将所有图像嵌入到生成结果中，使其不包含相对或绝对参照。 您可以通过设置resolveAssets标记的值来定义此值，此值可使用以下任意选项。 默认情况下，结果文档中不会解析任何引用。

<table>
 <tbody> 
  <tr> 
   <th>价值</th> 
   <th>描述</th> 
  </tr> 
  <tr> 
   <td>无</td> 
   <td>不解析任何引用。</td> 
  </tr> 
  <tr> 
   <td>全部</td> 
   <td>将所有引用的图像嵌入到源XDP文档中。</td> 
  </tr> 
  <tr> 
   <td>相对</td> 
   <td>在源XDP中嵌入通过相对引用引用的所有图像<br /> 文档。</td> 
  </tr> 
  <tr> 
   <td>绝对</td> 
   <td>在源XDP中嵌入通过绝对引用引用的所有图像<br /> 文档。</td> 
  </tr> 
 </tbody> 
</table>

您可以在XDP源标记或父XDP结果标记中指定resolveAssets属性的值。 如果将属性指定给XDP结果标记，则该属性将由作为XDP结果子项的所有XDP源元素继承。 但是，显式指定源元素的属性会仅覆盖该源文档的结果元素的设置。

#### 解析XDP文档中的所有源引用 {#resolve-all-source-references-in-an-xdp-document}

要解析源XDP文档中的所有引用，请为以下对象指定resolveAssets属性：\
生成文档至全部，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

您还可以单独为所有源XDP文档指定属性以获得相同的属性\
结果。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### 解析XDP文档中的所选源引用 {#resolve-selected-source-references-in-an-xdp-document}

通过指定resolveAssets属性，可以选择指定要解析的源引用。 单个源文档的属性将覆盖生成XDP文档的设置。 在此示例中，还将解析包含的片段。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### 有选择地解析绝对或相对参照 {#selectively-resolve-absolute-or-relative-references}

可以选择性地解析所有或部分源文档中的绝对或相对参照，如下例所示：

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### 将表单片段动态插入XFA表单 {#dynamically-insert-form-fragments-into-an-xfa-form}

您可以使用Assembler服务创建一个XFA表单，该表单是从片段插入到的其他XFA表单创建的。 使用此功能，您可以使用片段创建多个表单。

支持动态插入表单片段支持单一源代码控制。 您可以维护常用组件的单一来源。 例如，您可以为公司横幅创建片段。 如果横幅发生更改，您只需修改片段。 包含片段的其他表单保持不变。

表单设计器使用LiveCycle设计器创建表单片段。 这些片段是XFA表单中唯一命名的子表单。 表单设计器还使用设计器创建具有唯一名称插入点的XFA表单。 您（程序员）编写DDX文档来指定如何将片段插入XFA表单。

下图显示了两个XML表单（XFA模板）。 左侧的表单包含一个名为myInsertionPoint的插入点。 右侧的表单包含一个名为myFragment的片段。

![将表单片段插入到XFA表单中](assets/as_assembler_fragment_assy_assembled.png)

将表单片段插入到XFA表单中

当汇编程序服务解释以下DDX文档时，它会创建一个包含其他XML表单的XML表单。 myFragmentSource文档中的myFragment子表单插入到myFormSource文档的myInsertionPoint中。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### 将XDP文档打包为PDF {#package-an-xdp-document-as-pdf}

您可以使用Assembler服务将XDP文档打包为PDF文档，如此DDX文档中所示。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## 拆分 PDF 文档 {#disassemble-pdf-documents}

您可以使用Assembler服务拆分PDF文档。 该服务可以从源文档中提取页面，或者根据书签划分源文档。 通常，如果 PDF 文档最初是从多个单独文档（例如对帐单集合）创建的，则此任务很有用。

### 从源文档中提取页面 {#extract-pages-from-a-source-document}

在下图中，从源文档中提取页面1-3，并将其放置在新的生成文档中。

![从源文档提取特定页面](assets/as_intro_page_extraction.png)

从源文档提取特定页面

以下示例是用于分解文档的DDX文档。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### 根据书签拆分源文档 {#divide-a-source-document-based-on-bookmarks}

在下图中，DocA被分为多个结果文档。 页面上的第一个级别1书签标识新生成文档的开始。

![根据书签将源文档划分为多个文档](assets/as_intro_pdfsfrombookmarks.png)

根据书签将源文档划分为多个文档

以下示例是一个DDX文档，它使用书签拆解源文档。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## 确定文档是否符合PDF/A标准 {#determine-whether-documents-are-pdf-a-compliant}

您可以使用Assembler服务来确定PDF文档是否符合PDF/A标准。 PDF/A 是一种用于长期保存文档内容的存档格式。字体将嵌入到文档中，并且文件是未压缩的。因此，PDF/A 文档通常比标准 PDF 文档大。此外，PDF/A 文档不包含音频和视频内容。

## 获取有关PDF单据的信息 {#obtain-information-about-a-pdf-document}

您可以使用Assembler服务获取有关PDF文档的以下信息：

* 文本信息。

   * 文档每一页上的单词
   * 文档每一页上的每个单词的位置
   * 文档每页每个段落中的句子

* 书签，包括页码、标题、目标和外观。 您可以导出此\
  PDF文档中的数据并将其导入PDF文档。

* 文件附件，包括文件信息。 对于页面级别的附件，它还包括\
  文件附件注释的位置。 您可以从PDF文档中导出此数据，并且\
  将其导入PDF文档。

* 打包文件，包括文件信息、文件夹、包、架构和字段数据。 您可以从PDF文档中导出此数据，并将其导入PDF文档中。

## 验证DDX文档 {#validate-ddx-documents}

您可以使用Assembler服务来确定DDX文档是否有效。 例如，如果从以前的LiveCycle版本升级，则验证将确保DDX文档有效。

## 呼叫其他服务 {#call-other-services}

您可以使用导致Assembler服务调用以下LiveC循环服务的DDX文档。 Assembler服务只能调用随LiveCycle一起安装的那些服务。

**Reader扩展服务**：使Adobe Reader用户能够对生成的PDF文档进行数字签名。

**Forms服务**：合并XDP文件和XML数据文件以生成包含已填充交互式表单的PDF文档。

**输出服务**：将动态XML表单转换为包含非交互式表单的PDF文档（拼合表单）。 Assembler服务拼合静态XML表单和Acrobat表单，而不调用Output服务。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

使用DDX和Assembler服务调用其他LiveC循环服务可以简化您的流程图。 它甚至可以减少您自定义工作流所花费的工作量。 (另请参阅
