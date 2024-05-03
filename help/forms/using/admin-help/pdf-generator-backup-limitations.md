---
title: PDF Generator备份限制
description: 了解PDF Generator备份限制。 PDF Generator使用的临时目录无法备份，因为它以设定的时间间隔清除内容。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
exl-id: a23db58d-1236-4689-93fc-dea508f8eb81
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 0%

---

# PDF Generator备份限制 {#pdf-generator-backup-limitations}

无法备份PDF Generator用于转换文件的临时目录。 即使服务已正确恢复，数据仍可能会丢失，因为PDF Generator会按设定的时间间隔查看和清除临时目录的内容。
