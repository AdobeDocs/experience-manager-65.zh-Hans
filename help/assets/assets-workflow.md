---
title: 使用工作流处理资源
description: 资源处理，用于转换格式、创建演绎版、管理资源、验证资源和运行工作流。
contentOwner: AG
feature: Workflow, Renditions
role: User, Admin
exl-id: e7c84385-efb3-4997-83ff-7a7f31582469
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 2%

---

# 处理数字资产 {#process-assets}

[!DNL Adobe Experience Manager Assets]允许您通过多种方式处理数字资产，以便稳健地处理资产。 您可以使用默认或自定义的处理方法来确保端到端业务流程的完成、审核和法规遵从性、发现和分发，以及数字资产的基本健全性。 您可以在实现所需的扩展和自定义的同时执行资源管理任务。

## 了解工作流 {#understand-workflows}

对于资产处理，[!DNL Experience Manager]使用工作流。 工作流有助于自动执行一个或多个业务逻辑。 默认情况下，提供了完成特定任务的精细步骤，开发人员可以创建自己的自定义步骤。 这些步骤可以按逻辑顺序组合以创建工作流。 例如，工作流可以根据特定条件对已上传的图像应用水印，例如将其上传到的文件夹、图像分辨率等。 另一个示例是配置为给元数据添加水印并同时添加元数据、创建演绎版、添加智能标记和发布到数据存储的工作流。

## [!DNL Experience Manager]中可用的默认工作流 {#default-workflows}

默认情况下，使用[!UICONTROL DAM更新资产]工作流处理所有上传的资产。 该工作流会为每个上传的资源执行，并完成基本资源管理任务，例如演绎版生成、元数据写回、页面提取、媒体提取和转码。

要查看默认可用的各种工作流模型，请参阅[!DNL Experience Manager]中的&#x200B;**[!UICONTROL 工具>工作流>模型]**。

![某些默认工作流](assets/aem-default-workflows.png)

*图： [!DNL Experience Manager].*&#x200B;中提供了某些默认工作流

## 应用工作流以处理资产 {#applying-workflows-to-assets}

将工作流应用于数字资产与应用于网站页面相同。 有关如何创建和使用工作流的完整指南，请参阅[启动工作流](/help/sites-authoring/workflows-participating.md)。

在数字资产中使用工作流来激活资产或创建水印。 资产的许多工作流都会自动打开。 例如，会自动打开在编辑图像后自动创建演绎版的工作流。

>[!NOTE]
>
>如果在经典UI中可用的工作流在启用了触屏的UI中不可用，例如[!UICONTROL 请求激活]和[!UICONTROL 请求停用]，请参阅[创建工作流模型](/help/sites-developing/workflows-models.md#classic2touchui)。

## 将工作流应用于资产 {#apply-a-workflow-to-an-asset}

<!-- 
TBD: Add animated GIF for these steps instead of all these screenshots.
-->
要将工作流应用于资产，请执行以下步骤：

1. 导航到要启动工作流的资产位置，然后单击该资产以打开资产页面。 从菜单中选择&#x200B;**[!UICONTROL 时间线]**&#x200B;以显示时间线。

   ![时间线–1](assets/timeline.png)

1. 单击底部的&#x200B;**[!UICONTROL 操作]**&#x200B;以打开可用于该资产的操作列表。

1. 单击列表中的&#x200B;**[!UICONTROL 启动工作流]**。

1. 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;对话框中，从列表中选择工作流模型。

1. （可选）指定可用于引用工作流实例的工作流标题。

   ![选择工作流，提供标题，然后单击“开始”](assets/start-workflow.png)

1. 单击&#x200B;**[!UICONTROL 开始]**，然后单击&#x200B;**[!UICONTROL 继续]**。 工作流的每个步骤都会作为事件显示在时间轴中。

   ![chlimage_1-256](assets/chlimage_1-52.png)

## 将工作流应用于多个资产 {#applying-a-workflow-to-multiple-assets}

1. 从[!DNL Assets]控制台中，导航到要启动工作流的资产位置，然后选择资产。 从菜单中选择&#x200B;**[!UICONTROL 时间线]**&#x200B;以显示时间线。

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. 单击底部的&#x200B;**[!UICONTROL 操作]** ![向上V形](assets/do-not-localize/chevron-up-icon.png)。
1. 单击&#x200B;**[!UICONTROL 启动工作流]**。 在&#x200B;**[!UICONTROL 启动工作流]**&#x200B;对话框中，从列表中选择工作流模型。

   ![启动工作流](assets/start-workflow.png)

1. （可选）指定工作流的标题，该标题可用于引用工作流实例。
1. 单击 **[!UICONTROL 开始]** ，然后在对话 **[!UICONTROL 框中单击确]** 认。 该工作流会在您选择的所有资产上运行。

## 将工作流应用于多个文件夹 {#applying-a-workflow-to-multiple-folders}

将工作流应用于多个文件夹的过程与将工作流应用于多个资产的过程类似。 在[!DNL Assets]界面中选择文件夹，然后执行[将工作流应用于多个资产](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets)过程的步骤2 - 7。

## 将工作流应用于收藏集 {#applying-a-workflow-to-a-collection}

请参阅[对收藏集](/help/assets/manage-collections.md#running-a-workflow-on-a-collection)应用工作流。

## 自动启动工作流以有条件地处理资产 {#auto-execute-workflow-on-some-assets}

管理员可以配置工作流以根据预定义条件自动执行和处理资源。 此功能对于业务线用户和营销人员非常有用，例如在特定文件夹上创建自定义工作流。 假设某个机构照片拍摄的所有资产都可以添加水印，或者自由职业者上传的所有资产都可以经过处理以创建特定演绎版。

对于工作流模型，用户可以创建用于执行该模型的工作流启动器。 工作流启动器监视内容存储库中的更改，并在满足预定义条件时执行工作流。 管理员可以向营销人员提供创建工作流和配置启动器的访问权限。 用户可以修改默认的[!UICONTROL DAM更新资产]工作流，以添加处理特定资产所需的额外步骤。 该工作流将在所有新上传的资源上执行。 使用以下方法之一来限制对特定资源执行额外的步骤：

* 创建[!UICONTROL DAM更新资产]工作流的副本，并修改该工作流以在特定文件夹层次结构上执行。 这种方法对于几个文件夹很有用。
* 可以使用[OR拆分](/help/sites-developing/workflows-step-ref.md#or-split)添加额外的处理步骤，因为根据需要有条件地适用于任意数量的文件夹。

## 最佳实践和限制 {#best-practices-limitations-tips}

* 在设计工作流时，请考虑您对所有类型的演绎版的需求。 如果您预计将来不需要节目，请从工作流中删除其创建步骤。 之后无法批量删除节目。 长时间使用[!DNL Experience Manager]后，不需要的演绎版可能会占用大量存储空间。 对于单个资源，您可以从用户界面手动删除演绎版。 对于多个资源，您可以自定义[!DNL Experience Manager]以删除特定演绎版，或删除这些资源并重新上传。
* 默认情况下，[!UICONTROL DAM更新资产]工作流包括创建缩略图和Web呈现的一些步骤。 如果从工作流中删除任何默认呈现版本，则[!DNL Assets]的用户界面无法正确呈现。

>[!MORELIKETHIS]
>
>* [申请并参与工作流](/help/sites-authoring/workflows.md)
>* [创建工作流模型并扩展工作流功能](/help/sites-developing/workflows.md)
>* [执行工作流的方法](/help/sites-administering/workflows-starting.md)
>* [工作流最佳实践](/help/sites-developing/workflows-best-practices.md)
