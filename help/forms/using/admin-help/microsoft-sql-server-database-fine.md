---
title: Microsoft SQL Server 数据库：优化配置
description: 了解如何微调Microsoft SQL Server数据库的配置。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
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
source-wordcount: '299'
ht-degree: 5%
---
# Microsoft SQL Server 数据库：优化配置 {#microsoft-sql-server-database-fine-tuning-the-configuration}

在使用Microsoft SQL Server时，您应该更改默认配置设置。 在Oracle Enterprise Manager中右键单击本地服务器以访问属性对话框。

## 内存设置 {#memory-settings}

将最小内存分配更改为尽可能大的数字。 如果数据库在单独的计算机上运行，请使用所有内存。 默认设置不会积极分配内存，这几乎会阻碍任何数据库的性能。 在生产计算机上分配内存时应尽可能积极。

## 处理器设置 {#processor-settings}

修改处理器设置，最重要的是，选中Boost SQL Server Priority On Windows复选框，以便服务器使用尽可能多的周期。 “使用NT光纤”设置不太重要，但您也可以选择它。

## 数据库设置 {#database-settings}

更改数据库设置。 最重要的设置是“恢复时间间隔”，它指定崩溃后等待恢复的最长时间。 默认设置为1分钟。 使用较大的值（从5分钟到15分钟）可以提高性能，因为它使服务器有更多的时间将更改从数据库日志写回数据库文件。

>[!NOTE]
>
>此设置不会影响事务性行为，因为它仅更改启动时必须执行的日志文件重放的长度。

将日志和数据文件的空间分配大小设置为比初始数据库大得多。 考虑数据库在一年中的增长量。 理想情况下，日志和数据文件以连续的方式分配，这样数据就不会最终分散到整个磁盘上。
