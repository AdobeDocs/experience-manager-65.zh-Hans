---
title: AEM内容和Commerce 2024年发行说明
description: Adobe Experience Manager内容和Commerce 2024年发行说明。
exl-id: 372e6a46-72bb-4db4-ad01-534ca723ae58
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 1788e5f77d4c46a548710361e9e5dae3c6daab28
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 26%

---

# Commerce integration frameworkGitHub版本概述

## 系统要求概述

查看下表中，您当前使用或计划将来使用的CIF版本的最低系统要求。

| 组件 | 系统要求 |
|:-------|:-----------------------------------------------------------------------------------------------:|
| CIF加载项 | 最低配置：AEM 6.5.18、Adobe Commerce 2.3.5 GraphQL架构 |
| CIF核心组件 | [系统要求](https://github.com/adobe/aem-core-cif-components/blob/master/VERSIONS.md) |
| AEM 项目原型 | [系统要求](https://github.com/adobe/aem-project-archetype/blob/master/VERSIONS.md) |

## 发行日期： 2024年10月

| 组件 | 版本 | 详细信息 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF核心组件 | 2.15.0 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.15.0) |

### 错误修复 {#bug-fixes-October}

* 修复了UI测试，以便能够与核心CIF组件正常配合使用。
* 解决了类别URL格式在云实例中无法按预期发挥作用的问题。

## 发行日期： 2024年9月

| 组件 | 版本 | 详细信息 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF核心组件 | 2.14.2 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.14.2) |

### 改进功能 {#improvements-September}

* 使类别限制可定制。

### 错误修复 {#bug-fixes-September}

* 商业字段未与资产元数据模式编辑器正确集成。
* 拖放式旋转产品多字段问题。
* 拖放的轮播类别多字段问题
* 单击不适用于类别和产品编辑器页面上的页面信息中的菜单。
* 订单号在订单确认页面中不可见。

## 发行日期： 2024年1月

| 组件 | 版本 | 详细信息 |
|:-------|:-------:|-----------------------------------------------------------------------------------------------------------:|
| CIF核心组件 | 2.12.6 | [GitHub](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-2.12.6) |

### 错误修复 {#bug-fixes-january}

* 修复了产品收藏集组件中的“添加到购物车”按钮和“添加到愿望清单”按钮
