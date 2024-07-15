---
title: 针对EMC Documentum&amp；reg；用户的连接器备份战略
description: 了解如何为EMC Documentum&amp；reg；用户创建Connector的备份战略。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b759b936-5907-4311-a5cc-60f321476368
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# 针对EMC Documentum®用户的Connector备份战略 {#backup-strategy-for-connector-for-emc-documentum-users}

如果安装了Connector for EMC Documentum® ，则除了本章中的说明之外，您的备份和恢复策略还必须包括备份（或恢复）安装ECM系统的计算机。 (请参阅ECM Documentum®文档)。

使用ECM存储库并执行以下任务来备份AEM表单环境：

* 按照本文档中所述的说明备份AEM表单。
* 按照[备份EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)中的说明备份ECM Documentum®系统。

通过使用ECM存储库并执行以下任务来恢复AEM表单环境：

* 按照[恢复EMC Documentum® Content Server](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)中的说明恢复各自的ECM系统。
* 按照本文档中所述的说明还原AEM表单。
