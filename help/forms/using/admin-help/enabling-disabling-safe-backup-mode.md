---
title: 启用和禁用安全备份模式
description: 在“备份设置”页上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。 了解如何启用和禁用安全备份模式。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# 启用和禁用安全备份模式 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在“备份设置”页上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。

当AEM Forms处于安全备份模式时，它会正常运行，只是它不会主动从GDS目录中删除文件。

>[!NOTE]
>
>设置此选项不会备份您的系统；它准备您的系统以进行备份。

## 启用安全备份模式 {#enable-safe-backup-mode}

1. 在管理控制台中，单击设置>核心系统设置>备份设置。
1. 在“备份设置”页上，选择“在安全备份模式下操作” ，然后单击“确定”。

>[!NOTE]
>
>如果系统已经在安全备份模式下运行，则单击“确定”时不会创建新的保留。

## 禁用安全备份模式 {#disable-safe-backup-mode}

1. 在管理控制台中，单击设置>核心系统设置>备份设置。
1. 在“备份设置”页上，取消选择“在安全备份模式下操作” ，然后单击“确定”。
