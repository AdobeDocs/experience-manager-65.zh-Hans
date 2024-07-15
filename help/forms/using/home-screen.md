---
title: 主屏幕
description: AEM Forms应用程序主屏幕的组件描述
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# 主屏幕{#home-screen}

登录AEM Forms应用程序时，您将被重定向到主屏幕。

## 默认主屏幕 {#default-home-screen}

默认情况下，主屏幕会显示所有表单，包括起点和任务(如果连接的服务器启用了AEM Forms Workflow)，以及关联的缩略图。 您可以在AEM Forms服务器中指定缩略图。

下图在默认的“主页”屏幕上用重要组件的标注进行注释。

![Forms应用程序主屏幕](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **菜单按钮**：选择&#x200B;**菜单**&#x200B;按钮以导航到“任务”、“Forms”、“发件箱”和“设置”。 如果您的AEM Forms应用程序已连接到AEM Forms JEE服务器，则可以看到任务选项。 “任务”选项还存储从进程中的任务创建的草稿。 对于AEM Forms OSGi服务器，任务选项是隐藏的。 Outbox在与服务器同步之前存储已保存的表单和草稿。 当应用程序与服务器](../../forms/using/sync-app.md)进行[同步时，发件箱中所有保存的表单和草稿都将上载到AEM Forms服务器。 有关设置的信息，请参阅[更新常规设置](../../forms/using/update-general-settings.md)。
1. **任务或表单**：选择列出的要处理的任务或表单。
1. **水平省略号**：表示操作对表单可用。 点按省略号会显示作者提供的操作和描述。 选择省略号时，**删除草稿**&#x200B;和&#x200B;**完成**&#x200B;选项可见。
1. **刷新图标**：选择刷新图标，以便您可以将应用程序与AEM Forms服务器同步。

### 自定义主屏幕 {#customizing-the-home-screen}

![常规设置](assets/gen-settings.png)

您可以从应用程序的&#x200B;**[常规设置](../../forms/using/update-general-settings.md)**&#x200B;或HTMLWorkspace上的&#x200B;**首选项**&#x200B;选项卡更改应用程序的默认主屏幕。

对应用程序上的主屏幕设置所做的更改会影响当前登录用户或当前移动设备上的用户的主屏幕。

但是，在HTMLWorkspace中所做的更改将会影响登录到AEM Forms服务器的所有AEM Forms应用程序用户。
