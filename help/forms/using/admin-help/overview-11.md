---
title: 运行状况监视器概述
seo-title: 运行状况监视器概述
description: 本文档提供了运行状况监视器的概述以及有关如何访问该监视器的详细信息。
seo-description: 本文档提供了运行状况监视器的概述以及有关如何访问该监视器的详细信息。
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 运行状况监视器{#overview-of-health-monitor}概述

运行状况监视器提供有关AEM表单系统的关键信息，如服务器信息、内存使用情况和处理器使用情况。 还提供了Work Manager统计信息，例如队列中工作项或作业的数量及其状态。 您可以使用运行状况监视器执行以下任务：

* 验证您的系统是否正常运行
* 查看信息，帮助在系统问题发生时进行诊断
* 对显示问题的工作项或任务执行操作
* 从作业管理器数据库中清除过时的记录

管理控制台中的“运行状况监视器”页面有三个选项卡：

* “系统”选项卡显示资源监控图表和有关表单服务器（或群集环境中的节点）的信息。 （请参阅[查看系统信息](/help/forms/using/admin-help/view-system-information.md#view-system-information)。）
* “工作管理器”选项卡显示与“工作管理器”相关的数据，如“工作管理器”队列中的工作项数。 您可以使用各种标准筛选信息，或使用操作工具管理单个工作项。 （请参阅[查看与Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)相关的统计信息。）
* 通过“作业清除计划程序”选项卡，可以从作业管理器数据库中清除过时的记录。 （请参阅[从作业管理器数据库中清除记录](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。）

运行状况监视器网页中填充了通过Gemfire API收集的统计信息。 此API会自动发现群集中的所有节点。 它还解决了在从后台代理服务器或负载平衡器收集统计信息时发生的安全问题。 可以使用Java选项来微调运行状况监视器，从而降低对AEM表单环境性能的影响。 （请参阅[微调运行状况监视器性能](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)。）

**访问运行状况监视器**

1. 在管理控制台中，单击页面右上角的运行状况监视器。
