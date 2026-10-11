---
title: 在升级到MySQL的6.5.12.0时无法备份数据库。
description: 当用户升级到Experience Manager 6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库。
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
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
source-wordcount: '102'
ht-degree: 11%
---
# 在升级到 6.5.12.0 时，MySQL 数据库备份失败 {#issue}

当用户升级到Experience Manager 6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库，它显示以下错误：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 应用到 {#applies-to}

* Experience Manager 6.5 Forms

## 解决办法 {#solution}

要解决此问题，请将数据库的max_packet_size增加到100 M，或者根据位于{AEM_HOME}/mysql的my.ini文件中的要求进行增加。
