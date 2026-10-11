---
title: 跟踪流程
description: 如何通过搜索进程并查看其详细信息来跟踪进程。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 381a46c6-c73c-476a-a1a0-20d921069c37
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%
---
# 跟踪流程 {#tracking-processes}

在“跟踪”页面上，您可以搜索已启动或参与的活动或已完成的流程，并查看流程详细信息。 流程详细信息显示属于流程一部分的任务、分配和表单。 您也可以使用之前启动的流程的表单数据启动新流程。

## 搜索流程和任务 {#search-for-processes-and-tasks}

您可以根据进程名称或使用AEM Forms工作区管理员设置的搜索模板来搜索进程实例和相关任务。

您可以设置要在搜索结果中显示的列。

>[!NOTE]
>
>搜索结果不包括出现在您有权访问的组或共享列表中的任务，除非您实际参与了任务。 结果不包括管理员清除的已完成进程实例。

### 按进程名称搜索 {#search-by-process-name}

1. 在“跟踪”页面的左侧窗格中，选择一个进程名称。 您为其启动或完成任务的所有进程实例都会显示在主窗格中。
1. 单击进程实例可查看有关该进程实例的详细信息。

### 使用搜索模板搜索任务 {#search-for-a-task-using-a-search-template}

1. 在“跟踪”页面的左侧列表中，选择&#x200B;**搜索模板**&#x200B;并选择搜索模板。
1. 如果模板支持搜索参数，则要缩小搜索参数，请填写模板字段，然后单击&#x200B;**搜索**。 显示您参与的所有符合搜索条件的任务的列表。

## 查看进程详细信息 {#view-process-details}

在跟踪页面上，您可以选择流程并查看其详细信息。 您可以根据各种参数搜索进程以查看任务详细信息。 对于有多个用户同时接收任务的流程，您还可以查看其状态选项卡，其中启用了文档审阅工具。

**状态：**&#x200B;单击任务时，进程中的任务状态将显示在“选定操作”列中。 但是，进程状态不可用。

1. 从搜索结果列表中选择流程实例，以查看属于流程实例一部分的任务的详细信息。
1. 要查看有关任务的详细信息，请执行以下一个或多个操作：

   * 要查看任务的注释和附件，请单击“附件”选项卡。
   * 要查看任务分配详细信息，请单击“分配”选项卡。
   * 要查看关联的表单，请单击表单按钮。
