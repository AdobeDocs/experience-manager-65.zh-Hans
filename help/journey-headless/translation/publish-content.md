---
title: 发布翻译的内容
description: 了解如何发布翻译的内容并在该内容更新时更新翻译。
exl-id: 32c387fe-fa1b-499b-861f-b4822f5e139e
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 80%

---

# 发布翻译的内容 {#publish-content}

了解如何发布翻译的内容并在该内容更新时更新翻译。

## 迄今为止的故事 {#story-so-far}

在 AEM Headless 翻译历程的上一个文档[翻译内容](configure-connector.md)中，您已了解如何使用 AEM 翻译项目来翻译 Headless 内容。您现在应：

* 了解什么是翻译项目。
* 能够创建翻译项目。
* 使用翻译项目来翻译 Headless 内容。

现在，您的初始翻译已完成，本文将引导您完成该内容的发布流程的下一步，以及如何在语言根中的基础内容发生更改时更新您的翻译。

## 目标 {#objective}

本文档可帮助您了解如何在 AEM 中发布 Headless 内容以及如何创建持续工作流以使您的翻译保持最新。阅读本文档后，您应：

* 了解 AEM 的创作-发布模型。
* 了解如何发布翻译的内容。
* 能够为翻译的内容实施持续更新模型。

## AEM 的创作-发布模型 {#author-publish}

在发布内容之前，最好是了解 AEM 的创作-发布模型。简而言之，AEM 将系统用户分成了两个组。

1. 创建和管理内容与系统的用户
1. 使用系统中的内容的用户

因此，AEM 实际分为两个实例。

1. **作者**&#x200B;实例是内容作者和管理员用于创建和管理内容的系统。
1. **发布**&#x200B;实例是将内容交付给使用者的系统。

在创作实例上创建内容后，必须将内容传输到发布实例以供使用。从创作传输到发布的过程称作&#x200B;**发布**。

## 发布翻译的内容 {#publishing}

在您对翻译的内容的状态感到满意后，必须发布此内容以供 Headless 服务使用。此任务不是翻译专家的责任，此处记录它是为了说明完整的工作流。

>[!NOTE]
>
>通常，在翻译完成后，翻译专家会告知内容所有者翻译已可供发布。随后，内容所有者将发布翻译。
>
>为了完整起见，提供了以下步骤。

发布翻译的最简单方法是导航到项目资源文件夹。

```text
/content/dam/<your-project>/
```

此路径下提供了每种翻译语言的子文件夹，并且您可以选择要发布的语言。

1. 转到&#x200B;**导航** > **资源** > **文件**，然后打开项目文件夹。
1. 您将在此处看到语言根文件夹和所有其他语言文件夹。选择您希望发布的一种或多种本地化语言。
   ![选择语言文件夹](assets/select-language-folder.png)
1. 单击&#x200B;**管理发布**。
1. 在&#x200B;**管理发布**&#x200B;窗口中，确保自动在&#x200B;**操作**&#x200B;下选中&#x200B;**发布**，并在&#x200B;**计划**&#x200B;下自动选中&#x200B;**现在**。单击&#x200B;**下一步**。
   ![管理发布选项](assets/manage-publication-options.png)
1. 在下一个&#x200B;**管理发布**&#x200B;窗口中，确认已选择一条或多条适当的路径。单击&#x200B;**发布**。
   ![管理发布范围](assets/manage-publication-scope.png)
1. AEM通过屏幕顶部的弹出消息确认发布操作。
   ![资源发布横幅](assets/resources-published-message.png)

您的翻译的 Headless 内容现已发布！它现在可以由 Headless 服务访问和使用。

>[!TIP]
>
>您可以在发布时选择多个项目（即多个语言文件夹），以便一次性发布多个翻译。

发布内容时还有其他选项（例如，计划发布时间），它们超出了此历程的范围。有关更多信息，请参阅本文档末尾的[其他资源](#additional-resources)部分。

## 更新翻译的内容 {#updating-translations}

翻译很少是一次性活动。通常，您的内容作者会在初始翻译完成后继续在语言根中添加和修改您的内容。这意味着您还必须更新翻译的内容。

具体的项目要求定义了翻译的更新频率，以及在执行更新之前需遵循的决策流程。 在您决定更新翻译后，AEM中的流程就会变得非常简单。 由于初始翻译是基于翻译项目的，因此任何更新也是如此。

但是和以前一样，如果您选择自动创建翻译项目或手动创建翻译项目，则流程会略有不同。

### 更新自动创建的翻译项目 {#updating-automatic-project}

1. 导航到&#x200B;**导航** > **资源** > **文件**。请记住，AEM 中的 Headless 内容将存储为称作内容片段的资源。
1. 选择项目的语言根。在这种情况下，已选择`/content/dam/wknd/en`。
1. 单击边栏选择器并显示&#x200B;**引用**&#x200B;面板。
1. 单击&#x200B;**语言副本**。
1. 选中&#x200B;**语言副本**&#x200B;复选框。
1. 展开“引用”面板底部的&#x200B;**更新语言副本**&#x200B;部分。
1. 在&#x200B;**项目**&#x200B;下拉列表中，选择&#x200B;**添加到现有翻译项目**。
1. 在&#x200B;**现有翻译项目**&#x200B;下拉列表中，选择为初始翻译创建的项目。
1. 单击&#x200B;**开始**。

![将项目添加到现有翻译项目](assets/add-to-existing-project.png)

内容将添加到现有翻译项目中。要查看翻译项目，请执行以下操作：

1. 导航到&#x200B;**导航** > **项目**。
1. 单击刚刚更新的项目。
1. 单击该语言或已更新的某种语言。

您会看到新作业信息卡已根据需要添加到项目中。

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

您可能会发现，新信息卡上列出的统计数据（资源和内容片段数量）有所不同。这是因为 AEM 识别自上次翻译以来发生变化的内容，并且仅包括必须翻译的内容。这包括已更新内容的重新翻译以及新内容的首次翻译。

从此时起，您可以[像处理初始翻译一样启动和管理您的翻译作业。](translate-content.md#using-translation-project)

### 更新手动创建的翻译项目 {#updating-manual-project}

要更新翻译，您可以将新作业添加到负责翻译已更新内容的现有项目中。

1. 导航到&#x200B;**导航** > **项目**。
1. 单击必须更新的项目。
1. 单击窗口顶部的&#x200B;**添加**&#x200B;按钮。
1. 在&#x200B;**添加拼贴**&#x200B;窗口中，单击&#x200B;**翻译作业**，然后单击&#x200B;**提交**。

   ![添加拼贴](assets/add-translation-job-tile.png)

1. 在新翻译作业的信息卡上，单击信息卡顶部的>形按钮，然后选择&#x200B;**更新目标**&#x200B;以定义新作业的目标语言。

   ![更新目标](assets/update-target.png)

1. 在&#x200B;**选择目标语言**&#x200B;对话框中，使用下拉列表选择语言，然后单击&#x200B;**完成**。

   ![选择目标语言](assets/select-target-language.png)

1. 设置新翻译作业的目标语言后，单击作业信息卡底部的省略号按钮以查看作业的详细信息。
1. 作业在首次创建时为空。通过点按或单击&#x200B;**添加**&#x200B;按钮并使用路径浏览器将内容添加到作业，[就像您最初创建翻译项目时所做的那样。](translate-content.md#manually-creating)

>[!TIP]
>
>路径浏览器的功能强大的过滤器在查找已更新的内容时同样有用。
>
>可在[其他资源](#additional-resources)部分中详细了解路径浏览器。

从此时起，您可以[像处理初始翻译一样启动和管理您的翻译作业。](translate-content.md#using-translation-project)

## 历程结束？ {#end-of-journey}

恭喜！您已完成 Headless 翻译历程！您现在应：

* 大致了解 Headless 内容交付的含义。
* 基本了解 AEM 的 Headless 功能。
* 了解 AEM 的翻译功能以及它们如何与 Headless 内容相关联。
* 能够开始翻译您自己的 Headless 内容。

您现在可以在 AEM 中翻译您自己的 Headless 内容了。不过，AEM 是一个功能强大的工具，并且提供了许多其他选项。查看[“其他资源”部分](#additional-resources)中的一些其他资源，详细了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [管理翻译项目](/help/sites-administering/tc-manage.md) – 了解翻译项目的详细信息以及人工翻译工作流和多语言项目等附加功能。
* [创作概念](/help/sites-authoring/author.md) – 更详细地了解 AEM 的创作和发布模型。 虽然本文档侧重于创作页面而非内容片段，但该理论仍然适用。
* [发布页面](/help/sites-authoring/publishing-pages.md) – 了解发布内容时可用的附加功能。虽然本文档侧重于创作页面而非内容片段，但该理论仍然适用。
* [创作环境和工具](/help/sites-authoring/author-environment-tools.md#path-selection) – AEM 提供各种机制来组织和编辑您的内容，包括强大的路径浏览器。
