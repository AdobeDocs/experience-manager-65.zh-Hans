---
title: 搜索功能
description: 向Communities站点添加和配置搜索
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# 搜索功能 {#search-feature}

搜索功能可与各种其他功能（如论坛）配合使用，以提供搜索内容的功能。

添加搜索由社区成员输入的帖子(称为用户生成的内容(UGC))的功能时，有两个组件： [搜索](#search)和[搜索结果](#search-results)。

包含`Search Results`组件的页面支持搜索和显示结果。

包含`Search`组件的页面提供了启动搜索的位置，搜索结果会显示在`Search Results`页面上。

搜索功能可与允许网站访客和成员查看内容的任何其他功能一起使用。

## 搜索 {#search-features}

### 将搜索添加到页面 {#add-search-to-a-page}

要将`Search`组件添加到创作模式下的页面，请使用组件浏览器找到`Communities / Search`并将其拖动到页面上的适当位置。 使用`Search`需要`Search Results.`的第二页

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含所需的客户端库`cq.social.hbs.search`时，`Search`组件的显示方式如下所示。

![添加搜索](assets/add-search.png)

### 配置添加的搜索 {#configure-the-added-search}

选择要访问的已放置的`Search`组件，并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜索设置]**&#x200B;选项卡下，指定访客输入查询时搜索路径的方式。

![搜索设置](assets/search-settings.png)

* **[!UICONTROL 搜索路径]**
通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。 例如，要将搜索限制到特定论坛，请选择放置在页面中的论坛组件：

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 结果页]**
结果将显示在使用浏览器选择包含`Search Results`组件的页面时指定的单独页面上。

## 搜索结果 {#search-results}

### 将搜索结果添加到页面 {#add-search-results-to-a-page}

要将`Search Results`组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Search Results`

并将其拖动到页面上的适当位置。 与搜索组件不同，不需要第二页，因为结果将显示在同一页上。

如果在网站内的其他位置使用搜索，则此包含`Search Results`的页面可能会配置为是`Search`的任何或所有实例的`Result Page`。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含所需的客户端库`cq.social.hbs.search`时，`Search Result`组件的显示方式如下：

![搜索结果](assets/search-result1.png)

### 配置添加的搜索结果 {#configure-the-added-search-result}

选择要访问的已放置的`Search Results`组件，并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 搜索结果设置]**&#x200B;选项卡下，可以指定访客输入查询时搜索中包含的路径。

![搜索结果设置](assets/search-result-settings.png)

* 每页&#x200B;**[!UICONTROL 个搜索结果]**

  定义每个页面显示的主题/帖子数。 默认值为10。

* **[!UICONTROL 搜索路径]**

  通过使用“添加项目”按钮添加搜索路径，内容搜索受到限制。

## 附加信息 {#additional-information}

可在面向开发人员的[Search Essentials](search-implementation.md)页面上找到更多信息。
