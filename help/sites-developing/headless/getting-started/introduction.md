---
title: Headless快速入门指南
description: 通过本快速入门指南，了解Adobe Experience Manager (AEM) 6.5强大的Headless功能的基础知识，例如内容模型、内容片段和GraphQL API。
exl-id: 55ebd893-b3cc-47c5-ad84-46df984197fb
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
source-wordcount: '304'
ht-degree: 39%
---
# Headless快速入门指南 {#introduction}

Headless快速入门指南为已熟悉AEM和Headless技术的用户制定了五个步骤来创建、管理和交付使用Adobe Experience Manager (AEM) 6.5的体验的简单途径。 每份指南都建立在上一份指南的基础之上，因此建议按顺序仔细地研究这些内容。

1. [创建配置](create-configuration.md)
1. [创建内容片段模型](create-content-model.md)
1. [创建资产文件夹](create-assets-folder.md)
1. [创建内容片段](create-content-fragment.md)
1. [访问和交付内容片段](create-api-request.md)

>[!TIP]
>
>本快速入门指南假定您已了解 AEM 和 Headless 技术。
>
>如果您不熟悉AEM或Headless，请参阅[Headless文档历程](/help/journey-headless/overview.md)，获取Headless的端到端介绍以及AEM如何支持它。

## 受众 {#audience}

Headless快速入门指南中描述的任务对于AEM的Headless功能的基本端到端演示是必需的。 具有测试 AEM 实例管理员访问权限的任意用户可以按照这些指南来了解 AEM 中的 Headless 投放，但用户最好具有开发人员经验。

但是，在生产情况中，任务通常由不同角色执行不同的次数。 例如：

* **管理员**&#x200B;必须为内容设置初始配置和文件夹结构（通常只需设置一次或者在偶发的情况下进行设置）。
* **信息架构师**&#x200B;根据组织需求的演变添加新模型。
* **内容作者**&#x200B;会根据架构师定义的模型不断创建内容，以作为内容片段。

Headless快速入门指南指出了通常执行所述任务的人员以及执行频率。

## 后续步骤 {#next-step}

准备好了解详细信息？ 首先阅读Headless快速入门指南的第一部分： [创建配置。](create-configuration.md)
