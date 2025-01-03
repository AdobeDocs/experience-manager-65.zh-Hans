---
title: 为Microsoft SharePoint配置连接器
description: 配置适用于Microsoft SharePoint的连接器，以启用AEM表单与Microsoft SharePoint之间的通信。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 98cbaaf64c0268be1afe7196a7bbbf5c93f02148
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# 为Microsoft SharePoint配置连接器

>[!NOTE]
> 
> 确保用户具有访问管理员控制台的管理员权限。

Microsoft SharePoint的连接器支持在AEM表单与Microsoft SharePoint之间进行通信。 有关其他背景信息，请参阅[服务参考](https://www.adobe.com/go/learn_aemforms_services_63)中的“Connectors for ECM”。

1. 在管理控制台中，单击服务>Microsoft SharePoint的连接器。
2. 为您的SharePoint服务器指定以下设置：

   **SharePoint服务器主机名：** SharePoint服务器上Web应用程序的主机名端口号，格式为`[hostname]:'port'`。

   **用户名：**&#x200B;用于连接到SharePoint服务器的用户帐户。

   **密码：**&#x200B;用于连接到SharePoint服务器的用户帐户的密码

   **域名：** SharePoint服务器所在的域。

3. 单击“保存”。

## Microsoft SharePoint配置服务 {#microsoft-sharepoint-configuration-service}

Microsoft SharePoint配置服务`(MSSharePointConfigService)`允许您为具有模拟权限的AEM表单用户指定凭据。 有关模拟权限的信息，请参阅[配置Microsoft SharePoint的连接器](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html)。 按照以下步骤指定`MSSharePointConfigService`的设置：

1. 在管理控制台中，单击服务>应用程序和服务>服务管理。
1. 导航服务列表并单击`MSSharePointConfigService`。
1. 在“配置”页上指定以下设置：

   * 具有模拟权限的用户的用户名
   * 上述用户的密码

1. 单击“保存”。
