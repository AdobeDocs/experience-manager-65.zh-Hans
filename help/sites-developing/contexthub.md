---
title: ContextHub
description: ContextHub是一个用于存储、操作和呈现上下文数据的框架
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3fd50655-7461-4900-a3b8-c01b04c7ba7a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 1%
---
# ContextHub{#contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 通过客户端JavaScript API，可访问数据以使内容个性化。

>[!NOTE]
>
>[We.Retail引用实施](/help/sites-developing/we-retail.md)实现了ContextHub，当您将ContextHub集成到您自己的项目中时，可以将其用作引用。

>[!CAUTION]
>
>包含[We.Retail引用实施](/help/sites-developing/we-retail.md) (`/libs/settings/cloudsettings/legacy`)使用的示例ContextHub配置的路径只能用作创建您自己的配置的引用。
>
>请勿在项目中使用作为您自己的ContextHub配置。

## 持久性 {#persistence}

ContextHub存储在客户端上保留上下文数据。 通过ContextHub JavaScript API，您可以访问存储，以根据需要创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多个[示例存储类型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM控制台[创建存储](ch-configuring.md#creating-a-contexthub-store)。
* 开发人员可以[创建自定义商店类型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 开发人员可以通过JavaScript [访问存储数据](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)。

## 分段 {#segmentation}

ContextHub包括管理区段并确定当前上下文解析哪些区段的分段引擎。 定义了多个区段。 您可以使用JavaScript API [确定已解析的区段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 演示文稿 {#presentation}

通过[ContextHub工具栏](/help/sites-authoring/ch-previewing.md)，营销人员和作者可以查看和处理存储数据，以模拟创作页面时的用户体验。 工具栏由提供对ContextHub存储的访问权限的UI模块组组成。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供了多个[示例模块类型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM控制台以[添加UI模块](ch-configuring.md#adding-a-ui-module)，并[在UI模式中将它们分组](ch-configuring.md#adding-a-ui-mode)。

* 开发人员可以[创建自定义模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

开发人员需要[将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md)。
