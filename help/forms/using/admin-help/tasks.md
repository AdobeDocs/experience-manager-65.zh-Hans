---
title: 处理任务
seo-title: 处理任务
description: 使用“任务搜索”页可按用户名或任务ID搜索任务。 了解有关处理任务的更多信息。
seo-description: 使用“任务搜索”页可按用户名或任务ID搜索任务。 了解有关处理任务的更多信息。
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# 处理任务{#working-with-tasks}

使用“任务搜索”页可按用户名或任务ID搜索任务。 搜索结果显示在“任务列表”页上，您可以在该页访问任务的历史记录。 如果用户的任务过多，或者用户收到错误的任务分配，您也可以重新分配任务。

>[!NOTE]
>
>执行任务搜索时，不会返回以数字符号(#)开头的用户名结果。 如果可能，请避免创建以数字符号开头的用户名。

## 搜索与用户{#search-for-tasks-associated-with-a-user}关联的任务

1. 在管理控制台中，单击服务>表单工作流>任务搜索。
1. 在搜索依据中，选择用户名。 如果您知道要搜索的部分用户名，请在框中键入。 单击“查找用户”。
1. 此时将显示“查找用户”页。 您可以通过按用户名或电子邮件进行搜索来进一步优化搜索。 找到要查找的用户后，选择该名称旁边的单选按钮，然后单击“确定”。
1. 默认情况下，任务搜索会查找当前分配给用户的任务。 要搜索之前分配给用户的任务，请选择显示未分配任务。 要搜索用户已完成的任务，请选择显示已完成的任务。
1. 单击搜索。 此时将显示“任务列表”页，其中列出了搜索结果。

## 在知道任务ID {#search-for-a-task-when-you-know-its-task-id}时搜索任务

1. 在管理控制台中，单击服务>表单工作流>任务搜索。
1. 在搜索依据中，选择任务ID并在框中键入任务ID。
1. 单击搜索。 此时将显示“任务列表”页，其中列出了搜索结果。

## 使用任务列表{#working-with-the-task-list}

任务搜索的结果显示在“任务列表”页上。 您可以选择任务以打开“任务历史记录”页。 从此处，您可以将任务分配给其他用户。

将显示包含以下信息的任务：

**任务ID:** 在实例化任务（由用户启动）后，工作流分配的正整数。您可以使用此标识符跟踪任务的生命周期。 单击任务ID可查看有关任务历史记录的详细信息，或将任务重新分配给其他用户。

**状态：** 已分配表示任务当前已分配给用户。“未分配”表示任务之前已分配给用户。 状态也可以是“已完成”。

**活动：** 显示初始操作或生成任务的流程操作的表单和名称。

**进程ID:** 在实例化进程时（即，当用户或自动步骤启动进程时），由表单工作流分配的此正整数。您可以使用此标识符在流程实例的生命周期中跟踪该实例。

**进程名称 — 版本：** 在Workbench中定义的进程名称。

**应用程序：** 流程所属的应用程序的名称，在Workbench中定义。

**创建日期：** 创建任务的日期和时间。

## 查看任务历史记录并重新分配任务{#viewing-task-history-and-reassigning-tasks}

“任务历史记录”页显示已分配给特定任务的用户和组的列表。

对于每个任务分配，列表会显示以下信息：

**名称：** 用户的名称。

**状态：** 已分配表示任务当前已分配给用户。“未分配”表示任务以前已分配给用户。

**工作列表ID:** 任务所属用户队列的数字标识符。一个进程可在多个用户之间共享。

**类型：** 指示如何分配任务：

**初始：** 最初为用户分配了任务。

**转发：** 原始任务所有者将任务分配给其他用户。

**拒绝：** 已转发的任务被拒绝或任务未完成而返回到工作列表。

**声明：** 用户在共享工作列表中声明了该任务。

**呈报：** 在未进行用户交互的情况下经过的预定时间（如Workbench中的“用户”操作中设置的），并且已为另一用户分配了任务。

**咨询：** 任务所有者已将此任务转发给其他用户，以供咨询，这些用户可以打开表单、保存数据、修改附件和注释，但无法完成该步骤。用户必须将任务返回给与用户协商的任务所有者。

**管理员重新分配：** 该任务已由管理员重新分配。

**分配日期：** 将任务分配给用户的日期和时间。

### 为任务{#assigning-a-new-user-to-a-task}分配新用户

“分配用户”页列出了可分配给任务的用户。 单击“任务历史记录”页上的“分配新用户”，即可访问“分配用户”页。

1. 在“分配用户”页面的“搜索对象”框中，键入部分或全部所需的用户名或电子邮件地址。
1. 在使用下，选择名称或电子邮件地址，然后单击查找。 将显示与搜索匹配的用户。
1. 从列表中选择用户，然后单击“确定”。 此时将显示“任务历史记录”页，其中包含新的用户分配。
