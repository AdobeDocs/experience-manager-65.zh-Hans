---
title: 安装功能包18912以进行批量资源迁移
description: 功能包18912允许您通过FTP批量摄取资源，或将资源从Dynamic Media Classic迁移到Adobe Experience Manager上的Dynamic Media中。 Adobe支持部门提供了此可选功能包。
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 53ea2cf7-d633-4ab9-a869-ce76eb1c01e5
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%
---
# 安装功能包18912以进行批量资源迁移{#installing-feature-pack-for-bulk-asset-migration}

功能包18912的安装是&#x200B;*可选*。

功能包18912允许您通过FTP将资源直接批量摄取到Adobe Experience Manager上的Dynamic Media - Scene7模式。 它还允许您将资源从Dynamic Media Classic迁移到Experience Manager上的Dynamic Media - Scene7模式。 此功能包可从[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)获得。

>[!IMPORTANT]
>
>您可以使用功能包在Experience Manager中自行将资产从Dynamic Media Classic批量迁移到Dynamic Media - Scene7模式。 您也可以使用Dynamic Media Classic中的FTP功能批量迁移资源。 但是，由于涉及的复杂性，Adobe并&#x200B;*不*&#x200B;建议您使用这两种方法中的任何一种。
>
>因此，在通过[Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html)完成迁移项目时，此迁移功能包仅&#x200B;*支持*。

在安装功能包之前，请创建服务用户并将该信息提供给Adobe支持。

另请参阅[配置Dynamic Media - Scene7模式](/help/assets/config-dms7.md)。

**要安装用于批量资源迁移的功能包18912：**

1. 在您的Experience Manager实例中，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**，然后选择&#x200B;**[!UICONTROL 创建用户]**。 此服务用户必须具有对`/content/dam.`的&#x200B;*读/写*&#x200B;权限
1. 在&#x200B;**[!UICONTROL ID]**&#x200B;和&#x200B;**[!UICONTROL 密码]**&#x200B;字段中，输入用户名和密码；例如，**FTP用户**。 此名称将以创建资产的用户的身份显示在时间轴中。 从FTP上传资源时，如果资源上传到FTP服务器并推送到Experience Manager，则会认为该资源已创建。
1. 联系[Experience Manager的Adobe客户支持](https://experienceleague.adobe.com/?support-solution=General#support)以请求访问功能包18912以供下载。 当您联系支持人员时，可能需要以下信息：

   * 创作实例的服务器IP地址，包括端口号（默认情况下，端口号为4502）。
   * 上一步中的Experience Manager服务用户用户名和密码。

1. Experience Manager的Adobe客户支持为您提供FTP凭据以及功能包18912的访问权限。
1. 当您收到功能包18912时，请安装它。

   有关在Experience Manager中使用软件分发和包的详细信息，请参阅[如何使用包](/help/sites-administering/package-manager.md)。
