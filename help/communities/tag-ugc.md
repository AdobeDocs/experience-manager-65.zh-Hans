---
title: 标记用户生成的内容
description: 用户生成内容的标记(UGC)是社区成员帮助其他成员搜索内容的方式
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 4%

---

# 标记用户生成的内容 {#tagging-user-generated-content}

## 概述 {#overview}

用户生成内容标记(UGC)是社区成员帮助其他成员搜索内容的一种方法。

通常，标记由作者和管理员在创作环境中应用。 标记UGC是唯一的，因为UGC标记由发布环境中的社区成员应用。

两个应用程序的标记命名空间和分类是相同的。

## Communities功能 {#communities-features}

可配置为允许标记的AEM Communities功能包括：

* [博客](blog-feature.md)
* [日程表](calendar.md)
* [文件库](file-library.md)
* [论坛](forum.md#configuretheaddedforum)
* [问题与解答](working-with-qna.md)

## 管理标记 {#administering-tags}

请参阅[管理标记](../../help/sites-administering/tags.md#tagging-console)以创建和管理标记命名空间和分类。

有关开发人员信息，请参阅[Tag Essentials](tag.md)。

请参阅[使用Social Tag Cloud](tagcloud.md)，将Social Tag Cloud组件添加到页面，以便使用应用的标记搜索已发布的UGC。

### 标记权限 {#tag-permissions}

默认权限设置为不允许发布环境中的每个人读取标记命名空间。

由于标记应用于发布环境中的UGC，因此需要为社区成员启用读取权限，以便他们能够选择要应用的标记。

请参阅[设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。

下面是管理员对组`Community Engage Members`的`/etc/tag/discussions`应用读取权限时，它在CRXDE中的显示方式。

![标记权限](assets/tag-permissions.png)
