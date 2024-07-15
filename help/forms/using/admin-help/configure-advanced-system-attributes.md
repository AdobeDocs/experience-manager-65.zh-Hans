---
title: 配置高级系统属性
description: 使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 配置高级系统属性 {#configure-advanced-system-attributes}

使用“配置高级系统属性”页可以修改配置文件中的某些设置，而无需导出、编辑和导入文件。 （请参阅[导入和导出配置文件](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。）

1. 在管理控制台中，单击&#x200B;**[!UICONTROL 设置>用户管理>配置>配置高级系统属性]**。
1. （可选）更改以下任何会话属性：

   **会话超时限制（分钟）：**&#x200B;用户自动注销系统之前的时间（以分钟为单位）。 默认情况下，AEM表单组件（如Workbench）会在两小时后超时，无论处于何种活动状态或未处于何种非活动状态，用户必须再次登录。 有效值为`1`到`1440`。 默认值为`120` （2小时）。 此设置将更新配置文件中的`SAML/Producer/assertionValidityInMinutes`条目密钥。

   >[!NOTE]
   >
   >不应将会话超时限制设置为低于10分钟，因为系统可能无法正常运行。 建议值为10-120（分钟）。

   **断言阈值（秒）：**&#x200B;由于群集中AEM表单应用程序服务器之间的系统时间差异，偏移延迟的缓冲时间。 AEM forms根据此属性中指定的时间量（以秒为单位）回溯用户的登录时间。 有效值为`0`到`3600`。 默认值为`60`。 此设置将更新配置文件中的`SAML/Producer/assertionThresholdInSeconds`条目密钥。

   **允许的最大断言续订次数：**&#x200B;无需登录即可透明续订用户会话的最大次数。 有效值为`0`到`9999`。 值为`0`表示断言未续订。 默认值为 10。此设置将更新配置文件中的`SAML/Producer/maxAssertionRenewalCount`条目密钥。

1. （可选）更改以下任何目录同步属性：

   **同步统计信息日志记录：**&#x200B;指定用户管理是否在同步过程中记录详细的统计信息。 （请参阅[在同步期间启用或禁用详细日志记录](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)。）

   **同步完成程序Cron表达式：**&#x200B;用户管理重试同步失败的间隔。 （请参阅[配置目录同步重试选项](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)。）

   **群集作业锁定超时（分钟）：**&#x200B;在群集环境中使用。 如果一个节点上的同步失败且未释放群集锁定，此值指定另一个节点在强制获取锁定之前等待的分钟数。 默认值为`15`分钟。 有效值为`1`到`1440`分钟。

1. （可选）更改以下属性，然后单击&#x200B;**[!UICONTROL 确定]**：

   **用户管理器事件审核：**&#x200B;选择此选项可启用目录同步事件和身份验证事件（如成功、失败和锁定）的审核。 默认情况下，除非安装了需要审核的组件(如Rights Management)，否则不会选择此选项。 此设置将更新配置文件中的`APSAuditService`条目密钥。

   **自动创建动态组：**&#x200B;启用基于电子邮件域的自动创建动态组。 （请参阅[创建动态组](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)。）

您还可以通过单击重新加载还原为原始用户管理设置。
