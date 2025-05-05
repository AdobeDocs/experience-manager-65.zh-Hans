---
title: 配置富文本编辑器以创建无障碍网页和站点。
description: 配置富文本编辑器以创建无障碍网页和站点。
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# 配置RTE以创建可访问的网页和站点 {#configure-rte-for-accessibility}

Adobe Experience Manager支持符合各种辅助功能标准的多种标准辅助功能。 此外，开发人员可以自定义或扩展功能，以提供有助于使用使用富文本编辑器(RTE)的Experience Manager组件创建无障碍内容的功能。

在设计网页并将内容添加到页面时，内容开发人员和作者可以使用RTE的功能来提供与辅助功能相关的信息。 例如，通过标题和段落元素添加结构信息。

要配置和自定义这些功能，请[为组件配置RTE插件](#configure-the-plugin-features)。 例如，`paraformat`插件允许您添加其他块级语义元素，包括扩展支持的标题级别数超过默认提供的基本`H1`、`H2`和`H3`。

RTE包含在启用了触屏操作的用户界面和Classic用户界面的各种组件中。 但是，使用RTE的主要组件是可用于两个界面的&#x200B;**Text**&#x200B;组件。 以下图像显示了启用了一系列插件（包括`paraformat`）的RTE：

在触屏UI中处于全屏模式的![文本组件(RTE)。](assets/chlimage_1-206.png)

*图：已启用触屏的用户界面中的文本组件。*

![经典UI中文本组件的“编辑”对话框(RTE)。](assets/chlimage_1-207.png)

*图：经典用户界面中的文本组件。*

有关各种界面中可用的RTE功能之间的差异，请参阅[插件及其功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。

## 配置插件功能 {#configure-the-plugin-features}

有关配置RTE的完整说明，请参阅[配置富文本编辑器](/help/sites-administering/rich-text-editor.md)页。 这涵盖了所有问题，包括关键步骤：

* [插件和功能](/help/sites-administering/rich-text-editor.md#aboutplugins)。
* [配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
* [激活插件并配置功能属性](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
* [配置RTE的其他功能](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。

通过在CRXDE Lite中的相应`rtePlugins`子分支中配置插件，您可以激活该插件的所有功能或特定功能。

![CRXDE Lite显示示例rtePlugin。](assets/chlimage_1-208.png)

### 示例 — 指定RTE选择字段中可用的段落格式 {#example-specifying-paragraph-formats-available-in-rte-selection-field}

可以通过以下方式选择新的语义块格式：

1. 根据您的RTE，确定并导航到[配置位置](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations)。
1. [启用段落选择字段](/help/sites-administering/rich-text-editor.md)；通过[激活插件](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins)。
1. [在“段落”选择字段中指定可用的格式](/help/sites-administering/rich-text-editor.md)。
1. 然后，内容作者可以从RTE中的选择字段中使用段落格式。 它们可以访问：

   * 使用触屏UI中的段落枕图标。
   * 在经典UI中使用&#x200B;**格式**&#x200B;字段（弹出选择器）。

利用RTE中通过段落格式选项提供的结构元素，AEM为开发无障碍内容奠定了良好的基础。 内容作者无法使用RTE设置字体大小、颜色或其他相关属性的格式，从而阻止创建内联格式。 相反，他们必须选择相应的结构元素（如标题），并使用从“样式”选项中选择的全局样式。 这确保了标记干净，为使用自己的样式表和结构正确的内容浏览的用户提供了更大的选项。

## 使用源编辑功能 {#use-of-the-source-edit-feature}

在某些情况下，内容作者会发现必须检查和调整使用RTE创建的HTML源代码。 例如，在RTE内创建的一段内容可能需要额外的标记以确保符合WCAG 2.0。可以使用RTE的[源编辑](/help/sites-administering/rich-text-editor.md#aboutplugins)选项完成此操作。 您可以在`misctools`插件[&#128279;](/help/sites-administering/rich-text-editor.md#aboutplugins)上指定`sourceedit`功能。

>[!CAUTION]
>
>请仔细使用`sourceedit`功能。 键入错误和/或不支持的功能可能会导致更多问题。

## 添加对更多HTML元素和属性的支持 {#add-support-for-more-html-elements-and-attributes}

要进一步扩展AEM的辅助功能，可以基于RTE扩展具有其他元素和属性的现有组件（如&#x200B;**Text**&#x200B;和&#x200B;**Table**&#x200B;组件）。

以下过程说明了如何使用&#x200B;**Caption**&#x200B;元素扩展&#x200B;**Table**&#x200B;组件，该元素向辅助技术用户提供有关数据表的信息：

### 示例 — 将标题添加到“表属性”对话框中 {#example-adding-the-caption-to-the-table-properties-dialog}

在`TablePropertiesDialog`的构造函数中，添加一个用于编辑描述的其他文本输入字段。 请注意，必须将`itemId`设置为`caption`（即DOM属性的名称）才能自动处理其内容。

在&#x200B;**Table**&#x200B;中，显式设置或删除DOM元素中的属性。 此值由`config`对象中的对话框传递。 请注意，应使用相应的`CQ.form.rte.Common`方法设置/删除DOM属性（`com`是`CQ.form.rte.Common`的快捷方式），以避免浏览器实施中的常见缺陷。

>[!NOTE]
>
>此过程仅适用于Classic用户界面。

### 示例 — 在文本中使用强调内容时创建无障碍HTML {#create-accessible-html-for-text}

RTE可以使用`strong`和`em`标记代替`b`和`i`。 将以下节点作为同级节点添加到对话框中的`uiSettings`和`rtePlugins`节点。

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### 分步说明 {#step-by-step-instructions}

1. 启动CRXDE Lite。 例如：[http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. 复制：

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >如果中间文件夹尚不存在，您可能需要创建这些文件夹。

1. 复制：

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   到:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`。

1. 打开以下文件进行编辑（双击打开）：

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. 在`constructor`方法中，行读取之前：

   ```
   var dialogRef = this;
   ```

   添加以下代码：

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. 打开以下文件：

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`。

1. 在`transferConfigToTable`方法的末尾添加以下代码：

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. 使用&#x200B;**全部保存……**&#x200B;保存更改

>[!NOTE]
>
>纯文本字段不是允许用于标题元素值的唯一输入类型。 您可以使用任何ExtJS构件，该构件通过其`getValue()`方法提供标题值。
>
>要为其他元素和属性添加编辑功能，请确保两者：
>
>* 每个相应字段的`itemId`属性均设置为相应DOM属性(`TablePropertiesDialog`)的名称。
>* 在DOM元素上显式设置和/或删除了属性(`Table`)。

>[!MORELIKETHIS]
>
>* [WCAG 2.0快速指南](/help/managing/qg-wcag.md)
>* [创建可访问的内容（符合WCAG 2.0）](/help/sites-authoring/creating-accessible-content.md)
