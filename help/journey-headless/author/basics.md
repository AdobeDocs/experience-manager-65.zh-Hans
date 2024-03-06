---
title: 学习创作基础知识
description: 了解使用内容片段为 Headless CMS 创作内容的概念和机制。
exl-id: 125c4d0b-1572-4dba-823d-cdef2778f275
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 75%

---

# 使用 AEM 为 Headless 创作基本内容 {#author-headless-basics}

## 迄今为止的故事 {#story-so-far}

在 [AEM Headless 内容作者历程](overview.md)的开头，[简介](introduction.md)涵盖了与针对 Headless 进行创作相关的基本概念和术语。

本文基于这些内容编写，以便您了解如何为 AEM Headless 项目创作您自己的内容。

## 目标 {#objective}

* **受众**：初学者
* **目标**：介绍 Headless CMS 创作的基础知识：
   * 使用 AEMaaCS 进行创作简介
   * 内容片段简介

## 基本处理 {#basic-handling}

在您掌握内容片段之前，这里提供了有关如何使用 AEM 的（非常）简短的介绍....但没有什么能真正取代登录和尝试使用系统的体验。

### 创作和发布 {#author-preview-publish}

AEM 安装通常至少包含两个环境：

* 创作
* 发布

您登录并使用创作环境来生成您的内容。准备就绪后，您可以发布您的内容以使其公开可用。对于 Headless，这针对的是其他应用程序；对于网页，这针对的是网络上的读者。

有关更多详细信息，请参阅创作概念。

### 登录 {#signing-in}

与大多数系统一样，您必须登录。 作为作者，您将获得：

* 用户（帐户）名
* 密码
* 用于访问登录屏幕的链接

您的帐户将配置有您需要的任何权限。如果您有任何问题，Adobe 建议您联系您的内部项目支持团队。

### 导航 {#navigation}

首次登录时，简短的在线教程将重点介绍用户界面的一些主要功能。

之后，您可以使用导航面板访问 AEM 的关键区域。对于内容片段，您将使用 **资产控制台**.

要打开“导航”面板，请选择左上角的Adobe图标，然后按小指南针图标：

![“导航”面板](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>尽管内容片段是AEM的一项功能 **站点**，可在 **资产** 控制台。 这是一个技术细节，应该不会影响您，但了解它可能会有所帮助。

在控制台中，您可以选择文件夹以导航到您的内容片段，或选择痕迹导航（在标题中）以导航到备份树。

![痕迹导航](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### 操作、选择、查看 {#actions-selecting-viewing}

此 **资产** 控制台已专用 **操作工具栏**、和 **快速操作** 在选择资源（例如，文件夹或内容片段）后可以使用的区段。

快速操作适用于单个资源，请参阅 **巴塞尔** 在以下示例中：

![快速操作](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

操作工具栏提供对全部操作的访问权限 — 适用于当前方案。 可用的操作可能会发生更改；例如，根据您的位置或您是否已选择多个资源：

![操作工具栏](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

您可以使用视图选择器选择用于查看资源的格式：

![视图选择器](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

您可以使用边栏选择器查看有关项目的其他信息。 这样还可以访问其他操作。

![左边栏](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## 创作内容片段 {#authoring-content-fragments}

虽然这是对 AEM 用户界面 (UI) 的非常简要的介绍，但希望您有机会尝试一下。现在，我们开始探究您真正感兴趣的内容 – Headless 的内容片段。

我们必须从头到尾探究这些内容，但您的实例可能已创建文件夹和/或片段，并且它们可能位于不同的位置。准则是一样的。

### 编排和导航 {#organizing-and-navigating}

除非您的内容片段非常少，否则您将需要编排内容 - 以便您（和其他人）能够再次找到它们。

#### 创建文件夹 {#creating-folder}

为此，您可以在中创建一系列文件夹 **文件** 资产控制台的部分。 选择&#x200B;**创建**&#x200B;选项（右上角），然后选择&#x200B;**文件夹**：

![“创建文件夹”选项](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

随后将打开一个对话框，您可在其中输入详细信息，然后用&#x200B;**创建**&#x200B;进行确认：

![“创建文件夹”对话框](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### 使用路径和标记限制文件夹中可用的内容片段模型 {#tags-paths-for-models-in-folder}

此部分的内容略为深入一些。如果你只是从头开始尝试，你并不真的需要它，但当你有很多片段时，它最有用。 即使您尚未使用它，也建议您了解它。

您的内容架构师将创建您的当前项目以及其他一些项目所需的所有内容片段模型。为了帮助您和其他作者简化工作，您可以限制可用于特定文件夹的模型列表。

创建文件夹后，您可以打开文件夹&#x200B;**属性**。这里提供了各种选项卡，其中包含有关文件夹的信息和配置详细信息。具体而言，对于内容片段，您可以使用&#x200B;**策略**&#x200B;选项卡为此文件夹定义特定的路径和/或标记。这将限制可在文件夹中使用的内容片段模型，因为这意味着内容片段模型必须先满足这些要求，之后才能用于在此文件夹中生成片段。

![创建文件夹属性 – 策略](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>您可以参阅“内容片段模型”下的更多详细信息 - 允许 Assets 文件夹中的内容片段模型。

之后，您可以浏览这些文件夹以创建和编辑您的内容片段。

#### 以防万一 – 文件夹云服务配置 {#cloud-services-folder}

以防万一...

您可能会获得一个初始文件夹，可以在其中创建文件夹。这是因为必须将一些配置详细信息应用于根文件夹（此操作通常由开发人员或系统管理员执行）。您可能对此不感兴趣，但如果需要，您可以查看 **配置** 在 **Cloud Service** 文件夹的 **属性**：

![创建文件夹属性 – 配置](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>您可以参阅“将配置应用于 Assets 文件夹”下的更多信息。

### 创建内容片段 {#creating-fragment}

创建内容片段非常相似 — 您只需使用 **内容片段** 选项：

![“创建内容片段”选项](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

此时将打开向导。 第一步是选择片段将基于的内容片段模型：

![创建内容片段 — 选择模型](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

继续使用后 **下一个** 您可以提供详细信息(**基本** 和 **高级**)对于您的片段：

![创建内容片段 – 提供名称](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

确认 **创建** 然后你可以 **打开** 编辑器中的片段。

### 编辑片段 {#editing-fragment}

您可以在创建片段后立即打开它，也可以通过从资产控制台中选择它来打开片段。

在编辑器首次打开时，您将看到：

* 左侧的图标列表 – 可利用这些图标访问各种功能区域。编辑器在&#x200B;**变体**&#x200B;选项卡中打开，将在此处完成大部分编辑工作。您可能还对&#x200B;**批注**&#x200B;和&#x200B;**元数据**&#x200B;选项卡感兴趣。

* 包含有关片段的信息的标头，以及对各种操作的访问权限。

* 主要编辑区域，这取决于用于创建片段的模型。

例如：

* 只需要多条信息（其中一些信息具有特定类型）的片段。对于 Headless 内容，引用很重要，您将在历程的后面部分中了解相关信息。

  ![内容片段编辑器 – 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* 一个让您编写长段文本的片段。这里提供了用于管理文本并设置其格式的其他选项。您甚至可以在全屏编辑器中打开各个文本字段（使用右侧的类似小屏幕的图标）

  ![内容片段编辑器 – Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>可能需要项目特定的文档来帮助作者详细了解如何成功填写某些字段。
>
>有关一般详细信息，请参阅“内容片段模型 – 数据类型和属性”。

使用&#x200B;**保存**&#x200B;或&#x200B;**保存并关闭**&#x200B;来确认更新。

>[!NOTE]
>
>有关更多详细信息，您可以参阅“变体 – 创作内容片段”。

#### 您（可能）无需担心的事情 {#what-you-probably-do-not-need-to-worry-about}

好吧，这似乎是一个有点奇怪的部分，但在您打开内容片段编辑器并开始浏览之后，您将看到各种选项，它们（可能）不适用于您（作为内容作者）的 Headless 历程。因此，这只是一个快速提示，说明您应该能够在 Headless 上下文中忽略的内容：

* **内容片段模型**

  您将在编辑器顶部看到内容片段模型的名称 - 位于片段名称的正下方。这也是一个可将您转至模型编辑器的链接。
实际上，内容片段模型对您的内容片段至关重要，因为它们定义了您使用的结构。不过，创建和编辑这些模型（通常）是另一个角色（即内容架构师）的责任。

  >[!NOTE]
  >
  >如果您想了解详细信息，可以参阅“AEM Headless 内容架构师历程”。

* **关联的内容**

  这一点非常明显，因为它是编辑器中的一个选项卡。

  对于相当多的版本，内容片段已在 AEM 中提供。最初，它们在创作页面时可用于“传统”用途....并且它们仍在此上下文中使用。这可能涉及关联资产（例如图像），虽然这些资产未嵌入片段中，但在创作页面时，作者需要能够使用这些资产。

* **预览**

  这是编辑器中的另一个选项卡，它提供了技术视图，主要供开发人员使用。

* **更新页面引用**

  可从 **...**（省略号）下拉列表中执行此操作。Headless 作者对它并不感兴趣，因为它与页面创作有关。

### 发布 {#publishing}

<!-- needs more details -->

完成片段后，您可以&#x200B;**发布**&#x200B;它，以便 Headless 应用程序可使用它。

发布操作在编辑器中可用(或者从 **资产** 控制台)：

![内容片段编辑器 – 我的片段](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## 后续内容 {#whats-next}

现在您已了解基础知识，下一步是[了解引用](references.md)。这将介绍和讨论可用的各种引用，以及如何使用片段引用（针对 Headless 的创作的关键部分）创建结构层次。

## 其他资源 {#additional-resources}

* [创作概念](/help/sites-authoring/author.md)

* [基本处理](/help/sites-authoring/basic-handling.md) – 此页面主要基于&#x200B;**Sites**&#x200B;控制台，但许多/大多数功能也用于在 **Assets** 控制台下创作&#x200B;**内容片段**。

   * [“导航”面板](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [标头](/help/sites-authoring/basic-handling.md#the-header)

   * [操作工具栏](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)

   * [查看和选择资源](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [边栏选择器](/help/sites-authoring/basic-handling.md#rail-selector)

* [使用内容片段](/help/assets/content-fragments/content-fragments.md)

   * [管理内容片段](/help/assets/content-fragments/content-fragments-managing.md)

      * [将配置应用到 Assets 文件夹](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [创建内容片段](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [变体 - 创作片段内容](/help/assets/content-fragments/content-fragments-variations.md)

   * [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [内容片段模型 – 数据类型](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [内容片段模型 – 属性](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [内容片段模型 – 允许 Assets 文件夹中的内容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* 快速入门指南
   * [创建资源文件夹Headless快速入门指南](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Headless 内容架构师历程](/help/journey-headless/architect/overview.md)

* [AEM Headless 翻译历程](/help/journey-headless/translation/overview.md)
