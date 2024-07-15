---
title: Communities 订阅
description: 社区成员通过电子邮件与其他成员进行交互
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Communities 订阅 {#communities-subscriptions}

## 概述 {#overview}

自社区[FP1](deploy-communities.md#latestfeaturepack)起，社区成员可使用称为订阅的功能通过电子邮件与社区进行交互。

订阅类似于[通知](notifications.md)，因为成员可以在关注博客文章、论坛主题或问题与解答时订阅。

订阅与通知的区别在于：

* 当成员跟随其他成员时，不能订阅。
* 成员唯一要执行的操作是在执行操作时选择`Email Subscriptions`。
* 配置电子邮件回复后，成员只需回复收到的电子邮件，即可有效地发布内容。

### 要求 {#requirements}

**配置电子邮件**

必须配置电子邮件以使订阅正常工作并使成员通过电子邮件回复。

有关设置电子邮件的说明，请参阅[配置电子邮件](email.md)。

**启用订阅并关注**

必须将组件配置为启用以下订阅&#x200B;*和*。 允许订阅的功能包括[博客](blog-feature.md)、[论坛](forum.md)和[问题与解答](working-with-qna.md)。

## 来自以下项的订阅 {#subscriptions-from-following}

![订阅正在关注](assets/subscription-following.png)

**关注**&#x200B;按钮提供了将条目作为活动、订阅和/或通知进行关注的方法。 每次选择&#x200B;**关注**&#x200B;按钮时，都可以打开或关闭选择。

如果选择了任何跟进方法，则按钮的文本将更改为&#x200B;**跟进**。 为方便起见，可以选择`Unfollow All`关闭所有方法。

仅当论坛、问题与解答或博客配置为启用电子邮件订阅时，**关注**&#x200B;按钮才会包含`Email Subscriptions`选项。 将显示此按钮：

* 在启用的论坛、问题与解答或博客的主功能页上，将为该功能下的所有活动发送电子邮件。

* 对于特定条目，例如论坛主题、问题或博客文章。当存在针对该特定条目的活动时，将发送电子邮件。

## 通过电子邮件回复 {#reply-by-email}

当[配置为通过电子邮件回复](email.md#configure-polling-importer)时，订阅的成员将收到一封包含已发布内容的电子邮件以及指向在线内容的链接。

如果他们回复电子邮件，则他们在回复中输入的内容将显示为在线内容。

![电子邮件回复](assets/email-reply.png)

发布回复所花费的时间由[轮询导入程序的更新时间间隔](email.md#configure-polling-importer)控制。

![QA](assets/qa.png)
