---
title: 自适应表单组件的内联样式
seo-title: 自适应表单组件的内联CSS属性
description: 虽然可以在自适应表单上应用自定义样式，但也可以在自适应表单的各个组件上应用内联CSS属性。
seo-description: 虽然可以在自适应表单上应用自定义样式，但也可以在自适应表单的各个组件上应用内联CSS属性。
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---


# 自适应表单组件{#inline-styling-of-adaptive-form-components}的内联样式

您可以使用[主题编辑器](../../forms/using/themes.md)指定样式，从而定义自适应表单的整体外观和样式。 此外，还可以将内联CSS样式应用于单个自适应表单组件并立即预览更改。 内联样式将覆盖主题中提供的样式。

## 应用内联CSS属性{#apply-inline-css-properties}

向组件添加内联样式：

1. 在表单编辑器中打开表单，并将模式更改为样式模式。 要将模式更改为样式模式，请在页面工具栏中，点按![画布下拉框](assets/canvas-drop-down.png) > **样式**。
1. 在页面中选择一个组件，然后点按编辑按钮![edit-button](assets/edit-button.png)。 样式属性在提要栏中打开。

   您还可以从提要栏的表单层次结构树中选择组件。 表单层次结构树在提要栏中可用作表单对象。

   您还可以从提要栏中选择组件。 在样式模式下，您可以看到在表单对象下列出的组件。 但是，提要栏中的表单对象列表会列表字段和面板等组件。 字段和面板是可包含文本框和单选按钮等组件的通用组件。

   从提要栏中选择组件时，您会看到所有列出的子组件以及选定组件的属性。 您可以选择特定的子组件并设置其样式。

1. 单击提要栏中的选项卡以指定CSS属性。 您可以指定以下属性：

   * Dimension和位置（显示设置、填充、高度、宽度、边距、位置、z索引、浮动、清除、溢出）
   * 文本(字体系列、权重、颜色、大小、行高和对齐方式)
   * 背景（图像和渐变、背景颜色）
   * 边框（宽度、样式、颜色、半径）
   * 效果（阴影、空间）
   * 高级（允许您为组件编写自定义CSS）

1. 同样，您也可以对组件的其他部分（如构件、题注和帮助）应用样式。
1. 点按&#x200B;**完成**&#x200B;以确认更改，或点按&#x200B;**取消**&#x200B;以放弃更改。

## 示例：字段组件{#example-inline-styles-for-a-field-component}的内联样式

以下图像描述了在将内联样式应用于文本字段之前和之后的文本字段。

![应用内联样式之前的文本框组件](assets/no-style.png)

应用内联样式属性之前的文本框组件

注意应用以下CSS属性后，文本框样式的更改，如下图所示。

<table>
 <tbody>
  <tr>
   <td><p>选择器</p> </td>
   <td><p>CSS属性</p> </td>
   <td><p>值</p> </td>
   <td><p>效果</p> </td>
  </tr>
  <tr>
   <td><p>字段</p> </td>
   <td><p>边界</p> </td>
   <td><p>边框宽度= 2px</p> <p>边框样式=实色</p> <p>边框颜色=#1111</p> </td>
   <td><p>在字段周围创建黑色2px宽边框</p> </td>
  </tr>
  <tr>
   <td><p>文本框</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>将背景颜色更改为CornflowerBlue(#6495ED)</p> <p>注意：您可以在值字段中指定颜色名称或其十六进制代码。</p> </td>
  </tr>
  <tr>
   <td><p>标签</p> </td>
   <td><p>尺寸和位置&gt;宽度</p> </td>
   <td><p>100px</p> </td>
   <td><p>将标签的宽度修复为100px</p> </td>
  </tr>
  <tr>
   <td>字段帮助图标</td>
   <td>“文本”&gt;“字体颜色”</td>
   <td>#2ECC40</td>
   <td>更改帮助图标面的颜色。</td>
  </tr>
  <tr>
   <td><p>长描述</p> </td>
   <td><p>text-align</p> </td>
   <td><p>居中</p> </td>
   <td><p>将帮助的详细说明对齐到中心</p> </td>
  </tr>
 </tbody>
</table>

![应用内联样式后的文本框样式](assets/applied-style.png)

应用内联样式属性后的文本框组件

按照上述步骤，您可以选择面板、提交按钮和单选按钮等其他组件并设置其样式。

>[!NOTE]
>
>样式属性因您选择的组件而异。

