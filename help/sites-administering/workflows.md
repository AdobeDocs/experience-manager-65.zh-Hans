---
title: 管理工作流
seo-title: 管理工作流
description: 了解如何在AEM中管理工作流。
seo-description: 了解如何在AEM中管理工作流。
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 2%

---

# 管理工作流{#administering-workflows}

工作流可让您自动执行Adobe Experience Manager(AEM)活动。 工作流：

* 由一系列按特定顺序执行的步骤组成。

   * 每个步骤都执行不同的活动；例如等待用户输入、激活页面或发送电子邮件消息。

* 可以与存储库、用户帐户和AEM服务中的资产交互。
* 可以协调涉及AEM任何方面的复杂活动。

您的组织已建立的业务流程可以表示为工作流。 例如，发布网站内容的过程通常包括各利益相关方批准和注销等步骤。 这些流程可以作为AEM工作流实施，并应用于内容页面和资产。

* [启动工作流](/help/sites-administering/workflows-starting.md)
* [管理工作流实例](/help/sites-administering/workflows-administering.md)
* [管理对工作流的访问权限](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 应用和参与工作流：[使用工作流](/help/sites-authoring/workflows.md)。
>* 创建工作流模型和扩展工作流功能：[开发和扩展工作流](/help/sites-developing/workflows.md)。
>* 改进使用大量服务器资源的工作流的性能：[并发工作流处理](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing)。

>



## 工作流模型和实例{#workflow-models-and-instances}

[AEM中](/help/sites-developing/workflows.md#model) 的工作流模型是业务流程的表示和实现：

* 通常，它们会在页面或资产上执行操作，以获得特定结果。
* 这些页面和/或资产称为工作流有效负载。
* 工作流模型由执行特定任务的一系列步骤组成。
* 随着工作流的继续，负载会逐步传递。

启动（执行）工作流模型时，会创建工作流实例。 工作流模型可以多次启动，每次都会生成一个不同的工作流实例。 对于每个实例，将执行工作流模型定义的步骤。

>[!CAUTION]
>
>执行的步骤是工作流模型&#x200B;*在生成实例时定义的步骤*。 有关更多详细信息，请参阅[开发工作流](/help/sites-developing/workflows.md#model)。

工作流实例在以下生命周期内进行：

1. 将启动工作流模型，并创建并运行工作流实例。

   1. 启动模型时，将标识工作流实例的有效负荷。
   1. 实例实际上是模型的副本（与创建时一样）。
   1. AEM作者、管理员或服务可以启动工作流模型。

1. 将执行工作流模型的第一步。
1. 该步骤已完成，工作流引擎使用该模型来确定要执行的下一步。
1. 执行并完成工作流模型中的后续步骤。
1. 完成最后一步后，将完成工作流实例，从而将其存档。

AEM提供了许多有用的工作流模型。 此外，您组织中的开发人员可以创建自定义工作流模型，并根据您业务流程的特定需求进行定制。

## 工作流步骤{#workflow-steps}

执行工作流步骤时，这些步骤将与工作流实例关联。 工作流实例的历史记录包括有关为实例执行的每个步骤的信息。 此信息对于调查执行过程中出现的问题非常有用。

用户或服务会根据步骤的类型执行工作流步骤：

* 当用户执行步骤时，会为他们分配一个工作项目，该项目会放在其收件箱中。 用户负责手动完成该步骤，以便工作流实例继续运行。
* 当服务执行步骤时，工作流实例在完成后自动进入下一步。

>[!NOTE]
>
>如果发生错误，服务/步骤实施应处理错误情景的行为。 工作流引擎本身将重试该作业，然后记录错误并停止实例。

## 工作流状态和操作{#workflow-status-and-actions}

工作流可以具有以下状态之一：

* **正在运行**:工作流实例正在运行。
* **已完成**:工作流实例已成功结束。

* **已暂停**:将工作流标记为已暂停。但是，有关此状态的已知问题，请参阅下面的警告说明。
* **中止**:工作流实例已终止。
* **过时**:工作流实例的进度要求执行后台作业，但在系统中找不到该作业。执行工作流时出错时，可能会发生这种情况。

>[!NOTE]
>
>执行“流程步骤”会导致错误时，该步骤会显示在管理员的收件箱中，并且工作流状态为&#x200B;**RUNNING**。

根据当前状态，当您需要干预工作流实例的正常进程时，可以对运行工作流实例执行以下操作：

* **暂停**:暂停会将工作流状态更改为“已暂停”。请参阅下面的警告：

>[!CAUTION]
>
>将工作流状态标记为“暂停”存在已知问题。 在此状态下，可以对收件箱中暂停的工作流项目执行操作。

* **恢复**:在暂停的同一执行点使用相同的配置重新启动暂停的工作流。
* **终止**:结束工作流执行并将状态更改为 **ABORTED**。无法重新启动中止的工作流实例。
