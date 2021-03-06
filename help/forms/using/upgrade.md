---
title: 升级到 AEM 6.5 Forms
seo-title: Upgrade to AEM 6.5 Forms
description: 您可以从AEM 6.3 Forms和AEM 6.4 Forms直接升级到AEM 6.5 Forms。
seo-description: You can perform a direct upgrade from AEM 6.3 Forms and AEM 6.4 Forms to AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
role: Admin
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
source-git-commit: 2e6d688818e9cc337444bcda2a49485e9167a113
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# 升级到 AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM 6.5 Forms包含一些新增功能和增强功能，可简化表单和信函的创建、管理和用户体验。 要了解AEM 6.5 Forms的所有新增功能和增强功能，请参阅 [新增功能摘要文档](../../forms/using/whats-new.md).

您可以升级现有LiveCycle或AEM Forms安装，以获取AEM 6.5 Forms中提供的新功能和增强功能，同时保持现有数据、流程和资产完好无损。 升级时，还会保留元数据和进程状态。 您可以选择升级路径以开始升级。

下图显示了OSGi上AEM Forms的可用升级路径：

![](do-not-localize/osgi-upgrade-path.png)

您可以从以下位置执行直接升级：

* OSGi上的AEM 6.3 Forms
* AEM 6.4 Forms on OSGi

您还可以从

* OSGi上的AEM 6.0 Forms
* OSGi上的AEM 6.1 Forms
* AEM 6.2 Forms on OSGi

下图显示了JEE上AEM Forms的可用升级路径：

![](do-not-localize/jee-upgrade-6-5.png)

您可以从以下位置执行直接升级：

* AEM 6.3 JEE上的Forms
* AEM 6.4 JEE上的Forms
* JEE上的AEM 6.5.x.x

您还可以从

* LiveCycleES2
* LiveCycleES3
* LiveCycleES4 SP1
* AEM 6.0 Forms on JEE
* AEM 6.1 Forms on JEE
* AEM 6.2 JEE上的Forms

AEM 6.5.12.0 Forms on JEE提供了两种类型的安装程序：完整安装程序和修补程序安装程序。

**完整安装程序**:您可以使用完整安装程序设置新的AEM Forms实例，或从JEE上的AEM 6.3 Forms、JEE上的AEM 6.4执行升级，以及从JEE上的AEM 6.5.x.x到JEE上的AEM 6.5.12.0 Forms的就地升级。

**修补程序安装程序**:修补程序安装程序适用于已在使用AEM 6.5.x.x版本的客户。 您可以使用修补程序安装程序升级到最新版本的AEM Forms。

下图描述了使用完整和修补程序安装程序的传感器。

![](assets/full-and-patch-installer.png)

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
