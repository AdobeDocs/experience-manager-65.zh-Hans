---
title: 升级到 AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: 您可以从AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1直接升级到AEM 6.3 Forms。
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 1e39455e-f588-42a2-91f5-daefcfed82a0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 6%

---

# 在OSGi上升级到AEM 6.5 Forms {#upgrade-to-aem-forms-osgi}

您可以从AEM 6.3 Forms或AEM 6.4 Forms直接升级到AEM 6.5 Forms。

直接从升级路径 **AEM 6.0 Forms、AEM 6.1 Forms**&#x200B;和 **AEM 6.2 Forms** 到AEM 6.5 Forms不可用。 执行中间 [升级到AEM 6.2 Forms](https://helpx.adobe.com/experience-manager/6-2/forms/using/upgrade.html), [升级到AEM 6.3 Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/upgrade.html)或 [升级到AEM 6.4 Forms](/help/forms/using/upgrade.md) 然后，从AEM 6.3 Forms或AEM 6.4 Forms升级到AEM 6.5 Forms。

请执行以下操作，从AEM 6.3 Forms或AEM 6.4 Forms升级到AEM 6.5 Forms:

1. 将现有AEM实例升级到AEM 6.5。下面列出了步骤：

   1. 安装AEM 6.3 Forms或AEM 6.4 Forms的最新Service Pack和修补程序。 有关详细信息，请参阅 [AEM维护中心](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html).
   1. 为升级准备源实例。 有关详细步骤，请参阅 [升级到AEM 6.5](/help/sites-deploying/upgrade.md).
   1. 下载 [AEM 6.5快速入门](/help/sites-deploying/deploy.md#getting%20the%20software).
   1. **（仅基于Unix/Linux的安装）** 如果您使用UNIX或Linux作为基础操作系统，请打开“终端”窗口，导航到包含crx-quickstart的文件夹，然后运行以下命令：

      `chmod -R 755 ../crx-quickstart`

   1. 将您的AEM实例升级到AEM 6.3。有关分步说明，请参阅 [升级到AEM 6.5](/help/sites-deploying/upgrade.md).

      在继续执行后续步骤之前，请等待ServiceEvent REGISTERED和ServiceEvent UNEXIVERTED消息停止出现在 &lt;crx-repository>/error.log文件。

      >[!NOTE]
      >
      >服务器启动并运行后，一些AEM Forms包仍处于安装状态。 每次安装的包数可能有所不同。 您可以安全地忽略这些包的状态。 这些包列在https://&#39;上[服务器]:[端口]“/system/console/”。

1. 安装AEM Forms附加组件包。 下面列出了这些步骤：

   1. 打开 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登录 Software Distribution。
   1. 点按标题菜单中的 **[!UICONTROL Adobe Experience Manager]**。
   1. 在 **[!UICONTROL 过滤器]** 部分：
      1. 选择 **[!UICONTROL Forms]** 从 **[!UICONTROL 解决方案]** 下拉列表。
      1. 选择包的版本和类型。 您还可以使用 **[!UICONTROL 搜索下载]** 选项来筛选结果。
   1. 点按适用于您的操作系统的包名称，选择 **[!UICONTROL 接受EULA条款]**，然后点按 **[!UICONTROL 下载]**.
   1. 打开[包管理器](https://docs.adobe.com/content/help/zh-Hans/experience-manager-65/administering/contentmanagement/package-manager.html)，并单击&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。
   1. 选择包并单击 **[!UICONTROL 安装]**.

      您还可以使用 [AEM Forms版本](https://helpx.adobe.com/cn/aem-forms/kb/aem-forms-releases.html) 文章。

      >[!NOTE]
      >
      >安装包后，系统会提示您重新启动AEM实例。 **不要立即停止服务器。** 在停止AEM Forms服务器之前，请等待ServiceEvent REGISTERED和ServiceEvent UNREGISTERED消息停止显示在 &lt;crx-repository>/error.log文件和日志稳定。 另请注意，一些包可以保持已安装状态。 您可以安全地忽略这些包的状态。

1. 重新启动AEM实例。

1. 执行安装后活动。

   * **运行迁移实用程序**

      迁移实用程序使早期版本的自适应表单和通信管理资产与AEM 6.5表单兼容。 您可以从AEM Software Distribution下载该实用程序。 有关配置和使用迁移实用程序的分步信息，请参阅 [迁移实用程序](../../forms/using/migration-utility.md).

      如果您使用 [集成草稿和提交组件的示例](https://helpx.adobe.com/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) 使用数据库并从以前的版本升级，然后在执行升级后运行以下SQL查询：

      ```sql
      UPDATE metadata m, additionalmetadatatable am
      SET m.dataType = am.value
      WHERE m.id = am.id
      AND am.key = 'dataType'
      ```

      ```sql
      DELETE from additionalmetadatatable
      WHERE `key` = 'dataType'
      ```

   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置Adobe Sign**

      如果您在以前的AEM Forms版本中配置了Adobe Sign，请从AEM云服务中重新配置Adobe Sign。 有关更多详细信息，请参阅 [将Adobe Sign与AEM Forms集成](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **支持jQuery**

      在AEM 6.5 Forms中，jQuery版本已更新为3.2.1,jQuery UI版本已更新为1.12.1。AEM Form在 **noConflict** 模式。 因此，如果您使用的是任何其他jQuery版本，则在执行升级时不会显示任何问题。 但是，当您升级到AEM 6.5 Forms时：

      * 确保自定义组件（如果有）与支持的jQuery版本兼容。
      * 从自定义组件中删除不支持的API。 请参阅 [升级指南](https://jquery.com/upgrade-guide/3.0/) ，以获取已删除API的列表。 例如，将删除对load()、 .unload()和.error()API的支持。 使用.on()方法代替上述API。 例如，将$(&quot;img&quot;)。load(fn)更改为$(&quot;img&quot;)。on(&quot;load&quot;, fn)。
   * **(如果仅从AEM 6.2 Forms或以前的版本升级)重新配置分析和报表**

      在AEM 6.4 Forms中，不提供用于展示的源流量变量和成功事件流量变量。 因此，当您从AEM 6.2 Forms或更早版本升级时，AEM Forms将停止向Adobe Analytics服务器发送数据，并且自适应表单的Analytics报表不可用。 此外，AEM 6.4 Forms还为表单分析版本引入了流量变量，并为字段逗留时间的成功事件引入了流量变量。 因此，请为您的AEM Forms环境重新配置分析和报表。 有关详细步骤，请参阅 [配置分析和报表](../../forms/using/configure-analytics-forms-documents.md).


1. 验证服务器是否成功升级，所有数据是否也已成功迁移，并且可以正常运行。

   * **验证包的状态：** 确保所有包都处于活动状态。
   * **验证复制和反向复制：** 发布、填写和提交一些迁移的表单。 同时验证提交的数据。
   * **验证对管理员和开发人员用户界面的访问权限：** 从管理员帐户登录AEM实例，并验证您是否有权访问以下URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   在AEM 6.4 Forms中，crx-repository的结构已发生更改。 如果从6.3 Forms升级到AEM 6.5 Forms，请使用更改的路径进行重新创建的自定义。 有关更改路径的完整列表，请参阅 [Forms在AEM中重组存储库](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md).
