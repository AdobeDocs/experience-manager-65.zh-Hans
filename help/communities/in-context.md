---
title: 上下文审核
description: 了解管理员和受信任的社区成员如何在Adobe Experience Manager社区中执行审查方操作。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 47b3c19c-5228-4b72-b78c-7ed71b308921
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 上下文审核 {#in-context-moderation}

对于AEM Communities，管理员和受信任的社区成员可以直接在发布社区内容的已发布页面上执行审核。

使用[审核控制台](moderation.md)时，为内容显示的信息包含指向已发布页面的链接，以允许访问在上下文中审核时可用的其他审核操作。

## 审核操作 {#moderation-actions}

访问审核概述，了解[审核操作](moderate-ugc.md#moderation-actions)的说明。

## 审核用户界面 {#moderation-ui}

在发布实例上向审查方呈现的UI包含在用于发布和管理用户生成内容(UGC)的对话框中。 UI的元素由网站访客的状态决定，无论它们是否……

1. 发布内容的成员。
1. 受信任的成员审查方。
1. 管理员。
1. 已登录，但不是内容的管理员、审查方或作者。
1. 未登录。

## 示例 {#example}

使用在[AEM Communities快速入门](getting-started.md)时创建的[Geometrixx参与](http://localhost:4503/content/sites/engage/en.html)网站，可以在论坛中设置一个主题，以便在Publish环境中体验各种审核活动。 请参阅下文。

创建站点时，通过将Aaron McDonald (`aaron.mcdonald@mailinator.com`)添加到社区参与审查方组，将其识别为受信任的社区成员。

可以使用[成员控制台](members.md)将Rebekah Larsen (`rebekah.larsen@trashymail.com`)添加为community-engage-members组的成员。

有关社区用户组的详细信息，请访问[管理用户和用户组](users.md)。

### 创建论坛帖子 {#create-the-forum-posts}

* 以Rebekah Larsen的身份登录(rebekah.larsen@trashymail.com)

   * 选择论坛
   * 选择新的Post
   * 输入主题

     蜂鸣喂鸟机什么时候换花蜜

   * 输入正文文本

     我每年都挂一只蜂鸟喂食器，可没取得多少成功。 他们似乎来了一两天，就这样了。 我每周换一次会不会太长？ 我一定要早点改吗？

   * 选择Post
   * 选择注销

* 以Aaron McDonald (aaron.mcdonald@mailinator.com)登录

   * 选择论坛
   * 对于“蜂鸟”主题，请选择“阅读更多”
   * 输入Post回复的评论

     我每周换一次衣服，从5月到10月都有。

   * 选择回复
   * 选择注销

* 以Andrew Schaeffer身份登录(andrew.schaeffer@trashymail.com)

   * 选择论坛
   * 对于“蜂鸟”主题，请选择“阅读更多”
   * 输入Post回复的评论

     我销售花蜜和饲料 — 请访问https://my.viral.url/

   * 选择回复
   * 选择注销

### 匿名网站访客(#5) {#anonymous-site-visitor}

以下是未登录(5)的站点访客所看到的论坛视图。

匿名网站访客只能查看论坛，但不得发布任何内容，也不得执行任何审核操作。

![community-forum-visitor](assets/community-forum-visitor.png)

### 新成员(#4) {#new-member}

在作者中，以管理员身份登录，并使用[成员控制台](members.md)将Boyd Larsen (boyd.larsen@dodgit.com)添加为community-engage-members组的新成员，然后注销。

在发布时，以Boyd Larsen身份登录，并通过选择`Forum`来访问线程，然后为hummingbird帖子选择`Read more`。

注意：

* 博伊德没有参加论坛。
* 博伊德无法删除任何内容。
* Boyd已登录，可以回复或标记内容。

让Boyd选择Flag来标记Andrew发布的内容。

注销

![community-forum-member](assets/community-forum-member.png)

### 管理员(#3) {#administrator}

以管理员（管理员）身份登录，并通过选择“论坛”访问该会话，然后选择“阅读更多帖子”。

注意：

* 管理员可以标记、删除、编辑、拒绝、剪切、关闭、固定、功能。
* 管理员可以选择管理以访问审核控制台。

![community-admin-forum](assets/community-admin-forum.png)

选择管理菜单项，以便您可以从Publish环境中访问[审核控制台](moderation.md)。

请注意，对于管理员，所有可审核内容均可见，而不仅仅是Geometrixx参与社区网站中的内容。

搜索过滤器是一个可切换打开或关闭的侧面板。

注销。

![moderation-console-publish](assets/moderation-console-publish.png)

### 社区审查方(#2) {#community-moderator}

以Aaron McDonald (`aaron.mcdonal@mailinator.com`)（社区审查方）登录，并通过选择“论坛”来访问主题，然后阅读Hummingbird帖子的更多信息。

注意：

* Aaron可以回复、删除、编辑或拒绝自己的帖子。
* Aaron还可以标记/允许、回复、删除、编辑、拒绝其他内容。
* Aaron可以剪切论坛主题，将其移至他主持的另一个论坛。
* Aaron可以选择管理以访问审核控制台。

![社区论坛 — 审查方](assets/community-forum-moderator.png)

选择管理菜单项，以便您可以从Publish环境中访问[审核控制台](moderation.md)。

请注意，对于社区审查方，只能看到GeometrixxEngage社区站点中的可审查内容。

请注意，社区审查方具有和管理员相同的选项（图像已关闭搜索侧栏），但没有对其他AEM控制台的访问权限。

注销。

![审查方访问](assets/moderator-access.png)

### 内容作者(#1) {#content-author}

以Rebekah Larsen (`rebekah.larsen@mailinator.com`)（启动线程的社区成员）身份登录，并通过选择“论坛”访问该线程，然后阅读Hummingbird帖子的更多信息。

注意：

* 丽贝卡可以删除或编辑自己的帖子。
* Rebekah还可以回复或标记其他内容。
* Rebekah无法访问审核控制台。

![community-forum-author](assets/community-forum-author.png)
