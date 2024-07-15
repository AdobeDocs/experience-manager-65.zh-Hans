---
title: 开始使用流程报告
description: 开始使用AEM Forms on JEE流程报告的步骤
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 0%

---

# 开始使用流程报告{#getting-started-with-process-reporting}

利用Process Reporting，AEM Forms用户能够查询当前在AEM Forms实施中定义的AEM Forms流程相关信息。 但是，流程报表不会直接从AEM Forms存储库访问数据。 数据首先按计划发布到Process Reporting存储库（*由ProcessDataPublisher和ProcessDataStorage服务*&#x200B;发布）。 然后，使用发布到存储库的Process Reporting数据生成Process Reporting中的报告和查询。 Process Reporting作为Forms Workflow模块的一部分安装。

本文详细介绍了将AEM Forms数据发布到Process Reporting存储库的步骤。 之后，您将能够使用Process Reporting运行报表和查询。 本文还介绍了可用于配置Process Reporting服务的选项。

## 流程报告先决条件 {#process-reporting-pre-requisites}

### 清除非基本流程 {#purge-non-essential-processes}

如果您当前使用的是Forms Workflow，则AEM Forms数据库可能包含大量数据

Process Reporting发布服务会发布数据库中当前可用的所有AEM Forms数据。 这意味着，如果数据库包含您不希望对其运行报表和查询的旧数据，则所有此类数据也将发布到存储库，即使报表不需要这些数据也是如此。 建议您在运行服务以将数据发布到Process Reporting存储库之前清除此数据。 这样做会同时提高发布者服务和查询报告数据的服务的性能。

有关清除AEM Forms进程数据的详细信息，请参阅[清除进程数据](/help/forms/using/admin-help/purging-process-data.md)。

>[!NOTE]
>
>有关清除实用程序的提示和技巧，请参阅Adobe Developer Connection有关[清除进程和作业](/help/forms/using/admin-help/purging-process-data.md)的文章。

## 配置Process Reporting服务 {#configuring-process-reporting-services}

### 计划流程数据发布 {#schedule-process-data-publishing}

Process Reporting服务会按计划将数据从AEM Forms数据库发布到Process Reporting存储库。

此操作可能会占用大量资源，并且可能会影响AEM Forms服务器的性能。 建议您在AEM Forms Server繁忙时段之外计划此时间。

默认情况下，数据发布安排在每天凌晨2:00运行。

要更改发布计划，请执行以下步骤：

>[!NOTE]
>
>如果您在某个群集中运行AEM Forms实施，请在群集的每个节点上执行以下步骤。

1. 停止AEM Forms Server实例。
1. &#x200B;AEM

   * （对于Windows）在编辑器中打开`[JBoss root]/bin/run.conf.bat`文件。
   * (对于Linux®、AIX®和Solaris™)编辑器中的`[JBoss root]/bin/run.conf.sh`文件。

1. 添加JVM参数`-Dreporting.publisher.cron = <expression>.`

   示例：以下cron表达式导致Process Reporting每五小时将AEM Forms数据发布到Process Reporting存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 保存并关闭`run.conf.bat`文件。

1. 重新启动AEM Forms Server实例。

1. 停止AEM Forms Server实例。
1. 登录到WebSphere®管理控制台。 在导航树中，单击&#x200B;**服务器** > **应用程序服务器**，然后在右窗格中单击服务器名称。

1. 在服务器基础结构下，单击&#x200B;**Java™和进程管理** > **进程定义**。

1. 在“其他属性”下，单击&#x200B;**Java™虚拟机**。

   在“通用JVM参数”框中，添加参数`-Dreporting.publisher.cron = <expression>.`

   **示例**：以下cron表达式导致Process Reporting每五小时将AEM Forms数据发布到Process Reporting存储库：

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击&#x200B;**应用**，单击“确定”，然后单击&#x200B;**直接保存到主配置**。
1. 重新启动AEM Forms Server实例。
1. 停止AEM Forms Server实例。
1. 登录到WebLogic管理控制台。 WebLogic管理控制台的默认地址为`https://[hostname]:[port]/console`。
1. 在“更改中心”下，单击&#x200B;**锁定和编辑**。
1. 在“域结构”下，单击&#x200B;**环境** > **服务器**，然后在右窗格中单击托管服务器名称。
1. 在下一个屏幕上，单击&#x200B;**配置**&#x200B;选项卡> **服务器启动**&#x200B;选项卡。
1. 在参数框中，添加JVM参数`-Dreporting.publisher.cron = <expression>`。

   **示例**：以下cron表达式导致Process Reporting每五小时将AEM Forms数据发布到Process Reporting存储库：

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 单击&#x200B;**保存**，然后单击&#x200B;**激活更改**。
1. 重新启动AEM Forms Server实例。

![processdatapublisherservice](assets/processdatapublisherservice.png)

>[!NOTE]
>
> 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

### ProcessDataStorage服务 {#processdatastorage-service}

ProcessDataStorageProvider服务从ProcessDataPublisher服务接收流程数据，并将该数据保存到Process Reporting存储库。

在每个发布周期，数据都会保存到预定义根文件夹的子文件夹中。

您可以使用管理控制台来配置根（**默认**： `/content/reporting/pm`）位置和子文件夹（**默认**： `/yyyy/mm/dd/hh/mi/ss`）层次结构格式，以便在其中存储流程数据。

#### 配置Process Reporting存储库位置 {#to-configure-the-process-reporting-repository-locations}

1. 使用管理员凭据登录到&#x200B;**管理控制台**。 管理控制台的默认URL为`https://'[server]:[port]'/adminui`
1. 导航到&#x200B;**主页** > **服务** > **应用程序和服务** >**服务管理**，然后打开&#x200B;**ProcessDataStorageProvider**&#x200B;服务。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **根文件夹**

   将存储流程数据以供生成报表的CRX位置。

   `Default`：`/content/reporting/pm`

   **文件夹层次结构**

   根据流程创建时间将存储流程数据的文件夹层次结构。

   `Default`：`/yyyy/mm/dd/hh/mi/ss`

1. 单击&#x200B;**保存**。

### ReportConfiguration服务 {#reportconfiguration-service}

ReportConfiguration服务由Process Reporting用于配置process Reporting查询服务。

#### 配置ReportingConfiguration服务 {#to-configure-the-reportingconfiguration-service}

1. 使用CRX管理员凭据登录到&#x200B;**配置管理器**。 配置管理器的默认URL为`https://'[server]:[port]'/lc/system/console/configMgr`
1. 打开&#x200B;**ReportingConfiguration**&#x200B;服务。
1. **记录数**

   对存储库运行查询时，结果可能包含许多记录。 如果结果集很大，则查询执行可能会占用服务器资源。

   为了处理大型结果集，ReportConfiguration服务将查询处理拆分为多批记录。 这样做可以减少系统负载。

   `Default`：`1000`

   **CRX存储路径**

   将流程数据存储到其中以便生成报表的CRX位置。

   `Default`：`/content/reporting/pm`

   >[!NOTE]
   >
   >此位置与ProcessDataStorage配置选项&#x200B;**根文件夹**&#x200B;中指定的位置相同。
   >
   >
   >如果在ProcessDataStorage配置中更新“根文件夹”选项，则必须在ReportConfiguration服务中更新“CRX存储路径”位置。

1. 单击&#x200B;**保存**&#x200B;并关闭&#x200B;**CQ配置管理器**。

### ProcessDataPublisher服务 {#processdatapublisher-service}

ProcessDataPublisher服务从AEM Forms数据库导入进程数据，并将该数据发布到ProcessDataStorageProvider服务进行存储。

#### 配置ProcessDataPublisher服务   {#to-configure-processdatapublisher-service-nbsp}

1. 使用管理员凭据登录到&#x200B;**管理控制台**。

   默认URL为`https://'server':port]/adminui/`。

1. 导航到&#x200B;**主页** > **服务** > **应用程序和服务** >**服务管理**，然后打开&#x200B;**ProcessDataPublisher**&#x200B;服务。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publish数据**

启用此选项以开始发布流程数据。 默认情况下，该选项处于禁用状态。

只有在正确设置了与Process Reporting组件相关的所有配置时，才启用Process Reporting。

或者，使用此选项可在不再需要流程数据发布时禁用它。

`Default`：`Off`

**批次间隔（秒）**

每次ProcessDataPublisher服务运行时，服务都会按批处理间隔第一次拆分自上次运行服务以来的时间。 然后，该服务单独处理每个AEM Forms数据间隔，以帮助控制发布者在一个周期内的每次运行（批处理）期间端到端处理的数据大小。

例如，如果发布器每天运行，则默认情况下，它会将处理拆分为24批，每批各处理一小时，而不是在一次运行中处理一天的所有数据。

`Default`：`3600`

`Unit`：`Seconds`

**锁定超时（秒）**

发布器服务在开始处理数据时获得锁定，以便发布器的多个实例不会同时开始运行和处理数据。

如果获取了锁的发布服务器服务在“锁定超时”值定义的秒数内处于空闲状态，则会释放其锁定，以便其他发布服务器服务实例可以继续处理。

`Default`：`3600`

`Unit`：`Seconds`

**来自**&#x200B;的Publish数据

AEM Forms环境包含自环境设置以来的数据。

默认情况下，ProcessDataPublisher服务会从AEM Forms数据库导入所有数据。

根据您的报告需求，如果您计划在特定日期和时间后运行报告和查询数据，建议您指定日期和时间。 然后，发布服务发布该时间之后的日期。

`Default`：`01-01-1970 00:00:00`

`Format`：`dd-MM-yyyy HH:mm:ss`

## 访问“流程报表”用户界面 {#accessing-the-process-reporting-user-interface}

“流程报表”的用户界面是基于浏览器的。

设置Process Reporting后，您可以在AEM Forms安装中的以下位置开始使用Process Reporting：

`https://<server>:<port>/lc/pr`

### 登录到流程报告 {#log-in-to-process-reporting}

导航到流程报表URL (https://&lt;server>：&lt;port>/lc/pr)时，将显示登录屏幕。

要登录“进程报告”模块，请指定您的凭据。

>[!NOTE]
>
>要登录“流程报表”用户界面，您需要具有以下AEM Forms权限：
>
>`PERM_PROCESS_REPORTING_USER`

![登录以处理报告](assets/capture1_new.png)

当您登录到“进程报告”时，将显示&#x200B;**[!UICONTROL 主页]**&#x200B;屏幕。

### 流程报告主屏幕 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**进程报告树视图：**&#x200B;主屏幕左侧的树视图包含进程报告模块的项。

树视图由以下顶级项目组成：

**报告：**&#x200B;此项包含随进程报告一起提供的现成报告。

有关预定义报表的详细信息，请参阅[进程报表中的预定义报表](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)。

**临时查询：**&#x200B;此项目包含用于执行基于筛选器的进程和任务搜索的选项。

有关特别查询的详细信息，请参阅[进程报表中的特别查询](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**自定义：**&#x200B;自定义节点显示您创建的自定义报表。

有关创建和显示自定义报告的过程，请参阅[进程报告中的自定义报告](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**进程报告标题栏：**&#x200B;进程报告标题栏包含一些可在用户界面中使用的通用选项。

**进程报告标题：**&#x200B;进程报告标题显示在标题栏的左角。

随时单击标题以返回主屏幕。

**上次更新时间：**&#x200B;进程数据已按计划从AEM Forms数据库发布到Process Reporting存储库。

上次更新时间显示将数据更新推入Process Reporting存储库的上次日期和时间。

有关数据发布服务以及如何计划此服务的详细信息，请参阅“开始使用流程报告”一文中的[计划流程数据发布](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)。

**进程报告用户：**&#x200B;登录用户名显示在上次更新时间的右侧。

**流程报表标题栏下拉列表：**&#x200B;位于“流程报表”标题栏右角的下拉列表包含以下选项：

* **[!UICONTROL 同步]**：将嵌入的Process Reporting存储库与AEM Forms数据库同步。
* **[!UICONTROL 帮助]**：查看有关流程报告的帮助文档。
* **[!UICONTROL 注销]**：注销进程报告


