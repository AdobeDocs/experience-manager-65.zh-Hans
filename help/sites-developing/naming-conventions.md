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
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---

# 命名约定 {#naming-conventions}

存储库中的节点遵循[Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository)的命名约定。 但是，AEM对页面节点名称施加进一步的约定。

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
