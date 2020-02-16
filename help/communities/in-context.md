---
title: 上下文内协调
seo-title: 上下文内协调
description: 如何执行审查方操作
seo-description: 如何执行审查方操作
uuid: 282a8bea-2822-4e5c-b9f4-4d9a5380d895
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ee104f6f-123b-4a6e-9031-849fc1318cc5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 上下文内协调 {#in-context-moderation}

对于AEM Communities，仲裁可能由管理员和受信任的社区成员直接在发布社区内容的已发布页面上执行。

使用审核控 [制台时](moderation.md)，为内容显示的信息包括指向已发布页面的链接，以允许访问在审核上下文中时可用的其他审核操作。

## 审核操作 {#moderation-actions}

有关审核操作的说明，请访问审核 [概述](moderate-ugc.md#moderation-actions)。

## 协调UI {#moderation-ui}

发布实例上向审查方显示的UI包含在用于发布和管理用户生成的内容(UGC)的对话框中。 UI的元素由站点访客的状态决定——无论他们是……

1. 发布内容的成员
1. 受信任的会员审查方
1. 管理员
1. 已登录，但管理员、版主和内容作者均不登录
1. 未登录

## 示例 {#example}

使用在 [AEM Communities入门时创建的Geometrixx Engage](http://localhost:4503/content/sites/engage/en.html) Site [](getting-started.md)，可以快速在论坛中设置一个线程，在该论坛上可以体验发布环境中的各种协调活动，如下所示。

Aaron mcDonald(aaron.mcdonald@mailinator.com)在创建网站时将其添加到社区参与审查者组，从而被确定为值得信赖的社区成员。

Rebekah Larsen(rebekah.larsen@trashymail.com)可以使用“成员”控制台添加为社区参与成员组 [的成员](members.md)。

有关社区用户组的详细信息，请访 [问“管理用户和用户组”](users.md)。

### 创建论坛帖子 {#create-the-forum-posts}

* 以丽贝卡·拉森(rebekah.larsen@trashymail.com)的身份登录

   * 选择论坛
   * 选择新帖子
   * 输入主题

      《蜂鸟喂食》中的花蜜

   * 输入正文文本

      我每年在蜂鸟寄宿器上吊死时，都没有什么成功。 看来他们来了一两天就到了。 我每周换一次，就这么久？ 我需要更早改变吗？
   * 选择帖子
   * 选择注销

* 以Aaron mcDonald的身份登录(aaron.mcdonald@mailinator.com)

   * 选择论坛
   * 对于Hummingbird主题，选择“阅读更多”
   * 输入帖子回复的评论

      我每周换一次，5月至10月再换一次。

   * 选择回复
   * 选择注销

* 以Andrew Schaeffer(andrew.schaeffer@trashymail.com)身份登录

   * 选择论坛
   * 对于Hummingbird主题，选择“阅读更多”
   * 输入帖子回复的评论

      我销售花蜜和饲料——请访问https://my.viral.url/

   * 选择回复
   * 选择注销

### 匿名网站访客(#5) {#anonymous-site-visitor}

以下是未登录(5)的站点访客所查看的论坛视图。

匿名网站访客只能查看论坛，但我不发布任何内容，也不能执行任何审核操作。

![chlimage_1](assets/chlimage_1.png)

### 新成员(#4) {#new-member}

在创作时，以管理员身份登录，然后使用“成员”控制台将Boyd Larsen(boyd.larsen@dodgit.com)添加为社区参与成员组的新 [成员](members.md)，然后再添加“注销”。

在发布时，以Boyd Larsen身份登录，通过选择线程访 `Forum`问线程，然 `Read more` 后进入蜂鸟帖子。

通知

* 博伊德没有参加论坛
* Boyd不能删除任何内容
* Boyd已登录，可回复或标记内容

让Boyd选择标记以标记Andrew发布的内容。

注销

![chlimage_1-1](assets/chlimage_1-1.png)

### Administrator (#3) {#administrator}

以管理员（管理员）身份登录，通过选择论坛，然后阅读帖子的更多内容来访问帖子。

通知

* 管理员可以标记、删除、编辑、拒绝、剪切、关闭、固定、功能
* 管理员可以选择“管理”以访问审核控制台

![社区管理论坛](assets/communityadmin-forum.png)

选择“管理”菜单项以从发布 [环境访问](moderation.md) “审核”控制台。

请注意，对于管理员，所有可审核的内容都可见，而不仅仅是Geometrixx Engage社区站点中的内容。

搜索筛选器是打开或关闭的侧面板。

注销.

![版本控制台发布](assets/moderationconsole-publish.png)

### 社区审查方(#2) {#community-moderator}

以社区主持人Aaron mcDonald(aaron.mcdonal@mailinator.com)的身份登录，通过选择“论坛”访问主题，然后为蜂鸟帖子阅读更多内容。

通知

* Aaron可以回复、删除、编辑或拒绝自己的帖子
* Aaron还可以标记／允许、回复、删除、编辑、拒绝其他内容
* 亚伦·坎·库特将论坛话题转到他主持的另一个论坛
* Aaron可以选择“管理”以访问协调控制台

![chlimage_1-2](assets/chlimage_1-2.png)

选择“管理”菜单项以从发布 [环境访问](moderation.md) “审核”控制台。

注意，对于社区审查方，只能看到Geometrixx Engage社区站点中可审核的内容。

请注意，社区审查方与管理员具有相同的选项（图像处于关闭的搜索提要栏状态），但无权访问其他AEM控制台。

注销.

![审查方访问](assets/moderatoraccess.png)

### 内容作者(#1) {#content-author}

以Rebekah Larsen(rebekah.larsen@mailinator.com)的身份登录，他是社区成员，他启动了该主题，通过选择“论坛”访问该主题，然后为蜂鸟帖子阅读更多内容。

通知

* Rebekah可以删除或编辑自己的帖子
* Rebekah还可以回复或标记其他内容
* Rebekah无法访问协调控制台

![chlimage_1-3](assets/chlimage_1-3.png)

