---
title: 为 AEM Forms 安装选择持久化类型
description: 明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: 621fe107-f4ac-42b1-8c7b-8abbcaac7380
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 6%
---
# 为 AEM Forms 安装选择持久化类型 {#choosing-a-persistence-type-for-an-aem-forms-installation}

明智地选择持久性类型。 它可帮助您构建高效且可扩展的AEM Forms环境。

持久性是在物理存储上存储内容的方法。 它定义了数据的实际数据结构和存储机制。 MicroKernels在AEM Forms中充当持久性管理器。 AEM Forms支持TarMK、MongoMK和RDBMK类型的持久性（微内核）。 您可以根据AEM Forms实例的用途和部署类型（单服务器、场或群集），为AEM Forms选择持久性类型。

>[!NOTE]
>
>LiveCycle ES4 SP1使用TarPM持久性存储内容。

下表列出了所有支持的持久性类型以及各种参数，可帮助您选择环境的持久性类型：

<table>
 <tbody>
  <tr>
   <th><strong>安装类型/成本</strong></th>
   <th><strong>tarmk</strong></th>
   <th><strong>MongoMk</strong></th>
   <th><strong>RDBMK</strong></th>
  </tr>
  <tr>
   <th><strong>独立设置</strong></th>
   <td>支持<br /> </td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>群集设置</strong></th>
   <td>不支持</td>
   <td>支持</td>
   <td>支持</td>
  </tr>
  <tr>
   <th><strong>许可成本</strong></th>
   <td>包含在AEM中 </td>
   <td>需要单独的许可证</td>
   <td>需要单独的许可证</td>
  </tr>
 </tbody>
</table>

TarMK旨在提高性能，而MongoMK和RDBMK旨在实现可扩展性。 Adobe强烈建议将TarMK作为所有AEM Forms部署方案（对于Author和Publish实例）的默认持久性技术，但[选择Mongo或关系数据库微内核而非TarMK](#p-choosing-mongo-or-a-relational-database-microkernel-over-tarmk-p)部分中概述的使用情况除外。

有关支持的微内核列表，请参阅[OSGi上的AEM Forms技术要求](/help/sites-deploying/technical-requirements.md)或[JEE上的AEM Forms支持的平台组合](/help/forms/using/aem-forms-jee-supported-platforms.md)篇文章。

## 在TarMK上选择Mongo或关系数据库微内核 {#choosing-mongo-or-a-relational-database-microkernel-over-tarmk}

可扩展（集群）AEM Forms环境是由两个或多个水平配置的活动创作实例组成的集合。 如果支持所有并发创作活动的单个服务器不再可持续，您可以选择运行多个创作实例。

JEE上的可缩放（集群）AEM Forms仅支持MongoMK和RDBMK持久性类型。 服务器的数量或可扩展环境的大小因每次安装而异。 有关注意事项和示例的列表，请参阅[推荐的部署](/help/sites-deploying/recommended-deploys.md)和/或[AEM Forms的架构和部署拓扑](/help/forms/using/aem-forms-architecture-deployment.md)文章。 您还可以联系AEM Forms支持，以获取有关使用RDBMK和TarMK的AEM Forms容量规划的详细信息。
