---
title: 创建配置Headless快速入门指南
description: 创建配置作为在AEM 6.5中开始使用Headless的第一步。
exl-id: f1df97a1-164f-4ed4-bb63-34caf35ae27c
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
source-wordcount: '296'
ht-degree: 68%
---
# 创建配置Headless快速入门指南 {#creating-configuration}

作为在AEM 6.5中开始使用Headless的第一步，您需要创建配置。

## 什么是配置？ {#what-is-a-configuration}

配置浏览器提供了通用配置 API、内容结构、针对 AEM 中配置的解析机制。

在 AEM 的 Headless 内容管理的上下文中，请将配置视为 AEM 中的工作区，您可以在其中创建内容模型，这将定义未来内容和内容片段的结构。 您可以使用多个配置来分隔这些模型。

>[!NOTE]
>
>如果您熟悉[全栈 AEM 实施中的页面模板](/help/sites-authoring/templates.md)，使用配置进行内容模型的管理的过程非常相似。

## 如何创建配置 {#how-to-create-a-configuration}

管理员只需要创建配置一次，或者在极少数情况下，需要新工作区用于组织内容模型时进行创建。 对于本指南快速入门，我们只需要创建一个配置。

1. 登录AEM，从主菜单选择&#x200B;**工具>常规>配置浏览器**。
1. 为您的配置提供&#x200B;**标题**。
   * 将根据标题自动生成名称，并根据[AEM命名约定](/help/sites-developing/naming-conventions.md)进行调整。它将成为存储库中的节点名称。
1. 查看以下选项：
   * **内容片段模型**
   * **GraphQL 持久查询**

   ![创建配置](assets/create-configuration.png)

1. 单击&#x200B;**创建**

如果需要，您可以创建多个配置。 配置也可以嵌套。

>[!NOTE]
>
>根据您的实施请求，可能还需要&#x200B;**内容片段模型**&#x200B;和 **GraphQL 持久查询**&#x200B;之外的配置选项。

## 后续步骤 {#next-steps}

使用此配置，您现在可以转到快速入门指南的第二部分并[创建内容片段模型](create-content-model.md)。

<!--
>[!TIP]
>
>For complete details about the Configuration Browser, [see the Configuration Browser documentation.](/help/sites-developing/configurations.md)
-->
