---
title: 针对EMC Documentum&reg；用户的连接器备份战略
description: 了解如何为EMC Documentum&reg；用户创建Connector的备份战略。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%
---
# 针对EMC Documentum®用户的Connector备份战略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果安装了Connector for EMC Documentum® ，则除了本章中的说明之外，您的备份和恢复策略还必须包括备份（或恢复）安装ECM系统的计算机。 （请参阅ECM Documentum®文档）。

通过使用ECM存储库并执行以下任务来备份AEM表单环境：

* 按照本文档中所述的说明备份AEM表单。
* 按照[备份EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)中的说明备份ECM Documentum®系统。

通过使用ECM存储库并执行以下任务来恢复AEM表单环境：

* 按照[恢复EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)中的说明恢复各自的ECM系统。
* 按照本文档中所述的说明还原AEM表单。
