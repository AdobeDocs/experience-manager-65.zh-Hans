---
title: Java内容存储库中节点的命名约定
description: 存储库中的节点遵循Java内容存储库的命名约定
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%
---
# 命名惯例 {#naming-conventions}

存储库中的节点遵循[Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository)的命名约定。 但是，AEM对页面节点名称实施了进一步的约定。

## 页面的命名约定 {#naming-conventions-for-pages}

这些命名惯例在各级实施：

* JcrUtil： [JCR实用程序](#jcr-utilities)的AEM实现。
* PageManager： [页面管理器](#page-manager)提供页面级操作的方法。
* 根据使用的UI：

  * [标准触屏UI](#standard-ui)
  * [经典 UI](#classic-ui)

### JCR实用程序 {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html)是JCR实用程序的AEM实现。 验证名称特别感兴趣的是它控制的字符映射以及以下验证：

* `isValidName`

  * 检查名称是否不为空且仅包含有效字符。
  * 可用于检查建议的名称是否有效。

* `createValidName`

  * 这会根据任意字符串创建一个有效标签。
  * 它可用于从标题创建名称。

### 页面管理器 {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)提供了基于[JCRUtil](#jcr-utilities)的页面级操作方法。

### 标准 UI {#standard-ui}

标准触屏优化UI：

* 在执行以下任一操作时，根据PageManager施加的限制验证名称：

  * 提供了页面标题以转换为节点名称
  * 提供了显式节点名称

### 经典 UI {#classic-ui}

经典UI施加了更严格的限制：

* 在出现以下任一情况时验证显式节点名称的名称：

  * 提供了页面标题以转换为节点名称
  * 提供了显式节点名称

* 有效字符（从经典UI中创建页面时，尽管`PageManagerImpl`允许使用其他字符，但实际上只有这些字符有效）：

  * &#39;a&#39;到&#39;z&#39;
  * &#39;A&#39;到&#39;Z&#39;
  * &#39;0&#39;到&#39;9&#39;
  * _ （下划线）
  * `-` （短划线/减号）
