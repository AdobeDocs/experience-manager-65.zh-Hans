---
title: 流程报表中的预定义报表
seo-title: Pre-defined reports in Process Reporting
description: 查询JEE上的AEM Forms进程数据，以创建有关长时间运行的进程、进程持续时间和工作流卷的报告
seo-description: Query for AEM Forms on JEE process data to create reports on long running processes, Process duration, and Workflow volume
uuid: 704a8886-90ea-4793-a3fc-f998f878c928
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d93375e-ec37-4445-96ea-d315676787b4
docset: aem65
exl-id: 34e55676-6332-4616-aecc-bcc8cc1e8a29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 0%

---

# 流程报表中的预定义报表 {#pre-defined-reports-in-process-reporting}

## 流程报表中的预定义报表 {#pre-defined-reports-in-process-reporting-1}

AEM Forms Process Reporting提供了以下功能 *开箱即用* 报表：

* **[长时间运行的进程](#long-running-processes)**:一份报告，其中包含所有AEM Forms进程，这些进程需要超过指定时间才能完成
* **[流程持续时间图](#process-duration-report)**:按持续时间划分的指定AEM Forms进程的报告
* **[工作流卷](#workflow-volume-report)**:按日期列出的指定流程的已运行和已完成实例的报告

## 长时间运行的进程 {#long-running-processes}

“长时间运行的进程”报表显示完成的AEM Forms进程超过指定时间。

### 执行长时间运行的进程报告 {#to-execute-a-long-running-process-report}

1. 要在“流程报表”中查看预定义报表的列表，请在 **流程报告** 树视图，单击 **报表** 节点。
1. 单击 **长时间运行的进程** 报表节点。

   ![long_running_node](assets/long_running_node.png)

   当您选择报表时， **报表参数** 面板。

   ![长时间运行的进程报告参数面板](assets/report_parameters_panel.png)

   参数:

   * **持续时间** (*强制*):指定持续时间和时间单位。 显示运行时间超过指定持续时间的所有AEM Forms进程。
   * **开始时间** (*可选*):选择日期。 过滤报表以显示在指定日期之后开始的流程实例。
   * **开始时间之前** (*可选*):选择日期。 过滤报表以显示在指定日期之前开始的流程实例。

1. 单击 **开始** 执行报告。

   报表显示在 **报表** 面板 **流程报告** 窗口。

   ![long_running_processes](assets/long_running_processes.png)

   使用 **报表** 面板来执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报表
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报表导出并下载到以逗号分隔的文件

## 流程持续时间报表  {#process-duration-report}

“进程持续时间”报表按每个实例运行的天数显示Forms进程的实例数。

### 执行进程持续时间报告 {#to-execute-a-process-duration-report}

1. 要在流程报表中查看预定义的报表，请在 **流程报告** 树视图，单击 **报表** 节点。
1. 单击 **进程持续时间** 报表节点。

   ![process_duration_node](assets/process_duration_node.png)

   当您选择报表时， **报表参数** 面板。

   ![长时间运行的进程报告参数面板](assets/process_duration_params.png)

   参数:

   * **选择流程** (*强制*):选择AEM Forms进程。

1. 单击 **开始** 执行报告。

   报表显示在 **报表** 面板。

   ![process_duration_report](assets/process_duration_report.png)

   使用 **报表** 面板来执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报表
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报表导出并下载到以逗号分隔的文件

## 工作流量报表 {#workflow-volume-report}

“工作流量”报表按日历日显示AEM Forms进程当前运行和已完成的实例数。

### 执行工作流量报告 {#to-execute-a-workflow-volume-report}

1. 要在流程报表中查看预定义的报表，请在 **流程报告** 树视图，单击 **报表** 节点。
1. 单击 **工作流卷** 报表节点。

   ![workflow_volume_node](assets/workflow_volume_node.png)

   当您选择报表时， **报表参数** 面板。

   ![长时间运行的进程报告参数面板](assets/workflow_volume_params.png)

   参数:

   * **选择流程** (*强制*):选择AEM Forms进程。

   * **开始时间** (*可选*):选择日期。 过滤报表以显示在指定日期之后开始的流程实例。

   * **开始时间之前** (*可选*):选择日期。 过滤报表以显示在指定日期之前开始的流程实例。

1. 单击 **开始** 执行报告。

   报表显示在 **报表** 面板 **流程报告** 窗口。

   ![workflow_volume_report](assets/workflow_volume_report.png)

   使用 **报表** 面板来执行以下操作。

   * **刷新**:使用存储中的最新数据刷新报表
   * **更改图例颜色**:选择并更改报表图例的颜色
   * **导出到CSV**:将数据从报表导出并下载到以逗号分隔的文件
