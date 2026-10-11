---
title: 需要哪些测试环境？
description: 测试时应考虑多个环境
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: 05f7a513-5ee7-4870-a691-4a0602e0cbb2
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
source-wordcount: '169'
ht-degree: 5%
---
# 需要哪些测试环境？{#which-test-environments-will-be-needed}

要定义哪些配置用于测试，应考虑以下事项：

**开发** — 用于单元和某些集成测试。

**测试** — 用于大多数测试。

**实时** — 用于最终性能和压力测试。 此外，还要与客户进行验收测试。

确定您需要哪些实例以及在何处进行（通常对于所有级别的测试，每个实例至少一个）：

**作者** — 此实例允许作者输入和发布内容。

**发布** — 此实例以发布的形式展示网站，以供访客访问。

已通过Dispatcher测试。

最后，必须考虑实际的硬件 — 任何性能测试都应在尽可能接近最终实时环境的配置下在系统上进行。 因此，还建议将项目启动拆分为：

**软启动** — 降低了可用性；这允许在生产环境的实际条件下进行性能测试、调整和优化。

**硬启动** — 完全可用。
