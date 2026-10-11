---
title: 启用和禁用安全备份模式
description: 在“备份设置”页面上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。 了解如何启用和禁用安全备份模式。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f0ab712f-ecd9-4be8-a7a5-fd1a7a8c9a0b
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
source-wordcount: '208'
ht-degree: 5%
---
# 启用和禁用安全备份模式 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

在“备份设置”页面上，您可以在安全备份模式下操作AEM表单，以便可靠地备份数据库和全局文档存储(GDS) (GDS)目录。

当AEM表单处于安全备份模式时，它会正常运行，只是它不会主动从GDS目录中删除文件。

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
