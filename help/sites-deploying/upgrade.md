---
title: 升级到Adobe Experience Manager 6.5
description: 了解将旧版Adobe Experience Manager (AEM)安装升级到AEM 6.5的基础知识。
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# 升级到Adobe Experience Manager (AEM) 6.5 {#upgrading-to-aem}

本节介绍如何将AEM安装升级到AEM 6.5：

* [规划升级](/help/sites-deploying/upgrade-planning.md)
* [使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [升级过程](/help/sites-deploying/upgrade-procedure.md)
* [升级代码和自定义项](/help/sites-deploying/upgrading-code-and-customizations.md)
* [升级前维护任务](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [执行就地升级](/help/sites-deploying/in-place-upgrade.md)
* [升级后检查和故障排除](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [可持续升级](/help/sites-deploying/sustainable-upgrades.md)
* [延迟内容迁移](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5中的存储库重组](/help/sites-deploying/repository-restructuring.md)

为了便于引用这些过程中涉及的AEM实例，在这些文章中使用了以下术语：

* 此 *源* 实例是从中升级的AEM实例。
* 此 *目标* 实例是您要升级到的实例。

>[!NOTE]
>
>作为提高升级可靠性的努力的一部分，AEM进行了全面的存储库重组。 有关如何与新结构对齐的更多信息，请参阅 [AEM中的存储库重组。](/help/sites-deploying/repository-restructuring.md)

## 更改了哪些内容？ {#what-has-changed}

以下是AEM最近几个版本中注释的主要更改：

AEM 6.0引入了新的Jackrabbit Oak存储库。 持久性管理器已替换为 [微内核](/help/sites-deploying/platform.md#contentbody_title_4). 从版本6.1开始，不再支持CRX2。 必须运行名为crx2oak的迁移工具才能从5.6.1实例迁移CRX2存储库。 有关更多信息，请参阅 [使用CRX2OAK迁移工具](/help/sites-deploying/using-crx2oak.md).

如果使用Assets Insights，并且您从AEM 6.2之前的版本进行升级，则必须迁移资产并通过JMX Bean生成ID。 对于Adobe的内部测试，TarMK环境上的125K资源在一小时内完成迁移，但结果可能有所不同。

6.3引入了新的格式用于 `SegmentNodeStore`，这是TarMK实施的基础。 如果您从AEM 6.3之前的版本升级，这需要在升级过程中迁移存储库，包括系统停机时间。

Adobe工程部门估计需要20分钟左右。 不需要重新编制索引。 此外，已发布新版本的crx2oak工具以与新的存储库格式配合使用。

**如果从AEM 6.3升级到AEM 6.5，则不需要此迁移。**

升级前维护任务已优化以支持自动化。

crx2oak工具命令行使用选项已更改为自动化友好并支持更多升级路径。

升级后的检查也变得有利于自动化。

定期收集修订垃圾和数据存储垃圾现在是必须定期执行的例行维护任务。 引入AEM 6.3后，Adobe支持并建议进行联机修订清理。 请参阅 [修订版清理](/help/sites-deploying/revision-cleanup.md) 有关如何配置这些任务的信息。

AEM最近推出了 [模式检测器](/help/sites-deploying/pattern-detector.md) 用于在您开始规划升级时评估升级的复杂性。 6.5还特别侧重于 [向后兼容性](/help/sites-deploying/backward-compatibility.md) 功能。 最后，以下方面的最佳实践 [可持续升级](/help/sites-deploying/sustainable-upgrades.md) 也会被添加。

有关最新AEM版本中其他哪些内容发生了更改的详细信息，请参阅完整的发行说明：

* [Adobe Experience Manager 6.5最新Service Pack发行说明](/help/release-notes/release-notes.md)

## 升级概述 {#upgrade-overview}

升级AEM是一个多步骤、有时甚至是多个月的过程。 以下概要概述了升级项目中包含的内容以及本文档中包含的内容：

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 升级流程 {#upgrade-overview-1}

下图概述了整体建议的流程，重点说明了升级方法。 请注意对Adobe引入的新功能的引用。 升级应从模式检测器开始(请参阅 [使用模式检测器评估升级复杂性](/help/sites-deploying/pattern-detector.md))，这可以让您根据生成的报告中的模式，决定要采用的与AEM 6.4兼容的路径。

6.5非常重视使所有新功能向后兼容，但是，如果您仍然看到一些向后兼容性问题，则兼容性模式可让您暂时推迟开发，以使自定义代码与6.5兼容。此方法可帮助您避免在升级后立即执行开发工作(请参阅 [AEM 6.5中的向后兼容性](/help/sites-deploying/backward-compatibility.md))。

最后，在您的6.5开发周期中，可持续升级下引入了功能(请参阅 [可持续升级](/help/sites-deploying/sustainable-upgrades.md))帮助您遵循最佳实践，使未来的升级更高效、更顺畅。

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
