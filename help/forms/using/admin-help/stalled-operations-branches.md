---
title: 使用停止的操作和分支
seo-title: Working with stalled operations and branches
description: “停止的操作”页和“停止的分支”页显示已停止的进程。
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 使用停止的操作和分支 {#working-with-stalled-operations-and-branches}

“停止的操作”页和“停止的分支”页显示已停止的进程。 当执行操作期间或之后发生错误或由于进程中蓄意停止操作而导致错误时，进程可能会停止：

* 操作可能因意外错误而停止。 但是，进程中的Stall Branch操作会故意阻止进程进一步运行，并要求管理员介入。
* 在规则评估期间，分支可能会在操作之间停止运行。

当进程停止时，除非问题得到修复并重新启动操作或分支，否则将不再运行其他操作。

对于每个停止的项目，列表显示以下信息：

**操作名称或分支名称：** 操作或分支的名称。

**状态：** 对于已停止的项目，始终处于停止状态。

**错误：** 问题的简短描述。

**进程ID:** 工作流在实例化进程时分配的正整数（即，当用户或自动步骤启动进程时）。 您可以使用此标识符在流程实例的生命周期中跟踪该实例。

**进程名称 — 版本：** 在Workbench中分配的流程的名称。

**停止日期：** 操作或分支停止的日期和时间。

您可以在“停止的操作”或“停止的分支”页面上执行以下任务：

* 选择一个错误以查看有关该错误的详细信息。 选择错误时，将显示“错误详细信息”页面。
* 终止或重试停止的操作或重试停止的分支。

## 终止或重试停止的操作或分支 {#terminating-or-retrying-stalled-operations-or-branches}

在“停止的操作”页上，您可以终止显示的流程实例。

当您终止某个进程实例时，该实例将停止运行，并且不再执行其他操作。 通常，仅当进程因错误而被阻止或无法使用且无法修复和重新启动时，才终止该进程。

在“停止的操作”页或“停止的分支”页上，可以重试操作或分支。

重试操作时，将发送Forms工作流请求以重新启动操作。 如果导致进程停止的错误已修复且重试请求成功，则进程从停止点开始再次运行，其状态将变为“正在运行”。 如果无法重新启动该操作，则它仍保持STALLED状态，您可能需要终止该操作。

### 终止停止的操作 {#terminate-a-stalled-operation}

1. 在管理控制台中，单击服务>表单工作流>停止操作错误。
1. 在“停止的操作”页上，选择要终止的项目，然后单击终止。

### 重试停止的操作或分支 {#retry-a-stalled-operation-or-branch}

1. 在管理控制台中，单击“服务”>“表单工作流”，然后单击“停止操作错误”或“停止的分支错误”。
1. 在“停止的操作”或“停止的分支”页面上，选择要重试的项目，然后单击“重试”。

## 查看有关停止操作或分支的错误详细信息 {#viewing-error-details-about-stalled-operations-or-branches}

如果从“停止操作”或“停止的分支”页上的停止项目列表中选择错误，则会显示“错误详细信息”页，其中显示有关错误的详细信息，可帮助您解决问题。

页面底部的框包含错误信息。

您还可以从“错误详细信息”页中终止或重试停止的操作，并重试停止的分支。

## 当呈报用户不存在时，进程不会停止 {#process-does-not-stall-when-escalation-user-does-not-exist}

当将AEM Forms用户服务中的“分配任务”操作配置为在特定时间段后将任务呈报给其他用户，并且在“分配任务”操作执行后但在呈报发生之前删除呈报用户时，会发生错误。

出现这种情况时，流程和任务的状态在配置的升级时间不会更改，并且升级不会发生，但进程不会停止。 服务器日志中显示以下消息：

&quot;为呈报指定的主体对于taskID无效： *数字*，指定队列： *数字*.&quot;

如果在生成任务之前（在“分配任务”操作执行之前）删除呈报用户，则进程会停止或引发InvalidPrincipal异常事件。

为防止出现此问题，在删除用户时，请搜索属于该用户的任务并相应地处理这些任务。 (请参阅 [处理任务](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
