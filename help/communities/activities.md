---
title: 活动流功能
description: 了解已登录社区成员的活动如何收集到流中，以便通过活动流组件进行过滤和显示。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# 活动流功能 {#activity-streams-feature}

## 简介 {#introduction}

已登录社区成员的活动（如在论坛或博客上发帖）将被收集到流中，该流可通过配置`Activity Streams`组件以各种方式过滤和显示。

当社区成员关注感兴趣的帖子或关注其他社区成员的活动时，关注功能会添加另一个活动视图。

本文档描述了：

* 将活动流组件添加到AEM站点
* 活动流组件的配置设置

### 将活动流添加到页面 {#adding-activity-streams-to-a-page}

如果想要将`Activity Streams`组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Activity Streams`

并将其拖动到应该显示活动流的页面上的适当位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/essentials-activities.md#essentials-for-client-side)时，`Activity Streams`组件的显示方式如下：

![活动流](assets/activity-component.png)

### 配置活动流 {#configuring-activity-streams}

选择放置的`Activity Streams`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**用户活动**&#x200B;选项卡下，指定要显示的活动：

![用户活动](assets/user-activities.png)

* **最大活动数**

  要显示的活动数

* **流资源路径**

  留空将默认使用社区站点或社区组。 流资源路径标识活动的源。 默认值为空白。

* **显示用户活动视图**

  如果选中，“活动”页面会包含一个选项卡，该选项卡会根据当前成员在社区内生成的活动来筛选活动。 默认值为选中。

* **显示所有活动视图**

  如果选中，活动页面将包含一个选项卡，其中包含当前成员有权访问的社区内生成的所有活动。 默认值为选中。

* **显示以下视图**

  如果选中，“活动”页面会包含一个选项卡，该选项卡会根据当前成员所关注的活动来筛选活动。 默认值为选中。

### 关注视图 {#following-view}

必须配置组件才能启用以下功能。 允许关注的功能包括[博客](/help/communities/blog-feature.md)、[论坛](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日历](/help/communities/calendar.md)、[文件库](/help/communities/file-library.md)和[评论](/help/communities/comments.md)。

![关注视图](assets/following-activities.png)

**关注**&#x200B;按钮提供了将条目作为活动、[通知](/help/communities/notifications.md)或[订阅](/help/communities/subscriptions.md)进行关注的方法。 每次选择&#x200B;**关注**&#x200B;按钮时，都可以打开或关闭选择。 `Email Subscriptions`选择仅在配置时存在。

如果选择了任何跟进方法，则按钮的文本将更改为&#x200B;**跟进**。 为方便起见，可以选择`Unfollow All`关闭所有方法。

出现&#x200B;**关注**&#x200B;按钮：

* 查看其他成员的配置文件时。
* 在主要功能页面上，例如论坛、问题与解答和博客。

   * 遵循该常规功能的所有活动。

* 特定条目，例如论坛主题、问题或博客文章。

   * 关注该特定条目的所有活动。

### 附加信息 {#additional-information}

可在面向开发人员的[Activity Streams Essentials](/help/communities/essentials-activities.md)页面上找到更多信息。
