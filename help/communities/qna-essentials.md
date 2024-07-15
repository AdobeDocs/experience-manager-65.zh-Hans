---
title: 问题与解答要点
description: 了解在Adobe Experience Manager社区中使用问题与解答(QnA)论坛功能的基础知识。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# 问题与解答要点 {#qna-essentials}

本页提供了有关使用问答(QnA)论坛功能的基本信息。

## 适用于客户端的Essentials {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">包括</a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.voting<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> 模板</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> 属性</td>
   <td>查看<a href="working-with-qna.md">问答论坛功能</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [问题与解答API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [QnA端点](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [服务器端自定义](server-customize.md)

### 问题与解答功能 {#qna-function}

包含[QnA函数](functions.md#qna-function)的社区站点结构具有已配置的`QnA`组件以及影响审核和标记的设置。 QnA函数支持识别[特权成员用户组](users.md#privileged-members-group)。

### 访问问题与解答论坛帖子(UGC) {#accessing-qna-forum-posts-ugc}

UGC应使用标准审核方法之一进行审核。
请参阅[审核用户生成的内容](moderate-ugc.md)。

截至AEM 6.1 Communities，使用用于UGC的[公用存储](working-with-srp.md)包括对UGC的编程访问，而不管选择的存储选项（如ASRP、MSRP或JSRP）如何。

**存储库中UGC的位置和格式可能会发生更改，而不会出现警告**。

请参阅：

* [存储资源提供程序概述](srp.md) — 简介和存储库使用情况概述。
* [SRP和UGC Essentials](srp-and-ugc.md) - SRP实用工具方法和示例。
* [使用SRP访问UGC](accessing-ugc-with-srp.md) — 编码准则。
* [SocialUtils重构](socialutils.md) — 将已弃用的实用工具方法映射到当前的SRP实用工具方法。
