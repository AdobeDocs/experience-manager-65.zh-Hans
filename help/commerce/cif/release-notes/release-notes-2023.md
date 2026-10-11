---
title: AEM内容和Commerce 2023年发行说明
description: Adobe Experience Manager内容和Commerce 2023年发行说明。
exl-id: 00349400-6860-4e3c-ba56-fa12afc5db1d
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 20%
---
# Commerce integration framework GitHub版本概述

## 系统要求概述

请查看下表中当前使用或计划将来使用的CIF版本的最低系统要求。

| 组件 | 系统要求 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF加载项 | 最低配置：AEM 6.5.8、Adobe Commerce 2.3.5 GraphQL架构 |
| CIF 核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期： 2023年12月

| 组件 | 版本 | 详细信息 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF 核心组件 | 2.12.4 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.4) |

### 错误修复 {#bug-fixes-december}

* 为页面v3资源类型注册的产品和类别重定向servlet
* 修复CIF AEP Extension Live Search事件

## 发行日期： 2023年11月

| 组件 | 版本 | 详细信息 |
|:-------|:-------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| CIF加载项 | 2023.11.23.00 | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Faem-commerce-addon-65-2023.11.23.00.zip) |
| CIF Venia参考站点 | 2023.11.08 | [GitHub](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2023.11.08) |

### 错误修复 {#bug-fixes-november}

* 在CIF配置控制台中显示40多个配置

## 发行日期： 2023年7月

| 组件 | 版本 | 详细信息 |
|:-------|:-------:|--------------------------------------------------------------------------------------------------------------:|
| CIF 核心组件 | 2.12.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.2) |

### 新增功能 {#what-is-new-july}

* `ProductList`组件中的产品筛选器挂钩
