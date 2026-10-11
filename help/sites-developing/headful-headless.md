---
title: AEM 中的 Headful 和 Headless
description: AEM 项目可以在 Headful 和 Headless 模型中实施，但这不是一个二选一的选择。 利用 AEM，可以在一个项目中灵活地运用这两种模型的优势。
exl-id: c9597c78-be05-42ff-84fe-f7451119e83d
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 75%
---
# AEM 中的 Headful 和 Headless {#headful-headless}

Adobe Experience Manager 项目可以在 Headful 和 Headless 模型中实施，但这不是一个二选一的选择。 利用 AEM，可以在一个项目中灵活地运用这两种模型的优势。 本文档概述了不同的模型，并描述了SPA集成的级别。

## 概述 {#overview}

AEM 提供了功能强大的工具来管理一个平台上的内容创建和交付操作。 这是传统的内容管理“Headful”模型，在该模型中，内容作者和开发人员在同一个平台上工作以将体验交付给内容消费者。

AEM 还可用于简单地管理内容，并允许呈现和交付要由另一个平台管理的内容。 这是内容管理“Headless”模型，在该模型中，内容作者和开发人员在不同的平台上工作以将体验交付给内容消费者。

但这不必是一个二选一的选择。 AEM 提供了前所未有的灵活性，使您能够在项目中灵活地运用这两种模型的优势。

![AEM 实施模型](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

在Headful或全栈模型中，内容在AEM存储库中进行管理，而基于Java、HTL等的AEM组件用于呈现用户体验的内容。 在此模型中，内容的创建、样式设置、呈现和交付操作都在 AEM 中进行。

在 Headless 模型中，内容在 AEM 存储库中管理，但通过 REST 和 GraphQL 等 API 交付到另一个系统以呈现用户体验的内容。 在此模型中，内容的创建操作是在 AEM 中进行的，但内容的样式设置、呈现和交付操作是在另一个平台中进行的。

单页应用程序 (SPA) 通常是 AEM 以 Headless 方式交付内容的目标。 但是，这些 SPA 不必完全在 AEM 外部。 利用 AEM，您可以决定 SPA 集成到 AEM 中的程度。 让我们举个例子。

## 网上商店示例 {#web-shop-example}

假设您将公司现有的网上商店作为 SPA， 其中包含所有产品详细信息和图像。 随后，您引入 AEM 来支持您的营销工作，例如促销网站、博客和活动内容。 如何将这两者集成？ AEM 支持一系列选项：

* **允许系统单独运行。**
* **通过GraphQL从AEM向网络商店提供有限的内容。** 内容可由作者在AEM中创建，但只能通过Web商店SPA查看。
* **在AEM中嵌入Web商店SPA。** 内容可由AEM中的作者创建，并在AEM的Web商店上下文中查看，但无法操作。
* **在AEM中嵌入Web商店SPA，并启用可编辑的点。** 内容可以由作者在AEM中创建，并在AEM的Web商店上下文中查看，而且作者在AEM中处理Web商店SPA内容的能力有限。
* **在AEM中嵌入Web商店SPA，并启用整个区域进行编辑。** 内容可以由作者在AEM中创建，并在AEM的Web商店上下文中查看，而且作者在AEM中处理Web商店SPA内容的能力有限。

在下一部分中，我们将更详细地探究这些集成级别。

>[!NOTE]
>
>当然，您还可以使用AEM SPA Editor框架将Web商店SPA重新实施为功能齐全的AEM SPA [。](/help/sites-developing/spa-walkthrough.md) 如果您已经拥有AEM并且想要创建Web商店或其他SPA，则推荐使用此方法，但本文档未包含此方法。

## SPA 集成级别 {#integration-levels}

SPA 集成归入 AEM 中包含四个级别的系列中。

* **级别 0：无集成**
  * SPA 和 AEM 单独存在，并且不交换任何信息。
  * 在两个独立的系统中单独创建、管理和交付内容。
* **级别 1：内容片段集成**
  * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的有限内容。
  * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
  * 在 AEM 中管理一些内容，在外部系统中管理另一些内容。
  * 只能在 SPA 中查看内容。
* **级别 2：将 SPA 嵌入 AEM**
  * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的内容。
  * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
  * 在 AEM 中管理一些内容，在外部系统中管理另一些内容。
  * 可在 AEM 中的上下文中查看内容。
  * 可在 AEM 中编辑有限内容。
* **级别 3：在 AEM 中嵌入并完全启用 SPA**
  * [内容片段](/help/assets/content-fragments/content-fragments.md)在 AEM 中用于创建和管理 SPA 的内容。
  * SPA 通过 AEM 的 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) 检索此内容。
  * 可在 AEM 中的上下文中查看内容。
  * 可在 AEM 中编辑大多数内容。

级别 1 是典型 Headless 实施的示例。 但是，内容作者只能在 SPA 中的上下文中查看其内容。 AEM 只是一项创作工具。

AEM 的优势和灵活性在级别 2 和级别 3 中变得明显，同时仍保留了 SPA 的优势。 内容作者既可以在 AEM 中创建其内容，也可以在 AEM 中的上下文中查看其内容。 虽然可以在 AEM 中创作 SPA，但它将作为 SPA 交付。

## 实施集成级别 {#implementing}

AEM 中提供了不同的工具，具体取决于您选择的集成级别。 每个级别均基于之前使用的工具而构建。 以下列表将链接到相关资源。

* **级别 1：**&#x200B;内容片段和 [AEM Headless 框架](/help/sites-developing/headless/introduction.md)可用于将 AEM 内容交付给 SPA。
* **级别 2：**&#x200B;除了级别 1 之外：
  * [RemotePage 组件](/help/sites-developing/spa-remote-page.md)可用于将外部 SPA 嵌入到 AEM 中，这样便能在上下文中查看 AEM 内容。
  * 还可以启用 SPA 上的某些点以[允许在 AEM 中进行有限编辑。](/help/sites-developing/spa-edit-external.md)
* **级别 3：**&#x200B;除了级别 2 之外：
  * 可以启用 SPA 的整个区域以允许在 AEM 中进行全面编辑。
