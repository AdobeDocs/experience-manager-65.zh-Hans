---
title: Live Copy 概述控制台
seo-title: Live Copy Overview Console
description: 了解Live Copy概述控制台的基础知识。
seo-description: Learn about the basics of the Live Copy Overview Console.
uuid: 6b1841ec-950e-455b-9b30-b5f5050a67b8
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 3763e985-7dd8-47fd-bfdf-2368b424c270
feature: Multi Site Manager
exl-id: 0c3488bd-5f32-4956-882c-93326a45b379
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 28%

---

# Live Copy 概述控制台{#live-copy-overview-console}

的 **Live Copy概述** 允许您：

* 查看/管理站点中的继承：

   * 查看Blueprint树和相应的Live Copy结构及其继承状态
   * 更改继承状态；例如，暂停、继续
   * 查看Blueprint和Live Copy属性

* 执行转出操作

## 打开 Live Copy 概述 {#opening-the-live-copy-overview}

您可以从以下位置打开 Live Copy 概述：

* [Blueprint 页面（站点控制台）的引用侧面板](#opening-live-copy-overview-references-for-a-blueprint-page)
* [Blueprint 页面的属性](#opening-live-copy-overview-properties-of-a-blueprint-page)

### 打开Live Copy概述 — Blueprint页面的引用 {#opening-live-copy-overview-references-for-a-blueprint-page}

可以从&#x200B;**站点**&#x200B;控制台的&#x200B;**引用**&#x200B;侧面板打开 **Live Copy 概述**：

1. 在 **站点** 控制台， [导航到Blueprint页面并将其选中](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
1. 打开 **[引用](/help/sites-authoring/basic-handling.md#references)** 面板和选择 **Live Copy**.

   ![chlimage_1-359](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >您还可以先打开引用，然后选择蓝图。

1. 选择 **Live Copy概述** 显示和使用与选定Blueprint相关的所有Live Copy的概述。
1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

### 打开Live Copy概述 — Blueprint页面的属性 {#opening-live-copy-overview-properties-of-a-blueprint-page}

可以在查看 Blueprint 页面的属性时打开 **Live Copy 概述**：

1. 打开相应的 Blueprint 页面的&#x200B;**属性**。
1. 打开 **Blueprint** 选项卡 – **Live Copy 概述**&#x200B;选项将显示在顶部工具栏中：

   ![chlimage_1-360](assets/chlimage_1-360.png)

1. 选择 **Live Copy概述** 显示和使用与当前Blueprint相关的所有Live Copy的概述。

   >[!NOTE]
   >
   >有关更多详细信息，另请参阅知识库文章 [Live Copy状态消息 — 最新/绿色/同步](https://helpx.adobe.com/experience-manager/kb/livecopy-status-message---up-to-date-green-in-sync.html).

1. 使用&#x200B;**关闭**&#x200B;以退出，并返回到&#x200B;**站点**&#x200B;控制台。

## 使用 Live Copy 概述 {#using-the-live-copy-overview}

的 **Live Copy概述** 还可用于对live copy执行以下操作：

1. 打开 **Live Copy 概述**。
1. 选择所需的Blueprint或Live Copy页面 — 工具栏将更新以显示可用的操作。 的 [操作](/help/sites-administering/msm.md#terms-used) 可用取决于您是否选择 [Blueprint](#actions-for-a-blueprint-page) 或 [live copy](#actions-for-a-live-copy-page) 页面：

### 适用于 Blueprint 页面的操作 {#actions-for-a-blueprint-page}

在选择 Blueprint 页面时，以下操作可用：

![chlimage_1-361](assets/chlimage_1-361.png)

* 编辑

   * 打开Blueprint页面进行编辑。

* [转出](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 执行转出以将更改从源推送到Live Copy。

### 适用于 Live Copy 页面的操作 {#actions-for-a-live-copy-page}

选择Live Copy页面时，可以执行以下操作：

![chlimage_1-362](assets/chlimage_1-362.png)

* 编辑

   * 打开Live Copy页面进行编辑。

* [关系状态](#relationship-status)

   * 查看有关状态和继承的信息。

* [同步](/help/sites-administering/msm.md#rollout-and-synchronize)

   * 同步Live Copy以将更改从源拉入Live Copy。

* [重置](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * 重置Live Copy页面可删除所有继承取消，并将页面返回到与源页面相同的状态。

* [暂停](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * 临时停用Live Copy及其Blueprint页面之间的Live关系。

* [继续](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 恢复允许您恢复已暂停的关系。

* [分离](/help/sites-administering/msm.md#detaching-a-live-copy)

   * 永久删除Live Copy及其Blueprint页面之间的Live关系。

## 关系状态 {#relationship-status}

的 **关系状态** 控制台有两个选项卡，提供了一系列功能：

* [关系状态信息](#relationship-status-information)
* [Live Copy信息](#live-copy-information)

### 关系状态信息 {#relationship-status-information}

此选项卡提供了有关Blueprint与Live Copy之间关系状态的详细信息：

![chlimage_1-363](assets/chlimage_1-363.png)

### Live Copy信息 {#live-copy-information}

利用此选项卡，可查看和编辑Live Copy配置：

![chlimage_1-364](assets/chlimage_1-364.png)
