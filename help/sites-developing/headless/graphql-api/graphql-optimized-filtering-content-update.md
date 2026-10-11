---
title: 更新内容片段以进行优化的 GraphQL 筛选
description: 了解如何在Adobe Experience Manager中为优化的GraphQL筛选更新内容片段，以便进行Headless内容交付。
exl-id: d78ec052-c091-49ca-9f36-a3d24eb9edd5
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
source-wordcount: '249'
ht-degree: 50%
---
# 更新内容片段以进行优化的 GraphQL 筛选 {#updating-content-fragments-for-optimized-graphql-filtering}

要优化 GraphQL 筛选的性能，可运行一个程序来更新内容片段。

>[!NOTE]
>
>更新内容片段后，可遵循[优化 GraphQL 查询](/help/sites-developing/headless/graphql-api/graphql-optimization.md)的建议。

## 前提条件 {#prerequisites}

确保您至少具有6.5.17.0版本的AEM。

## 更新内容片段 {#updating-content-fragments}

要运行该过程，请执行以下步骤：

1. [为&#x200B;**内容片段迁移作业配置**&#x200B;配置OSGi设置](/help/sites-deploying/configuring-osgi.md)：

   ![OSGi内容片段迁移作业配置](assets/cfm-graphql-update-01.png "OSGi内容片段迁移作业配置")

1. 在对话框中，按以下方式设置这两个参数：

   * **ContentFragmentMigration:Enabled** ： `1`
   * **ContentFragmentMigration:Enforce** ： `1`

1. **保存**&#x200B;规范 — 更新过程开始。

1. 请等待该过程完成。 当属性`cfGlobalVersion`出现在`/content/dam`上并且设置为`1`时，过程已完成。

1. 返回到OSGi配置以取消激活该过程。

   在&#x200B;**内容片段迁移作业配置**&#x200B;的对话框中，按以下方式设置这两个参数：

   * **ContentFragmentMigration:Enabled** ： `0`
   * **ContentFragmentMigration:Enforce** ： `0`

## 限制 {#limitations}

请注意以下限制：

* 只能在完全更新所有内容片段（由 JCR 节点 `/content/dam` 的 `cfGlobalVersion` 属性指示）后，才能优化 GraphQL 筛选器的性能

* 如果在运行更新过程后从包导入了内容片段（使用 `crx/de`），则直到再次执行更新过程后，才会在 GraphQL 查询结果中再次考虑这些内容片段。
