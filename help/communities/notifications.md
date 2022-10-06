---
title: 社区通知
seo-title: Communities Notifications
description: AEM Communities有显示已登录社区成员感兴趣事件的通知
seo-description: AEM Communities has notifications that display events of interest to the signed-in community member
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# 社区通知 {#communities-notifications}

## 概述 {#overview}

AEM Communities提供了通知部分，其中显示已登录社区成员感兴趣的事件。

通知类似于 [活动](/help/communities/essentials-activities.md) 和 [订阅](/help/communities/subscriptions.md) 因以下原因而产生：

* 成员发布内容。
* 成员选择跟随另一个成员。
* 成员选择遵循特定主题、文章和其他内容主题。
* 成员标记(@mention)用户生成内容中的另一个社区成员。

通知与活动和订阅的区别在于：

* 指向通知部分的链接始终显示在社区站点的标题中：

   * 活动需要 [活动流函数](/help/communities/functions.md#activity-stream-function) 包含在社区站点的结构中。
   * 订阅需要 [电子邮件的配置](/help/communities/email.md).

* 通知的实施是通过可扩展的可插拔渠道：

   * 活动仅在Web上可用。
   * 订阅仅使用电子邮件提供。

截至社区 [FP1](/help/communities/deploy-communities.md#latestfeaturepack)，则可用的通知渠道包括：

* 使用 `Notifications` 链接。
* 电子邮件渠道，在正确配置电子邮件时可用。

未来的渠道包括移动设备和台式机。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件，才能使电子邮件渠道正常运行通知。

有关设置电子邮件的说明，请参阅 [配置电子邮件](/help/communities/analytics.md).

**启用关注**

必须配置组件才能启用以下功能。 允许遵循的功能包括 [博客](/help/communities/blog-feature.md), [论坛](/help/communities/forum.md), [问题解答](/help/communities/working-with-qna.md), [日历](/help/communities/calendar.md), [文件库](/help/communities/file-library.md)和 [评论](/help/communities/comments.md).

**注意**:

* 社区中使用的组件 [网站模板](/help/communities/sites.md) 和 [组模板](/help/communities/tools-groups.md) 可能已配置为遵循。

* 成员配置文件已配置为允许其他成员跟踪。

## 以下通知 {#notifications-from-following}

![通知](assets/notifications.png)

的 **[!UICONTROL 关注]** 按钮提供了跟踪活动、订阅和/或通知条目的方法。 每次 **[!UICONTROL 关注]** 按钮时，可以打开或关闭选定内容。 的 `Email Subscriptions` 仅在配置后才存在选择。

如果选择了以下任何方法，则按钮的文本将更改为 **[!UICONTROL 关注]**. 为方便起见，可以选择 `Unfollow All` 以关闭所有方法。

的 **[!UICONTROL 关注]** 按钮：

* 查看其他成员的配置文件时。
* 在主功能页面（如论坛、QnA和博客）上：

   * 遵循该常规功能的所有活动。

* 对于特定条目（如论坛主题、问题解答问题或博客文章）：

   * 跟踪该特定条目的所有活动。

## 管理通知设置 {#managing-notification-settings}

通过从“通知”页面中选择“通知设置”链接，每个成员都可以管理通知的接收方式。

始终启用Web渠道。

![通知14](assets/notifications1.png)

电子邮件渠道，依赖于正确 [电子邮件的配置](/help/communities/email.md)，提供与Web渠道相同的设置。

默认情况下，电子邮件渠道处于关闭状态。

![通知2](assets/notifications2.png)

它可能由成员打开，但仍取决于是否配置了电子邮件。

![通知3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### Web通知 {#web-notifications}

A [向导创建的社区站点](/help/communities/sites-console.md) 现在包含指向的链接 `Notifications` 功能。 与消息不同，会为每个社区站点创建通知，而在站点创建过程中必须启用消息。

访问已发布的网站时，选择 `Notifications` 链接将显示该成员的所有通知。

![通知4](assets/notifications4.png)

### 电子邮件通知 {#email-notifications}

启用电子邮件渠道后，成员会收到一封电子邮件，其中包含指向Web上内容的链接。

![通知5](assets/notifications5.png)

## 自定义电子邮件通知 {#customize-email-notifications}

组织可以通过 [覆盖](/help/communities/client-customize.md#overlays) 模板位于 **/libs/settings/community/templates/email/html**.

例如，要修改提及次数电子邮件通知（适用于社区组件），请添加 **if** 动词条件 **提及** 在为其启用 **@mentions** 支持。

要修改博客评论中@mention的电子邮件通知模板，请将开箱即用模板放置： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
