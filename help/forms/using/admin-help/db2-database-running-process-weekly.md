---
title: DB2&reg；数据库：每周运行一个进程
description: 了解如何提高AEM Forms DB2&reg；数据库的性能。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
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
source-wordcount: '149'
ht-degree: 0%
---
# DB2®数据库：每周运行一个进程{#db-database-running-a-process-weekly}

如果AEM Forms DB2®数据库开始运行缓慢，则每周运行以下进程可以提高其性能：

1. 启动DB2®控制中心：

   (Windows)选择“开始”>“程序”>“® DB2®”>“常规管理工具”>“控制中心”。

   （Linux®和UNIX®）在命令提示符下，键入`db2jcc`命令。

1. 在DB2® Control Center对象树中，单击所有数据库。
1. 单击为AEM Forms创建的数据库，然后单击“表”文件夹。
1. 选择内容窗格中的所有数据库表，右键单击它们，然后选择运行统计信息。
1. 转到“统计信息”>“索引统计信息”。
1. 选择收集所有索引的统计信息，选择收集具有扩展详细统计信息的索引的统计信息，然后单击确定。

进程完成后，将显示一条消息。 关闭消息。
