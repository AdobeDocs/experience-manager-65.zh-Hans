---
title: 社区通知
description: AEM Communities具有显示登录社区成员感兴趣的事件的通知
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 社区通知 {#communities-notifications}

## 概述 {#overview}

AEM Communities提供了一个通知部分，用于显示已登录社区成员感兴趣的事件。

通知类似于[活动](/help/communities/essentials-activities.md)和[订阅](/help/communities/subscriptions.md)，因为它们可能源自：

* 成员过帐内容。
* 选择跟随其他成员的成员。
* 选择遵循特定主题、文章和其他内容线程的成员。
* 用户生成内容中的成员标记(@mention)另一个社区成员。

通知与活动和订阅的不同之处在于：

* 指向通知部分的链接始终显示在社区站点的标题中：

   * 活动需要在社区站点的结构中包含[活动流函数](/help/communities/functions.md#activity-stream-function)。
   * 订阅需要[配置电子邮件](/help/communities/email.md)。

* 通知的实施是通过可扩展且可插拔的渠道实现的：

   * 活动只能在Web上进行。
   * 只能使用电子邮件进行订阅。

截至社区[FP1](/help/communities/deploy-communities.md#latestfeaturepack)，可用的通知渠道为：

* 使用`Notifications`链接访问的Web渠道。
* 电子邮件渠道，在正确配置电子邮件时可用。

未来的渠道包括移动和桌面。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件才能使通知的电子邮件渠道正常工作。

有关设置电子邮件的说明，请参阅[配置电子邮件](/help/communities/analytics.md)。

**启用关注**

必须配置组件才能启用以下功能。 允许关注的功能包括[博客](/help/communities/blog-feature.md)、[论坛](/help/communities/forum.md)、[QnA](/help/communities/working-with-qna.md)、[日历](/help/communities/calendar.md)、[文件库](/help/communities/file-library.md)和[评论](/help/communities/comments.md)。

**注释**：

* 社区[站点模板](/help/communities/sites.md)和[组模板](/help/communities/tools-groups.md)中使用的组件可能已配置为遵循。

* 成员配置文件已配置为允许其他成员关注。

## 来自以下项的通知 {#notifications-from-following}

![通知](assets/notifications.png)

**[!UICONTROL 关注]**&#x200B;按钮提供了将条目作为活动、订阅和/或通知进行关注的方法。 每次选择&#x200B;**[!UICONTROL 关注]**&#x200B;按钮时，都可以打开或关闭选择。 `Email Subscriptions`选择仅在配置时存在。

如果选择了任何跟进方法，则按钮的文本将更改为&#x200B;**[!UICONTROL 跟进]**。 为方便起见，可以选择`Unfollow All`关闭所有方法。

将显示&#x200B;**[!UICONTROL 关注]**&#x200B;按钮：

* 查看其他成员的配置文件时。
* 在主要功能页面（如论坛、问题与解答和博客）上：

   * 遵循该常规功能的所有活动。

* 对于特定条目，例如论坛主题、问题或博客文章：

   * 关注该特定条目的所有活动。

## 管理通知设置 {#managing-notification-settings}

通过从“通知”页面中选择“通知设置”链接，每个成员都可以管理接收通知的方式。

Web渠道始终处于启用状态。

![通知14](assets/notifications1.png)

电子邮件渠道依赖于电子邮件[&#128279;](/help/communities/email.md)的正确配置，它提供的设置与Web渠道的设置相同。

默认情况下，电子邮件渠道处于关闭状态。

![通知2](assets/notifications2.png)

它可以由成员启用，但仍取决于配置的电子邮件。

![通知3](assets/notifications3.png)

## 查看通知 {#viewing-notifications}

### Web通知 {#web-notifications}

[向导创建的社区站点](/help/communities/sites-console.md)现在在横幅上方的站点标题栏中包含指向`Notifications`功能的链接。 与消息不同，通知是为每个社区站点创建的，而消息必须在站点创建过程中启用。

访问已发布的站点时，选择`Notifications`链接将显示该成员的所有通知。

![通知4](assets/notifications4.png)

### 电子邮件通知 {#email-notifications}

启用电子邮件渠道后，成员会收到一封电子邮件，其中包含指向Web上内容的链接。

![通知5](assets/notifications5.png)

## 自定义电子邮件通知 {#customize-email-notifications}

组织可以通过[覆盖](/help/communities/client-customize.md#overlays)位于&#x200B;**/libs/settings/community/templates/email/html**&#x200B;的模板来自定义电子邮件通知。

例如，要修改提及电子邮件通知（针对社区组件），请在启用&#x200B;**@mentions**&#x200B;支持的组件的模板中为谓词&#x200B;**提及**&#x200B;添加&#x200B;**if**&#x200B;条件。

要修改博客评论中发@mention的电子邮件通知模板，请将现成模板放置在： **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
