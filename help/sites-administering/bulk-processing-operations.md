---
title: 批量处理操作
seo-title: Bulk Processing Operations
description: null
seo-description: null
page-status-flag: never-activated
uuid: 62a6c379-a460-4f8f-a909-03d04fa8944b
contentOwner: sarchiz
discoiquuid: 47c2a80f-78ac-4372-86b4-06351a1dd58f
docset: aem65
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 2%

---


# 批量处理操作 {#bulk-processing-operations}

## 简介 {#introduction}

在最新版本的AEM中，“全选”按钮已扩展到所有视图：列表、列和卡片视图。 现在，“全选”按钮可选择给定文件夹或收藏集中的所有内容，而不只是选择在客户端浏览器中加载和显示的资产和页面。

已为批量操作启用关键操作： **移动**, **删除** 和 **复制**. 新的对话框将让客户了解批量处理不可用的操作有哪些。

## 使用方法 {#how-to-use}

一个名为的新按钮 **全选** 已添加到卡片视图、列表视图或列视图。 此按钮可用于任何视图中以选择数据集中的所有元素。

在AEM的先前版本中，选择的内容受到限制，限制了客户端浏览器中加载的内容。 引入此新更改是为了避免混淆正在执行批量操作的元素数量。

目前，已向批量处理添加了三个操作：

* 移动
* 复制
* 删除

将来将增加对更多操作的支持。
要使用此功能，您需要导航到要在页面或资产上执行批量操作的文件夹或收藏集。

然后，选择其中一个视图，如下所示：

### 信息卡视图 {#card-view}

![](assets/unu.png)

### 卡片视图中的批量选择 {#bulk-selection-in-card-view}

可以使用 **全选** 按钮：

![](assets/doi.png) ![](assets/trei.png)

### 列表视图 {#list-view}

列表视图的情况也相同：

![](assets/patru_modified.png)

### 列表视图中的批量选择 {#bulk-selection-in-list-view}

在列表视图中，使用 **全选** 按钮，或使用左侧的复选框进行批量选择。

![](assets/cinci.png) ![](assets/sase.png)

### 列视图 {#column-view}

![](assets/sapte.png)

### 列视图中的批量选择 {#bulk-selection-in-column-view}

![](assets/opt.png)

## 批量启用的操作 {#bulk-enabled-operations}

选择后，可以执行三个批量启用操作之一： **移动**, **复制** 或 **删除**.

这里， **移动** 操作。 在任何视图中，这都会导致所有资产都被移动到所选位置，而不仅仅是屏幕上加载的资产。

![](assets/noua.png)

对于未批量启用的其他操作，例如 **下载，** 将显示一条警告，仅声明操作中将仅包含浏览器中加载的元素。

![](assets/zece.png)
