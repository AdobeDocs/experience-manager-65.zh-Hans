---
title: 在升级到MySQL的6.5.12.0时无法备份数据库。
description: 当用户升级到Experience Manager6.5.12.0并单击“升级MySQL”时，配置管理器无法备份以前的Experience Manager Forms数据库。
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
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

要解决此问题，请将数据库的max_packet_size增加到100 M，或者根据位于{AEM_HOME}/mysql的my.ini文件中的要求进行增加。
