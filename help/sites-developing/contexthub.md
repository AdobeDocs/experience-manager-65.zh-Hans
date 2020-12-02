---
title: ContextHub
seo-title: ContextHub
description: ContextHub是存储、处理和呈现上下文数据的框架
seo-description: ContextHub是存储、处理和呈现上下文数据的框架
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---


# ContextHub{#contexthub}

ContextHub是存储、处理和呈现上下文数据的框架。 客户端Javascript API允许您访问数据以个性化内容。

>[!NOTE]
>
>[We.Retail引用实现](/help/sites-developing/we-retail.md)实现ContextHub，并可作为将ContextHub集成到您自己的项目中的引用。

>[!CAUTION]
>
>包含[We.Retail引用实现](/help/sites-developing/we-retail.md)(`/libs/settings/cloudsettings/legacy`)使用的示例ContextHub配置的路径应仅用作创建您自己的配置的引用。
>
>它不应在项目中用作您自己的ContextHub配置。

## 持久性{#persistence}

ContextHub在客户端上存储持续的上下文数据。 ContextHub Javascript API允许您根据需要访问存储以创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供多种[示例存储类型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM控制台创建[商店](ch-configuring.md#creating-a-contexthub-store)。
* 开发人员可以[创建自定义存储类型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 开发人员可以通过Javascript[访问存储数据](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)。

## 分段 {#segmentation}

ContextHub包含一个分段引擎，它管理区段并确定为当前上下文解析哪些区段。 定义了多个区段。 您可以使用Javascript API确定已解析的段[。](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)

## 演示文稿 {#presentation}

[ContextHub工具栏](/help/sites-authoring/ch-previewing.md)使营销人员和作者能够查看和操作存储数据，以在创作页面时模拟用户体验。 工具栏由提供对ContextHub存储区访问权限的UI模块组成。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供多种[示例模块类型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM控制台添加[UI模块](ch-configuring.md#adding-a-ui-module)，并以UI模式](ch-configuring.md#adding-a-ui-mode)将它们分组。[

* 开发人员可以[创建自定义模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

开发人员需要[将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md)。
