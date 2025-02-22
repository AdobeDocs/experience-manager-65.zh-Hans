---
title: 清除流程数据
description: 在调用长期进程时生成的进程数据可能会变得太大，从而导致AEM表单性能降低和使用不必要的磁盘空间。 了解如何清除流程数据。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# 清除流程数据 {#purging-process-data}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在调用长期进程时生成的进程数据可能会变得太大，从而导致AEM表单性能降低和使用不必要的磁盘空间。 当不再需要记录时，最好清除流程数据。 AEM forms提供了几种清除流程数据的方法：

* 您可以使用Administration Console执行一次性清除与长期进程相关的过时记录，或者计划定期自动清除。 （请参阅[清除作业管理器数据库中的记录](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)。）
* 您可以使用AEM表单Java API和Web服务API以编程方式清除与长期流程相关的流程数据。 (请参阅[使用AEM表单](https://www.adobe.com/go/learn_aemforms_programming_63)编程中的“清除进程数据”。)
* 使用流程清除工具，根据流程名称和其它参数清除流程。 有关详细信息，请参阅&#x200B;*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt中的进程清除工具自述文件。
