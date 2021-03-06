---
title: 发布翻译后的内容
description: 了解如何在内容更新时发布翻译内容和更新翻译。
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---

# 发布翻译后的内容 {#publish-content}

了解如何在内容更新时发布翻译内容和更新翻译。

## 迄今为止的故事 {#story-so-far}

在AEM无头翻译历程的上一文档中， [翻译内容、](configure-connector.md) 您学习了如何使用AEM翻译项目来翻译无头内容。 您现在应该：

* 了解翻译项目是什么。
* 能够创建新的翻译项目。
* 使用翻译项目来翻译您的无头内容。

现在，您的初始翻译已完成，本文将引导您完成发布该内容的下一步，以及在语言根目录更改中的基础内容时如何更新您的翻译。

## 目标 {#objective}

本文档可帮助您了解如何在AEM中发布无标题内容，以及如何创建持续工作流以保持翻译处于最新状态。 阅读本文档后，您应：

* 了解AEM的创作 — 发布模型。
* 了解如何发布翻译后的内容。
* 能够为翻译内容实施持续更新模型。

## AEM创作 — 发布模型 {#author-publish}

在发布内容之前，最好了解AEM创作 — 发布模型。 按照简化的术语，AEM会将系统的用户分成两组。

1. 创建和管理内容和系统的用户
1. 从系统中使用内容的用户

因此，AEM将实际分为两个实例。

1. 的 **作者** 实例是内容作者和管理员创建和管理内容的系统。
1. 的 **发布** 实例是向用户交付内容的系统。

在创作实例上创建内容后，必须将其传输到发布实例，才能供使用。 从作者转移到发布的过程称为 **出版物**.

## 发布翻译内容 {#publishing}

一旦您对翻译内容的状态感到满意，就必须发布该内容，以便无头服务能够使用该内容。 此任务通常不由翻译专家负责，但此处记录了此任务以说明完整的工作流。

>[!NOTE]
>
>通常，翻译完成后，翻译专家会通知内容所有者翻译已准备好发布。 然后，内容所有者发布这些内容。
>
>为完整起见，提供了以下步骤。

发布翻译的最简单方法是导航到项目资产文件夹。

```text
/content/dam/<your-project>/
```

在此路径下，您拥有每个翻译语言的子文件夹，并可以选择要发布的。

1. 转到 **导航** -> **资产** -> **文件** 并打开项目文件夹。
1. 此处显示语言根文件夹和所有其他语言文件夹。 选择要发布的本地化语言。
   ![选择语言文件夹](assets/select-language-folder.png)
1. 点按或单击 **管理发布**.
1. 在 **管理发布** 窗口，确保 **发布** 在下自动选择 **操作** 和 **现在** 在下选择 **计划**. 单击或点按&#x200B;**下一步**。
   ![管理发布选项](assets/manage-publication-options.png)
1. 下一步 **管理发布** ，请确认已选择正确的路径。 点按或单击 **发布**.
   ![管理发布范围](assets/manage-publication-scope.png)
1. AEM会在屏幕顶部显示一条弹出消息，以确认发布操作。
   ![资源已发布的横幅](assets/resources-published-message.png)

您翻译的无标题内容现已发布！ 现在，您的无头服务可以访问并使用它。

>[!TIP]
>
>发布时，您可以选择多个项目（即多个语言文件夹），以便一次发布多个翻译。

发布内容时还有其他选项，例如计划发布时间，这些选项不在此历程的范围之内。 请参阅 [其他资源](#additional-resources) 文档末尾的部分以了解详细信息。

## 更新翻译的内容 {#updating-translations}

翻译很少是一次性的练习。 通常，初始翻译完成后，内容作者会继续在语言根目录中添加和修改内容。 这意味着您还需要更新翻译内容。

具体的项目要求定义您执行更新之前需要更新翻译的频率以及遵循的决策过程。 一旦您决定更新翻译，AEM中的过程将非常简单。 由于初始翻译基于翻译项目，因此任何更新也是如此。

但是，与之前一样，如果您选择自动创建翻译项目或手动创建翻译项目，则该过程会略有不同。

### 更新自动创建的翻译项目 {#updating-automatic-project}

1. 导航到 **导航** -> **资产** -> **文件**. 请记住，AEM中的无标题内容存储为称为内容片段的资产。
1. 选择项目的语言根。 在本例中，我们已选择 `/content/dam/wknd/en`.
1. 点按或单击边栏选择器，并显示 **引用** 的上界。
1. 点按或单击 **语言副本**.
1. 检查 **语言副本** 复选框。
1. 展开部分 **更新语言副本** 的双曲余切值。
1. 在 **项目** 下拉列表，选择 **添加到现有翻译项目**.
1. 在 **现有翻译项目** 下拉列表，选择为初始翻译创建的项目。
1. 点按或单击 **开始**.

![将项目添加到现有翻译项目](assets/add-to-existing-project.png)

内容会添加到现有翻译项目。 要查看翻译项目，请执行以下操作：

1. 导航到 **导航** -> **项目**.
1. 点按或单击您刚刚更新的项目。
1. 点按或单击您更新的语言之一。

您会看到新的工作卡会相应地添加到项目中。

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

您可能会注意到新信息卡中列出的统计信息（资产数量和内容片段数）不同。 这是因为AEM可识别自上次翻译后发生的更改，并且仅包含需要翻译的内容。 这包括对更新内容进行重新翻译，以及首次翻译新内容。

从此，你 [像原稿一样，开始并管理翻译作业。](translate-content.md#using-translation-project)

### 更新手动创建的翻译项目 {#updating-manual-project}

要更新翻译，您可以向现有项目添加新作业，该作业负责翻译更新的内容。

1. 导航到 **导航** -> **项目**.
1. 点按或单击您需要更新的项目。
1. 点按或单击 **添加** 按钮。
1. 在 **添加拼贴** 窗口，点按或单击 **翻译作业** 然后 **提交**.

   ![添加拼贴](assets/add-translation-job-tile.png)

1. 在新翻译作业的卡片上，点按或单击卡片顶部的V形按钮，然后选择 **更新Target** 定义新作业的目标语言。

   ![更新目标](assets/update-target.png)

1. 在 **选择目标语言** 对话框中，使用下拉菜单选择语言，然后点按或单击 **完成**.

   ![选择目标语言](assets/select-target-language.png)

1. 设置新翻译作业的目标语言后，点按或单击作业卡片底部的省略号按钮以查看作业的详细信息。
1. 首次创建时，作业为空。 通过点按或单击 **添加** 按钮和使用路径浏览器 [与最初创建翻译项目时一样。](translate-content.md##manually-creating)

>[!TIP]
>
>路径浏览器功能强大的过滤器对于仅查找已更新的内容同样非常有用。
>
>您可以在 [其他资源部分。](#additional-resources)

从此，你 [像原稿一样，开始并管理翻译作业。](translate-content.md#using-translation-project)

## 历程结束？ {#end-of-journey}

恭喜！ 您已完成无头翻译历程！ 您现在应该：

* 概述什么是无标题内容交付。
* 了解AEM的无头功能。
* 了解AEM翻译功能以及它们与无标题内容的相关性。
* 能够开始翻译您自己的无头内容。

现在，您可以在AEM中翻译自己的无头内容。 但是，AEM是一款功能强大的工具，还有许多其他选项可供使用。 请查看 [“其他资源”部分](#additional-resources) 以进一步了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [管理翻译项目](/help/sites-administering/tc-manage.md)  — 了解翻译项目和其他功能（如人文翻译工作流和多语言项目）的详细信息。
* [创作概念](/help/sites-authoring/author.md)  — 更详细地了解AEM的创作和发布模型。 本文档重点介绍页面创作，而不是内容片段，但该理论仍适用。
* [发布页面](/help/sites-authoring/publishing-pages.md)  — 了解发布内容时可用的其他功能。 本文档重点介绍页面创作，而不是内容片段，但该理论仍适用。
* [创作环境和工具](/help/sites-authoring/author-environment-tools.md##path-selection) - AEM提供了各种可用于组织和编辑内容的机制，包括强大的路径浏览器。
