---
title: 编辑启动项
description: 为某个页面（或一组页面）创建启动项后，您可以在页面的启动项副本中编辑内容。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 21776f42-cd81-459d-b4b9-1d92e0aec164
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 7%

---

# 编辑启动项{#editing-launches}

## 编辑启动页面 {#editing-launch-pages}

为某个页面（或一组页面）创建启动项后，您可以在页面的启动项副本中编辑内容。

1. 打开页面进行编辑。
1. 在Sidekick中，选择&#x200B;**版本控制**&#x200B;选项卡，然后展开&#x200B;**启动项**&#x200B;组。 当前正在编辑的启动项的标题使用粗体字体。

   ![chlimage_1-13](assets/chlimage_1-13.jpeg)

1. 选择要处理的启动项，然后单击&#x200B;**切换**。
1. 开始编辑。

   >[!NOTE]
   >
   >您可以使用sidekick的&#x200B;**页面**&#x200B;选项卡执行&#x200B;**创建子页面**&#x200B;等操作。

## 编辑启动项配置 {#editing-a-launch-configuration}

创建启动项后，您可以更改启动项名称和启动项日期。 您还可以指定要与启动项关联的图像。

1. 打开启动项管理页面([http://localhost:4502/libs/launches/content/admin.html](http://localhost:4502/libs/launches/content/admin.html))。

1. 选择所需的启动项，然后单击&#x200B;**编辑**&#x200B;以打开对话框：

   * 在&#x200B;**常规**&#x200B;选项卡中，可以编辑：

      * **标题**
      * **上线日期**：该日期等于启动日期
      * **生产就绪**

     有关这些字段的用途和交互的信息，请参阅[启动项 — 事件的顺序](/help/sites-authoring/launches.md#launches-the-order-of-events)。

   * 在&#x200B;**图像**&#x200B;选项卡中，您可以上传图像文件。

1. 单击&#x200B;**保存**。

## 发现页面的启动状态 {#discovering-the-launch-status-of-a-page}

编辑页面的启动项时，有关该启动项的信息将显示在Sidekick的&#x200B;**版本控制**&#x200B;选项卡的底部：

* 启动项的名称。
* 自上次更改以来的时间。
* 执行上次更改的用户。
* **生产就绪**&#x200B;标志的状态（橙色=未设置；绿色=设置）。

![chlimage_1-186](assets/chlimage_1-186.png)
