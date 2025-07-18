---
title: 管理工作流
description: 了解如何使用工作流自动化Adobe Experience Manager活动。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: f1eb41d08bb35adb93237f0ad09daa5bcd07fac8
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 2%

---

# 管理工作流{#administering-workflows}

借助工作流，您可以自动化Adobe Experience Manager (AEM)活动。 工作流程：

* 由一系列按特定顺序运行的步骤组成。

   * 每个步骤执行不同的活动；例如等待用户输入、激活页面或发送电子邮件。

* 可与存储库中的资源、用户帐户和AEM服务进行交互。
* 可以协调涉及AEM任何方面的复杂活动。

您的组织已建立的业务流程可以表示为工作流。 例如，发布网站内容的流程通常包括各个利益相关者的批准和签署等步骤。 这些流程可以作为AEM工作流实施并应用于内容页面和资源。

* [启动工作流](/help/sites-administering/workflows-starting.md)
* [管理工作流实例](/help/sites-administering/workflows-administering.md)
* [管理对工作流的访问权限](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 应用和参与工作流： [使用工作流](/help/sites-authoring/workflows.md)。
>* 创建工作流模型和扩展工作流功能： [开发和扩展工作流](/help/sites-developing/workflows.md)。
>* 提高使用重要服务器资源的工作流的性能： [并发工作流处理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)。
>

## 工作流模型和实例 {#workflow-models-and-instances}

AEM中的[工作流模型](/help/sites-developing/workflows.md#model)是业务进程的表示和实现：

* 通常，它们通过作用于页面或资产来实现特定结果。
* 这些页面和/或资产称为工作流有效负载。
* 工作流模型由一系列执行特定任务的步骤组成。
* 随着工作流的进行，有效负载会从一个步骤传递到另一个步骤。

启动（执行）工作流模型时，将创建工作流实例。 工作流模型可以多次启动，每次都生成一个不同的工作流实例。 对于每个实例，将执行工作流模型定义的步骤。

>[!CAUTION]
>
>执行的步骤是在生成实例时由工作流模型&#x200B;*定义的步骤*。 有关详细信息，请参阅[开发和扩展工作流 — 模型](/help/sites-developing/workflows.md#model)。

工作流实例在以下生命周期中进度：

1. 启动工作流模型，并创建并运行工作流实例。

   1. 模型启动时会识别工作流实例的有效负载。
   1. 实例实际上是模型的副本（在创建时）。
   1. AEM作者、管理员或服务可以启动工作流模型。

1. 执行工作流模型的第一步。
1. 该步骤已完成，工作流引擎使用模型确定要执行的下一步。
1. 工作流模型中的后续步骤将被执行和完成。
1. 完成最后一个步骤后，工作流实例即完成并存档。

AEM中提供了许多有用的工作流模型。 此外，您组织中的开发人员可以创建自定义工作流模型，根据业务流程的特定需求进行定制。

## 工作流步骤 {#workflow-steps}

执行工作流步骤时，这些步骤与工作流实例相关联。 工作流实例的历史记录包含有关已为该实例执行的每个步骤的信息。 此信息对于调查执行期间发生的问题很有用。

用户或服务会执行工作流步骤，具体取决于步骤的类型：

* 当用户执行步骤时，会为其分配一个位于收件箱中的工作项目。 用户负责手动完成该步骤，以便工作流实例继续执行。
* 当服务执行某个步骤时，工作流实例在完成时自动进入下一步。

>[!NOTE]
>
>如果发生错误，服务/步骤实施应处理错误场景的行为。 工作流引擎本身会重试作业，然后记录错误并停止实例。

## 工作流状态和操作 {#workflow-status-and-actions}

工作流可以具有以下状态之一：

* **正在运行**：工作流实例正在运行。
* **已完成**：工作流实例已成功结束。

* **已挂起**：将工作流标记为已挂起。 但是，有关这种状态的已知问题，请参阅下面的警告说明。
* **已中止**：工作流实例已终止。
* **过时**：工作流实例的进程需要执行后台作业，但在系统中找不到该作业。 当执行工作流时出现错误时，可能会发生此情况。

>[!NOTE]
>
>如果执行流程步骤导致错误，该步骤将显示在管理员收件箱中，工作流状态为&#x200B;**正在运行**。

当必须干预工作流实例的正常进程时，根据状态，可以对正在运行的工作流实例执行操作：

* **暂停**：暂停会将工作流状态更改为“已暂停”。 请参阅下面的注意事项：

>[!CAUTION]
>
>将工作流状态标记为“暂停”有一个已知问题。 在此状态下，可以对收件箱中暂停的工作流项目执行操作。

* **恢复**：使用相同的配置，在暂停的工作流的同一执行点重新启动暂停的工作流。
* **终止**：结束工作流执行并将状态更改为&#x200B;**已中止**。 无法重新启动已中止的工作流实例。
