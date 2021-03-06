---
title: 部署最佳实践
seo-title: 部署最佳实践
description: 部署和维护最佳实践。
seo-description: 部署和维护最佳实践。
uuid: 4546ed2c-43d5-40f3-874f-567b324e78c2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4b5c0677-c630-4fae-867e-4f4583ac8507
exl-id: 4cbc0a30-d5f6-40ff-b7f6-8d64762e1970
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 15%

---

# 部署最佳实践{#deploying-best-practices}

部署最佳实践介绍了如何以最高效、最有效的方式部署或维护AEM。 这些主题涵盖 AEM 中的多个区域，此外还将不断增加新的主题。

以下区域提供了有关部署和维护最佳实践和建议的文档：

* [OAK](#oak)
* [社区](#communities)
* [UI](#ui)
* [演出](#performance)

有关管理、开发或创作的最佳实践，请参阅以下内容之一：

* [管理最佳实践](/help/sites-administering/administer-best-practices.md)
* [开发最佳实践](/help/sites-developing/best-practices.md)
* [创作最佳实践](/help/sites-authoring/best-practices.md)

以下各表中介绍了具体的文档并提供了相应链接。

## OAK {#oak}

[](/help/sites-deploying/platform.md) Oak是一个可扩展且性能卓越的分层内容存储库，是AEM的基础。

<table>
 <tbody>
  <tr>
   <td><p>可扩展性、性能和灾难恢复</p> </td>
   <td><a href="/help/sites-deploying/performance.md">性能和可扩展性</a></td>
   <td>提供白皮书，介绍技术敏捷性、高性能和可靠的灾难恢复功能</td>
  </tr>
  <tr>
   <td>推荐的OAK部署</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">推荐的部署</a></td>
   <td>描述部署方案</td>
  </tr>
  <tr>
   <td>Mongo拓扑</td>
   <td><a href="/help/sites-deploying/recommended-deploys.md">Mongo拓扑最佳实践</a></td>
   <td>描述mongo拓扑 — 何时使用哪种拓扑。</td>
  </tr>
  <tr>
   <td>数据存储选项</td>
   <td><a href="/help/sites-deploying/data-store-config.md">配置节点和数据存储</a></td>
   <td>本文档介绍有关存储二进制数据和内容节点的最佳实践。 包括有关使用Amazon S3数据存储的信息。</td>
  </tr>
  <tr>
   <td>在OAK中搜索</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">有关查询和索引的最佳实践</a><br /> </td>
   <td>介绍有关如何索引内容的最佳实践。</td>
  </tr>
 </tbody>
</table>

## 社区 {#communities}

AEM Communities简化了内部部署社区的创建和管理。 以下介绍了AEM Communities的最佳实践：

[社区内容存储](/help/communities/working-with-srp.md)  — 讨论用户生成内容(UGC)的新共享存储功能以及选择基础拓扑的注 [意事项](/help/communities/topologies.md)。

[推荐的社区部署](/help/sites-deploying/recommended-deploys.md#considerations-for-aem-communities)  — 描述推荐的社区部署。 |

## UI {#ui}

下面介绍了有关用户界面的最佳实践：

[面向客户的用户界面Recommendations](/help/sites-deploying/ui-recommendations.md)

AEM当前有两个UI:同一版本中的经典用户界面和触屏优化用户界面。 因此，客户必须在项目实施期间决定要使用哪些组件。 本文档旨在帮助查找正确的选择。

## 演出 {#performance}

以下列出了有关性能的最佳实践：

<table>
 <tbody>
  <tr>
   <td>质量保证最佳实践</td>
   <td><a href="/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance">质量保证最佳实践</a></td>
   <td>针对在<em>publish</em>环境中的性能测试专门定义测试概念时涉及的问题的标准化概述。 这主要是QA工程师、项目经理和系统管理员感兴趣的。</td>
  </tr>
  <tr>
   <td>将 Dispatcher 与 CDN 结合使用</td>
   <td><a href="https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html#using-dispatcher-with-a-cdn">将 Dispatcher 与 CDN 结合使用</a></td>
   <td>内容交付网络 (CDN)（如 Akamai Edge Delivery 或 Amazon Cloud Front）从距离最终用户较近的站点交付内容。</td>
  </tr>
  <tr>
   <td>性能优化</td>
   <td><a href="/help/sites-deploying/configuring-performance.md">性能优化</a></td>
   <td>一个关键问题是您的网站响应访客请求所花费的时间。</td>
  </tr>
  <tr>
   <td>性能测试</td>
   <td><a href="/help/sites-deploying/best-practices-for-performance-testing.md">性能测试的最佳实践</a></td>
   <td>介绍在AEM部署上运行性能测试的最佳实践。<br /> </td>
  </tr>
 </tbody>
</table>
