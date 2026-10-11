---
title: 创建内容片段Headless快速入门指南
description: 了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
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
source-wordcount: '378'
ht-degree: 73%
---
# 创建内容片段Headless快速入门指南 {#creating-content-fragments}

了解如何使用 AEM 的内容片段设计、创建、管理和使用独立于页面的内容，用于 Headless 投放。

## 什么是内容片段？ {#what-are-content-fragments}

[现在您已经创建了资源文件夹](create-assets-folder.md)，可以在其中存储您的内容片段，接下来可以创建片段！

内容片段允许您设计、创建、管理和发布独立于页面的内容。 利用这些功能，可准备内容以用于多个位置和多个渠道。

内容片段包含结构化内容，可以采用 JSON 格式投放。

## 如何创建内容片段 {#how-to-create-a-content-fragment}

内容作者将创建任意数量的内容片段，用于呈现他们创建的内容。 这将是他们在 AEM 中的主要任务。 对于本指南快速入门，我们只需要创建一个。

1. 登录AEM，从主菜单选择&#x200B;**导航> Assets**。
1. 导航到您之前创建的[文件夹。](create-assets-folder.md)
1. 单击&#x200B;**创建>内容片段**。
1. 内容片段的创建以两步向导的方式呈现。 首先选择要使用哪种模型来创建内容片段，然后单击&#x200B;**下一步**。
   * 可用的模型取决于&#x200B;[**您为资源文件夹定义的云配置**](create-assets-folder.md)，您将在该文件夹中创建内容片段。
   * 如果您收到消息 `We could not find any models`，请检查资源文件夹的配置。

   ![选择内容片段模型](assets/content-fragment-model-select.png)
1. 根据需要提供&#x200B;**标题**、**描述**&#x200B;和&#x200B;**标记**，然后单击&#x200B;**创建**。

   ![创建内容片段](assets/content-fragment-create.png)
1. 在确认窗口中单击&#x200B;**打开**。

   ![内容片段创建确认](assets/content-fragment-confirmation.png)
1. 在内容片段编辑器中提供内容片段的详细信息。

   ![内容片段编辑器](assets/content-fragment-edit.png)
1. 单击&#x200B;**保存**&#x200B;或&#x200B;**保存并关闭**。

内容片段可以引用其他内容片段，在需要时允许嵌套内容结构。

内容片段还可以引用 AEM 中的其他资源。 [这些资源需要存储在 AEM 中](/help/assets/manage-assets.md)，然后才能创建引用内容片段。

## 后续步骤 {#next-steps}

现在您已经创建了内容片段，接下来可以转到快速入门指南的最后一个部分并[创建 API 请求来访问和提供内容片段。](create-api-request.md)

>[!TIP]
>
>有关管理内容片段的完整详细信息，请参阅[内容片段文档](/help/assets/content-fragments/content-fragments.md)
