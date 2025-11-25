---
title: AEM Headless 翻译历程
description: 从这里开始，通过使用 AEM 强大的翻译工具来翻译您的 Headless 内容，实施引导式历程。
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Developer, User, Leader
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 93%

---

# AEM Headless 翻译历程 {#aem-headless-translation-journey}

从这里开始，通过使用 AEM 强大的翻译工具来翻译您的 Headless 内容，实施引导式历程。

## 简介 {#introduction}

Headless 实施对于向受众提供体验而言变得越来越重要，无论他们身在何处以及渠道、区域或区域设置如何。

Headless 实施放弃了传统的全栈解决方案中的页面和组件管理，专注于创建渠道中性的、可重用的内容片段，以及它们的跨渠道交付。通过使用 AEM 的功能强大的翻译工具，可以轻松翻译这些可重用的片段并将其交付给您的受众，无论他们身在何处。

本指南将引导您了解最重要的 Headless 翻译主题，以便在完成后，您将：

* 大致了解 Headless 内容交付的含义。
* 基本了解 AEM 的 Headless 功能。
* 了解 AEM 的翻译功能以及它们如何与 Headless 内容相关联。
* 能够开始翻译您自己的 Headless 内容。

目标是让您广泛了解 Headless 技术、AEM 提供 Headless 内容的方式以及翻译 Headless 内容的方式。如果您不熟悉所有这些主题，这将是您的理想起点。

如果您已熟悉 AEM、Headless 和翻译，则您可能已大致了解此历程。请考虑参阅[下面的“其他资源”部分](#additional-resources)下链接的技术文档。

## AEM 文档历程 {#documentation-journeys}

[文档历程](/help/journey-documentation/home.md)通过提供叙述来帮助可能是 AEM 新手的读者彻底理解和解决业务问题，同时假定读者拥有最少的主题或 AEM 知识，从而将许多不同且可能复杂的主题和功能联系起来。

文档历程是围绕最佳实践准则而设计的，其中参考了 Adobe 的最新研究、Adobe 顾问提供的成熟实施经验以及客户项目产生的反馈。

如果您想了解 Adobe 就如何使用 AEM 解决 Headless 业务案例提出的建议，则可以从 [AEM Headless 历程](/help/journey-headless/overview.md)开始。

## 受众 {#audience}

此历程专为翻译专家用户画像（通常称为翻译项目经理 (TPM)）设计。此历程列出了在 AEM 中翻译 Headless 内容的要求、步骤和方法。此历程可能会定义翻译专家必须与之交互的其他用户画像，但历程的视角是翻译专家的视角。

此历程假定读者具有在大型 CMS 系统上翻译内容的经验但不了解 Headless 技术或 AEM。

以下是在此历程中互动的用户画像。

| 用户画像 | 描述 | 历程中的角色 |
|---|---|---|
| 翻译专家 | 定义应翻译的内容并管理这些工作流 | 此历程的受众 |
| 内容作者 | 创建和管理以 Headless 方式交付的内容 | 内容作者创建翻译专家必须翻译的内容。 |
| 管理员 | 管理 AEM 的基本设置和配置 | 翻译专家与管理员共同进行翻译所需的配置更改，例如安装翻译连接器。 |
| 内容架构师 | 分析必须以 Headless 方式交付的数据的要求并定义此数据的结构 | 翻译专家与内容架构师共同定义内容的组织结构，以便可轻松地翻译内容。 |

此历程中的信息可能对所有用户画像都很有用，但某些信息对某些角色而言可能是多余的。请继续关注[即将推出的涵盖其他角色的历程。](/help/journey-documentation/home.md#journeys)

## Headless 翻译历程 {#the-journey}

您将在此历程中探究多个主题。以下文章为您提供了在 AEM 中翻译 Headless 内容的基础知识以及指向详细技术文档的链接。

虽然您可以直接进入历程的特定部分，但许多概念都是基于之前文章中的概念来构建的。因此，如果您是 AEM Headless 翻译新手，Adobe 建议您从头开始，然后循序渐进。

| # | 文章 | 描述 |
|---|---|---|
| 0 | AEM Headless 翻译历程 | 本文档 |
| 1 | [了解 AEM 中的 Headless 内容及其翻译方法](learn-about.md) | 了解 Headless 概念、它们如何映射到 AEM 以及 AEM 翻译理论。 |
| 2 | [AEM Headless 翻译快速入门](getting-started.md) | 了解如何组织您的 Headless 内容以及 AEM 的翻译工具的工作原理。 |
| 3 | [配置翻译集成](configure-connector.md) | 了解如何将 AEM 连接到翻译服务。 |
| 4 | [配置翻译规则](translation-rules.md) | 了解如何定义翻译规则，标识要翻译的内容。 |
| 5 | [翻译内容](translate-content.md) | 使用翻译集成和规则翻译您的 Headless 内容。 |
| 6 | [发布翻译的内容](publish-content.md) | 了解如何发布翻译的内容并在更新基础内容时更新翻译。 |

## 后续内容 {#what-is-next}

您现在已准备好开始您的 Adobe Headless 翻译历程。我们鼓励您继续此历程的下一部分，并阅读[了解 Headless 内容以及如何在 AEM 中翻译该内容](learn-about.md)一文

## 其他资源 {#additional-resources}

文档历程将提供叙述来指导您完成复杂、相互关联的流程和使用相关功能，从而向您说明 AEM 如何解决业务问题。历程说明了多项功能如何协作以满足单一业务需求。

因此，旅程旨在自立。 但是，其中多个可以相互关联。 查看这些附加历程，详细了解 AEM 的强大功能如何协作。

* [Headless 创作历程](/help/journey-headless/author/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个 Headless 项目中为内容建模。
* [Headless架构师历程](/help/journey-headless/architect/overview.md) — 从这里开始了解Adobe Experience Manager强大而灵活的Headless功能，以及如何对项目内容进行建模。
* [AEM Headless 开发人员历程](/help/journey-headless/developer/overview.md) – 从这里开始，引导您了解 AEM 强大而灵活的 Headless 特性、它们的功能以及如何在您的第一个开发项目中利用它们。
* [AEM技术文档](https://experienceleague.adobe.com/docs/experience-manager-65.html) — 如果您已对AEM和Headless技术有一定的了解，则可能需要直接参阅深入的技术文档。
   * [AEM as a Headless CMS 简介](/help/sites-developing/headless/introduction.md)
* [AEM Headless 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=zh-Hans) – 如果您更喜欢通过实践学习并有技术倾向，请参阅我们的按 API 和框架编排的实践教程，探究如何创建和使用基于 AEM Headless 的应用程序。
* [AEM 开发人员门户](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hans)
