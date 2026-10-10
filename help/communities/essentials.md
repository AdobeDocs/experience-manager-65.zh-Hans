---
title: 组件、功能和功能要点
description: 社区站点、模板和组的功能
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 16%
---
# 组件、功能和功能要点  {#component-function-and-feature-essentials}

Adobe Experience Manager (AEM) Communities功能要求站点访客成为成员并登录[社区站点](overview.md#communitiessites)，然后才能发布内容。 因此，[社区站点模板](sites.md)（从中创建社区站点[](sites-console.md)）设计为包括登录功能和用户配置文件、消息传送、搜索、审核和翻译。

当[社区组功能](functions.md#groups-function)包含在选定的社区站点模板中时，社区站点支持成员创建社区组。

以下是Communities组件、功能和特性的基本信息链接。

## 基本组件 {#base-components}

* [评论](essentials-comments.md)
* [审核](reviews-basics.md)
* [总计](tally.md)

  * [点赞](essentials-liking.md)
  * [评分](rating-basics.md)
  * [投票](essentials-voting.md)
  * *轮询（不再可用）*

## 具有函数的组件 {#components-with-functions}

* [活动流](essentials-activities.md)
* [博客](blog-developer-basics.md) (`Journal`)

* [日程表](calendar-basics-for-developers.md)
* [专题内容](essentials-featured.md)
* [文件库](essentials-file-library.md)
* [论坛](essentials-forum.md)
* [组](essentials-groups.md)
* [构思](ideation.md)
* [排行榜](leaderboard.md)
* [问题和答案](qna-essentials.md) `(QnA)`

## 特性 {#features}

* [客户端库](clientlibs.md)
* [社区网站](sites-for-developers.md)
* [组件OSGi事件](events.md)
* [组件侧载](sideloading.md)
* [消息](essentials-messaging.md)
* [富文本编辑器](rte.md)
* [评分和徽章](configure-scoring.md)
* [搜索](search-implementation.md)
* [社交图](essentials-socialgraph.md)
* [存储资源提供程序](srp-and-ugc.md) `(SRP)`

* [标记](tag.md)

## Javadocs {#javadocs}

[在线Javadocs](../../help/sites-developing/reference-materials.md)反映了AEM 6.3版本中可用的API。
社区API位于`com.adobe.cq.social.*`包中。

对于每个[功能包](deploy-communities.md#latestfeaturepack)，都提供了javadoc jar。 有关详细信息，请访问[使用Maven for Communities](maven.md#javadocs)。

## 附加信息 {#additional-information}

* [社交组件框架(SCF)](scf.md)

  * [客户端自定义](client-customize.md)
  * [服务器端自定义](server-customize.md)
  * [存储资源提供程序概述](srp.md)

* [编码指南](code-guide.md)
* [教程](tutorials.md)
* [疑难解答](troubleshooting.md)
