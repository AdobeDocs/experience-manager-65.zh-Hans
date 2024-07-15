---
title: 在JEE上升级到AEM 6.5 Forms
description: 您可以执行从AEM 6.1 Forms、AEM 6.2 Forms和LiveCycleES4 SP1到AEM 6.3 Forms的直接升级。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin,User
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 在JEE上升级到AEM 6.5 Forms {#upgrade-to-aem-forms-jee}

JEE上的AEM 6.5.18.0 Forms提供两种类型的安装程序：完整安装程序和修补程序安装程序。

**完整安装程序**：您可以使用[AEM 6.5.18.0 on JEE完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)来设置新的AEM Forms实例，或从JEE上的AEM 6.5.x.x Forms升级到JEE上的AEM 6.5.18.0 Forms。

**修补程序安装程序**： JEE修补程序安装程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)上的[AEM 6.5.18.0适用于已使用AEM 6.5.x.x版本的客户。 您可以使用修补程序安装程序升级到AEM Forms的最新版本。

下表描述了使用完整安装程序和修补程序安装程序的场景。

![完整和修补安装程序方案](assets/full-and-patch-installer.png)

执行以下过程，使用完整安装程序将JEE上的现有AEM Forms 6.5.x.x升级到JEE上的AEM 6.5.18.0 Forms：

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载AEM 6.5 Forms on JEE安装程序。 您需要有效的维护和支持合同才能使用安装程序。
1. 请参阅[升级核对清单和计划](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65)，了解为确保成功升级而执行的检查。
1. 请参阅[准备升级到AEM Forms](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65)，了解并执行相关任务以确保升级在最短服务器停机时间下正常运行。
1. 根据您现有的环境和应用程序服务器，选择以下文档之一并按照说明进行操作。

   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for JBoss](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for WebSphere](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [从AEM 6.3或AEM 6.4 Forms升级到AEM 6.5 Forms for JBoss Turnkey](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

无法从LiveCycleES2、LiveCycleES3、AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms直接升级到AEM 6.5 Forms。 您可以对LiveCycle或AEM Forms的一个或多个版本执行中间升级，然后升级到AEM 6.5 Forms。 有关中间版本和相应升级说明的列表，请参阅[选择升级路径](upgrade.md)。
