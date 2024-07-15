---
title: 适用于AEM Forms的Adobe Experience Manager (AEM)桌面应用程序
description: 适用于AEM Forms的Adobe Experience Manager (AEM)桌面应用程序
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: manage
noindex: true
role: Admin,User
exl-id: b87e07b1-4a19-4888-bad0-c0f5327b9ad3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 适用于AEM Forms的Adobe Experience Manager (AEM)桌面应用程序 {#aem-desktop-app-for-aem-forms}

AEM桌面应用程序允许您将Adobe Experience Manager (AEM) Assets存储库和AEM Forms二进制文件映射到您系统中的网络目录。 您可以在文件资源管理器中查看同步的资源和二进制文件，并根据需要使用各种应用程序编辑文件。 除了查看文件之外，您还可以创建、上载和删除二进制文件。 您还可以直接从软件打开、编辑和保存文件。 例如，您可以直接从Designer打开和编辑XDP文件。 在本地对资源所做的更改将反映在AEM Assets存储库和AEM Forms用户界面中。

您可以从AEM实例下载应用程序。 有关下载应用的详细信息，请参阅[AEM桌面应用发行说明](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html?lang=en)。

## AEM桌面应用程序支持的AEM Forms资源 {#aem-forms-assets-supported-in-aem-desktop-app}

您可以使用应用程序同步以下类型的AEM Forms二进制文件：表单模板(.xdp)、PDF表单(.pdf)、文档(.pdf)、图像、XML架构(.xsd)、样式表(.xfs)。 应用程序会将所有其他文件（不受支持的文件）列为0字节文件。 将不受支持的文件列为0字节文件可确保用户了解AEM Forms服务器上存在其他可用的资源。

>[!NOTE]
>
>文件名只能包含字母数字字符、连字符或下划线。

## 为AEM桌面应用程序启用AEM Forms {#enable-aem-forms-for-aem-desktop-app}

AEM桌面应用程序在Microsoft®Windows上使用WebDAV协议，在macOS X上使用SMB1连接到AEM Forms服务器。 开箱即用的AEM Forms服务器无法使二进制文件和其他资源与WebDAV或SMB客户端同步。 执行以下步骤，以便为AEM桌面应用程序启用AEM Forms：

1. 以管理员身份登录到AEM Forms。
1. 在创作实例中，单击![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager >工具]** ![锤子](assets/hammer.png) **[!UICONTROL >部署>操作> Web控制台]**。 Web控制台将在新窗口中打开。
1. 在Web控制台窗口中，找到并打开&#x200B;**[!UICONTROL FormsManager加载项配置]**&#x200B;选项。
1. 在FormsManager加载项配置对话框中，取消选中&#x200B;**[!UICONTROL 异步同步资源]**&#x200B;复选框，然后单击&#x200B;**[!UICONTROL 保存]**。
1. 重新启动AEM Forms服务器。 重新启动后，将启用AEM Forms服务器以接受内容并与AEM桌面应用程序共享内容。
1. 打开应用程序并连接到AEM Forms服务器。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。

   成功连接后，应用将填充`content/dam`和`content/dam/formsanddocuments`文件夹。 除了将文件从上述文件夹移动到本地文件夹外，您还可以使用应用程序在自动填充的文件夹之间移动内容。
