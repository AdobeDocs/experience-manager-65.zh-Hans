---
title: 编辑器限制
description: 触屏UI中的编辑器使用叠加与iframe中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 6%

---

# 编辑器限制{#editor-limitations}

触屏UI中的编辑器使用叠加与iframe中限定的内容进行交互。 这种交互方式会对编辑器的使用以及开发人员造成一些限制。 本页总结了这些限制，并在可能的情况下提供了解决方案或变通办法。

## 功能限制 {#functional-limitations}

使用编辑器创作页面时，作者可能会遇到以下功能限制。

### 链接无效 {#links-not-active}

在[编辑页面](/help/sites-authoring/editing-content.md)时，链接处于非活动状态。

* [切换到&#x200B;**预览**&#x200B;模式](/help/sites-authoring/editing-content.md#preview-mode)以使用内容中的链接进行导航。

### 结构页面 {#structure-pages}

不能将页面命名为`structure`。 名为`structure`的页面在页面编辑器中不可编辑。

## CSS限制 {#css-limitations}

开发人员在编辑器与CSS的交互中可能会遇到以下限制。

### 绝对定位的元素 {#absolutely-positioned-elements}

绝对定位的元素可能会导致其叠加的位置出现问题。

* 如果发生这种情况，请确保绝对定位元素的维度正确，因为编辑器将创建具有相同维度的叠加。

### vh单位 {#vh-units}

不支持`vh`个单位，因为iframe高度必须由Adobe Experience Manager (AEM)自动调整。

### 固定背景图像 {#fixed-background-images}

由于固定背景图像嵌入在iframe中，因此滚动时可能无法显示为固定背景图像。

* 在标题栏操作中选择&#x200B;**以发布的形式查看页面**&#x200B;可正确显示页面。

### 100%高度 {#height}

页面的body元素不支持100%高度。

* 解决方法是通过“拉伸”主体元素来实现全屏主体，如下所示：

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 边距折叠 {#margin-collapsing}

如果body元素的第一个子元素具有边距，则可以看到边距收缩问题。

* 解决方案是在body元素级别添加clearfix，如下所示：

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
