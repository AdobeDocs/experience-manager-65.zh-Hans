---
title: 迁移到AEM Commerce integration framework (CIF)加载项
description: 如何从旧版本迁移到AEM Commerce integration framework (CIF)加载项。
exl-id: c6c0c2fc-6cfa-4c64-b3d8-7e428b2a4b2e
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: b4056a4c1483dc8dcedc3c0f8f6b42f8dead0847
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# Experience Manager加载项的迁移指南 {#cif-migration}

本指南帮助确定您需要为Experience Manager加载项迁移更新的区域。

## CIF加载项

CIF加载项可通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&amp;2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&amp;2_group.propertyvalues.operation=equals&amp;2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=16)用于AEM 6.5。 它是兼容的，提供了与适用于Experience Manager as a Cloud Service的CIF加载项相同的功能。

请参阅[AEM内容和Commerce快速入门](getting-started.md)。

为支持部署 CIF 的项目，Adobe 提供了 [AEM CIF 核心组件](https://github.com/adobe/aem-core-cif-components)。

## 产品目录

CIF加载项不支持导入产品目录数据。 使用CIF附加组件主体，可以通过实时调用外部商务解决方案来按需请求产品和目录。 转到集成一章，了解有关集成商业解决方案的更多信息。

>[!TIP]
>
>如果没有可用的实时API，则应使用具有API的外部产品缓存进行集成。 示例[Magento开源](https://business.adobe.com/cn/products/magento/open-source.html)。

## 具有AEM渲染的产品目录体验

如果您将目录Blueprint与经典CIF结合使用，则需要更新产品目录工作流程。 CIF加载项现在使用AEM目录模板动态呈现产品目录体验。 不再需要复制产品数据或产品页面。

## 不可缓存的数据和购物交互

对不可缓存的数据和交互的客户端请求（例如，添加到购物车、搜索）应通过CDN/Dispatcher直接转到商务端点（商务解决方案或集成层）。 删除AEM只是代理的任何调用。
