---
title: Tag Essentials
description: 了解当社区组件配置为启用标记时，社区成员可以标记他们在发布环境中发布的内容。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 6e8af8cf-1239-46f9-b2fe-4aa80abc86ea
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 2%

---

# Tag Essentials {#tag-essentials}

在启用“标记”的情况下配置AEM Communities组件后，社区成员将能够标记他们在发布环境中发布的内容。

发布环境中应用的标记的基础基础结构与创作环境中应用于内容的标记的基础基础结构相同，例如页面和资产：

* 有关创建和管理标记的信息，请参阅[管理标记](../../help/sites-administering/tags.md)和[标记用户生成的内容](tag-ugc.md) (UGC)。

* 有关[标记框架](../../help/sites-developing/framework.md)以及在[自定义应用程序](../../help/sites-developing/building.md)中包括和扩展标记的信息，请参阅[针对开发人员的标记](../../help/sites-developing/tags.md)。

* 有关如何将`social tag cloud`组件添加到页面以突出显示发布环境中应用于UGC的标记的信息，请参阅[使用Social Tag Cloud](tagcloud.md)。

配置[社区站点](sites-console.md#tagging)或以下功能之一时，可以启用UGC标记：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md)
* [问题与解答](working-with-qna.md)

## 适用于客户端的Essentials {#essentials-for-client-side}

### 社交标记云 {#social-tag-cloud}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/commons/components/hbs/tagcloud</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>可包含</strong></a></td>
   <td>否</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.hbs.tagcloud</td>
  </tr>
  <tr>
   <td> <strong>模板</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/tagcloud.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/commons/components/hbs/tagcloud/clientlibs/tagcloud.css</td>
  </tr>
  <tr>
   <td><strong>属性</strong></td>
   <td>请参阅<a href="tagcloud.md">使用Social Tag Cloud</a></td>
  </tr>
 </tbody>
</table>

* [客户端自定义](client-customize.md)

## 服务器端的Essentials {#essentials-for-server-side}

* [社交标签云API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagcloud/api/package-summary.html)

* [社交标签管理器](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/commons/tagging/package-summary.html)

* [服务器端自定义](server-customize.md)

## 标记搜索 {#tag-searching}

自[功能包1](deploy-communities.md#latestfeaturepack) (FP1)起，使用[标记标题](../../help/sites-developing/framework.md#tag-characteristics)执行标记搜索。

在FP1之前，使用[标记ID](../../help/sites-developing/framework.md#tagid)执行了搜索。
