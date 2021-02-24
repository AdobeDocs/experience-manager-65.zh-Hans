---
title: 使用工作流处理资产
description: 资产处理功能，可转换格式、创建演绎版、管理资产、验证资产和运行工作流。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18e62f8fb46de20e1668b2dcdcedf68fe4622b50
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 3%

---


# 处理数字资产{#process-assets}

[!DNL Adobe Experience Manager Assets] 允许您通过多种方式处理数字资产，从而实现强大的资产处理。您可以使用默认或自定义的处理方法来确保端到端的业务流程完成、审核和合规性、发现和分发，以及数字资产的基本完整性。 您可以执行资产管理任务，同时实现所需的规模和自定义。

## 了解工作流{#understand-workflows}

对于资产处理，[!DNL Experience Manager]使用工作流。 工作流有助于实现业务逻辑或活动的自动化。 默认情况下，提供完成特定任务的细节步骤，开发人员可以创建自己的自定义步骤。 这些步骤可以按逻辑顺序组合，以创建工作流。 例如，工作流可以根据特定条件对上传的图像应用水印，例如上传到的文件夹、图像的分辨率等。 另一个示例是配置为水印和同时添加元数据、创建再现、添加智能标记和发布到数据存储的工作流。

## [!DNL Experience Manager] {#default-workflows}中可用的默认工作流

默认情况下，所有上传的资产均使用[!UICONTROL DAM更新资产]工作流进行处理。 该工作流会针对每个上传的资产执行，并实现基本的资产管理任务，如再现生成、元数据写回、页面提取、媒体提取和转码。

要查看默认情况下可用的各种工作流模型，请参阅[!DNL Experience Manager]中的&#x200B;**[!UICONTROL 工具>工作流>模型]**。

![部分默认工作流](assets/aem-default-workflows.png)

*图：中提供的部分默认工作流 [!DNL Experience Manager]。*

## 应用工作流以处理资产{#applying-workflows-to-assets}

将工作流应用于数字资产与对网站页面的操作相同。 有关如何创建和使用工作流的完整指南，请参阅[开始工作流](/help/sites-authoring/workflows-participating.md)。

使用数字资产中的工作流激活资产或创建水印。 资产的许多工作流会自动打开。 例如，编辑图像后自动创建演绎版的工作流将自动打开。

>[!NOTE]
>
>如果经典UI中的工作流在触屏优化UI中不可用，例如[!UICONTROL 请求激活]和[!UICONTROL 请求取消激活]，请参阅[建立工作流模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 将工作流应用于资产{#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
要将工作流应用于资产，请执行以下步骤：

1. 导航到您要为其开始工作流的资产所在的位置，然后单击资产以打开资产页面。 从菜单中选择&#x200B;**[!UICONTROL 时间轴]**&#x200B;以显示时间轴。

   ![时间轴–1](assets/timeline.png)

1. 单击底部的&#x200B;**[!UICONTROL 操作]**&#x200B;以打开资产可用操作的列表。

1. 单击列表中的&#x200B;**[!UICONTROL 开始工作流]**。

1. 在&#x200B;**[!UICONTROL 开始工作流]**&#x200B;对话框中，从列表中选择工作流模型。

1. （可选）指定可用于引用工作流实例的工作流的标题。

   ![选择工作流，提供标题并单击开始](assets/start-workflow.png)

1. 单击&#x200B;**[!UICONTROL 开始]**，然后单击&#x200B;**[!UICONTROL 继续]**。 工作流的每个步骤都会作为事件显示在时间轴中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 将工作流应用于多个资产{#applying-a-workflow-to-multiple-assets}

1. 从[!DNL Assets]控制台中，导航到您要为其开始工作流的资产所在的位置，然后选择资产。 从菜单中选择&#x200B;**[!UICONTROL 时间轴]**&#x200B;以显示时间轴。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 单击底部的&#x200B;**[!UICONTROL 动作]** ![向上](assets/do-not-localize/chevron-up-icon.png)。
1. 单击&#x200B;**[!UICONTROL 开始工作流]**。 在&#x200B;**[!UICONTROL 开始工作流]**&#x200B;对话框中，从列表中选择工作流模型。

   ![开始工作流](assets/start-workflow.png)

1. （可选）指定工作流的标题，可用于引用工作流实例。
1. 单击 **[!UICONTROL 开始]** ，然后在对话 **[!UICONTROL 框中单击确]** 认。 该工作流会在您选择的所有资产上运行。

## 将工作流应用到多个文件夹{#applying-a-workflow-to-multiple-folders}

将工作流应用到多个文件夹的过程与将工作流应用到多个资产的过程类似。 在[!DNL Assets]界面中选择文件夹，然后执行步骤[中将工作流应用到多个资产](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)的步骤2-7。

## 将工作流应用于集合{#applying-a-workflow-to-a-collection}

请参阅[对集合](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)应用工作流。

## 自动开始工作流以有条件地处理资产{#auto-execute-workflow-on-some-assets}

管理员可以将工作流配置为根据预定义的条件自动执行和处理资产。 此功能对于业务线用户和营销人员非常有用，例如，在特定文件夹上创建自定义工作流。 假设来自机构照片拍摄的所有资产都可以水印，或者可以处理由自由职业者上传的所有资产，以创建特定的演绎版。

对于工作流模型，用户可以创建执行该模型的工作流启动器。 工作流启动器监视内容存储库中的更改，并在满足预定义条件时执行工作流。 管理员可以向营销人员提供创建工作流和配置启动器的权限。 用户可以修改默认的[!UICONTROL DAM更新资产]工作流，以添加处理特定资产所需的额外步骤。 此工作流会对所有新上传的资产执行。 使用以下方法之一限制对特定资产执行额外步骤：

* 制作[!UICONTROL DAM更新资产]工作流的副本，并对其进行修改以在特定文件夹层次结构上执行。 此方法对于一些文件夹很有用。
* 额外的处理步骤可以使用[OR split](/help/sites-developing/workflows-step-ref.md#or-split)添加，如果条件适用于所需数量的文件夹。

## 最佳实践和限制{#best-practices-limitations-tips}

* 在设计工作流时，请考虑您对所有类型再现的需求。 如果您预计不会在将来需要再现，请从工作流中删除其创建步骤。 之后无法批量删除演绎版。 在延长使用[!DNL Experience Manager]后，不希望的再现可能会占用大量存储空间。 对于单个资产，您可以从用户界面中手动删除演绎版。 对于多个资产，您可以自定义[!DNL Experience Manager]以删除特定演绎版，或删除资产并再次上传这些资产。
* 默认情况下，[!UICONTROL DAM更新资产]工作流包括创建缩略图和Web演绎版的一些步骤。 如果从工作流中删除了任何默认演绎版，则[!DNL Assets]的用户界面无法正确呈现。

>[!MORELIKETHIS]
>
>* [应用并参与工作流](/help/sites-authoring/workflows.md)
>* [创建工作流模型并扩展工作流功能](/help/sites-developing/workflows.md)
>* [执行工作流的方法](/help/sites-administering/workflows-starting.md)
>* [工作流程最佳实践](/help/sites-developing/workflows-best-practices.md)

