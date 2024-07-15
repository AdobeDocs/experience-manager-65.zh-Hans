---
title: 在AEM Forms应用程序中使用自动保存
description: 了解如何使用AEM Forms应用程序中的自动保存功能以避免数据丢失。
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 1603eef1-d7c8-47d3-8cfa-55ec3eaadd64
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 在AEM Forms应用程序中使用自动保存{#using-autosave-in-aem-forms-app}

当用户在Adobe Experience Manager Forms应用程序中输入数据时，自动保存功能会定期保存数据。 AEM Forms应用程序中的自动保存功能可帮助您避免在应用程序意外关闭时丢失数据。

您的应用程序可能会意外关闭：

* 如果设备由于电池电量不足而关闭
* 如果用户终止应用程序
* 如果发生意外崩溃

您可以指定应用程序保存输入数据的时间间隔。

>[!NOTE]
>
>谨慎选择自动保存频率。 频繁的自动保存操作可能会对设备的性能产生显着影响。

执行以下步骤以使用AEM Forms应用程序中的自动保存功能：

1. 登录到应用程序，然后导航到&#x200B;**设置>常规**。
1. 在“常规”屏幕中，使用&#x200B;**自动保存频率**选项选择您希望应用程序保存输入数据的间隔。
   [![设置自动保存频率](assets/using-autosave-freq-07.png)](assets/using-autosave-freq-07-1.png)

1. 当您重新启动应用程序并以同一用户登录时，系统会提示您使用“恢复未保存的任务”对话框恢复任务。 在“恢复未保存任务”对话框中单击&#x200B;**确定**&#x200B;以继续处理保存的任务。 您可以单击&#x200B;**取消**&#x200B;以删除与上次触发的自动保存对应的已保存数据，并开始处理新任务。

   单击&#x200B;**确定**后，任务会使用与应用程序崩溃之前触发的最新自动保存对应的数据恢复。 它包括表单数据和与任务关联的所有附件。
   [![正在恢复任务&#x200B;](assets/autosave-flow.png)](assets/using-autosave-freq-06.png)**A.**&#x200B;正在运行的表单&#x200B;**B.**&#x200B;应用程序已强制关闭&#x200B;**C.**&#x200B;应用程序已重新启动，并恢复未保存任务对话框&#x200B;**D.**&#x200B;已使用原始数据还原表单
