---
title: 管理项目
seo-title: 管理项目
description: “项目”允许您通过将资源分组到一个实体中来组织项目，该实体可在“项目”控制台中进行访问和管理
seo-description: “项目”允许您通过将资源分组到一个实体中来组织项目，该实体可在“项目”控制台中进行访问和管理
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# 管理项目{#managing-projects}

通过“项目”，您可以将资源分组到一个实体中来组织项目。

在&#x200B;**项目**&#x200B;控制台中，您可以访问项目并对其执行操作：

![chlimage_1-255](assets/chlimage_1-255.png)

在“项目”中，您可以创建项目、将资源与项目关联，还可以删除项目或资源链接。您可能想要打开一个拼贴来查看其内容，以及向拼贴中添加一些项。本主题介绍了这些过程。

>[!NOTE]
>
>6.2 引入了将项目组织到文件夹中的功能。在“项目”页面上，您可以创建项目或文件夹。
>
>如果已创建某个文件夹，则会使用户转到该文件夹，用户可以在其中创建其他文件夹或项目。这有助于根据产品营销活动、位置、翻译语言等类别将项目组织到文件夹中。
>
>您可以在列表视图中查看项目和文件夹，也可以搜索项目和文件夹。

>[!CAUTION]
>
>For users in projects to see other users/groups while using Projects functionality like creating projects, creating tasks/workflows, seeing and managing the team, those users need to have read access on **/home/users** and **/home/groups**. The easiest way to implement this is to give the **projects-users** group read access to **/home/users** and **/home/groups**.

## 创建项目 {#creating-a-project}

AEM 提供了以下现成的模板，供您在创建项目时进行选择：

* 简单项目
* 媒体项目
* 产品照片拍摄项目
* 翻译项目

各种项目的创建过程都是相同的。各项目类型之间的不同之处在于可用的[用户角色](/help/sites-authoring/projects.md)和[工作流](/help/sites-authoring/projects-with-workflows.md)。要创建新项目，请执行以下操作：

1. 在&#x200B;**项目**&#x200B;中，点按/单击&#x200B;**创建**&#x200B;以打开&#x200B;**创建项目**&#x200B;向导：
1. 选择模板。Out of the box, Simple Project, Media Project, [Translation Project](/help/sites-administering/tc-manage.md), and [Product Photo Shoot Product](/help/sites-authoring/managing-product-information.md) are available and click **Next**.

   ![chlimage_1-256](assets/chlimage_1-256.png)

1. Define the **Title** and **Description** and add a **Thumbnail** image if required. 您还可以添加或删除用户以及他们所属的组。此外，也可单击&#x200B;**高级**&#x200B;以添加 URL 中使用的名称。

   ![chlimage_1-257](assets/chlimage_1-257.png)

1. 点按/单击&#x200B;**创建**。确认对话框会询问您是要打开新项目还是要返回到控制台。

### 将资源与项目关联 {#associating-resources-with-your-project}

由于项目使您能够将资源分组到一个实体中，因此您需要将资源关联到项目。这些资源称为&#x200B;**拼贴**。有关可添加的资源类型的说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

要将资源与项目关联，请执行以下操作：

1. 从&#x200B;**项目**&#x200B;控制台中打开您的项目。
1. 点按/单击&#x200B;**添加拼贴**，然后选择您要链接到项目的拼贴。您可以选择多种类型的拼贴。

   ![chlimage_1-258](assets/chlimage_1-258.png)

   >[!NOTE]
   >
   >有关可与项目关联的项目拼贴的详细说明，请参阅[项目拼贴](/help/sites-authoring/projects.md#project-tiles)。

1. 点按/单击&#x200B;**创建**。您的资源已链接到您的项目，从现在开始，您可以从您的项目访问该资源。

### 删除项目或资源链接 {#deleting-a-project-or-resource-link}

可使用同样的方法从控制台中删除项目或项目中的链接资源：

1. 导航到适当的位置：

   * 要删除项目，请转到&#x200B;**项目**&#x200B;控制台的顶层。
   * 要删除项目中的资源链接，请在&#x200B;**项目**&#x200B;控制台中打开相应的项目。

1. 单击&#x200B;**选择**&#x200B;并选择您的项目或资源链接，以进入选择模式。
1. 点按/单击&#x200B;**删除**。

1. 您需要在对话框中确认删除。确认后，将会删除项目或资源链接。点按/单击&#x200B;**取消选择**&#x200B;可退出选择模式。

>[!NOTE]
>
>在创建项目并将用户添加到各种角色时，将会自动创建与项目关联的组以管理关联的权限。例如，一个名为 Myproject 的项目将包含三个组，分别为 **Myproject 所有者**、**Myproject 编辑者**、**Myproject 观察者**。但是，如果删除该项目，这些组不会自动删除。管理员需要在&#x200B;**工具** > **安全** > **组**&#x200B;中手动删除这些组。

### 向拼贴中添加一些项 {#adding-items-to-a-tile}

在某些拼贴中，您可能想要添加多个项。例如，您可能会一次运行多个工作流或多个体验。

要向拼贴中添加一些项，请执行以下操作：

1. In **Projects**, navigate to the project and click the Add + icon on the tile you want to add an item to.

   ![chlimage_1-259](assets/chlimage_1-259.png)

1. 像创建新拼贴时一样，向拼贴中添加项。项目拼贴在[此处](/help/sites-authoring/projects.md#project-tiles)进行了介绍。在此示例中，添加了其他工作流。

   ![chlimage_1-260](assets/chlimage_1-260.png)

### 打开拼贴 {#opening-a-tile}

您可能想要查看当前拼贴中包含的各个项，或者修改或删除拼贴中的一些项。

要打开拼贴，以便查看其中的各个项或修改一些项，请执行以下操作：

1. 在“项目”控制台中，点按/单击省略号 (...)。

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. AEM 列出了该拼贴中的各个项。您可以进入选择模式来修改或删除一些项。

   ![chlimage_1-262](assets/chlimage_1-262.png)

## 查看项目统计信息 {#viewing-project-statistics}

要查看项目统计信息，请在&#x200B;**项目**&#x200B;控制台中单击&#x200B;**显示统计信息视图**。随即会显示每个项目的完成程度。Click **Show Statistics View** again to go to the **Projects** console.

![chlimage_1-263](assets/chlimage_1-263.png)

### 查看项目时间轴 {#viewing-a-project-timeline}

项目时间轴提供了项目中的资产上次使用时间的相关信息。To view the project timeline, click/tap **Timeline**, then enter selection mode and select the project. 资产会显示在左侧窗格中。Click/tap **Timeline** to return to the **Projects** console.

![chlimage_1-264](assets/chlimage_1-264.png)

### 查看活动/不活动的项目 {#viewing-active-inactive-projects}

To toggle between your active and inactive projects, in the **Projects** console, click **Toggle Active Projects**. 如果该图标旁边显示有复选标记，则显示的是活动的项目。

![chlimage_1-265](assets/chlimage_1-265.png)

如果该图标旁边显示有一个 x，则显示的是不活动的项目。

![chlimage_1-266](assets/chlimage_1-266.png)

## 将项目设为不活动或活动 {#making-projects-inactive-or-active}

如果您已完成项目，但仍希望保留有关该项目的信息，您可能需要将项目设为不活动。

要将项目设为不活动（或活动），请执行以下操作：

1. 在&#x200B;**项目**&#x200B;控制台中，打开您的项目，然后找到&#x200B;**项目信息**&#x200B;拼贴。

   >[!NOTE]
   如果该拼贴不在您的项目中，您可能需要添加它。请参阅[添加拼贴](#adding-items-to-a-tile)。

1. Tap/click **Edit**.
1. 将选择器从&#x200B;**活动**&#x200B;更改为&#x200B;**不活动**（反之亦然）。

   ![chlimage_1-267](assets/chlimage_1-267.png)

1. 点按/单击&#x200B;**完成**&#x200B;以保存更改。

