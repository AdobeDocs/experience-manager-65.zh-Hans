---
title: 资产测试的命名惯例
description: 存储库中的节点遵循Java内容存储库的命名约定。 但是，Adobe Experience Manager对资源节点的名称实施了进一步的约定。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 9%
---
# 资产测试的命名惯例{#naming-conventions-for-assets-testing}

存储库中的节点遵循[Java内容存储库](/help/sites-developing/the-basics.md#java-content-repository)的命名约定。 但是，Adobe Experience Manager对资源节点的名称实施了进一步的约定。

## 经典 UI {#classic-ui}

经典UI施加了更严格的限制：

* 当满足以下任一条件时验证显式节点名称的资源名称：

  * 提供了资产标题以转换为节点名称
  * 提供了显式节点名称

* 有效字符（从经典UI中创建资产时，只有这些字符实际有效）：

  * &#39;a&#39;到&#39;z&#39;
  * &#39;A&#39;到&#39;Z&#39;
  * &#39;0&#39;到&#39;9&#39;
  * _ （下划线）
  * `-` （短划线/减号）
