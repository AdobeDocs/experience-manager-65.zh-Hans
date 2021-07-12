---
title: 管理表单元数据
seo-title: 管理表单元数据
description: 元数据可以更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。
seo-description: 元数据可以更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。
uuid: d982df6f-a256-4bad-868f-74fcd08350f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: ba571f8e-8bd3-48eb-82e1-c93b14ffe44a
docset: aem65
role: Admin
exl-id: f82bbd39-b655-47a9-bca9-21d7cd30c082
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 1%

---

# 管理表单元数据{#manage-form-metadata}

## 概述  {#overview-nbsp}

元数据可以更轻松地对资产进行分类和组织，并帮助正在查找特定资产的用户。

AEM Forms默认为每种资产类型提供一组定义的元数据。 除了默认元数据之外，您还可以向每种资产类型添加自定义元数据。 AEM Forms还为您提供了有效创建、管理和交换表单所有这些元数据的正确方法。

如果您是开发人员或网站所有者，则可以自定义Forms Portal(AEM Forms的最终用户界面)，以反映您在组织中使用的元数据。 有关Forms Portal的更多信息，请参阅[在门户上发布表单简介](../../forms/using/introduction-publishing-forms.md)。

## AEM Forms中的元数据 {#metadata-in-aem-forms}

在AEM Forms中，与资产关联的元数据属性列表取决于其类型。 此外，如果添加任何自定义元数据属性，则该属性会添加到添加了自定义元数据的类型的所有资产中。

### 资产类型 {#asset-types}

AEM Forms支持以下资产类型：

* 表单模板（XFA表单）
* PDF forms
* 文档（平面PDF）
* 自适应表单
* 资源
* XFS

#### 元数据的广泛列表 {#extensive-list-of-metadata}

以下是AEM Forms中支持的元数据属性的详尽列表：

<table>
 <tbody> 
  <tr> 
   <td><strong>属性名称</strong></td> 
   <td><strong>资产类型</strong></td> 
   <td><strong>描述</strong><br /> </td> 
  </tr> 
  <tr> 
   <td>标题</td> 
   <td>除资源外</td> 
   <td>表单的显示名称。<br /> </td> 
  </tr> 
  <tr> 
   <td>描述</td> 
   <td>除资源外</td> 
   <td>表单的描述。 用户可以指定此值。<br /> </td> 
  </tr> 
  <tr> 
   <td>类型</td> 
   <td>所有</td> 
   <td><p>指定资产类型的只读值。 它可以具有以下值之一：</p> 
    <ul> 
     <li>表单模板</li> 
     <li>PDF表单、PDF表单(Acroform)或PDF表单（签名）</li> 
     <li>文档，文档（签名）</li> 
     <li>自适应表单</li> 
     <li>资源</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>创建时间</td> 
   <td>所有</td> 
   <td>指定资产创建时间的只读值。</td> 
  </tr> 
  <tr> 
   <td>上次修改日期</td> 
   <td>所有</td> 
   <td>一个只读值，指定上次修改资产的时间。</td> 
  </tr> 
  <tr> 
   <td>作者</td> 
   <td>除资源外</td> 
   <td><p>基于表单类型自动计算的只读值。</p> 
    <ul> 
     <li>PDF/表单模板/文档 — 从上传的二进制文件中获取。</li> 
     <li>自适应表单 — 在表单创建时登录用户。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>状态</td> 
   <td>除资源外</td> 
   <td><p> 一个只读值，用于定义表单的以下状态之一：</p> 
    <ul> 
     <li>无值：如果表单从未发布。</li> 
     <li>已发布：发布表单时。</li> 
     <li>已修改：表单在发布后被修改一次的时间。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>上次发布日期</td> 
   <td>除资源外</td> 
   <td>一个只读值，指定上次发布表单的时间。</td> 
  </tr> 
  <tr> 
   <td>发布开/关时间</td> 
   <td>除资源外</td> 
   <td><p>表单计划自动发布/取消发布的时间。 用户在编辑元数据时会设置此值。</p> 
    <ul> 
     <li>“发布”和“关闭”时间都应超出当前日期。 </li> 
     <li>“发布结束”时间应该超出“发布正时”时间。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>提交URL</td> 
   <td><p>表单模板</p> <p>PDF表单</p> </td> 
   <td><p>配置用户指定的URL，以将表单数据提交到Servlet。</p> <p>可以使用以下任何方法配置提交URL，这些方法按优先顺序列出：</p> 
    <ul> 
     <li>在AEM Forms Designer中创建XFA表单时，使用HTTP提交按钮直接在表单模板中指定提交URL。</li> 
     <li>在AEM Forms UI中，选择一个表单，然后在编辑元数据属性时指定提交URL。</li> 
     <li>在Forms门户中，编辑搜索和制表人组件，并在表单链接选项卡下指定提交URL。</li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td>HTML渲染配置文件</td> 
   <td>表单模板</td> 
   <td>以HTML格式渲染表单模板时使用的HTML渲染配置文件。</td> 
  </tr> 
  <tr> 
   <td>呈现格式</td> 
   <td><p>表单模板</p> <p>自适应表单</p> </td> 
   <td><p>此选项允许用户在发布表单时指定表单的呈现格式：</p> 
    <ul> 
     <li>HTML</li> 
     <li>PDF</li> 
     <li>两者</li> 
    </ul> <p>此选项用于限制仅在对最终用户可见的表单门户上呈现格式。</p> </td> 
  </tr> 
  <tr> 
   <td>标记</td> 
   <td>除资源外</td> 
   <td>与表单关联的标签，以便于快速、轻松地搜索。</td> 
  </tr> 
  <tr> 
   <td>引用</td> 
   <td><p>自适应表单</p> <p>表单模板</p> <p>资源</p> </td> 
   <td><p>此表单所关联的资产（其他表单或资源）列表。 这些资产可以分为以下两类：</p> 
    <ul> 
     <li>指：当前表单引用的资产。</li> 
     <li>引用者：指流动资产的资产。</li> 
    </ul> <p>这些资产显示为链接，单击即可直接访问它们的元数据。<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>表单模型(XDP/XSD)选择</td> 
   <td>自适应表单</td> 
   <td><p>指定创作自适应表单时使用的表单模型。 此属性可以具有以下值：</p> 
    <ul> 
     <li>表单模板：从存储库中现有的表单模板中选择表单模板。 此值可以更新。</li> 
     <li>XML架构：上传XSD文件。 此值可以更新。</li> 
     <li>无</li> 
    </ul> 
    <div>
      选择表单模型后，可以更新但不能删除该模型。 
    </div> </td> 
  </tr> 
 </tbody> 
</table>

## 查看表单元数据 {#view-form-metadata}

资产具有现有的属性值，这些属性值可在只读模式下查看。 此元数据在表单上传或表单创建时发起。

1. 导航到要查看其元数据的资产位置。

1. 使用以下方法之一打开属性页面：

   1. 单击“快速操作”中的查看属性![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)图标。

      >[!NOTE]
      >
      >快速操作是指将鼠标悬停在缩略图上时显示的操作项目。

   1. 选择表单，然后单击工具栏中显示的查看属性![e_reviewmode_properties_n](assets/e_reviewmode_properties_n.png)图标。
   1. 当不在选择模式下时，通过单击表单缩略图导航到表单详细信息页面。 现在，单击右上角的![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)眼睛图标，然后单击右下方列表中的“属性”。

1. 打开的属性页面会显示一个架构，其中仅包含那些包含某些值的元数据属性。

   属性页面的工具栏包含两个操作图标：

   * 编辑：![aem6forms_edit](assets/aem6forms_edit.png)编辑元数据属性值
   * 查看：![aem6forms_eye_viewon](assets/aem6forms_eye_viewon.png)导航到表单详细信息页面，该页面会在预览模式下打开表单。

   内容部分分为两部分：

   * 左侧面板包含表单的缩略图
   * 右侧面板包含只读模式下的元数据属性，这些属性分布于各种选项卡中。


## 添加/更新表单元数据值 {#add-update-form-metadata-values}

您可以编辑现有元数据属性的值，或向现有元数据属性字段添加新值（例如，当元数据字段为空时）。

### 更新元数据属性值 {#update-metadata-property-values}

1. 按照上一节中所述的步骤，打开可在其中查看所选表单现有元数据的属性页面。

1. 在工具栏中，单击编辑图标![aem6forms_edit](assets/aem6forms_edit.png) ，将页面模式从只读更改为读/写。

1. 打开的属性页面包含一个架构，其中包含可编辑的输入字段和静态文本的混合内容。

1. 静态文本中显示的属性是您无法编辑的属性。

1. 您可以导航到其他选项卡，以查找放置在其下方的元数据属性的输入字段。

   此页面的工具栏包含两个与查看模式不同的操作图标：

   * 取消：![aem6forms_close](assets/aem6forms_close.svg_w24.png)取消迄今为止对元数据属性值所做的任何更改
   * 完成：![aem6forms_check](assets/aem6forms_check.png)保存迄今为止对元数据属性值所做的所有更改

   这两个操作都会将用户引导回包含更新值的属性页面的只读模式。

### 更新表单缩略图 {#update-the-form-thumbnail}

属性页面中的左侧面板显示表单的缩略图。 默认情况下，显示的缩略图是在表单创建（自适应表单）或表单上传时生成的缩略图。

对于所有表单类型，您都可以选择通过单击&#x200B;**[!UICONTROL 上传图像]**&#x200B;并从本地目录浏览图像文件来上传图像。 选定的图像将用作缩略图，而不是默认的缩略图。

对于自适应表单，提供了额外的功能，该功能允许用户生成缩略图作为当前自适应表单预览的快照。 由于AEM Forms还支持自适应表单的创作，因此每当您更改自适应表单时，自适应表单的预览可能会发生更改。 生成缩略图的功能可帮助您根据当前预览状态为自适应表单获取新的缩略图。 单击&#x200B;**[!UICONTROL 生成预览]**&#x200B;以执行此操作。

>[!NOTE]
>
>* 缩览图使用方形图像。 当您使用非方形图像并在列表视图中查看缩略图时，缩略图会被剪贴。
>* 上传或生成新图像后，缩略图将被此图像替换，无法重置为之前的图像。

>



## 添加自定义元数据 {#add-custom-metadata}

除了开箱即用提供的元数据之外，AEM Forms还支持新的自定义元数据。

提供了一种工具（元数据架构编辑器），用于定义元数据布局的架构；即，表单&#x200B;**[!UICONTROL Properties]**&#x200B;页面中显示内容的布局。 利用元数据架构编辑器，可添加或修改资产的自定义架构。

AEM Forms在此工具中公开了支持的表单类型的元数据架构。 这样，您就可以访问这些架构，并使用元数据架构编辑器中提供的功能来添加自定义属性。

### 导航元数据架构编辑器 {#navigate-the-metadata-schema-editor}

1. 导航到&#x200B;**[!UICONTROL 工具>资产>元数据架构]**。

1. 从列出的架构表单中，单击&#x200B;**[!UICONTROL forms]**。

1. 在打开的列表中，单击要为其添加自定义元数据的资产类型。

   >[!NOTE]
   >
   >这些架构包含现成提供的元数据属性，这些属性不得更改/编辑（选中复选框，然后单击工具栏中的编辑），以避免出现功能问题。

1. 单击的任何资产类型都会打开包含`extendedmetadata`选项的列表。 编辑此架构。

1. 选中`extendedmetadata`旁边的复选框，然后单击工具栏中显示的编辑![aem6forms_edit](assets/aem6forms_edit.png)图标。

1. AEM Forms会打开选定资产类型的元数据架构编辑器/表单生成器（在本例中为自适应表单）。

   ![自适应表单类型的元数据架构编辑器](assets/metadata-schema-editor-for-adaptive-form-type.png)

   元数据编辑器

   1. 左侧面板包含放置字段的选项卡部分，右侧面板显示所有可用的UI组件以及从左侧面板中选择的字段的属性。

   1. 锁定的部分不可编辑，其中包含现成提供的所有元数据属性的字段。

   1. 您可以通过单击+符号添加其他选项卡。

   1. 您可以添加所需类型的自定义字段，方法是将&#x200B;**[!UICONTROL 构建表单]**&#x200B;部分中的字段组件拖动到架构页面。
   1. 单击该字段后，可在&#x200B;**[!UICONTROL Settings]**&#x200B;部分下提供此字段的规范。

### 在架构编辑器中添加自定义元数据属性 {#add-custom-metadata-property-in-schema-editor}

1. 导航到要在其中添加自定义属性的选项卡（现有或新）。

1. 将所需类型的组件从&#x200B;**[!UICONTROL 构建表单]**&#x200B;部分拖至左侧面板，并放置在方便的位置。

   >[!NOTE]
   >
   >您无法移动锁定的部分，但可以将组件放置在任何空格中。

1. 单击之前拖动的组件。 在右侧面板中打开的设置选项卡中，填写以下字段的信息：

   1. 指定字段标签，该标签将用作架构中放置的字段上方的显示名称(例如：部门)
   1. 在映射到属性字段下，您可以看到预填充的值&#x200B;**`。/jcr:content/metadata/default`**。 将“**default**”更改为所需的属性名称，该属性名称用于将属性存储在crx存储库中(例如：&#39;。/jcr:content/metadata/department&#39;)

      >[!NOTE]
      >
      >请勿更改前缀“。/jcr:content/metadata/&#39; ，它定义存储属性的路径。
      >
      >此外，属性名称必须是唯一的，以避免为存储库中同一位置的两个或多个属性写入值。 因此，建议您更改值“default”。

   1. 根据需要填写其他设置。 例如：如果要将字段设为必填字段，请选择“必填”选项。
   1. 要删除添加的字段，请选择该字段，然后单击删除![delete-1](assets/delete-1.png)图标。

1. 如有必要，请按照步骤1-3添加其他属性。
1. 进行所有更改后，单击&#x200B;**完成**。

   您已成功添加自定义元数据属性。

AEM Forms中的所有自适应表单现在都包含此附加的元数据属性。 您可以从属性页面中编辑该属性。
