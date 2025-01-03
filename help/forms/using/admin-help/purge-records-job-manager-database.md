---
title: 从作业管理器数据库中清除记录
description: 较大的流程数据可能会导致AEM表单性能降低。 当不再需要记录时，最好清除流程数据。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# 从作业管理器数据库中清除记录 {#purge-records-from-the-job-manager-database}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在调用长期进程时生成的进程数据可能会变得太大，从而导致AEM表单性能降低和使用不必要的磁盘空间。 当不再需要记录时，最好清除流程数据。

您可以使用管理控制台执行一次性清除过时记录或计划定期自动清除。 在[清除进程数据](/help/forms/using/admin-help/purging-process-data.md#purging-process-data)中讨论了清除过时记录的其他方法。

**访问“作业清除计划程序”页**

1. 在Administration Console中，单击页面右上角的运行状况监视器。
1. 单击“作业清除计划程序”选项卡。

有关当前已调度清除的信息将显示在“作业清除计划程序信息”框中。

>[!NOTE]
>
>单击“停止计划程序”可停止未来计划的任何清除，但不会停止正在进行的清除作业。

**计划一次性清除**

1. 仅选择一次。
1. 在“清除已完成的记录过滤器”区域中，指定在多少天或多少周之后记录将被视为过时并准备清除。

   >[!NOTE]
   >
   >与尚未完成的进程相关的记录不会被清除，即使这些记录早于指定的期限。

1. 指定何时进行清除。 选中使用当前日期和时间复选框，或清除此复选框，然后单击日历图标和时钟图标以指定执行清除的日期和时间。

   >[!NOTE]
   >
   >如果指定的开始日期和时间是过去的时间，则在单击“开始计划程序”后，清除会立即发生。

1. 单击“Start Scheduler（启动计划程序）”。 任何以前计划的计划程序设置都将替换为新设置。

**配置自动清除计划**

1. 选择重复间隔间隔时间，并指定两次清除间隔的天数或周数。
1. 在“清除已完成的记录过滤器”区域中，指定在多少天或多少周之后记录将被视为过时并准备清除。 不能将该值设置为`0`。

   >[!NOTE]
   >
   >与尚未完成的进程相关的记录不会被清除，即使这些记录早于指定的期限。

1. 指定清除的开始时间。 选中使用当前日期和时间复选框，或清除此复选框，然后单击日历图标和时钟图标以指定执行清除的日期和时间。

   >[!NOTE]
   >
   >如果指定的开始日期和时间是过去的时间，则AEM forms会根据指定的日期计算逻辑的下一个开始日期。 例如，如果安排从4月7日开始每周执行作业清除，现在为4月9日，则第一次清除发生在4月14日。

1. 单击“Start Scheduler（启动计划程序）”。 任何以前计划的计划程序设置都将替换为新设置。
