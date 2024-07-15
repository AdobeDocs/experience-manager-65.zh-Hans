---
title: 使用社交标签云
description: 了解如何将Social Tag Cloud组件添加到页面，以使登录的社区成员快速识别趋势主题并找到标记的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 56af5362-78de-4308-8958-63a45e8573cc
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 4%

---

# 使用社交标签云 {#using-social-tag-cloud}

## 简介 {#introduction}

`Social Tag Cloud`组件突出显示社区成员在发布内容时应用的标记。 它是一种用于识别趋势主题并允许网站访客快速找到标记内容的方法。

如需确定当前趋势的其他方法，请访问[活动趋势](trends.md)。

此页面记录了`Social Tag Cloud`组件对话框设置并描述了用户体验。

有关开发人员的详细信息，请参阅[标记软件包](tag.md)。

有关创建和管理标记以及已将标记应用于哪些内容的信息，请参阅[管理标记](../../help/sites-administering/tags.md)。

## 添加社交标记云 {#adding-a-social-tag-cloud}

要在创作模式下将`Social Tag Cloud`组件添加到页面，请使用组件浏览器找到`Communities / Social Tag Cloud`，并将其拖动到应显示标记云的页面上的适当位置。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](tag.md#essentials-for-client-side)时，`Social Tag Cloud`组件的显示方式如下：

![社交标签](assets/social-tag.png)

## 配置Social标记云 {#configuring-social-tag-cloud}

选择放置的`Social Tag Cloud`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 社交标签云]**&#x200B;选项卡下，指定要显示的标签，如果标签是活动链接，则指定搜索结果的页面位置：

![social-tag-cloud](assets/social-tag-cloud.png)

* **[!UICONTROL 要显示的社交标签]**
确定要显示的UGC标记。 下拉选项包括：

   * `From page and child pages`
   * `All tags`

  默认值为`From page and child pages`，其中“page”引用下面的&#x200B;**Page**&#x200B;设置。

* **[!UICONTROL 页面]**

  (如果不是`All tags)`，则为必需。页面的UGC路径 如果留空，则默认显示当前页面。

* **[!UICONTROL 标记上无链接]**

  如果选中，则标记将以纯文本形式显示在标记云中。 如果未选中，则标记将显示为活动链接，这些链接会搜索应用了该标记的所有内容。 默认值为未选中，需要设置&#x200B;**[!UICONTROL 搜索结果路径]**。

* **[!UICONTROL 搜索结果路径]**

  放置`Search Result`组件的页面的路径，配置为引用UGC，其中包含&#x200B;**页面**&#x200B;设置指定的UGC路径。

## 更改社交标签云的显示 {#change-display-of-social-tag-cloud}

要编辑&#x200B;**Social标签云**&#x200B;的显示，请输入[设计模式](../../help/sites-authoring/default-components-designmode.md)并双击放置的`Social Tag Cloud`组件以打开包含其他选项卡的对话框。

使用&#x200B;**[!UICONTROL Social Tag Cloud （设计）]**&#x200B;选项卡，指定标记的显示方式。 标记可以是简单标记、默认命名空间中的单个词或分层分类：

![social-tag-cloud-design](assets/social-tag-cloud-design.png)

* **[!UICONTROL 显示完整的标题路径]**

  如果选中，则显示父标记的标题以及每个应用标记的命名空间。

  例如：

   * 已选中：`Geometrixx Media: Gadgets / Cars`
   * 取消选中： `Cars`

  简单的标记没有区别。

  默认值为未选中。

* **[!UICONTROL 仅显示叶标记]**

  如果选中，则仅显示不包含其他标记的应用标记。

  例如，假定的TagID为：

  `Geometrixx Media: Gadgets / Cars`

  有三个标记可以应用：

  `Geometrixx Media (the namespace)`、`Gadgets` 和 `Cars`

   * 选中：如果应用，则仅显示`Cars`。
   * 取消选中： `Geometrixx Media`、`Gadgets`和`Cars`如果应用，则显示。

  简单标记是叶标记。

  默认值为未选中。

* **[!UICONTROL 链接模板]**

  通过组件编辑对话框启用链接时，用于显示标记云中链接的模板（默认模板除外）。

* **[!UICONTROL 所有标记的大小相同]**

  如果选中，则标记云中的所有单词的样式都相同。 如果未选中，则单词的样式将根据其使用情况而有所不同。 默认值为未选中。

## 附加信息 {#additional-information}

可在面向开发人员的[Tag Essentials](tag.md)页面上找到更多信息。

有关创建和管理标记的信息，请参阅[标记用户生成的内容](tag-ugc.md) (UGC)。
