---
title: 编写测试计划
description: 单个测试用例合并到测试计划中
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
exl-id: ee5df2c8-ab31-4be9-8ede-3c96f26fc626
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
source-wordcount: '194'
ht-degree: 4%
---
# 编写测试计划{#compiling-your-test-plan}

然后，各个测试用例将合并到您的测试计划中，该计划还将定义：

**优先级**

某些测试将比其他测试更有意义，因此建议指明其优先级。

例如，某些测试可能会影响“执行/不执行”决策，因此必须在每个测试的临时版本中进行确认。

**迭代**

如果您的项目使用任何形式的开发迭代（涉及提供多个版本），则您可能需要或希望指出每个迭代的结果。 这可用于指示：

* 哪些测试将包含在哪个迭代中。
* 多次迭代中重复显示的测试结果。
* 定期重复对基本功能进行优先级测试和测试。

**测试者**

在某一时刻，您可以分配适当的测试团队或特定的测试人员（可能取决于可用性和/或经验）。

**摘要或概述**

出于报告目的，您将需要提供测试结果的概述：

* 已覆盖测试的百分比。
* 成功/失败百分比。
* 与优先级测试相关的具体数字。
