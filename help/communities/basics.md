---
title: 社区组件基础知识
description: 在编辑模式下将社区功能添加到AEM站点并配置组件
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 1%

---

# 社区组件基础知识 {#communities-components-basics}

## 概述 {#overview}

本文档的创作部分介绍了如何在创作编辑模式下将社区功能添加到AEM站点，并描述了组件配置。

可以使用AEM实例和交互式[社区组件指南](components-guide.md)来探索组件。

## 访问社区组件 {#accessing-communities-components}

在创作页面内容时，如果基础模板允许对页面设计进行更改，则可以启用组件浏览器中尚未提供的组件，将其作为网站设计的一部分。

可用的Communities组件在[此处](author-communities.md#available-communities-components)列出。

>[!NOTE]
>
>有关一般创作信息，请查看[页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。
>
>如果不熟悉AEM，请查看有关[基本处理](../../help/sites-authoring/basic-handling.md)的文档。

### 进入设计模式 {#entering-design-mode}

如果在组件浏览器(sidekick)中找不到&#x200B;**Communities**&#x200B;组件，则需要输入`Design Mode`以添加其他Communities组件。 可能还需要添加[所需的客户端库](#required-clientlibs) (clientlibs)。

有关详细信息，请参阅[在设计模式下配置组件](../../help/sites-authoring/default-components-designmode.md)。

以下是选择一些Communities组件并在组件浏览器中查看这些组件的图像：

![组件设计](assets/component-design.png)

现在，组件浏览器中提供了选定的组件：

![组件设计1](assets/component-design1.png)

## 所需的Clientlibs {#required-clientlibs}

组件正常使用(JavaScript)和样式设置(CSS)需要[客户端库](../../help/sites-developing/clientlibs.md) (clientlibs)。

将Communities组件添加到页面时，如果结果为错误或意外外观，则首先要尝试为Communities组件添加所需的clientlibs。 有关详细信息，请参阅[社区组件的Clientlibs](clientlibs.md)。

### 示例：最初放置的审阅没有客户端库…… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...以及客户端库 {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## 标记 {#tagging}

许多Communities功能可以配置为允许成员标记在发布环境中输入（发布）的内容。

如果允许标记，则可以设置社区站点的配置以限制向发布环境中的成员显示的命名空间。 查看[社区站点控制台](sites-console.md#tagging)。

允许标记的功能： [博客](blog-feature.md)、[日历](calendar.md)、[文件库](file-library.md)、[论坛](forum.md)

使用标记的功能： [搜索](search.md)，[社交标记云](tagcloud.md)

有关创作信息：

* [使用标记](../../help/sites-authoring/tags.md)

有关管理信息：

* 正在创建标记命名空间（分类）： [管理标记](../../help/sites-administering/tags.md)
* 社区站点配置：请参阅[标记](sites-console.md#tagging)
* [标记用户生成的内容](../../help/sites-authoring/tags.md)

有关开发人员信息：

* [AEM 标记框架](../../help/sites-developing/framework.md)
* [标记Essentials](tag.md)
