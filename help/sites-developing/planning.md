---
title: 规划
seo-title: 规划
description: 为测试制定计划所需知识
seo-description: 为测试制定计划所需知识
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---


# 规划{#planning}

本文档介绍了您在规划测试时需要了解的信息。 此外，您还应在进行测试之前回答以下问题：

* [需要哪些测试环境？](/help/sites-developing/test-environments.md)
* [定义测试案例](/help/sites-developing/test-cases.md)
* [测试 — 何时与谁一起进行？](/help/sites-developing/when-who.md)

## 开始之前 {#before-you-start}

在开始实际分析和定义测试之前，请查看以下信息：

**AEM架构**  — 请参阅基本概念，以向您介绍AEM的架构和基本原则。

**文档**  — 有关更多信息，请参阅任何文档部分或操作方法文章。

**测试的基本原则**  — 您应该了解软件测试和质量保证的基本原则。您最好应具有测试项目的经验。

许多网站、书籍和课程都涉及这些原则，因此本文件不会详细讨论这些原则。

**要避免的假设**  — 最大的假设（定期提供）是您的网站每天需要为数百万个请求提供服务。在某些情况下，这可能是真的，但不能假定。

尽管未来的数字无法以100%的准确度进行预测，但观察您的现有网站和所体验的流量将给出一个很好的指示。 然后，您可以根据预期/希望流量增加的因素进行估计。

**对质量的承诺**  — 至关重要的是，任何测试者都必须保持中立，只报告测试结果。

项目经理有责任根据结果决定并启动行动。

**参与**  — 尽管项目经理有责任确保所有各方都充分参与任何会议（状态、研讨会等），但您也应努力尽早参与项目周期，包括信息收集和需求分析流程。

**让客户参与**  — 在类似的主题中，尽量让客户参与定义测试案例和计划。

## 测试类型{#types-of-tests}

测试有各种标准分类，在测试AEM项目时适合使用。 您应该熟悉这些内容，以决定要使用哪些内容：

>[!NOTE]
>
>这些文件按应用程序的时间顺序列出。

**单位测试**  — 由开发团队进行的测试（通常），可确保各个元素正常运行，尽管是单独进行的。

**集成测试**  — 组合后测试模块。这些测试在单元测试之后，但在系统测试之前进行。

**烟雾测试**  — 这些是快速且脏的测试，用于证明软件正在运行且提供高级功能。细节未经测试。

**功能测试**  — 用于测试软件的功能。将设计一系列测试以涵盖所有功能详细信息，包括预期和意外输入和/或错误输入。

黑盒测试是完整单元/组件/模块的功能测试，在不了解相关元素内部工作情况的情况下执行。

**系统测试**  — 一旦系统完全集成并安装在合适的平台上，这些测试就会对整个系统进行测试。

他们会黑盒测试功能。

**性能测试**  — 测试AEM时，性能测试至关重要。

它们用于说明不同条件下的性能：

* 标准

   网站在90%的时间内会遇到的条件。 例如，当只有一部分作者使用系统时。

* 峰值

   因特殊情况将在一段时间内按比例经历的条件；例如，当所有作者同时使用系统或发布新内容并增加查看您网站的访客数时。

* 极端

   当您的网站上发布了新的、极其有趣的内容时，可用于模拟性能预测。 那么，极端峰值可能会出现 — 尽管这未必是完全可预测的。

   当特定事件的票证可供使用或首次发布期待已久的网站时，有时会发现这些情况。

然后，将结果用于调节应用程序。

**应力测试**  — 进行应力测试以确认元件或应用程序在极端条件下的行为方式。特别是，这些测试用于显示行为在元素失败时、以及如何恶化。

**回归测试**  — 使用回归测试来确认在以前版本的软件中已验证的功能仍然正常运行。

回归测试是自动化（如果可能）的好候选项，可确保快速、一致地重复测试。

**验收测试**  — 验收测试是一种特殊类别，因为它们用于指示客户对项目的验收。

验收测试列表可能包含上述各类测试的组合，并且被选择以验证项目是否满足客户的要求

有关更多详细信息，请参阅[接受和注销](/help/sites-developing/acceptance-signoff.md)。

## 入门 {#getting-started}

在开始详细的测试案例和测试计划之前，您可以：

**定义目标**  — 定义您的高级别目标，以作为在测试进行过程中进行微调的起点。您将需要：

* 根据详细需求规范测试功能。
* 根据[目标量度](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics)测试性能。

其中包括。

**从现有网站收集流量统计信息**  — 此信息可从日志文件中提取 — 有关更多详细信息，请参阅性能监控。

这些数字将指示现有网站上的当前流量（流量和分布），并可用于形成新网站的基点。

**从外部网站收集流量统计信息**  — 如果可能，您可以尝试从其他网站收集流量统计信息以进行比较，但并非总是发布这些数据。

**确认目标量度**  — 量度用于定义网站质量的定量度量，因为它们表示要实现的性能目标。

应在项目开始时与客户一起定义它们。 有关更多信息，请参阅[目标量度](/help/sites-developing/planning.md)。
