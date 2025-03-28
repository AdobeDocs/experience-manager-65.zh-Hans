---
title: 标签要点
description: 了解Tally如何作为一个抽象类，提供从成员那里收集关于他们如何评价特定产品和服务的反馈的标准方法。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0b508df9-1a24-4728-a254-f913eeb9b391
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 标签要点 {#tally-essentials}

Tally是一个抽象类，它提供了一种标准方法，用于收集成员关于他们如何评价特定产品和服务的反馈。 不支持匿名反馈。 网站访客必须注册并登录才能参与并登录以更改其反馈。 登录要求通过阻止多个帖子来促进审核并提高反馈的价值。

通过扩展抽象tally类，可创建自定义的tally组件。

[点赞](essentials-liking.md)是一种简单的计数的实现，它表达积极的意见。

[投票](essentials-voting.md)是一种简单形式的计数的实现，表示正面或负面意见。

[评级](rating-basics.md)是一种使用星型系统表示从正到负的一系列意见的计分方法。

自AEM 6.1起，轮询组件不再可用。

[评论](reviews-basics.md)是[评论](essentials-comments.md)和[评级](rating-basics.md)的混合的SCF组件。

## 适用于客户端的Essentials {#essentials-for-client-side}

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [计费API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数的端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已过帐的表(UGC) {#accessing-posted-tallies-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅[审核用户生成的内容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用用于UGC的[公用存储](working-with-srp.md)包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）如何。

**存储库中UGC的位置和格式可能会发生更改，而不会出现警告**。

请参阅：

* [存储资源提供程序概述](srp.md) — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用工具方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 编码准则。
* [SocialUtils重构](socialutils.md) — 将已弃用的实用工具方法映射到当前SRP实用工具方法。
