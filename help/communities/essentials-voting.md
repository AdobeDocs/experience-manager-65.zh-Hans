---
title: Voting Essentials
description: 了解如何使用投票组件，该组件允许成员通过选择向上或向下箭头指示其意见来对特定内容进行评级。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: e8ff751f-404a-498d-8e90-62a13ab593ff
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# Voting Essentials {#voting-essentials}

投票组件（[tally](tally.md)子类）是一种有用的工具，它允许成员通过简单地选择上箭头或下箭头来表示其意见来对特定内容进行评级。

允许将投票组件的多个实例放在同一页面上；必须为每个实例配置唯一的`tally name`属性。

不支持匿名发布投票。 网站访客必须注册并登录才能参与投票一次。 登录的访客（会员）可随时更改其投票权。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/tally/components/hbs/voting</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>是 — 可在<i>设计</i>模式下编辑属性</td>
  </tr>
  <tr>
   <td> <a href="client-customize.md#clientlibs-for-scf"><strong>clientlibs</strong></a></td>
   <td> cq.social.hbs.voting</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td><p> /libs/social/tally/components/hbs/voting/voting.hbs<br /> /libs/social/tally/components/hbs/voting/activity-title.hbs</p> </td>
  </tr>
  <tr>
   <td><strong>CSS</strong></td>
   <td> /libs/social/tally/components/hbs/voting/clientlibs/votingcomponent.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td><p>查看<a href="voting.md">使用投票</a></p> </td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [计费API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/api/package-summary.html)

* [计数的端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/tally/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 访问已过帐投票(UGC) {#accessing-posted-voting-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅[审核用户生成的内容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用用于UGC的[公用存储](working-with-srp.md)包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）如何。

**存储库中UGC的位置和格式可能会发生更改，而不会出现警告**。

请参阅：

* [存储资源提供程序概述](srp.md) — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用工具方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 编码准则。
* [SocialUtils重构](socialutils.md) — 将已弃用的实用工具方法映射到当前的SRP实用工具方法。
