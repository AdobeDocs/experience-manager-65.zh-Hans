---
title: 活动趋势
description: 将社区活动列表组件添加到页面
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 1%

---

# 活动趋势 {#activity-trends}

## 简介 {#introduction}

`Community Activity List`组件允许您添加有关成员的帖子及查看的趋势信息，以及内容的帖子及查看的趋势信息。

本文档描述了：

* 正在将`Community Activity List`组件添加到[社区站点](/help/communities/overview.md#community-sites)。

* `Community Activity List`组件的配置设置。

### 要求 {#requirement}

`Community Activity List`的数据仅在为社区站点许可和配置Adobe Analytics时可用。

查看[Analytics社区功能配置](/help/communities/analytics.md)。

### 将社区活动列表添加到页面 {#adding-a-community-activity-list-to-a-page}

要将`Community Activity List`组件添加到创作模式下的页面，请找到组件`Communities / Community Activity List`并将其拖动到页面上的适当位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

首次放到社区站点的页面时，该组件的显示方式如下：

![社区活动](assets/community-activity.png)

### 配置社区活动列表  {#configuring-community-activity-list}

选择放置的`Community Activity List`组件，然后选择`Configure`图标，以打开“编辑”对话框。

![配置](assets/configure-new.png)

在&#x200B;**备注**&#x200B;选项卡下，指定是否显示已上传文件的备注以及如何显示：

![属性](assets/activity-list-properties.png)

* **类型**

  指定显示有关社区成员还是用户生成内容(UGC)的数据。

  选择自：

   * `Members`
   * `Content`

  默认值为`Members`。

* **显示标题**

  在数据上方显示的描述性标题，如`Trending Content`。
默认无标题。

* **显示计数**

  要列出的项目数。
默认值为10。

* **活动类型**

  选择以下选项之一：

   * `Views`（页面访问量）
   * `Posts`（正在创建UGC）
   * `Follows`
   * `Likes`

  缺省值为“视图”。

* **时段**

  选择以下选项之一：

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  默认值为`Total`。

* **上下文路径**

  这样，您可以将活动范围设定为网站的子集，如特定的博客。
默认设置是整个社区站点。

* **成员计数聚合**

  取消选择（关闭）时，仅计数顶级帖子。 例如，如果上下文是根页面（默认），则`Posts`的`Activity Type`从不显示任何活动，因为无法将内容发布到根页面。 选中后，将包含所有下级页面上的计数。
默认值为选中。

### 具有四个组件的示例页面 {#example-page-with-components}

**热门访客**&#x200B;配置：类型=成员，活动类型=视图

**顶级参与者**&#x200B;配置：类型=成员，活动类型=帖子

**热门内容**&#x200B;配置：类型=内容，活动类型=视图，

**趋势内容**&#x200B;配置：类型=内容，活动类型=帖子

![个组件](assets/activity-list-components.png)
