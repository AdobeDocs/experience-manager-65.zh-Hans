---
title: 电子商务概述
description: AEM通用电子商务作为标准安装的一部分提供，它提供了电子商务框架的完整功能。
feature: Commerce Integration Framework
exl-id: 3567bd28-73aa-401a-8aa9-a62a99d2a613
solution: Experience Manager,Commerce
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 2%

---

# 电子商务概述{#ecommerce-overview}

AEM通用电子商务作为标准安装的一部分提供，它提供了电子商务框架的完整功能。

Adobe提供以下两个版本的Commerce integration framework：

|                         | CIF内部部署 | CIF Cloud |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| 支持的 AEM 版本 | 内部部署AEM或AMS 6.x | AEM AMS 6.4和6.5 |
| 后端 | - AEM， Java™ <br> — 整体集成，预生成映射（模板）<br> - JCR存储库 | - Adobe Commerce <br>- Java和JavaScript <br> — 没有存储在JCR存储库中的Commerce数据 |
| 前端 | AEM服务器端渲染的页面 | 混合页面应用程序（混合渲染） |
| 产品目录 |  — 产品导入器、编辑器、AEM <br>中的缓存 — 包含AEM或代理页面的常规目录 |  — 无产品导入<br> — 通用模板<br> — 通过连接器的按需数据 |
| 可扩展性 |  — 最多可支持数百万个产品（取决于用例） <br> — 在Dispatcher上缓存 |  — 无卷限制<br>- Dispatcher或CDN上的缓存 |
| 标准化数据模型 | 否 | 是，Adobe Commerce GraphQL架构 |
| 可用性 | 是：<br> - SAPCommerce Cloud(扩展已更新，以支持AEM 6.4和Hybris 5 （默认）)，并保持与Hybris 4 <br>的兼容性 — SalesforceCommerce Cloud(连接器开源，以支持AEM 6.4) | 通过GitHub的开源提供。 <br> Adobe Commerce (支持2.3.2（默认）并与2.3.1兼容)。 |
| 何时使用 | 有限用例：对于较小的情况，根据需要导入静态目录 | 大多数用例中的首选解决方案 |


## 部署其他实施 {#deploying-other-implementations}

对于AEM和Adobe Commerce，请使用[Commerce integration framework](/help/commerce/cif/introduction.md)查看[AEM和Adobe Commerce集成](/help/commerce/cif/integrating/magento.md)。

>[!NOTE]
>
>有关概念和管理电子商务实施的信息，请参阅[管理电子商务](/help/commerce/cif-classic/administering/ecommerce.md)。
>
>有关扩展电子商务功能的信息，请参阅[开发电子商务](/help/commerce/cif-classic/developing/ecommerce.md)。
