---
title: 自定义表单门户组件的模板
seo-title: 自定义表单门户组件的模板
description: 在表单列表中显示自定义元数据
seo-description: 在表单列表中显示自定义元数据
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms Portal
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---


# 自定义表单门户组件的模板{#customizing-templates-for-forms-portal-components}

## 前提条件 {#prerequisites}

[管理表单元数据](../../forms/using/manage-form-metadata.md)

HTML和CSS的工作知识

## 概述 {#overview}

利用AEM Forms用户界面，可向任何表单添加元数据。 自定义元数据可在列出和搜索您组织的表单时增强用户体验。

Forms Portal允许您在表单列表中使用自定义元数据。 在为资产创建自定义模板时，您可以修改其布局，并将自定义元数据与CSS样式集结合使用。

请执行以下步骤，为各种Forms Portal组件创建自定义模板。

## 创建自定义模板{#creating-a-nbsp-custom-template}

1. 在/apps下创建sling:Folder节点

   添加“fpContentType”属性。 根据为其定义自定义模板的组件，为属性指定相应的值。

   * 搜索和制表程序组件：&quot;/libs/fd/fp/formTemplate&quot;
   * 草稿和提交组件：

      * 草稿部分：/libs/fd/fp/draftsTemplate
      * 提交部分：/libs/fd/fp/submissionsTemplate
   * 链接组件：/libs/fd/fp/linkTemplate

   添加在选择布局模板时要显示的标题。

   >[!NOTE]
   >
   >标题可以与您创建的sling:Folder的节点名称不同。

   下图描述了搜索和制表器组件的配置。
   ![创建sling:Folder](assets/1.png)

1. 在此文件夹中创建一个用作自定义模板的文件template.html。
1. 按如下所述编写自定义模板并使用自定义元数据。

## 工作示例{#working-example}

以下是自定义模板的示例实施，在该模板中，Forms Portal为Search &amp; Lister组件获取自定义GeometrixxGov卡布局。

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## 自定义模板{#technical-specifications-for-custom-templates}的技术规范

任何Forms Portal组件的自定义模板都包括可重复和非可重复的条目。 可重复条目是要列出的基本实体。 可重复条目的示例包括搜索和制表人、草稿和提交以及链接组件。

Forms Portal为占位符提供了用于显示自定义/OOTB元数据的语法。 占位符在显示表单、草稿或提交的结果后填充。

要包含可重复条目，请将属性&#x200B;**data-repeatable**&#x200B;的值配置为&#x200B;**true**。

*在所讨论的示例中，自定义模板的顶部存在两个Div元素。第一个具有“__FP_boxes-container”CSS类，可用作所列表单的容器元素。 第二个包含“__FP_boxes”CSS类的是基本实体的模板，在本例中为“表单”。 Div元素中存在的&#x200B;**data-repeatable**属性的值为&#x200B;**true**。*

每个占位符都有一个排他的OOTB元数据集。 要在表单上的特定位置显示自定义元数据，请在该位置添加&#x200B;**${metadata_prop}属性**。

*在示例中，元数据属性在多个实例中使用。例如，它以规定方式用在&#x200B;**description**、**name**、**formUrl**、**htmlStyle**、**pdfUrl**、**pdfStyle**和&#x200B;**路径**中。*

## 现成的元数据{#out-of-the-box-metadata}

各种Forms Portal组件提供了一组可用于列表的专用OOTB元数据。

### 搜索和制表程序组件{#search-amp-lister-component}

* **标题：** 表单的标题
* **名称**:表单的名称（大多数情况下与标题相同）
* **描述**:表单的描述
* **formUrl**:将表单渲染为HTML的URL
* **pdfUrl**:将表单渲染为PDF的URL
* **assetType**:资产的类型。有效值包括&#x200B;**表单**、**PDF表单**、**打印表单**&#x200B;和&#x200B;**自适应表单**

* **htmlStyle**&amp;  **pdfStyle**:用于渲染的HTML和PDF图标的显示样式。有效值为“**__FP_display_none**”或空白。

>[!NOTE]
>
>请记住在自定义样式表中使用__FP_display_none类。

* **downloadUrl**:用于下载资产的URL。

在用户界面上支持本地化、排序和使用配置属性（仅限搜索和制表人）：

1. **本地化支持**:要本地化任何静态文本，请使 `${localize-YOUR_TEXT}` 用属性并使本地化值可用（如果不存在）。
   *在所讨论的示例中，属性和 `${localize-Apply}` 用 `${localize-Download}` 于将应用和下载文本本地化。*

1. **支持排序**:单击HTML元素以对搜索结果排序。要在表格布局中实施排序，请在特定表标题中添加“data-sortKey”属性。 此外，将其值添加为要排序的元数据。
例如，对于网格视图中的“标题”标题，“data-sortKey”标题的值为“title”。 单击标题可对特定列中的值进行排序。

1. **使用配置属性**:搜索和制表程序组件具有多个可在用户界面上使用的配置。例如，要显示通过编辑对话框保存的HTML工具提示文本，请使用`${config-htmlLinkText}`属性。 **同样，对于PDF工具提示文本，请使** `${config-pdfLinkText}` 用属性。

### 链接组件{#link-component}

* **标题：** 表单的标题
* **formUrl**:将表单渲染为HTML的URL
* **target**:链接的Target属性。有效值为“_blank”和“_self”。
* **linkText**:链接标题

### 草稿和提交组件{#drafts-amp-submissions-component}

* **路径**:草稿/提交元数据节点的路径。将其与.HTML扩展一起用作URL，以打开草稿或提交。
* **contextPath**:AEM实例的上下文路径
* **firstLetter**:自适应表单标题的首字母（大写），保存为草稿或已提交。
* **formName**:自适应表单的标题，保存为草稿或已提交。
* **draftID**:所列草稿的ID（仅在“草稿”部分的模板中使用）。
* **submitID**:列出的提交的ID（仅在“提交”部分的模板中使用）。
* **状态**:已提交表单的状态。（仅在“提交”部分的模板中使用）。
* **描述**:与草稿或提交关联的自适应表单的描述。
* **diffTime**:草稿的当前时间和上次保存操作之间的差异。或者，当前时间与上次提交操作之间用于提交的时间差。
* **iconClass**:用于显示草稿/提交的第一个字母的CSS类。Forms Portal包括以下类，这些类提供各种不同的彩色背景。
* **所有者**:创建草稿/提交的用户。
* **今天**:创建草稿或提交日期（DD:MM:YYYY格式）。
* **TimeNow**:创建草稿或提交的时间，以HH:MM:SS 24小时格式表示

*注意:*

1. 对于“草稿和提交”组件下“草稿”部分中的删除选项，请将CSS类命名为“__FP_deleteDraft”。 此外，还包括值&#x200B;**${draftID}**&#x200B;的属性“draftID”，该值是相应草稿的草稿ID草稿。

1. 在创建用于打开草稿和提交的链接时，您可以将&#x200B;**${path}.html**&#x200B;指定为锚点标记的&#x200B;**href**&#x200B;属性的值。

![“草稿和提交”节点](assets/raw-image-with-index.png)

**A**. 容器元素

**具有固** 定层次结构的B.“路径”元数据，以获取每个表单存储的缩略图。

**C.** 用于每个表单模板部分的数据可重复属性

**将“应** 用”字符串本地化

**E.** 使用配置属性pdfLinkText

**F.** 使用“pdfUrl”元数据

## 提示、技巧和已知问题{#tips-tricks-and-known-issues}

1. 请勿在任何自定义模板中使用单引号(&#39;)。
1. 对于自定义元数据，请仅将此属性存储在&#x200B;**jcr:content/metadata**&#x200B;节点上。 如果将其存储在任何其他位置，则Forms Portal无法显示元数据。
1. 请确保任何自定义元数据或现有元数据的名称中不包含冒号(:)。 如果存在，则无法在用户界面上显示它。
1. **data-** repeatable对链接组件没有任何意 **** 义。Adobe建议您避免在链接组件的模板中使用此属性。

## 相关文章

* [启用表单门户组件](/help/forms/using/enabling-forms-portal-components.md)
* [创建表单门户页面](/help/forms/using/creating-form-portal-page.md)
* [使用API在网页上列出表单](/help/forms/using/listing-forms-webpage-using-apis.md)
* [使用草稿和提交组件](/help/forms/using/draft-submission-component.md)
* [自定义草稿和提交表单的存储](/help/forms/using/draft-submission-component.md)
* [将草稿和提交组件与数据库集成的示例](/help/forms/using/integrate-draft-submission-database.md)
* [自定义表单门户组件的模板](/help/forms/using/customizing-templates-forms-portal-components.md)
* [在门户上发布表单简介](/help/forms/using/introduction-publishing-forms.md)