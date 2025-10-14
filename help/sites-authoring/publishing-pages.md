---
title: 发布内容页面
description: 了解如何在Adobe Experience Manager 6.5中发布内容页面。
exl-id: 61144bbe-6710-4cae-a63e-e708936ff360
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 2a843cefdd881e3cab60b2ddba12a26d0a498d13
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 64%

---

# 发布页面 {#publishing-pages}

在创作环境中创建并审阅内容后，[将其发布到公共网站](/help/sites-authoring/author.md#concept-of-authoring-and-publishing)（您的发布环境）。

这称为“发布页面”。当您要从发布环境中删除页面时，此过程称为“取消发布”。在发布和取消发布时，页面会保留在创作环境中以供进一步更改，直到将其删除为止。

您还可以立即发布/取消发布页面，或者在预定义的未来日期/时间发布/取消发布页面。

>[!NOTE]
>
>与发布相关的某些术语可能会混淆：
>
>* **发布/取消发布**
>  &#x200B;>  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
>  &#x200B;>  这两个术语与发布/取消发布同义。
>
>* **复制**
>  &#x200B;>  这些是技术术语，用于描述数据（例如页面内容、文件、代码、用户注释）从一个环境移动到另一个环境，例如发布或反向复制用户注释时。

## 权限不足 {#insufficient-privileges}

如果您没有必要的权限来发布特定页面：

* 将触发一个工作流，通知请求发布的适当人员。
* 您的开发团队可能已自定义此[工作流](/help/sites-developing/workflows-models.md#main-pars-procedure-6fe6)。
* 将显示一条简短的消息，通知您工作流已经触发。

## 发布页面 {#publishing-pages-1}

根据您所在的位置，可以通过下列方式发布：

* [从页面编辑器中](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)
* [从 Sites 控制台中](/help/sites-authoring/publishing-pages.md#publishing-from-the-console)

### 从编辑器中发布 {#publishing-from-the-editor}

如果您在编辑页面，则可以直接从编辑器中发布该页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开相应的菜单，然后选择&#x200B;**发布页面**&#x200B;选项。

   ![screen_shot_2018-03-21at152734](assets/screen_shot_2018-03-21at152734.png)

1. 根据页面是否包含需要发布的引用：

   * 如果不包含要发布的引用，则将直接发布页面。
   * 如果页面包含需要发布的引用，则将在&#x200B;**发布**&#x200B;向导中列出该内容，从该向导中可以：

      * 指定要与页面一起发布的资产或标记，然后使用&#x200B;**发布**&#x200B;完成该过程。

      * 使用&#x200B;**取消**&#x200B;中止操作。

   ![chlimage_1](assets/chlimage_1.png)

1. 选择&#x200B;**发布**&#x200B;会将页面复制到发布环境。在页面编辑器中，会显示一个确认发布操作的信息横幅。

   ![screen_shot_2018-03-21at152840](assets/screen_shot_2018-03-21at152840.png)

   当在控制台中查看同一页面时，将显示更新的发布状态。

   ![pp-01](assets/pp-01.png)

>[!NOTE]
>
>从编辑器中发布是一种简单的发布方式，即仅发布选定的一个或多个页面，而不发布任何子页面。

>[!NOTE]
>
>无法发布编辑器中按[别名](/help/sites-authoring/editing-page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 从控制台中发布 {#publishing-from-the-console}

Sites 控制台中有两个用于发布的选项：

* [快速发布](/help/sites-authoring/publishing-pages.md#quick-publish)
* [管理发布](/help/sites-authoring/publishing-pages.md#manage-publication)

#### 快速发布 {#quick-publish}

**快速发布**&#x200B;适用于一些简单的情况，可立即发布选定的页面，而无需进行任何进一步的交互。正因为这一点，任何未发布的引用也将被自动发布。

要使用“快速发布”发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**快速发布**&#x200B;按钮。

   ![pp-02](assets/pp-02.png)

1. 在“快速发布”对话框中，单击&#x200B;**发布**&#x200B;以确认发布，或单击&#x200B;**取消**&#x200B;以取消发布。 请记住，任何未发布的引用也将被自动发布。

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. 在发布页面时，将显示确认发布的警报。

>[!NOTE]
>
>“快速发布”是一种简单的发布方式，即只会发布选定的一个或多个页面，而不会发布任何子页面。

#### 管理发布 {#manage-publication}

与“快速发布”相比，**管理发布**&#x200B;提供了更多选项，允许包含子页面、自定义引用和启动任何适用的工作流，并且还提供了在以后的日期发布的选项。

要使用“管理发布”发布或取消发布页面，请执行以下操作：

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。

   ![pp-02-1](assets/pp-02-1.png)

1. 此时会启动&#x200B;**管理发布**&#x200B;向导。第一步，**选项**，让你：

   * 选择发布或取消发布选定的页面。
   * 选择立即还是在以后的日期执行该操作。

   稍后发布会启动一个在指定时间发布选定的一个或多个页面的工作流程。相反，稍后取消发布则会启动一个在指定时间取消发布选定的一个或多个页面的工作流程。

   如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-administering/workflows.md)以终止相应的工作流程。

   ![chlimage_1-2](assets/chlimage_1-2.png)

   单击&#x200B;**下一步**&#x200B;以继续。

1. 在“管理发布”向导的下一个步骤&#x200B;**范围**&#x200B;中，您可以定义发布/取消发布的范围，例如包括子页面和/或包括引用。

   ![screen_shot_2018-03-21at153354](assets/screen_shot_2018-03-21at153354.png)

   如果您因一时疏忽而忘记在启动“管理发布”向导之前选择某个页面，则可以使用&#x200B;**添加内容**&#x200B;按钮将其他页面添加到要发布的页面列表中。

   单击“添加内容”按钮会启动[路径浏览器](/help/sites-authoring/author-environment-tools.md#path-browser)以供选择内容。

   选择所需的页面，然后单击&#x200B;**选择**&#x200B;以将该内容添加到向导，或单击 **取消** 以取消所做的选择并返回到向导。

   返回到向导后，您可以在列表中选择一个项目以配置其进一步的选项，例如：

   * 包括其子项。
   * 将其从选定内容中删除。
   * 管理其已发布的引用。

   ![pp-03](assets/pp-03.png)

   单击&#x200B;**包括子项**&#x200B;会打开一个对话框，它允许您：

   * 仅包括下级子项.
   * 仅包括已修改的页面.
   * 仅包括已发布的页面.

   单击&#x200B;**添加**&#x200B;可根据选择的选项将子页面添加到要发布或取消发布的页面列表中。单击&#x200B;**取消**&#x200B;可取消所做的选择并返回到向导。

   ![chlimage_1-3](assets/chlimage_1-3.png)

   返回到向导后，您将看到根据您在“包括子项”对话框中选择的选项添加的页面。

   您可以通过选择页面，然后单击&#x200B;**已发布引用**&#x200B;按钮，来查看和修改该页面要发布或取消发布的引用。

   ![pp-04](assets/pp-04.png)

   **已发布引用**&#x200B;对话框将显示选定内容的引用。 默认情况下，这些引用全部处于选中状态并将进行发布/取消发布，但您可以取消选中以取消选中它们，以便将它们排除在操作之外。

   单击&#x200B;**完成**&#x200B;以保存更改，或单击&#x200B;**取消**&#x200B;以取消选择并返回向导。

   返回到向导后，**引用**&#x200B;列将进行相应的更新，以反映您选择的要发布或取消发布的引用。

   ![pp-05](assets/pp-05.png)

1. 单击&#x200B;**发布**&#x200B;以完成。

   返回到 Sites 控制台后，将显示一条确认发布的通知消息。

1. 如果发布的页面与工作流程相关联，则这些工作流程可能会显示在发布向导的最后一个步骤&#x200B;**工作流程**&#x200B;中。

   >[!NOTE]
   >
   >根据用户可能拥有也可能没有的权限，显示&#x200B;**工作流**&#x200B;步骤。
   >
   >有关详细信息，请参阅[权限不足](/help/sites-authoring/publishing-pages.md#insufficient-privileges)、[管理工作流的访问权限](/help/sites-administering/workflows-managing.md)和[将工作流应用到页面](/help/sites-authoring/workflows-applying.md#main-pars-text-5-bvhbkh-refd)。

   资源将按触发的工作流程分组，并且每组都提供了用于执行以下操作的选项：

   * 定义工作流程的标题。
   * 保留工作流包，前提是工作流具有[多资源支持](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)。
   * 在选择保留工作流程包的选项时，定义工作流程包的标题。

   单击&#x200B;**发布**&#x200B;或&#x200B;**稍后发布**&#x200B;以完成发布。

   ![chlimage_1-4](assets/chlimage_1-4.png)

>[!TIP]
>
>计划发布的内容会复制内容并遵循发布工作流程。 如果要临时隐藏已发布的内容而不取消发布，请考虑在页面属性中提供&#x200B;[**开始时间**&#x200B;和&#x200B;**结束时间**。](/help/sites-authoring/editing-page-properties.md#on-time)

## 取消发布页面 {#unpublishing-pages}

取消发布页面将从发布环境中删除该页面，以便不再将其提供给您的读者。

通过[与发布类似的方式](/help/sites-authoring/publishing-pages.md#publishing-pages)，可以取消发布一个或多个页面：

* [从页面编辑器中](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-editor)
* [从 Sites 控制台中](/help/sites-authoring/publishing-pages.md#unpublishing-from-the-console)

### 从编辑器中取消发布 {#unpublishing-from-the-editor}

在编辑页面时，如果您希望取消发布该页面，请选择&#x200B;**页面信息**&#x200B;菜单中的&#x200B;**取消发布页面**，这与[发布页面](/help/sites-authoring/publishing-pages.md#publishing-from-the-editor)非常类似。

>[!NOTE]
>
>无法取消发布编辑器中按[别名](/help/sites-authoring/editing-page-properties.md#advanced)处理的页面。编辑器中的发布选项仅适用于通过其实际路径访问的页面。

### 从控制台中取消发布 {#unpublishing-from-the-console}

正如[使用“管理发布”选项发布页面](/help/sites-authoring/publishing-pages.md#manage-publication)一样，也可以使用它来取消发布页面。

1. 在站点控制台中选择一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。在第一个步骤&#x200B;**选项**&#x200B;中，选择&#x200B;**取消发布**，而不是默认选项&#x200B;**发布**。

   ![chlimage_1-5](assets/chlimage_1-5.png)

   正如稍后发布会启动一个工作流程，以在指定时间发布此版本页面一样，稍后取消激活也会启动一个工作流程，以在指定时间取消发布选定的一个或多个页面。

   如果您要稍后撤消发布/取消发布页面，请转到[“工作流程”控制台](/help/sites-administering/workflows.md)以终止相应的工作流程。

1. 要完成取消发布，请按照与[发布页面](/help/sites-authoring/publishing-pages.md#manage-publication)类似的过程继续完成向导。

## 发布和取消发布树 {#publishing-and-unpublishing-a-tree}

如果输入或更新了大量内容页面（所有内容页面都位于同一根页面下），则可以更轻松地通过一个操作来发布整个树。

您可以使用 Sites 控制台上的[管理发布](/help/sites-authoring/publishing-pages.md#manage-publication)选项来完成此操作。

1. 在 Sites 控制台中，选择您希望发布或取消发布的树的根页面，然后选择&#x200B;**管理发布**。
1. 此时会启动&#x200B;**管理发布**&#x200B;向导。选择发布或取消发布以及应在何时开始，然后选择&#x200B;**下一步**&#x200B;以继续。
1. 在&#x200B;**范围**&#x200B;步骤中，选择根页面，然后选择&#x200B;**包括子项**。

   ![chlimage_1-6](assets/chlimage_1-6.png)

1. 在&#x200B;**包括子项**&#x200B;对话框中，取消选中以下选项：

   * 仅包括直接子项
   * 仅包括已发布的页面

   这些选项默认处于选中状态，因此您必须记得取消选择它们。 单击&#x200B;**添加**&#x200B;以确认并将内容添加到发布/取消发布。

   ![chlimage_1-7](assets/chlimage_1-7.png)

1. **管理发布**&#x200B;向导列出了树的内容以供审阅。 您可以通过添加其他页面或删除所选页面来进一步自定义选择。

   ![screen_shot_2018-03-21at154237](assets/screen_shot_2018-03-21at154237.png)

   请记住，您还可以通过&#x200B;**已发布引用**&#x200B;选项查看要发布的引用。

1. [继续正常的“管理发布”向导](#manage-publication)以完成发布或取消发布树的过程。

## 确定发布状态 {#determining-publication-status}

您可以确定页面的发布状态：

* 在[&#x200B; Sites 控制台上的资源概述信息](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)中

  ![screen-shot_2019-03-05at112019](assets/screen-shot_2019-03-05at112019.png)

  Sites 控制台的[信息卡](/help/sites-authoring/basic-handling.md#card-view)、[列](/help/sites-authoring/basic-handling.md#column-view)和[列表](/help/sites-authoring/basic-handling.md#list-view)视图中将显示发布状态。

* 在[时间线](/help/sites-authoring/basic-handling.md#timeline)中

  ![screen_shot_2018-03-21at154420](assets/screen_shot_2018-03-21at154420.png)

* 在[“页面信息”菜单](/help/sites-authoring/author-environment-tools.md#page-information)中（编辑页面时）

  ![screen_shot_2018-03-21at154456](assets/screen_shot_2018-03-21at154456.png)
