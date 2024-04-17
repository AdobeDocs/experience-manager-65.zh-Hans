---
title: 测试和跟踪工具
description: AEM提供了用于测试组件UI的框架和用于测试和调试组件的机制
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: bb5d1c7c-56ce-4d1e-a3cb-4e74d6922137
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 1%

---

# 测试和跟踪工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM 提供：

* [用于测试组件UI的框架](/help/sites-developing/hobbes.md).
* [用于测试和调试组件的机制](/help/sites-developing/developer-mode.md).

以下是两个开源测试工具：

**硒**

Selenium用于在浏览器中测试功能，每个活动有一个用户。 它将测试步骤（单击次数）记录为HTML表或Java™类。

有关更多信息，请参阅 [https://www.selenium.dev/](https://www.selenium.dev/).

**JMet**

JMeter用于跟踪请求，可用于功能、性能和压力测试。

有关更多信息，请参阅 [https://jmeter.apache.org/](https://jmeter.apache.org/).

还有许多用于自动化测试和管理测试计划的专有工具。

### 跟踪 {#tracking}

以下工具可轻松使用。 但是，在所有情况下，关键问题是向项目团队的所有成员（合作伙伴和客户）提供数据。

**Bugzilla**

可根据自己的要求配置的错误跟踪系统。

**电子表格**

虽然不是专门用于跟踪错误的工具，但电子表格通常 *mis*&#x200B;用于此目的，因为它们易于理解，并且大多数用户都对其功能具有体验。

如果这些电子表格用于跟踪，则：

* 它们应该保持简单。
* 应尽量减少单个电子表格的数量。
* 它们必须定期更新。
* 只应维护一个主副本，每个人都应知道主副本的位置。
* 它们应可供所有项目成员访问。
* 如果安全性是一个问题（通常发生在大公司）并且不能进行通用访问，那么只要每个人都知道这些电子表格是副本并且不能更新，就可以分发副本。

同样，还有许多用于跟踪错误和功能要求的专有工具。
