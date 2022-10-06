---
title: 流程报表的工作原理
seo-title: How Process Reporting Works
description: JEE流程报表中构成AEM Forms的服务描述以及流程报表UI简介
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# 流程报表的工作原理 {#how-process-reporting-works}

“流程报告”是AEM Forms JEE上的报告模块。

“流程报表”允许您对AEM Forms流程和任务运行报表。

“流程报表”使用嵌入的“流程报表”存储库发布Forms数据。 然后，它使用该数据来运行报表。

Process Reporting包含以下模块：

* [ProcessDataPublisher服务](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage服务](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi服务](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [查询数据Servlet](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [流程报表用户界面](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## 流程报告架构 {#process-reporting-architecture-br}

![处理报告架构](assets/processreportingarchitecture.png)

## 流程报告模块 {#process-reporting-modules}

### ProcessDataPublisher服务 {#processdatapublisher-service-br}

ProcessDataPublisher服务器在AEM Forms数据库上定期运行，并提取自上次运行服务以来更改的数据。 然后，它会将数据发布到进程数据存储服务。

有关配置服务的详细信息，请参阅 [配置ProcessDataPublisher服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### ProcessDataStorageProvider服务 {#processdatastorageprovider-service-br}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收进程数据，并将数据保存到Process Reporting存储库。

有关配置服务的详细信息，请参阅 [配置ProcessDataStorageProvider服务](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### OSGi服务 {#osgi-service-br}

QueryDataServlet使用此服务从Process Reporting存储库获取报表数据。

### QueryDataServlet服务 {#querydataservlet-service-br}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获取相关的报告数据，处理该数据，并将该数据返回到用户界面。

### 流程报表用户界面 {#process-reporting-user-interface-br}

“流程报表”用户界面是基于Web浏览器的界面。 使用此界面可查看从AEM Forms数据库发布的流程和任务信息。

### QueryDataServlet服务 {#querydataservlet-service-br-1}

QueryDataServlet服务接受来自Process Reporting用户界面的查询。

然后，该服务使用OSGi服务获取相关的报告数据，处理该数据，并将该数据返回到用户界面。

### 自定义报表 {#custom-reports-br}

您可以创建自己的自定义报表，并在“流程报表”用户界面的“自定义报表”选项卡中显示这些报表。

有关创建自定义报表的步骤，请参阅文章中的创建自定义报表 [流程中的自定义报表](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
