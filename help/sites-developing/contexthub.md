---
title: ContextHub
seo-title: ContextHub
description: ContextHub是存储、操作和呈现上下文数据的框架
seo-description: ContextHub是存储、操作和呈现上下文数据的框架
uuid: 14e6ff4f-ffbe-454a-b2ec-a35333526e27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: acf5c17a-95b7-43ba-9734-241e20f4f374
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# ContextHub{#contexthub}

ContextHub是一个用于存储、操作和呈现上下文数据的框架。 客户端Javascript API允许您访问数据以个性化内容。

>[!NOTE]
>
>We. [Retail引用实施](/help/sites-developing/we-retail.md) (We.Retail Reference Implementation)实现ContextHub，并在将ContextHub集成到您自己的项目中时用作引用。

>[!CAUTION]
>
>包含 [We.Retail引用实施](/help/sites-developing/we-retail.md) ( `/libs/settings/cloudsettings/legacy`)所使用的示例ContextHub配置的路径应仅用作创建您自己的配置的引用。
>
>它不应在项目中用作您自己的ContextHub配置。

## 持久性 {#persistence}

ContextHub在客户端上存储持续的上下文数据。 ContextHub Javascript API允许您访问存储，以根据需要创建、更新和删除数据。 因此，ContextHub表示页面上的数据层。

每个ContextHub存储都是预定义存储类型的实例：

* ContextHub提供了多 [种示例存储类型](/help/sites-developing/ch-samplestores.md)。
* 使用AEM控制台可 [创建商店](/help/sites-administering/contexthub-config.md#creating-a-contexthub-store)。
* 开发人员可 [以创建自定义存储类型](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)。
* 开发人员可 [以通过Javascript访问存储数据](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores) 。

## 分段 {#segmentation}

ContextHub包括分段引擎，该引擎管理区段并确定为当前上下文解析哪些区段。 定义了多个区段。 您可以使用Javascript API确定已 [解析的区段](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)。

## 演示文稿 {#presentation}

ContextHub工 [具栏使营销人员和作者能够查看和操作商店数据](/help/sites-authoring/ch-previewing.md) ，以模拟创作页面时的用户体验。 工具栏由提供对ContextHub存储区访问权限的UI模块组成。

每个ContextHub UI模块都是预定义模块类型的实例：

* ContextHub提供多 [种示例模块类型](/help/sites-developing/ch-samplemodules.md)。
* 使用AEM控制台 [添加UI模块](/help/sites-administering/contexthub-config.md#adding-a-ui-module)，并在UI [模式中对它们分组](/help/sites-administering/contexthub-config.md#adding-a-ui-mode)。

* 开发人员可 [以创建自定义模块类型](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)。

开发人员需 [要将ContextHub组件添加到页面](/help/sites-developing/ch-adding.md)。
