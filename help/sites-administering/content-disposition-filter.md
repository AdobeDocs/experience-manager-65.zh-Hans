---
title: 内容处置过滤器
description: 了解如何使用内容处置过滤器来防御XSS攻击。
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 内容处置过滤器 {#content-disposition-filter}

内容处置过滤器是针对SVG文件的XSS攻击的安全功能。

安装后，该过滤器将阻止对所有资源的访问。 例如，您无法在线查看PDF。 本节将介绍如何根据需要配置过滤器。

## 配置内容处置过滤器 {#configure-content-disposition-filter}

您可以在GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)中查看[Apache Sling内容处置过滤器。

“内容处置过滤器”选项提供了以下功能：

* **内容处置路径：**&#x200B;应用过滤器的路径列表，后跟要排除在该路径上的mime类型列表。 此路径必须是绝对路径，并且末尾可能包含通配符(`*`)，以便每个资源路径与给定的路径前缀匹配。 例如： `/content/*:image/jpeg,image/svg+xml`将过滤器应用于`/content?`中除JPG和SVG图像之外的每个节点。

* **排除的资源路径：**&#x200B;排除的资源列表，每个资源路径都必须作为绝对和完全限定的路径提供。 不支持前缀匹配/通配符。

* **为所有资源路径启用：**&#x200B;此标志控制是否为所有路径启用此筛选器，排除的资源路径所定义的排除路径除外。 将此标记设置为“true”会导致忽略内容处置路径。 与配置无关，只覆盖包含名为`jcr:data`或`jcr:content/jcr:data`的属性的资源路径。
