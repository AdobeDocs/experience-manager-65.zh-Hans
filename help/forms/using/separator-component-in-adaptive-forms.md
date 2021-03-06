---
title: 自适应表单中的分隔符组件
seo-title: 自适应表单中的分隔符组件
description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
seo-description: 您可以使用分隔符组件以可视方式分隔表单的各个部分。
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: 自适应表单
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 自适应表单中的分隔符组件{#separator-component-in-adaptive-forms}

可以使用分隔符组件以可视方式分隔表单的面板。 您可以通过指定分隔符组件的以下属性来定义分隔符组件的整体外观和样式：

* **元素名称：** 指定组件的名称。SOM表达式使用元素名称字段中指定的值来寻址组件。
* **粗细：** 以像素为单位指定分隔符组件的粗细。

* **CSS类：** 指定分隔符组件的自定义CSS类

* **内联样式：** 现在，通过AEM Forms，您可以将内联CSS样式应用于单个自适应表单组件并实时预览更改。

您可以使用布局模式定义分隔符组件跨越的列数。 有关更多信息，请参阅[使用布局模式调整组件大小](../../forms/using/resize-using-layout-mode.md)。

要指定分隔符组件的属性，请执行以下操作：

1. 选择分隔符组件，然后点按![cmppr](assets/cmppr.png)。 将在侧栏中打开属性。
1. 单击内联CSS属性部分中的选项卡以指定CSS属性。 例如：a.在字段选项卡中，单击&#x200B;**添加项目**。 将添加一行包含两个字段。
1. 在左侧的第一个字段中，指定要应用的CSS3属性。 例如， **border**。 您还可以通过单击向下箭头按钮来选择属性。 下拉列表并不详尽，您可以在此字段中指定任何受支持的CSS3属性名称。
1. 在相邻的字段中，为指定的CSS3属性指定有效值。 例如，**3px纯黑**。
1. 单击&#x200B;**Add Item**&#x200B;以指定其他属性及其值。
1. 单击&#x200B;**预览**&#x200B;以预览表单中的更改。
1. 单击&#x200B;**确定**&#x200B;以确认更改，或单击&#x200B;**取消**&#x200B;以退出对话框而不进行任何更改。
