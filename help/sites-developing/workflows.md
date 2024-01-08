---
title: 开发和扩展工作流
description: AEM提供了多种工具和资源，用于创建工作流模型、开发工作流步骤以及以编程方式与工作流交互
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 3%

---


# 开发和扩展工作流{#developing-and-extending-workflows}

AEM提供了多种工具和资源，用于创建工作流模型、开发工作流步骤，以及用于以编程方式与工作流交互。

借助工作流，您可以自动执行在AEM环境中管理资源和发布内容的流程。 工作流由一系列步骤组成，每个步骤都完成一个离散的任务。 您可以使用逻辑和运行时数据来确定流程何时可以继续，并从多个可能的步骤中选择下一个步骤。

例如，创建和发布网页的业务流程包括不同参与者的批准和签发任务。 这些流程可以使用AEM工作流建模并应用于特定内容。

下面介绍了主要方面，而以下页面介绍了更多详细信息：

* [创建工作流模型](/help/sites-developing/workflows-models.md)
* [扩展工作流功能](/help/sites-developing/workflows-customizing-extending.md)
* [以编程方式与工作流交互](/help/sites-developing/workflows-program-interaction.md)
* [工作流步骤参考](/help/sites-developing/workflows-step-ref.md)
* [工作流过程参考](/help/sites-developing/workflows-process-ref.md)
* [工作流最佳实践](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>有关以下内容的信息：
>
>* 参与工作流，请参阅 [使用工作流](/help/sites-authoring/workflows.md).
>* 管理工作流和工作流实例，请参阅 [管理工作流](/help/sites-administering/workflows.md).
>* 有关端到端的Community文章，请参阅 [使用Adobe Experience Manager工作流修改数字资源。](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html)
>* 请参阅 [“向AEM专家提问”工作流网络研讨会](https://communities.adobeconnect.com/p5s33iburd54/).
>* 对信息位置的更改请参阅 [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md) 和 [工作流最佳实践 — 位置](/help/sites-developing/workflows-best-practices.md#locations).
>

## 型号 {#model}

A `WorkflowModel` 表示工作流的定义（模型）。 它由以下部分组成 `WorkflowNodes` 和 `WorkflowTransitions`. 过渡连接节点并定义 *流量*. 模型始终具有开始节点和结束节点。

### 运行时模型 {#runtime-model}

工作流模型的版本已更新。 运行工作流实例时，它会使用和保留工作流的运行时模型（在工作流启动时可用）。

运行时模型为 [生成时间 **同步** 在工作流模型编辑器中触发](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

对发生的工作流模型、生成的运行时模型或两者进行编辑， *之后* 已启动的特定实例未应用于该实例。

>[!CAUTION]
>
>执行的步骤由 [运行时模型](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)，在生成 **同步** 操作在工作流模型编辑器中触发。
>
>如果在此时间点之后更改了工作流模型(不包括 **同步** 因此，运行时实例不会反映这些更改。 只有更新后生成的运行时模型才会反映这些更改。 例外情况是基础ECMA脚本，这些脚本仅保留一次，以便进行这些更改。

### 步骤 {#step}

每一步都完成一个离散的任务。 有不同类型的工作流步骤：

* 参与者（用户/组）：这些步骤将生成工作项并将其分配给用户或组。 用户必须完成工作项目才能推进工作流。
* 进程(脚本、Java™方法调用)：这些步骤由系统自动执行。 ECMA脚本或Java™类将实施该步骤。 可以开发服务来侦听特殊的工作流事件，并根据业务逻辑执行任务。
* 容器（子工作流）：此类型的步骤会启动另一个工作流模型。
* OR拆分/联接：使用逻辑来确定要在工作流中执行下一个步骤。
* AND拆分/连接：允许同时执行多个步骤。

所有步骤共享以下通用属性： `Autoadvance` 和 `Timeout` 警报（可脚本）。

### 过渡 {#transition}

A `WorkflowTransition` 表示两个对象之间的过渡 `WorkflowNodes` 的 `WorkflowModel`.

* 它定义了两个连续步骤之间的链接。
* 可以应用规则。

### 工作项 {#workitem}

A `WorkItem` 是通过 `Workflow` 实例 `WorkflowModel`. 它包含 `WorkflowData` 实例所执行的操作以及对 `WorkflowNode` 描述底层工作流步骤。

* 它用于识别任务，并放入相应的收件箱中。
* 工作流实例可以有一个或多个 `WorkItems` 同时（取决于工作流模型）。
* 此 `WorkItem` 引用工作流实例。
* 在存储库中， `WorkItem` 存储在工作流实例下方。

### 有效负荷 {#payload}

引用必须通过工作流进行高级处理的资源。

有效负载实施引用存储库中的资源（按路径、UUID或URL）或序列化Java™对象。 引用存储库中的资源是灵活的，并且Sling可带来高效率。 例如，引用的节点可以呈现为表单。

### 生命周期 {#lifecycle}

在启动新工作流（通过选择相应的工作流模型并定义有效负载）时创建，并在处理结束节点时结束。

可以对工作流实例执行以下操作：

* 终止
* 暂停
* 继续
* 重新启动

已完成的实例和已终止的实例将被存档。

### 收件箱 {#inbox}

每个用户帐户都有其自己的工作流收件箱，已在其中进行分配 `WorkItems` 可访问。

此 `WorkItems` 会直接分配给用户帐户或分配给其所属的组。

### 工作流类型 {#workflow-types}

工作流模型控制台中指明了各种类型的工作流：

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **默认**

  这些类型是标准AEM实例中包含的现成工作流。

* 自定义工作流（控制台中没有指示器）

  这些工作流是作为新工作流创建的，或从覆盖了自定义设置的现成工作流创建的。

* **旧版**

  在早期版本的AEM中创建的工作流。 这些工作流可在升级期间保留，或作为工作流包从以前的版本导出，然后导入到新版本中。

### 瞬态工作流 {#transient-workflows}

标准工作流在运行时保存运行时（历史记录）信息。 您还可以将工作流模型定义为 **瞬态** 以避免这样的历史继续存在。 此工作流用于性能调整，因为它节省了用于保存信息的时间和资源。

临时工作流可用于满足以下条件的任何工作流：

* 经常运行。
* 不需要工作流历史记录。

在加载许多资产时，引入了临时工作流，在这些资产中，资产信息非常重要，但工作流运行时历史记录并不重要。

>[!NOTE]
>
>请参阅 [创建临时工作流](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 以了解更多详细信息。

>[!CAUTION]
>
>当工作流模型标记为临时时，在少数情况下，运行时信息仍必须保留：
>
>* 有效负载类型（例如，视频）需要外部步骤进行处理；在这种情况下，需要运行时历史记录来确认状态。
>* 工作流输入 **AND拆分**. 在这种情况下，需要运行时历史记录才能确认状态。
>* 瞬态工作流进入参与者步骤后，会在运行时将模式更改为非瞬态模式。 由于任务将传递到个人，因此必须保留历史记录。
>

>[!CAUTION]
>
>在临时工作流中，您不应使用 **跳转步骤**.
>
>原因在于 **跳转步骤** 创建一个sling作业以在以下位置继续工作流： `goto` 点。 它否定了使工作流成为瞬态的目的，并在日志文件中生成错误。
>
>使用 **OR拆分** 在临时工作流中进行选择。

>[!NOTE]
>
>请参阅 [Assets最佳实践](/help/assets/performance-tuning-guidelines.md#transient-workflows) 有关临时工作流如何影响资产性能的更多信息。

### 多资源支持 {#multi-resource-support}

激活 **多资源支持** 对于工作流模型，这意味着即使选择多个资源，也会启动一个工作流实例。 每个组件都作为包附加。

如果 **多资源支持** 不会为您的工作流模型激活，并且已选择多个资源，然后为每个资源启动单个工作流实例。

>[!NOTE]
>
>请参阅 [为多资源支持配置工作流](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 以了解更多详细信息。

### 工作流暂存 {#workflow-stages}

工作流暂存有助于在处理任务时可视化工作流的进度。 它们可用于概述工作流完成处理的程度。 当工作流运行时，用户可以查看由描述的进度 **Stage** （相对于单个步骤）。

由于各个步骤名称可以是特定的和技术性的，因此可以定义阶段名称以提供工作流进度的概念性视图。

例如，对于包含六个步骤和四个阶段的工作流：

1. 您可以 [配置工作流暂存（显示工作流进度），然后将相应的暂存分配给工作流中的每个步骤](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress)：

   * 可以创建多个阶段名称。
   * 然后，为每个步骤分配单个阶段名称（可以为一个或多个步骤分配阶段名称）。

   | **步骤名称** | **阶段（分配给步骤）** |
   |---|---|
   | 步骤 1 | 创建 |
   | 步骤 2 | 创建 |
   | 步骤 3 | 审核 |
   | 步骤 4 | 批准 |
   | 步骤 5 | 完成 |
   | 步骤 6 | 完成 |

1. 运行工作流时，用户可以根据舞台名称（而不是步骤名称）查看进度。 工作流进度显示在中 [工作流项目的任务详细信息窗口的“工作流信息”选项卡](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 列于 [收件箱](/help/sites-authoring/inbox.md).

### 工作流和Forms {#workflows-and-forms}

通常，工作流用于处理AEM中的表单提交。 它可以与 [核心组件表单组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) 在标准AEM实例中可用，或者使用 [AEM Forms解决方案](/help/forms/using/aem-forms-workflow.md).

创建表单时，可以轻松将表单提交与工作流模型相关联。 例如，将内容存储在存储库的特定位置，或者通知用户表单提交及其内容。

### 工作流和翻译 {#workflows-and-translation}

工作流也是 [翻译](/help/sites-administering/translation.md) 进程。
