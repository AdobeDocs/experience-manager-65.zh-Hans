---
title: 配置富文本编辑器插件
description: 了解如何配置Adobe Experience Manager富文本编辑器插件以启用各个功能。
contentOwner: AG
exl-id: 6bfd6caa-a68a-40ba-9826-4ba02cd1dbfb
translation-type: tm+mt
source-git-commit: 443115b306ff34ee98da9403222874a9700d8aed
workflow-type: tm+mt
source-wordcount: '4397'
ht-degree: 3%

---

# 配置富文本编辑器插件{#configure-the-rich-text-editor-plug-ins}

RTE功能通过一系列插件提供，每个插件都具有features属性。 您可以配置features属性以启用或禁用一个或多个RTE功能。 本文具体介绍如何配置RTE插件。

有关其他RTE配置的详细信息，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。

>[!NOTE]
>
>使用CRXDE Lite时，建议使用[!UICONTROL 保存全部]选项定期保存更改。

## 激活插件并配置features属性{#activateplugin}

要激活插件，请按照以下步骤操作。 仅当您首次配置插件时，才需要执行某些步骤，因为相应的节点不存在。

默认情况下，RTE中启用了`format`、`link`、`list`、`justify`和`control`插件及其所有功能。

>[!NOTE]
>
>为避免在本文中出现重复，相应的`rtePlugins`节点称为`<rtePlugins-node>`。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在配置任何RTE插件之前，创建`<rtePlugins-node>`的父节点（如果它不存在）：

   * 根据您的组件，父节点为：

      * `config: .../text/cq:editConfig/cq:inplaceEditing/config`
      * 备用配置节点：`.../text/cq:editConfig/cq:inplaceEditing/inplaceEditingTextConfig`
      * `text: .../text/dialog/items/tab1/items/text`
   * 类型：**jcr:primaryType** `cq:Widget`
   * 二者都具有以下属性：

      * **名称** `name`
      * **类型** `String`
      * **值** `./text`


1. 根据要配置的接口，如果节点不存在，请创建节点`<rtePlugins-node>`:

   * **名称** `rtePlugins`
   * **类型** `nt:unstructured`

1. 在下面，为要激活的每个插件创建一个节点：

   * **类型** `nt:unstructured`
   * **命** 名所需的插件的插件ID

激活插件后，请遵循以下准则配置`features`属性。

|  | 启用所有功能 | 启用一些特定功能 | 禁用所有功能 |
|---|---|---|---|
| 名称 | 功能 | 功能 | 功能 |
| 类型 | 字符串 | String[](多字符串；将类型设置为“字符串”并单击“多重”(CRXDE Lite) | 字符串 |
| 值 | `*` （星号） | 设置为一个或多个特征值 | - |

## 了解findreplace插件{#findreplace}

`findreplace`插件不需要任何配置。 它开箱即用。

使用替换功能时，应与查找字符串同时输入要替换的替换字符串。 但是，在替换字符串之前，您仍可以单击“查找”以搜索该字符串。 如果在单击“查找”后输入替换字符串，则搜索将重置为文本的开头。

单击查找时，查找和替换对话框变得透明，单击替换时变得不透明。 这允许作者审阅作者将替换的文本。 如果用户单击“全部替换”，对话框将关闭并显示所做替换的数量。

## 配置粘贴模式{#paste-modes}

使用RTE时，作者可以在以下三种模式之一粘贴内容：

* **浏览器模式**:使用浏览器的默认粘贴实现粘贴文本。它不是推荐的方法，因为它可能引入不需要的标记。

* **纯文本模式**:将剪贴板内容粘贴为纯文本。在[!DNL Experience Manager]组件中插入之前，它会删除复制内容中的所有样式和格式元素。

* **MS Word模式**:从MS Word复制时，粘贴带有格式的文本（包括表格）。不支持从其他源（如网页或MS Excel）复制和粘贴文本，并仅保留部分格式。

### 配置RTE工具栏{#configure-paste-options-available-on-the-rte-toolbar}上可用的粘贴选项

可以在RTE工具栏中为作者提供以下三个图标中的一些、全部或无图标：

* **[!UICONTROL 粘贴(Ctrl+V)]**:可以预先配置以与上述三种“粘贴”模式之一相对应。

* **[!UICONTROL 粘贴为文本]**:提供纯文本模式功能。

* **[!UICONTROL 从Word粘贴]**:提供MS Word模式功能。

要配置RTE以显示所需的图标，请执行以下步骤。

1. 导航到您的组件，例如`/apps/<myProject>/components/text`。
1. 导航到节点`rtePlugins/edit`。 如果节点不存在，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点上创建`features`属性并添加一个或多个功能。 保存所有更改。

### 配置粘贴(Ctrl+V)图标和快捷键{#configure-the-behavior-of-the-paste-ctrl-v-icon-and-shortcut}的行为

可以使用以下步骤预配置&#x200B;**[!UICONTROL 粘贴(Ctrl+V)]**&#x200B;图标的行为。 此配置还定义作者用于粘贴内容的键盘快捷键Ctrl+V的行为。

配置允许以下三种类型的使用案例：

* 使用浏览器的默认粘贴实现粘贴文本。 它不是推荐的方法，因为它可能引入不需要的标记。 使用下面的`browser`进行配置。

* 将剪贴板内容粘贴为纯文本。 在AEM组件中插入之前，它会去除复制内容中的所有样式和格式元素。 使用下面的`plaintext`进行配置。

* 从MS Word复制时，粘贴带有格式的文本（包括表格）。 不支持从其他源（如网页或MS Excel）复制和粘贴文本，并仅保留部分格式。 使用下面的`wordhtml`进行配置。

1. 在您的组件中，导航到`<rtePlugins-node>/edit`节点。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点中，使用以下详细信息创建一个属性：

   * **名称** `defaultPasteMode`
   * **类型** `String`
   * **** 值所需的粘贴模式 `browser` `plaintext`或之一 `wordhtml`。

### 配置粘贴内容{#pasteformats}时允许的格式

可以进一步配置粘贴为Microsoft-Word(`paste-wordhtml`)模式，以便您能够显式定义从其他项目（如Microsoft Word）在AEM中粘贴时允许使用哪些样式。

例如，如果在AEM中粘贴时应仅允许使用粗体格式和列表，则可以过滤掉其他格式。 这称为可配置粘贴过滤，可针对以下两种情况执行此操作：

* [文本](#paste-modes)
* [链接](#linkstyles)

对于链接，您还可以定义自动接受的协议。

要配置将文本从其他项目粘贴到AEM时允许使用的格式，请执行以下操作：

1. 在您的组件中，导航到节点`<rtePlugins-node>/edit`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`edit`节点下创建一个节点以保存HTML粘贴规则：

   * **名称** `htmlPasteRules`
   * **类型** `nt:unstructured`

1. 在`htmlPasteRules`下创建一个节点，以保存允许的基本格式的详细信息：

   * **名称** `allowBasics`
   * **类型** `nt:unstructured`

1. 要控制接受的各个格式，请在`allowBasics`节点上创建以下一个或多个属性：

   * **名称** `bold`
   * **名称** `italic`
   * **名称** `underline`
   * **名称** `anchor` （用于链接和命名锚记）
   * **名称** `image`

   所有属性均为&#x200B;**Type** `Boolean`，因此在相应的&#x200B;**Value**&#x200B;中，您可以选择或删除复选标记以启用或禁用该功能。

   >[!NOTE]
   >
   >如果未显式定义，则使用默认值true并接受格式。

1. 也可以使用一系列其他属性或节点来定义其他格式，这些属性或节点也应用于`htmlPasteRules`节点：

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>类型</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td>allowBlockTags</td>
   <td>String[]</td>
   <td><p>定义允许的块标记列表。</p> <p>几个可能的块标记包括：</p>
    <ul>
     <li>标题(h1、h2、h3)</li>
     <li>(p)段</li>
     <li>列表(ol、ul)</li>
     <li>表（表）</li>
    </ul> </td>
  </tr>
  <tr>
   <td>fallbackBlockTag</td>
   <td>字符串</td>
   <td><p>定义块标记，该标记用于任何块，这些块具有未包含在allowBlockTags中的块标记。</p> <p> 在大多数情况下，p就够了。</p> </td>
  </tr>
  <tr>
   <td>表</td>
   <td>nt:unstructured</td>
   <td><p>定义粘贴表时的行为。<br /> </p> <p>此节点必须具有属性<code>allow</code>（类型<code>Boolean</code>），以定义是否允许粘贴表。</p> <p>如果将<code>allow</code>设置为<code>false</code>，则必须指定属性<code>ignoreMode</code>（类型<code> String</code>）以定义如何处理粘贴的表内容。 <code>ignoreMode</code>的有效值为：</p>
    <ul>
     <li><code>remove</code>:删除表内容。</li>
     <li><code>paragraph</code>:将表单元格转换为段落。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>列表</td>
   <td>nt:unstructured</td>
   <td><p>定义粘贴列表时的行为。<br /> </p> <p>必须具有属性<code>allow</code>（键入<code>Boolean</code>）来定义是否允许粘贴列表。</p> <p>如果将<code>allow</code>设置为<code>false</code>，则必须指定属性<code>ignoreMode</code>（键入<code>String</code>）以定义如何处理粘贴的任何列表内容。 <code>ignoreMode</code>的有效值为：</p>
    <ul>
     <li><code>remove</code>:删除列表内容。</li>
     <li><code>paragraph</code>:将列表项目转换为段落。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

有效`htmlPasteRules`结构的示例：

```xml
"htmlPasteRules": {
    "allowBasics": {
        "italic": true,
        "link": true
    },
    "allowBlockTags": [
        "p", "h1", "h2", "h3"
    ],
    "list": {
        "allow": false,
        "ignoreMode": "paragraph"
    },
    "table": {
        "allow": true,
        "ignoreMode": "paragraph"
    }
}
```

1. 保存所有更改。

## 配置文本样式{#textstyles}

作者可以应用样式来更改部分文本的外观。 这些样式基于您在CSS样式表中预定义的CSS类。 格式化内容使用`class`属性包含在`span`标签中以引用CSS类。 例如：

`<span class=monospaced>Monospaced Text Here</span>`

首次启用样式插件时，不提供默认样式。 弹出列表为空。 要为作者提供样式，请执行以下操作：

* 启用样式下拉选择器。
* 指定样式表的位置。
* 指定可从“样式”下拉列表中选择的单个样式。

对于以后（重新）的配置，例如要添加更多样式，请仅按照说明引用新样式表并指定其他样式。

>[!NOTE]
>
>还可以为[表或表单元格](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles)定义样式。 这些配置需要不同的过程。

### 启用样式下拉选择器列表{#styleselectorlist}

通过启用样式插件即可完成此操作。

1. 在您的组件中，导航到节点`<rtePlugins-node>/styles`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`styles`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

1. 保存所有更改。

>[!NOTE]
>
>启用样式插件后，“样式”下拉列表将显示在编辑对话框中。 但是，列表为空，因为未配置样式。

### 指定样式表位置{#locationofstylesheet}

然后，指定要引用的样式表的位置：

1. 导航到文本组件的根节点，例如`/apps/<myProject>/components/text`。
1. 将属性`externalStyleSheets`添加到`<rtePlugins-node>`的父节点：

   * **名称** `externalStyleSheets`
   * **Type** `String[]` (多字符串；单击 **** 多重CRXDE)
   * **值要包含** 的每个样式表的路径和文件名。使用存储库路径。

   >[!NOTE]
   >
   >您可以在以后随时添加对其他样式表的引用。

1. 保存所有更改。

>[!NOTE]
>
>在对话框（经典UI）中使用RTE时，您可能希望指定为富文本编辑而优化的样式表。 由于技术限制，CSS上下文在编辑器中丢失，因此您可能希望模拟此上下文以改进所见即所得的体验。
>
>富文本编辑器使用ID为`CQrte`的容器 DOM元素，该元素可用于提供不同的样式以供查看和编辑：
>
>
```
>#CQ td {
> // defines the style for viewing
> }
>```
>
>
```
>#CQrte td {
> // defines the style for editing
> }
>```

### 在弹出列表{#stylesindropdown}中指定可用的样式

1. 在组件定义中，导航到节点`<rtePlugins-node>/styles`，如[启用样式下拉选择器](#styleselectorlist)中所创建。
1. 在节点`styles`下，创建一个新节点（也称为`styles`）以保存要使用的列表:

   * **名称** `styles`
   * **类型** `cq:WidgetCollection`

1. 在`styles`节点下创建一个新节点以表示单个样式：

   * **名称**，您可以指定名称，但应适合样式
   * **类型** `nt:unstructured`

1. 将属性`cssName`添加到此节点以引用CSS类：

   * **名称** `cssName`
   * **类型** `String`
   * **值** CSS类的名称(没有前面的“。”;例如，`cssClass`而不是`.cssClass`

1. 将属性`text`添加到同一节点；这定义了选择框中显示的文本：

   * **名称** `text`
   * **类型** `String`
   * **** 值样式描述；显示在“样式”(Style)下拉选择框中。

1. 保存更改。

   对每个所需样式重复上述步骤。

### 配置RTE，以使用日语{#jpwordwrap}实现最佳换行

使用AEM创作日文内容的作者可以将样式应用于字符，以避免在不需要换行时换行。 这允许作者让句子在所需位置断开。 此功能的样式基于CSS样式表中预定义的CSS类。

>[!NOTE]
>
>此功能至少需要AEM 6.5 Service Pack 1。

要创建作者可应用于日文文本的样式，请执行以下步骤：

1. 在样式节点下创建新节点。 请参阅[指定新样式](#stylesindropdown)。
   * 名称: `jpn-word-wrap`
   * 类型：&#39;nt:unstructure

1. 将属性`cssName`添加到节点以引用CSS类。 此类名称是日文换行功能的保留名称。
   * 名称: `cssName`
   * 类型: `String`
   * 值：`jpn-word-wrap`（没有前面的`.`）

1. 将属性文本添加到同一节点。 该值是作者在选择样式时看到的样式名称。
   * 名称：`text`
*类型： 
`String`
   * 值: `Japanese word-wrap`

1. 创建样式表并指定其路径。 请参阅[指定样式表](#locationofstylesheet)的位置。 将以下内容添加到样式表。 根据需要更改背景颜色。

   ```css
   .text span.jpn-word-wrap {
       display:inline-block;
   }
   .is-edited span.jpn-word-wrap {
       background-color: #ffddff;
   }
   ```

   ![使作者可使用日文换行功能的样式表](assets/rte_jpwordwrap_stylesheet.jpg)

## 配置段落格式{#paraformats}

在RTE中创作的任何文本都放置在块标记中，默认为`<p>`。 通过启用`paraformat`插件，可使用下拉选择列表指定可分配给段落的其他块标记。 段落格式通过指定正确的块标记来确定段落类型。 作者可以使用“格式”选择器选择和分配它们。 示例块标签包括标准段落&lt;p>和标题&lt;h1>、&lt;h2>等。

>[!CAUTION]
>
>此插件不适用于结构复杂的内容，如列表或表。

>[!NOTE]
>
>如果无法将块标记（例如&lt;hr>标记）分配给段落，则它对于段落格式插件不是有效的用例。

首次启用“段落格式”插件时，不提供默认的段落格式。 弹出列表为空。 要为作者提供段落格式，请执行以下操作：

* 启用“格式”下拉选择器列表。
* 指定可从下拉列表中选择为段落格式的块标记。

对于以后（重新）的配置，例如要添加更多格式，请仅按照说明的相关部分操作。

### 启用“格式”下拉选择器{#formatselectorlist}

首先启用参数格式插件：

1. 在您的组件中，导航到节点`<rtePlugins-node>/paraformat`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`paraformat`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*` （星号）

>[!NOTE]
如果未进一步配置插件，则启用以下默认格式：
* 段落 ( `<p>`)
* 标题 1 ( `<h1>`)
* 标题 2 ( `<h2>`)
* 标题 3 ( `<h3>`)



>[!CAUTION]
配置RTE的段落格式时，请勿将段落标记&lt;p>作为格式选项删除。 如果删除了`<p>`标记，则内容作者无法选择&#x200B;**段落格式**&#x200B;选项，即使配置了其他格式也是如此。

### 指定可用的段落格式{#paraformatsindropdown}

段落格式可通过以下方式进行选择：

1. 在组件定义中，导航到节点`<rtePlugins-node>/paraformat`，如在[启用格式下拉选择器](#styleselectorlist)中创建的。
1. 在`paraformat`节点下创建新节点，以保存格式列表:

   * **名称** `formats`
   * **类型** `cq:WidgetCollection`

1. 在`formats`节点下创建新节点，它保存单个格式的详细信息：

   * **名称**，您可以指定名称，但该名称应适合格式（例如，myparagraph， myheading1）。
   * **类型** `nt:unstructured`

1. 对于此节点，添加属性以定义使用的块标记：

   * **名称** `tag`
   * **类型** `String`
   * **** 值格式的块标签；例如：p、h1、h2等。

      您无需输入定界尖括号。

1. 对于同一节点，添加另一个属性，以使描述性文本显示在下拉列表中：

   * **名称** `description`
   * **类型** `String`
   * **值** 此格式的描述性文本；例如，“段落”、“标题1”、“标题2”等。此文本将显示在“格式”选择列表中。

1. 保存更改。

   对每个所需格式重复这些步骤。

>[!CAUTION]
如果定义自定义格式，则会删除默认格式（`<p>`、`<h1>`、`<h2>`和`<h3>`）。 重新创建`<p>`格式，因为它是默认格式。

## 配置特殊字符{#spchar}

在标准AEM安装中，当为特殊字符(`specialchars`)启用`misctools`插件时，将立即可使用默认选择；例如，copyright和trademark符号。

您可以配置RTE，以使您自己选择的字符可用；通过定义不同的字符或整个序列。

>[!CAUTION]
添加自己的特殊字符将覆盖默认选择。 如果需要，请（重新）在您自己的选择中定义这些字符。

### 定义单个字符{#definesinglechar}

1. 在您的组件中，导航到节点`<rtePlugins-node>/misctools`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`misctools`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String[]`
   * **值** `specialchars`

          （或`String / *`，如果应用此插件的所有功能）

1. 在`misctools`下创建一个节点以保存特殊字符配置：

   * **名称** `specialCharsConfig`
   * **类型** `nt:unstructured`

1. 在`specialCharsConfig`下创建另一个节点以保存字符列表:

   * **名称** `chars`
   * **类型** `nt:unstructured`

1. 在`chars`下添加一个新节点以保存单个字符定义：

   * **名** 称可以指定名称，但应反映字符；例如，一半。
   * **类型** `nt:unstructured`

1. 要添加到此节点，请添加以下属性：

   * **名称** `entity`
   * **类型** `String`
   * **** 评估所需字符的HTML表示形式；例如， `&189;` 分数半。

1. 保存更改。

在CRXDE中，保存属性后，将显示所表示的字符。 请参见下面的“一半”示例。 重复上述步骤，使作者可以使用更多特殊字符。

![在CRXDE中，添加一个要在RTE工具栏中可用的单](assets/chlimage_1-106.png "个字符在CRXDE中，添加一个要在RTE工具栏中可用的单个字符")

### 定义字符范围{#definerangechar}

1. 使用[定义单个字符](#definesinglechar)中的步骤1到3。
1. 在`chars`下添加一个新节点以保存字符范围的定义：

   * **名** 称可以指定名称，但应反映字符范围；比如铅笔。
   * **类型** `nt:unstructured`

1. 在此节点（根据特殊字符范围命名）下添加以下两个属性：

   * **名称** `rangeStart`

      **类型** `Long`
      **值**  [](https://unicode.org/) 范围中第一个字符的Unicoderepresentation（十进制）

   * **名称** `rangeEnd`

      **类型** `Long`
      **值**  [](https://unicode.org/) 范围中最后一个字符的Unicoderepresentation（十进制）

1. 保存更改。

   例如，定义范围为9998 - 10000时提供以下字符。

   ![在CRXDE中，定义要在RTE中可用的字符范围](assets/chlimage_1-107.png)

   *图：在CRXDE中，定义要在RTE中可用的字符范围*

   ![RTE中的可用特殊字符在弹出窗口中显示给作者](assets/rtepencil.png "RTE中的可用特殊字符在弹出窗口中向作者显示")

## 配置表样式{#tablestyles}

样式通常应用于文本，但也可以对表或几个表单元格应用一组单独的样式。 从“单元格属性”或“表属性”对话框的“样式”选择器框中，作者可以使用这种样式。 当在文本组件（或衍生组件）中编辑表时，而不是在标准表组件中编辑表时，这些样式可用。

>[!NOTE]
您只能为经典UI定义表和单元格的样式。

>[!NOTE]
在RTE组件中或从RTE组件中复制和粘贴表取决于浏览器。 并非所有浏览器都支持开箱即用。 根据表结构和浏览器，您可能会获得不同的结果。 例如，当您在经典UI和触屏UI中复制和粘贴Mozilla Firefox中RTE组件中的表时，不会保留表的布局。

1. 在组件中，导航到节点`<rtePlugins-node>/table`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`table`节点上创建`features`属性：

   * **名称** `features`
   * **类型** `String`
   * **值** `*`

   >[!NOTE]
   如果不想启用所有表功能，可以创建`features`属性：
   * **类型** `String[]`

   * **值** 1或2，如下所示：
      * `table` 允许编辑表属性；包括样式。
      * `cellprops` 以允许编辑单元格属性，包括样式。


1. 定义CSS样式表的位置以引用这些样式表。 请参阅[指定样式表的位置](#locationofstylesheet)，因为这与定义文本](#textstyles)的[样式时相同。 如果您定义了其他样式，则可以定义位置。
1. 在`table`节点下，创建以下新节点（根据需要）：

   * 定义整个表的样式（可在&#x200B;**表属性**&#x200B;下找到）：

      * **名称** `tableStyles`
      * **类型** `cq:WidgetCollection`
   * 定义单个单元格的样式（可在&#x200B;**单元格属性**&#x200B;下使用）：

      * **名称** `cellStyles`
      * **类型** `cq:WidgetCollection`


1. 创建一个新节点(在`tableStyles`或`cellStyles`节点下（视情况而定）)以表示单个样式：

   * **名** 称您可以指定名称，但应反映样式。
   * **类型** `nt:unstructured`

1. 在此节点上创建属性：

   * 定义要引用的CSS样式

      * **名称** `cssName`
      * **类型** `String`
      * **** 值CSS类的名称(例如，不 `.`带前面 `cssClass` 的名 `.cssClass`称)
   * 定义要在下拉选择器中显示的描述性文本

      * **名称** `text`
      * **类型** `String`
      * **值** 要显示在选择列表中的文本


1. 保存所有更改。

对每个所需样式重复上述步骤。

### 为辅助功能{#hiddenheader}配置表中的隐藏标题

有时，您可能会在列标题中创建不带可视文本的数据表（假定该标题的用途由列与其他列的可视关系所隐含）。 在这种情况下，必须在标题单元格的单元格中提供隐藏的内部文本，以允许屏幕阅读器和其他辅助技术帮助有各种需求的读者了解列的用途。

为增强此类情况下的辅助功能，RTE支持隐藏的标题单元格。 此外，它还提供与表中隐藏标题相关的配置设置。 这些设置允许您在编辑和预览模式下对隐藏的标题应用CSS样式。 要帮助作者在编辑模式下识别隐藏的标题，请在代码中包含以下参数：

* `hiddenHeaderEditingCSS`:指定在编辑RTE时应用于隐藏标题单元格的CSS类的名称。
* `hiddenHeaderEditingStyle`:指定在编辑RTE时应用于隐藏标题单元格的样式字符串。

如果在代码中同时指定CSS和样式字符串，则CSS类优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

要帮助作者在预览模式下对隐藏的标题应用CSS，您可以在代码中包含以下参数：

* `hiddenHeaderClassName`:指定在预览模式下应用于隐藏标题单元格的CSS类的名称。
* `hiddenHeaderStyle`:指定在预览模式下应用于隐藏标题单元格的样式字符串。

如果在代码中同时指定CSS和样式字符串，则CSS类优先于样式字符串，并可能覆盖样式字符串所做的任何配置更改。

## 为拼写检查器{#adddict}添加词典

激活拼写检查插件后，RTE将对每种相应语言使用词典。 然后，根据网站的语言选择这些语言，即采用子树的语言属性或从URL中提取语言；例如。 `/en/`分支被选为英语，`/de/`分支被选为德语。

>[!NOTE]
如果尝试检查未安装的语言，则会看到消息`Spell checking failed`。 标准词典与相应的自述文件一起位于`/libs/cq/spellchecker/dictionaries`。 请勿修改文件。

标准AEM安装包含美国英语(`en_us`)和英语(`en_gb`)的词典。 要添加更多词典，请执行以下步骤。

1. 导航到页面[https://extensions.openoffice.org/](https://extensions.openoffice.org/)。

1. 执行下列操作之一以查找您选择的语言的词典：

   * 搜索您选择的语言的词典。 在词典页面上，找到指向原始源或作者网页的链接。 在此页面上找到v2.x的词典文件。
   * 在[https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries](https://wiki.openoffice.org/wiki/User:Khirano/Dictionaries)搜索v2.x词典文件。

1. 下载包含拼写定义的存档。 解压文件系统上的存档内容。

   >[!CAUTION]
   仅支持OpenOffice.org v2.0.1或更早版本的`MySpell`格式的词典。 由于词典现在是存档文件，建议您在下载后验证存档。

1. 找到.aff和.dic文件。 将文件名保持为小写。 例如，`de_de.aff`和`de_de.dic`。
1. 加载位于`/apps/cq/spellchecker/dictionaries`的存储库中的.aff和.dic文件。

>[!NOTE]
RTE拼写检查器可按需使用。 它不会在您开始键入文本时自动运行。 要运行拼写检查器，请单击工具栏中的[!UICONTROL 拼写检查器]。 RTE会检查单词的拼写并突出显示拼写错误的单词。
如果合并了拼写检查器建议的任何更改，则文本更改和拼写错误的单词的状态不再突出显示。 要运行拼写检查器，请再次点按/单击拼写检查器按钮。

## 配置撤消和重做操作的历史记录大小{#undohistory}

RTE允许作者撤消或重做上次的一些编辑。 默认情况下，历史记录中会存储50个编辑。 您可以根据需要配置此值。

1. 在组件中，导航到节点`<rtePlugins-node>/undo`。 如果这些节点不存在，请创建它们。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`undo`节点上创建以下属性：

   * **名称** `maxUndoSteps`
   * **类型** `Long`
   * **值** 您希望在历史记录中保存的撤消步骤数。默认为 50。使用`0`可完全禁用撤消/重做。

1. 保存更改。

## 配置Tab键大小{#tabsize}

当在任何文本中按下制表符字符时，会插入预定义的空格数；默认情况下，这是三个不中断空格和一个空格。

要定义制表符大小，请执行以下操作：

1. 在您的组件中，导航到节点`<rtePlugins-node>/keys`。 如果节点不存在，请创建这些节点。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`keys`节点上创建以下属性：

   * **名称** `tabSize`
   * **类型** `String`
   * **值** 要用于制表符的空格字符数。

1. 保存更改。

## 设置缩进边距{#indentmargin}

启用缩进（默认）后，您可以定义缩进大小：

>[!NOTE]
此缩进大小仅应用于文本的段落（块）；它不会影响实际列表的缩进。

1. 在组件中，导航到节点`<rtePlugins-node>/lists`。 如果这些节点不存在，请创建它们。 有关详细信息，请参阅[激活插件](#activateplugin)。
1. 在`lists`节点上创建`identSize`参数：

   * **名称**: `identSize`
   * **类型**: `Long`
   * **值**:缩进边距所需的像素数。

## 配置可编辑空间的高度{#editablespace}

>[!NOTE]
仅当在对话框中使用RTE时（在经典UI中不是就地编辑），才适用。

您可以定义组件对话框中显示的可编辑空间的高度：

1. 在组件的对话框定义中的`../items/text`节点上，创建新属性：

   * **名称** `height`
   * **类型** `Long`
   * **以** 像素为单位评估编辑画布的高度。

   >[!NOTE]
   这不会更改对话框窗口的高度。

1. 保存更改。

## 为链接{#linkstyles}配置样式和协议

在AEM中添加链接时，您可以定义：

* 要使用的CSS样式
* 协议自动接受

要配置如何从其他项目在AEM中添加链接，请定义HTML规则。

1. 使用CRXDE Lite，找到项目的文本组件。
1. 在与`<rtePlugins-node>`相同的级别创建新节点，即在`<rtePlugins-node>`的父节点下创建节点：

   * **名称** `htmlRules`
   * **类型** `nt:unstructured`

   >[!NOTE]
   `../items/text`节点具有以下属性：
   * **名称** `xtype`
   * **类型** `String`
   * **值** `richtext`

   `../items/text`节点的位置可能因对话框的结构而异；两个示例包括：
   * `/apps/myProject>/components/text/dialog/items/text`
   * `/apps/<myProject>/components/text/dialog/items/panel/items/text`


1. 在`htmlRules`下，创建新节点。

   * **名称** `links`
   * **类型** `nt:unstructured`

1. 在`links`节点下，根据需要定义属性：

   * 内部链接的CSS样式：

      * **名称** `cssInternal`
      * **类型** `String`
      * **** 值CSS类的名称(不带前面的“。”;例如，`cssClass`而不是`.cssClass`
   * 外部链接的CSS样式

      * **名称** `cssExternal`
      * **类型** `String`
      * **** 值CSS类的名称(不带前面的“。”;例如，`cssClass`而不是`.cssClass`
   * 有效&#x200B;**协议**&#x200B;的数组。 支持的协议有`http://`、`https://`、`file://`和`mailto:`。

      * **名称** `protocols`
      * **类型** `String[]`
      * **值** 1或多个协议
   * **defaultProtocol** (String类型的 **属性**):用户未明确指定协议时使用的协议。

      * **名称** `defaultProtocol`
      * **类型** `String`
      * **值**（一个或多个）默认协议
   * 如何处理链接的目标属性的定义。 创建新节点：

      * **名称** `targetConfig`
      * **类型** `nt:unstructured`

      在节点`targetConfig`上：定义所需的属性：

      * 指定目标模式：

         * **名称** `mode`
         * **类型** `String`)
         * **值**:

            * `auto`:意味着选择了自动目标

               （由外部链接的`targetExternal`属性或内部链接的`targetInternal`属性指定）。

            * `manual`:不适用
            * `blank`:不适用
      * 内部链接的目标:

         * **名称** `targetInternal`
         * **类型** `String`
         * **评** 估内部链接的目标(仅当模式为时使 `auto`用)
      * 外部链接的目标:

         * **名称** `targetExternal`
         * **类型** `String`
         * **值** 外部链接的目标(仅在模式时使 `auto`用)。








1. 保存所有更改。
