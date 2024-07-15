---
title: 参与工作流
description: 工作流通常包括需要人员对页面或资源执行活动的步骤。工作流选择用户或组来执行活动，并将工作项分配给该人员或组。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 39%

---

# 参与工作流{#participating-in-workflows}

工作流通常包括需要人员对页面或资源执行活动的步骤。工作流选择用户或组来执行活动，并将工作项分配给该人员或组。

## 处理您的工作项 {#processing-your-work-items}

您可以执行以下操作来处理工作项：

* **完成**

  您可以完成一个工作项，从而使工作流进入到下一步。

* **代理人**

  如果某个步骤已分配给您，但由于某种原因您无法采取操作，则您可以将该步骤委派给其他用户或组。

  可向其进行委派的用户取决于工作项分配到的对象：

   * 如果将工作项分配给某个组，则可以向该组的成员进行委派。
   * 如果将工作项分配给某个组，然后该组又将其委派给某个用户，则可以向该组的成员和该组进行委派。
   * 如果将工作项分配给单个用户，则不能委派工作项。

* **回退**

  如果您发现需要重复一个步骤或一系列步骤，您可以执行回退。这使您能够选择在工作流中先前发生的步骤以进行重新处理。 工作流会返回到您指定的步骤，然后从此处继续执行。

## 参与工作流 {#participating-in-a-workflow}

### 已分配工作流操作通知 {#notifications-of-assigned-workflow-actions}

为您分配了工作项（例如，**批准内容**）后，将显示各种警报和/或通知：

* 网站控制台的&#x200B;**状态**&#x200B;列指示页面何时处于工作流中：

  ![workflowstatus-1](assets/workflowstatus-1.png)

* 当您或您所属的组被指定为工作流的一部分时，该工作项将显示在AEM Workflow收件箱中。

  ![工作流收件箱](assets/workflowinbox.png)

### 完成参与者步骤 {#completing-a-participant-step}

执行指示的操作后，您可以完成工作项目，从而允许工作流继续。 请按下列步骤完成工作项目。

1. 选择工作流步骤，然后单击顶部导航栏中的&#x200B;**完成**&#x200B;按钮。
1. 在生成的对话框中，选择&#x200B;**下一步**；即下一步要执行的步骤。 下拉列表会显示所有相应的目标。 也可以输入&#x200B;**注释**。

   ![工作流完成](assets/workflowcomplete.png)

   列出的步骤数取决于工作流模型的设计。

1. 单击&#x200B;**确定**&#x200B;确认操作。

### 委派参与者步骤 {#delegating-a-participant-step}

请按下列步骤委派工作项目。

1. 单击顶部导航栏中的&#x200B;**委派**&#x200B;按钮。
1. 在对话框中，使用下拉列表选择要将工作项委派到的&#x200B;**用户**。 您还可以添加&#x200B;**评论**。

   ![workflowdelegate](assets/workflowdelegate.png)

1. 单击&#x200B;**确定**&#x200B;确认操作。

### 对参与者步骤执行回退 {#performing-step-back-on-a-participant-step}

请按下列步骤回退。

1. 单击顶部导航栏中的“回退”按钮。
1. 在生成的对话框中，选择“上一步”；即下一步要执行的步骤 — 即使该步骤出现在工作流的前面。 下拉列表会显示所有相应的目标。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 单击确定以确认操作。
