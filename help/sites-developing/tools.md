---
title: 测试与跟踪工具
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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 5%
---
# 测试与跟踪工具{#testing-and-tracking-tools}

## 测试 {#testing}

AEM 提供：

* [用于测试组件UI的框架](/help/sites-developing/hobbes.md)。
* [用于测试和调试组件的机制](/help/sites-developing/developer-mode.md)。

以下是两个Open Source测试工具：

**硒**

Selenium用于在浏览器中测试功能，每个活动有一个用户。 它将测试步骤（单击次数）记录为HTML表或Java™类。

有关详细信息，请参阅[https://www.selenium.dev/](https://www.selenium.dev/)。

**JMeter**

JMeter用于跟踪请求，可用于功能、性能和压力测试。

有关详细信息，请参阅[https://jmeter.apache.org/](https://jmeter.apache.org/)。

还有许多用于自动化测试和管理测试计划的专有工具。

### 跟踪 {#tracking}

以下工具可轻松使用。 但是，在所有情况下，关键问题是向项目团队的所有成员（合作伙伴和客户）提供数据。

**Bugzilla**

可根据自己的要求配置的错误跟踪系统。

**电子表格**

虽然不是专门用于错误跟踪的工具，但电子表格通常会&#x200B;*mis*&#x200B;用于此目的，因为它们易于理解，并且大多数用户都对其功能具有经验。

如果这些电子表格用于跟踪，则：

* 它们应该保持简单。
* 应尽量减少单个电子表格的数量。
* 它们必须定期更新。
* 只应维护一个主副本，每个人都应知道主副本的位置。
* 它们应可供所有项目成员访问。
* 如果安全性是一个问题（通常发生在大公司）并且不能进行通用访问，那么只要每个人都知道这些电子表格是副本并且不能更新，就可以分发副本。

同样，还有许多用于跟踪错误和功能要求的专有工具。
