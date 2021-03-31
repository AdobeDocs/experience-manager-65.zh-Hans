---
title: 用于共享资产的专用文件夹
description: 了解如何在 [!DNL Adobe Experience Manager Assets] 中创建专用文件夹并与其他用户共享该文件夹，并为他们分配各种权限。
contentOwner: AG
role: 商务从业人员
feature: 协作
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 4%

---


# [!DNL Adobe Experience Manager Assets] {#private-folder}中的专用文件夹

您可以在[!DNL Adobe Experience Manager Assets]用户界面中创建专供您使用的专用文件夹。 您可以将此专用文件夹共享给其他用户，并为其分配各种权限。 根据您分配的权限级别，用户可以对文件夹执行各种任务，例如视图文件夹中的资产或编辑资产。

>[!NOTE]
>
>专用文件夹至少有一个具有“所有者”角色的成员。

## 创建和共享{#create-share-private-folder}专用文件夹

要创建和共享专用文件夹，请执行以下操作：

1. 在[!DNL Assets]控制台中，单击工具栏中的&#x200B;**[!UICONTROL 创建]**，然后从菜单中选择&#x200B;**[!UICONTROL 文件夹]**。

   ![创建资产文件夹](assets/Create-folder.png)

1. 在&#x200B;**[!UICONTROL 创建文件夹]**&#x200B;对话框中，输入文件夹的标题和名称（可选），然后选择&#x200B;**[!UICONTROL 专用]**&#x200B;选项。

1. 单击&#x200B;**[!UICONTROL 创建]**。将创建专用文件夹。

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. 要与其他用户共享文件夹以及为其分配权限，请选择文件夹，然后单击工具栏中的&#x200B;**[!UICONTROL 属性]**。

   ![信息选项](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >在您共享文件夹之前，该文件夹对任何其他用户都不可见。

1. 在&#x200B;**[!UICONTROL 文件夹属性]**&#x200B;页面中，从&#x200B;**[!UICONTROL 添加用户]**&#x200B;列表中选择用户，为专用文件夹中的用户分配角色，然后单击&#x200B;**[!UICONTROL 添加]**。

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >您可以向与其共享文件夹的用户分配各种角色，如`Editor`、`Owner`或`Viewer`。 如果您为用户分配了`Owner`角色，则用户对该文件夹具有`Editor`权限。 此外，用户还可以与他人共享文件夹。 如果您分配了`Editor`角色，则用户可以编辑您的专用文件夹中的资产。 如果您为用户分配了查看者角色，则用户只能视图您的专用文件夹中的资产。

   >[!NOTE]
   >
   >专用文件夹至少有一个具有`Owner`角色的成员。 因此，管理员无法从专用文件夹中删除所有所有者成员。 但是，要从专用文件夹中删除现有所有者（以及管理员本身），管理员必须将其他用户添加为所有者。

1. 单击&#x200B;**[!UICONTROL 保存]**。根据您分配的角色，当用户登录[!DNL Assets]时，将为用户分配一组针对您的专用文件夹的权限。
1. 单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭确认消息。
1. 您向用户共享文件夹时，用户会收到共享通知。使用用户凭据登录[!DNL Assets]以视图通知。

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. 单击[!UICONTROL 通知]以打开通知列表。

   ![通知列表](assets/Assets-Notification.png)

1. 单击管理员共享的专用文件夹条目以打开该文件夹。

>[!NOTE]
>
>要创建专用文件夹，您需要对要创建专用文件夹的父文件夹进行读取和修改[访问控制权限](/help/sites-administering/security.md#permissions-in-aem)。 如果您不是管理员，则默认情况下，`/content/dam`上不会为您启用这些权限。 在这种情况下，在尝试创建专用文件夹之前，请先获取您的用户ID/组的这些权限。

## 删除专用文件夹{#delete-private-folder}

您可以通过选择文件夹并从顶部菜单中选择[!UICONTROL 删除]选项，或使用键盘上的Backspace键来删除文件夹。

![顶部菜单中的“删除”选项](assets/delete-option.png)

>[!CAUTION]
>
>如果从CRXDE Lite中删除专用文件夹，则存储库中会保留冗余用户组。

>[!NOTE]
>
>如果使用上述方法从用户界面中删除文件夹，则关联的用户组也会被删除。
>
>但是，可以使用创作实例(`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`)中JMX中的`clean`方法，从存储库中删除现有的冗余、未使用和自动生成的用户组。
