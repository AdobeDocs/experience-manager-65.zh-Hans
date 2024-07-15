---
title: 使用起点
description: 通过Workbench中定义的移动设备使用Adobe Experience Manager Forms进程的步骤。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: dd8748cee7a4b3ba91795a51928bd8590c47ef27
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


# 使用起点{#working-with-startpoints}

起点调用在Workbench中创建的进程。 它与表单相关联，该表单在提交表单时调用该流程。

>[!NOTE]
>
>在引用此概念时，术语起点、开始过程和形式可互换使用。

要从Adobe Experience Manager (AEM) Forms应用程序启动进程，您的进程必须具有类型为&#x200B;**Workspace**&#x200B;的起点。 此外，必须为起点选择&#x200B;**[!UICONTROL 在移动设备Workspace中可见]**&#x200B;选项。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**启动Workbench中定义的进程**

1. 若要查看AEM Forms应用程序中可用的起点，请转到[主屏幕](../../forms/using/home-screen.md)。
1. 在&#x200B;**[!UICONTROL 主页]**&#x200B;屏幕上，默认显示&#x200B;**[!UICONTROL 所有Forms]**&#x200B;列表。

   起点与表单相关联。 在列表中选择与表单关联的起点以将其打开。

   与起点关联的表单打开。

1. 在&#x200B;**[!UICONTROL 起点]**&#x200B;表单中输入详细信息。

   您可以使用[附件](../../forms/using/add-attachments.md)按钮向此任务添加注释。

1. 填写表单后，选择&#x200B;**[!UICONTROL 提交]**&#x200B;按钮。

如果应用程序处于离线状态，则表单及其数据将保存在“发件箱”文件夹中。

如果应用程序处于联机状态，则任务将与AEM Forms服务器同步，并分配给进程中指定的用户。

若要使用任务列表中的任务，请参阅[打开任务](/help/forms/using/open-task.md)。
