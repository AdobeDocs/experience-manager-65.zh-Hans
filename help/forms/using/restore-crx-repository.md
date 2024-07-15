---
title: 无法恢复适用于JEE群集服务器的损坏的CRX存储库
description: 了解如何恢复损坏的CRX存储库的步骤。
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# 无法恢复损坏的CRX存储库 {#unable-to-restore-corrupt-crx-repository}

## 问题 {#issue}

对于使用关系数据库的JEE上的AEM Forms ，托管AEM Forms和关系数据库的计算机上的时间应始终绝对同步。 如果这些计算机上的时间不同步，则JEE服务器上的AEM Forms的CRX存储库可能会变得无法访问。 它可能已损坏，并且无法通过URL访问。 已记录`AuthenticationsupportService missing`错误。

## 先决条件 {#prerequisites}

在执行上述步骤之前，请备份CRX存储库。

## 解决方案 {#solution}

1. 转到`https://[AEM Forms Server]:[port]/system/console/bundles`。

1. 找到`oak-core`包并检查它是否正在运行。

1. 如果`oak-core`包未运行，请重新启动该包。 如果![暂停按钮](/help/forms/using/assets/stop.png)图标出现在`oak-core`包之前，则表示该包处于运行状态。

1. 如果问题仍未解决，请从备份中恢复CRX存储库，或者在备份不可用时重建CRX存储库。


## 应用于 {#applies-to}

此解决方案适用于JEE群集上的AEM Forms 。
