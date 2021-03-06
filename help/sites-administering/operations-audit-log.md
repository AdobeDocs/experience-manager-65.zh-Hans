---
title: AEM 6中的审核日志维护
seo-title: AEM 6中的审核日志维护
description: 了解AEM中的审核日志维护。
seo-description: 了解AEM中的审核日志维护。
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: 运营
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# AEM 6{#audit-log-maintenance-in-aem}中的审核日志维护

符合审核日志记录条件的AEM事件会生成大量存档数据。 由于复制、资产上传和其他系统活动，此数据会随着时间而快速增长。

“审核日志维护”包括几个功能部分，这些功能允许在特定策略下自动维护审核日志。

它作为可配置的每周维护任务实施，并可通过操作仪表板监控控制台访问。

有关更多信息，请参阅[操作功能板文档](/help/sites-administering/operations-dashboard.md)。

审核日志清除选项有三种类型：

1. [页面审核日志清除](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM审核日志清除](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [复制审核日志记录](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

每个规则都可以通过在AEM Web Console中创建规则来配置。 配置完这些维护任务后，您可以通过转到&#x200B;**工具 — 操作 — 维护 — 每周维护窗口**&#x200B;并运行&#x200B;**审核日志维护任务**&#x200B;来触发它们。

## 配置页面审核日志清除{#configure-page-audit-log-purging}

请按照以下步骤配置审核日志清除：

1. 通过将浏览器指向`http://localhost:4502/system/console/configMgr/`，转到Web控制台管理

1. 搜索名为&#x200B;**页面审核日志清除规则**&#x200B;的项目，然后单击该项目。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 接下来，根据您的要求配置清除计划程序。 可用选项包括：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 规则将应用到的内容路径；
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）；
   * **审核日志类型：** 应清除的审核日志类型。

   >[!NOTE]
   >
   >内容路径仅适用于存储库中`/var/audit/com.day.cq.wcm.core.page`节点的子项。

1. 保存规则。
1. 您刚刚创建的规则需要显示在操作功能板中才能执行。 为此，请从AEM欢迎屏幕中转到&#x200B;**工具 — 操作 — 维护**。

1. 按&#x200B;**每周维护窗口**&#x200B;卡。

1. 您将在&#x200B;**AuditLog Maintenance Task**&#x200B;卡下找到已存在的维护任务。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 您可以检查下次执行的日期、对其进行配置，或通过按“播放”按钮手动执行。

在AEM 6.3中，如果计划维护窗口在审核日志清除任务完成之前关闭，则任务会自动停止。 在下一个维护窗口打开时，系统将恢复运行。

**在AEM 6.5中**，您可以通过单击停止图标手动停止正在运行的审核日志清除 **** 任务。下次执行时，任务将安全地恢复。

>[!NOTE]
>
>停止维护任务意味着暂停其执行，而不丢失已在进行中的作业的跟踪。

## 配置DAM审核日志清除{#configure-dam-audit-log-purging}

1. 导航到位于&#x200B;*https://&lt;serveraddress>的系统控制台：&lt;serverport>/system/console/configMgr*
1. 搜索&#x200B;**DAM审核日志清除**&#x200B;规则，然后单击结果。
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审计策略规则的名称；
   * **内容路径：** 规则将应用到的内容路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志DAM事件类型：** 应清除的DAM审核事件类型。

1. 单击&#x200B;**Save**&#x200B;以保存配置

## 配置复制审核日志清除{#configure-replication-audit-log-purging}

1. 导航到位于&#x200B;*https://&lt;serveraddress>的系统控制台：&lt;serverport>/system/console/configMgr*
1. 搜索&#x200B;**复制审核日志清除计划程序**&#x200B;并单击结果
1. 在下一个窗口中，相应地配置规则。 选项包括：

   * **规则名称：** 审核策略规则的名称
   * **内容路径：** 规则将应用到的内容路径
   * **最低年龄：** 需要保留审核日志的时间（以天为单位）
   * **审核日志复制事件类型：** 应清除的复制审核事件类型

1. 单击&#x200B;**Save**&#x200B;以保存配置。
