---
title: 批量编辑器
description: 了解如何在不需要可视化页面上下文时使用批量编辑器进行有效编辑。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: c63e044c-4d2a-44d3-853b-8e7337e1ee03
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: eae057caed533ef16bb541b4ad41b8edd7aaa1c7
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 0%

---


# 批量编辑器{#the-bulk-editor}

当不需要可视页面上下文时，批量编辑器允许进行有效编辑，因为它允许您：

* 搜索（和显示）多个页面中的内容；可使用GQL(Google查询语言)完成此操作
* 直接在批量编辑器中编辑此内容
* 保存更改（到原始页面）
* 将此内容导出到以制表符分隔的(.tsv)电子表格文件

>[!NOTE]
>
>您也可以将内容导入存储库，但默认情况下，批量编辑器将禁用此功能，因为可在 **工具** 控制台。

本节介绍如何在中使用批量编辑器 **工具** 控制台。 通常，管理员使用批量编辑器来搜索和编辑多个项目。 通过使用GQL查询填充表，然后选择要处理的内容项来做到这一点。 作者通常使用批量编辑器作为自定义批量编辑器应用程序的一部分，可通过访问 [产品列表](/help/sites-authoring/default-components.md#productlist) 组件。

>[!CAUTION]
>
>使用 [弃用经典UI](/help/release-notes/deprecated-removed-features.md) 在AEM 6.4中，批量编辑器已被弃用，因此Adobe不打算进一步增强批量编辑器。

## 批量编辑器的示例用例 {#example-use-case-for-the-bulk-editor}

例如，如果您需要填写特定调查的用户的所有姓名和电子邮件地址，批量编辑器可以提供该信息，并且您可以将它导出到电子表格中。

Geometrixx网站中包含一个说明此用例的示例：

1. 导航至 **支持** 页面，然后转到 **客户服务满意度** 调查。
1. **编辑** 该 **表单的开头** 段落。 在对话框中，单击 **高级** 选项卡，展开 **操作配置**，然后单击 **查看数据……**.

   ![客户满意度调查示例](assets/custsatsurvey.png)

1. 批量编辑器是完全可自定义的，不过在此示例中，批量编辑器不允许用户编辑内容，但仅允许用户将信息导出到电子表格。

   ![批量编辑器控制台](assets/bulkeditor.png)

## 如何使用批量编辑器 {#how-to-use-the-bulk-editor}

通过批量编辑器，您可以：

* [根据查询参数搜索内容，以列形式显示结果的指定属性，编辑此内容并保存更改](#searching-and-editing-content)
* [以将此内容导出到以制表符分隔的电子表格](#exporting-content)

* [从制表符分隔的电子表格导入内容](#importing-content)

### 搜索和编辑内容 {#searching-and-editing-content}

要使用批量编辑器同时编辑多个项目，请执行以下操作：

1. 在 **工具** 控制台，单击 **导入程序** 文件夹以展开它。
1. 双击 **批量编辑器**.
1. 输入您的选择要求：

<table>
 <tbody>
  <tr>
   <td>字段</td>
   <td>属性</td>
  </tr>
  <tr>
   <td>根路径</td>
   <td>指示批量编辑器搜索的根路径。<br /> 例如， <code>/content/geometrixx/en</code>. 批量编辑器将搜索所有子节点。</td>
  </tr>
  <tr>
   <td>查询参数</td>
   <td>使用GQL参数，输入您希望批量编辑器在存储库中查找的搜索字符串。 例如， <code>type:Page</code> 查找根路径中的所有页面， <code>text:professional</code> 查找所有包含“professional”一词的页面，并且 <code>"jcr:title":English</code> 查找所有标题为“English”的页面。 您只能搜索字符串。</td>
  </tr>
  <tr>
   <td>“内容模式”复选框</td>
   <td>选中此复选框，以便您可以读取 <code>jcr:content</code> 搜索结果的子节点（如果存在）。 仅用于页面。 属性名称带有前缀 <code>"jcr:content/"</code></td>
  </tr>
  <tr>
   <td>属性/列</td>
   <td>选中希望Bulk Editor返回的属性的复选框。 您选择的属性是结果窗格中的列标题。 缺省情况下，节点路径显示在结果中。</td>
  </tr>
  <tr>
   <td>自定义属性/列</td>
   <td>输入未在 <strong>属性/列</strong> 字段。 这些自定义属性会显示在结果窗格中。 您可以使用逗号分隔多个属性，以添加多个属性。 <i>注意：</i> 如果添加尚不存在的自定义属性，AEM WCM将显示空单元格。 修改并保存空单元格时，该属性将添加到节点中。 新创建的属性必须遵循节点类型约束和属性命名空间。</td>
  </tr>
 </tbody>
</table>

例如：

![批量编辑器过滤器选项](assets/searchfilter.png)

1. 单击 **Search**. 批量编辑器将显示结果。
以上示例中，将返回符合搜索条件的所有页面，并显示所请求的列。

   ![批量编辑器结果](assets/chlimage_1-39.png)

1. 双击单元格，以便进行任何更改。

   ![批量编辑](assets/srchresultedit.png)

1. 单击 **保存** 以保存更改( **保存** 按钮会在您编辑单元格后激活)。

   >[!CAUTION]
   >
   >您在此处所做的更改将写入存储库内容；例如，中引用的页面 **路径**.

#### 其他GQL查询参数 {#additional-gql-query-parameters}

* **路径：** 仅搜索此路径下的节点。 如果指定了多个带有路径前缀的术语，则只考虑最后一个术语。
* **类型：** 仅返回给定节点类型的节点。 这包括主要和mixin类型。 您可以指定多个逗号分隔的节点类型。 GQL返回任何指定类型的节点。
* **订购：** 按给定属性对结果进行排序。 您可以指定多个以逗号分隔的属性名称。 要以降序排序结果，只需在属性名称的前面加一个减号即可。 例如，order：-name。 使用加号将按升序返回结果，这也是默认设置。
* **限制：** 使用间隔限制结果的数量。 例如，limit：10..20间隔从零开始，开始是包含的，结束是排除的。 您还可以指定一个open `interval:limit:10..` 或 `limit:..20`
如果省略这些点并且只指定了一个值，则GQL最多返回此数量的结果。 例如， `limit:10` （返回前十个结果）。

### 导出内容 {#exporting-content}

如有必要，可将内容导出到Excel电子表格以进行任何更改。 例如，您可能希望导出邮件列表，并直接在Excel中更改列出的所有电话号码的区号，或添加其他行。

要导出内容，请执行以下操作：

1. 搜索内容（如所述） [搜索和编辑内容](#searching-and-editing-content).
1. 单击 **导出** 以便您可以将更改导出到制表符分隔的Excel电子表格中。 AEM WCM会询问您要将文件下载到的位置。

   >[!NOTE]
   >
   >默认情况下，更改将编码在 [Windows-1252](https://en.wikipedia.org/wiki/Windows-1252) （也称为CP-1252）。 您可以选中UTF-8以将UTF-8中的更改导出。

   ![导出结果](assets/srchrsesultexport.png)

1. 选择位置并确认您要下载该文件。
1. 下载文件后，您可以从电子表格程序(例如，Microsoft® Excel)中打开它。 电子表格程序会导入文件并将其转换为电子表格格式。

   ![电子表格中的导出结果](assets/exportinexcel.png)

### 导入内容 {#importing-content}

默认情况下，当您打开“批量编辑器”时，导入功能处于隐藏状态。 只需添加参数 `hib=false` 到URL时显示 **导入** 按钮。 您可以从任何制表符分隔的形式( `.tsv`)文件。 要使导入正常工作，列标题（单元格的第一行）必须与要导入到的表的列标题匹配。

>[!NOTE]
>
>重新导入内容时，将擦除这些节点之前的任何内容。 请注意不要覆盖重要信息。

要导入内容：

1. 打开批量编辑器。
1. 添加 `?hib=false` 到URL，例如：
   `https://localhost:4502/etc/importers/bulkeditor.html?hib=false`
1. 单击 **导入**.
1. 选择 `.tsv` 文件。 数据将导入到存储库中。
