---
title: 在升级到MySQL的6.5.12.0时无法备份数据库。
description: 当用户升级到Experience Manager6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库。
source-git-commit: a9d59e00efe8f0c2cbfca51901c441a2d65b70f2
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# 在升级到6.5.12.0 for MySQL时无法备份数据库 {#issue}

当用户升级到Experience Manager6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库，它显示以下错误：

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 应用于 {#applies-to}

* Experience Manager6.5 Forms

## 解决方案 {#solution}

要解决此问题，请将数据库的max_packet_size增加到100 M，或者根据位于的my.ini文件中的要求增加 {AEM_HOME}/mysql。