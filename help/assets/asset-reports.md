---
title: 有关资产使用和共享的报告
description: 有关 [!DNL Adobe Experience Manager Assets] 中您的资产的报告，可帮助您了解数字资产的使用情况、活动和共享。
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# 资源报告 {#asset-reports}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=en) |
| AEM 6.5 | 本文 |

通过资产报告，您可以评估[!DNL Adobe Experience Manager Assets]部署的实用程序。 通过[!DNL Assets]，您可以为数字资源生成各种报告。 这些报表提供关于系统使用情况、用户如何与资源交互以及下载和共享哪些资源的有用信息。

使用报告中的信息获得关键成功指标以衡量在您的企业内和客户采用[!DNL Assets]的情况。

[!DNL Assets]报告框架使用[!DNL Sling]作业按顺序异步处理报告请求。 它可扩展到大型存储库。 异步报表处理提高了生成报表的效率和速度。

报告管理界面非常直观，包括细粒度选项和控件，可用于访问存档的报告和查看报告运行状态（成功、失败和排队）。

生成报告时，系统会通过电子邮件通知您（可选）和收件箱通知通知您。 您可以在报表列表页面中查看、下载或删除报表，该页面显示了之前生成的所有报表。

## 先决条件 {#prerequisite-for-reporting}

要生成报表，请执行以下操作：

* 从&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**&#x200B;启用[!UICONTROL Day CQ DAM事件记录器]服务。
* 选择要报告的活动或事件。 例如，要生成有关已下载资源的报告，请选择[!UICONTROL 已下载的资源]。

![在Web控制台中启用资源报告](assets/reports-config-day-cq-dam-event-recorder.png)

## 生成报表 {#generate-reports}

[!DNL Experience Manager Assets]为您生成以下标准报告：

* 上传
* 下载
* 期限
* 修改
* 发布
* [!DNL Brand Portal]发布
* 磁盘使用情况
* 文件
* 链接共享

[!DNL Adobe Experience Manager]管理员可以轻松地为您的实施生成和自定义这些报表。 管理员可以按照以下步骤生成报告：

1. 在[!DNL Experience Manager]界面中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 报表]**。

   ![用于导航资产报表的“工具”页面](assets/AssetsReportNavigation.png)

1. 在[!UICONTROL 资产报表]页面上，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。
1. 从&#x200B;**[!UICONTROL 创建报告]**&#x200B;页面中，选择要创建的报告，然后单击&#x200B;**[!UICONTROL 下一步]**。

   ![选择报表类型](assets/choose_report.png)

   >[!NOTE]
   >
   >默认情况下，内容片段和链接共享包含在资产[!UICONTROL 下载]报表中。 选择相应的选项以创建链接共享报表或从下载报表中排除内容片段。

   >[!NOTE]
   >
   >[!UICONTROL 下载]报表仅显示那些单独选择后下载的资源或使用快速操作下载的资源的详细信息。 但是，它不包括下载文件夹中资产的详细信息。

1. 在存储报告的CRX存储库中配置报告详细信息，如标题、描述、缩略图和文件夹路径。 默认情况下，文件夹路径为`/content/dam`。 您可以指定其他路径。

   ![添加报告详细信息的页面](assets/report_configuration.png)

   选择报表的日期范围。

   您可以选择立即生成报表，也可以选择在将来的日期和时间生成报表。

   >[!NOTE]
   >
   >如果选择稍后计划报表，请确保在日期和时间字段中指定日期和时间。 如果您未指定任何值，则报告引擎会将其视为将立即生成的报告。

   根据您创建的报告类型，配置字段可能会有所不同。 例如，**[!UICONTROL 磁盘使用情况]**&#x200B;报表提供了选项，以便在计算资源使用的磁盘空间时包含资源演绎版。 您可以选择在子文件夹中包括或排除资产以计算磁盘使用情况。

   >[!NOTE]
   >
   >**[!UICONTROL 磁盘使用情况]**&#x200B;报表不包含日期范围字段，因为它仅指示当前磁盘空间使用情况。

   磁盘使用情况报告的![详细信息页面](assets/disk_usage_configuration.png)

   创建&#x200B;**[!UICONTROL 文件]**&#x200B;报告时，您可以包含/排除子文件夹。 但是，您不能包含此报表的资产演绎版。

   ![文件报告的详细信息页面](assets/files_report.png)

   **[!UICONTROL 链接共享]**&#x200B;报表显示从[!DNL Assets]内与外部用户共享的资产的URL。 其中包括共享资产的用户的电子邮件 ID、接受共享资产的用户的电子邮件 ID、链接的共享日期和到期日期。列不可自定义。

   **[!UICONTROL 链接共享]**&#x200B;报告不包含子文件夹和呈现形式的选项，因为它仅发布显示在`/var/dam/share`下的共享URL。

   链接共享报告的![详细信息页面](assets/link_share.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 下一步]**。

1. 在&#x200B;**[!UICONTROL 配置列]**&#x200B;页中，默认情况下选择报表中显示的某些列。 您可以选择更多列。 取消选择要在报表中排除它的列。

   ![选择或取消选择的报表列](assets/configure_columns.png)

   要显示自定义列名或属性路径，请在CRX中的`jcr:content`节点下配置资产二进制文件的属性。 或者，通过属性路径选取器添加它。

   ![选择或取消选择的报表列](assets/custom_columns.png)

1. 单击工具栏中的&#x200B;**[!UICONTROL 创建]**。 此时将显示一条消息，通知已启动报表生成。
1. 在[!UICONTROL 资产报表]页面上，报表生成状态基于报表作业的当前状态，例如[!UICONTROL 成功]、[!UICONTROL 失败]、[!UICONTROL 已排队]或[!UICONTROL 已计划]。 通知收件箱中将显示相同的状态。要查看报告页面，请单击报告链接。 或者，选择报告，然后单击工具栏中的&#x200B;**[!UICONTROL 查看]**。

   <!--![A generated report](assets/report_page.png)-->
   [报告状态](assets/report-status.JPG)

   单击工具栏中的&#x200B;**[!UICONTROL 下载]**&#x200B;以CSV格式下载报表。

## 添加自定义列 {#add-custom-columns}

您可以向以下报表添加自定义列，以显示更多符合自定义要求的数据：

* 上传
* 下载
* 期限
* 修改
* 发布
* [!DNL Brand Portal]发布
* 文件

要向这些报表中添加自定义列，请执行以下步骤：

1. 在[!DNL Manager interface]中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Assets]** > **[!UICONTROL 报表]**。
1. 在[!UICONTROL 资产报表]页面上，单击工具栏中的&#x200B;**[!UICONTROL 创建]**。

1. 从&#x200B;**[!UICONTROL 创建报告]**&#x200B;页面中，选择要创建的报告，然后单击&#x200B;**[!UICONTROL 下一步]**。
1. 根据需要，配置标题、描述、缩略图、文件夹路径和日期范围等报表详细信息。

1. 要显示自定义列，请在&#x200B;**[!UICONTROL 自定义列]**&#x200B;下指定列的名称。

   ![为报告的自定义列指定名称](assets/custom_columns-1.png)

1. 使用属性路径选取器在CRXDE中的`jcr:content`节点下添加属性路径。 或者，在属性路径字段中键入路径。

   ![从jcr：content中的路径映射属性路径](assets/property_picker.png)

   要添加更多自定义列，请单击“添加”****&#x200B;并重复步骤5和6。

1. 单击工具栏中的&#x200B;**[!UICONTROL 创建]**。 此时将显示一条消息，通知已启动报表生成。

## 配置清除服务 {#configure-purging-service}

要删除您不再需要的报表，请从Web控制台配置DAM报表清除服务，以根据其数量和期限清除现有报表。

1. 从`https://[aem_server]:[port]/system/console/configMgr`访问Web控制台（配置管理器）。
1. 打开&#x200B;**[!UICONTROL DAM报告清除服务]**&#x200B;配置。
1. 在`scheduler.expression.name`字段中指定清除服务的频率（时间间隔）。 您还可以配置报告的期限和数量阈值。
1. 保存更改。

## 疑难解答信息、提示和限制 {#best-practices-and-limitations}

* 如果报表中的某些报表或数字不可用或按预期提供，请确保已启用[!UICONTROL Day CQ DAM事件记录器]服务。

* 删除不再需要的报表。 使用DAM报告清除服务中的配置选项来配置清除报告的标准。

* 如果未生成磁盘使用情况报表，并且您使用的是[!DNL Dynamic Media]，请确保所有资产都正确继续。 要解决此问题，请重新处理资源，然后再次生成报表。
