---
title: '"DB2数据库：每周运行进程”'
seo-title: "DB2 database: Running a process weekly"
description: 了解如何提高AEM Forms DB2数据库的性能。
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# DB2数据库：每周运行进程{#db-database-running-a-process-weekly}

如果您的AEM表单DB2数据库开始运行缓慢，则每周运行以下进程可以提高其性能：

1. 启动DB2控制中心：

   (Windows)选择“开始”>“程序”>“IBM DB2”>“一般管理工具”>“控制中心”。

   （Linux和UNIX）在命令提示符下，键入 `db2jcc` 命令。

1. 在DB2控制中心对象树中，单击“所有数据库”。
1. 单击为AEM表单创建的数据库，然后单击表文件夹。
1. 在“内容”窗格中选择所有数据库表，右键单击它们并选择“运行统计”。
1. 转到“统计”>“索引统计”。
1. 选择“收集所有索引的统计信息”，选择“收集具有扩展详细统计信息的索引的统计信息”，然后单击“确定”。

该过程完成后，会显示一条消息。 关闭消息。
