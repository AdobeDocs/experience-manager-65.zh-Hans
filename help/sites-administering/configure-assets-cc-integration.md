---
title: 配置AEM Assets与Experience Cloud的集成
description: 了解如何配置AEM Assets与Experience Cloud的集成。
contentOwner: AG
feature: Asset Management
role: User, Architect, Admin
exl-id: d167cf97-6829-45a7-ba46-2239d530b060
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---

# 配置AEM Assets与Experience Cloud的集成 {#configure-aem-assets-integration-with-experience-cloud-and-creative-cloud}

如果您是Adobe Experience Cloud客户，则可以将Adobe Experience Manager Assets中的资源与Adobe Creative Cloud同步，反之亦然。 您还可以将资源与Experience Cloud同步，反之亦然。 您可以通过[!DNL Adobe I/O]设置此同步。 [!DNL Adobe Marketing Cloud]的更新名称为[!DNL Adobe Experience Cloud]。

设置此集成的工作流是：

1. 使用公共网关在[!DNL Adobe I/O]中创建身份验证并获取应用程序ID。
1. 使用应用程序ID在AEM Assets实例上创建配置文件。
1. 使用此配置可同步您的资产。

在后端，AEM服务器通过网关验证您的配置文件，然后在Assets和Experience Cloud之间同步数据。

>[!NOTE]
>
>此功能在[!DNL Assets]中已弃用。 在[AEM和Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)中查找替换项。 如果您有任何疑问，请[联系Adobe客户支持](https://www.adobe.com/cn/account/sign-in.supportportal.html)。

<!-- Hiding this for now via cqdoc-16834.
![Flow of data when AEM Assets and Creative Cloud are integrated](assets/chlimage_1-48.png)

>[!NOTE]
>
>Sharing assets between Adobe Experience Cloud and Adobe Creative Cloud requires administrator privileges on the AEM instance.
-->

## 创建应用程序 {#create-an-application}

1. 登录到[https://legacy-oauth.cloud.adobe.io](https://legacy-oauth.cloud.adobe.io/)访问Adobe Developer网关接口。

   >[!NOTE]
   >
   >您需要管理员权限才能创建应用程序ID。

1. 从左窗格中，导航到&#x200B;**[!UICONTROL 开发人员工具]** > **[!UICONTROL 应用程序]**&#x200B;以查看应用程序列表。
1. 单击&#x200B;**[!UICONTROL 添加]** ![aem_assets_addcircle_icon](assets/aem_assets_addcircle_icon.png)以创建应用程序。
1. 从&#x200B;**[!UICONTROL 客户端凭据]**&#x200B;列表中，选择&#x200B;**[!UICONTROL 服务帐户（JWT断言）]**，这是用于服务器身份验证的服务器到服务器通信服务。

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. 指定应用程序的名称和可选说明。
1. 从&#x200B;**[!UICONTROL 组织]**&#x200B;列表中，选择要同步资产的组织。
1. 从&#x200B;**[!UICONTROL 作用域]**&#x200B;列表中，选择&#x200B;**[!UICONTROL dam-read]**、**[!UICONTROL dam-sync]**、**[!UICONTROL dam-write]**&#x200B;和&#x200B;**[!UICONTROL cc-share]**。
1. 单击&#x200B;**[!UICONTROL 创建]**。此时将显示一条消息，通知应用程序已创建。

   ![成功创建应用程序以将AEM Assets与Creative Cloud集成的通知](assets/chlimage_1-50.png)

1. 复制为新应用程序生成的&#x200B;**[!UICONTROL 应用程序ID]**。

   >[!CAUTION]
   >
   >请确保不会无意中复制&#x200B;**[!UICONTROL 应用程序密钥]**&#x200B;而非&#x200B;**[!UICONTROL 应用程序ID]**。

## 向Experience Cloud添加新配置 {#add-a-new-configuration}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧版Cloud Service]**。

1. 找到&#x200B;**[!UICONTROL Adobe Experience Cloud]**&#x200B;服务。 如果不存在配置，请单击&#x200B;**[!UICONTROL 立即配置]**。 如果存在配置，请单击&#x200B;**[!UICONTROL 显示配置]**，然后单击`+`以添加新配置。

   >[!NOTE]
   >
   >使用具有组织管理员权限的Adobe ID帐户。

1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，为新配置指定标题和名称，然后单击&#x200B;**[!UICONTROL 创建]**。

   ![命名新配置以集成AEM Assets和Creative Cloud](assets/aem-ec-integration-config1.png)

1. 在&#x200B;**[!UICONTROL 租户URL]**&#x200B;字段中，指定AEM Assets的URL。 过去，如果URL定义为`https://<tenant_id>.marketing.adobe.com`，请将其更改为`https://<tenant_id>.experiencecloud.adobe.com`。

   1. 导航到&#x200B;**工具>Cloud Service>旧版Cloud Service**。 在Adobe Experience Cloud下，单击&#x200B;**显示配置**。
   1. 选择要编辑的现有配置。 编辑配置并将`marketing.adobe.com`替换为`experiencecloud.adobe.com`。
   1. 保存配置。 测试MAC同步复制代理。

1. 在&#x200B;**[!UICONTROL 客户端ID]**&#x200B;字段中，粘贴您在过程[结束时复制的应用程序ID](#create-an-application)。

   ![提供集成AEM Assets和Creative Cloud所需的应用程序ID值](assets/cloudservices_tenant_info.png)

1. 在&#x200B;**[!UICONTROL 同步]**&#x200B;下，选择&#x200B;**[!UICONTROL 已启用]**&#x200B;以启用同步，然后单击&#x200B;**[!UICONTROL 确定]**。 如果选择&#x200B;**已禁用**，则同步将在单个方向上工作。

1. 在配置页面中，单击&#x200B;**[!UICONTROL 显示公钥]**&#x200B;以显示为您的实例生成的公钥。 或者，单击&#x200B;**[!UICONTROL 下载OAuth网关的公共密钥]**&#x200B;以下载包含公共密钥的文件。 然后，打开文件以显示公钥。

## 启用同步 {#enable-synchronization}

1. 使用过程[的最后一步中提到的以下方法之一显示公钥，向Experience Cloud](#add-a-new-configuration)添加新配置。 单击&#x200B;**[!UICONTROL 显示公钥]**。

1. 复制公钥并将其粘贴到您在[创建应用程序](#create-an-application)中创建的应用程序配置界面的&#x200B;**[!UICONTROL 公钥]**&#x200B;字段中。

   ![chlimage_1-53](assets/chlimage_1-53.png)

1. 单击&#x200B;**[!UICONTROL 更新]**。 立即将您的资源与AEM Assets实例同步。

## 测试同步 {#test-the-synchronization}

1. 单击本地AEM Assets实例用户界面上的AEM徽标，然后导航到&#x200B;**[!UICONTROL 工具]**> **[!UICONTROL 部署]**> **[!UICONTROL 复制]**以找到为同步创建的复制配置文件。
1. 在&#x200B;**[!UICONTROL 复制]**&#x200B;页面上，单击作者上的&#x200B;**[!UICONTROL 代理]**。
1. 从配置文件列表中，单击贵组织的默认复制配置文件以将其打开。
1. 在对话框中，单击&#x200B;**[!UICONTROL 测试连接]**。

   ![测试连接并为您的组织设置默认复制配置文件](assets/chlimage_1-54.png)

1. 复制恢复完成后，在测试结果结束时检查是否显示成功消息。

## 将用户添加到Experience Cloud {#add-users-to-experience-cloud}

1. 使用管理员凭据登录Experience Cloud。
1. 从边栏中，转到&#x200B;**[!UICONTROL 管理]**，然后单击&#x200B;**[!UICONTROL 启动Enterprise Dashboard]**。
1. 从边栏中，单击&#x200B;**[!UICONTROL 用户]**&#x200B;以打开&#x200B;**[!UICONTROL 用户管理]**&#x200B;页面。
1. 在工具栏中，单击&#x200B;**添加** ![aem_assets_add_icon](assets/aem_assets_add_icon.png)。
1. 添加一个或多个要提供与Creative Cloud共享资源的功能的用户。

<!-- TBD: Check.
   >[!NOTE]
   >
   >Only the users that you add to Experience Cloud can share assets from AEM Assets to Creative Cloud.

-->

## 在AEM Assets和Experience Cloud之间交换资源 {#exchange-assets-between-aem-and-experience-cloud}

1. 登录到AEM Assets。
1. 在Assets控制台中，创建一个文件夹并将一些资源上传到该文件夹。 例如，创建文件夹&#x200B;**mc-demo**&#x200B;并将资产上传到该文件夹。
1. 选择文件夹并单击&#x200B;**共享** ![assets_share](assets/do-not-localize/assets_share.png)。
1. 从菜单中选择&#x200B;**[!UICONTROL Adobe Experience Cloud]**，然后单击&#x200B;**[!UICONTROL 共享]**。 此时将显示一条消息，通知该文件夹已与Experience Cloud共享。

   >[!NOTE]
   >
   >在Adobe Experience Cloud中共享的上下文中不支持共享`sling:OrderedFolder`类型的Assets文件夹。 如果要共享文件夹，则在AEM Assets中创建该文件夹时，请勿选择&#x200B;**[!UICONTROL 已排序]**&#x200B;选项。

1. 刷新AEM Assets用户界面。 您在本地AEM Assets实例的Assets控制台中创建的文件夹将会复制到Experience Cloud用户界面。 在AEM服务器处理上传到AEM Assets中文件夹的资源后，该资源将显示在Experience Cloud中的文件夹副本中。
1. 您还可以在Experience Cloud中上传文件夹的已复制副本中的资产。 处理资源后，该资源将显示在AEM Assets的共享文件夹中。

<!-- Removing as per PM guidance via https://jira.corp.adobe.com/browse/CQDOC-16834?focusedCommentId=22881523&page=com.atlassian.jira.plugin.system.issuetabpanels:comment-tabpanel#comment-22881523.

## Exchange assets between AEM Assets and Creative Cloud {#exchange-assets-between-aem-assets-and-creative-cloud}

>[!CAUTION]
>
>The AEM to Creative Cloud Folder Sharing feature is deprecated. Customers are strongly advised to use newer capabilities, like [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) or [AEM desktop app](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html). Learn more in [AEM and Creative Cloud Integration Best Practices](/help/assets/aem-cc-integration-best-practices.md).

AEM Assets lets you share folders containing assets with Adobe Creative Cloud users.

1. In the Assets console, select the folder to share with Creative Cloud.
1. From the toolbar, click **[!UICONTROL Share]** ![assets_share](assets/do-not-localize/assets_share.png).
1. From the list, select the **[!UICONTROL Adobe Creative Cloud]** option.

   >[!NOTE]
   >
   >The options are available for users with read permissions on the root. Users must have the required permission to access the replication agent information of Marketing Cloud.

1. In the **[!UICONTROL Creative Cloud Sharing]** page, add the user to share the folder with and choose a role for the user. Click **[!UICONTROL Save]** and click **[!UICONTROL OK]**.

1. Log on to Creative Cloud with the credentials of the user you shared the folder with. The shared folder is available in Creative Cloud.

The AEM Assets-Marketing Cloud synchronization is designed in a way that the user machine instance from where the asset is uploaded retains the right to modify the asset. Only these changes are propagated to the other instance.

For example, if an asset is uploaded from an AEM Assets (on premises) instance, the changes to the asset from this instance are propagated to the Marketing Cloud instance. However, the changes done from the Marketing Cloud instance to the same asset aren’t propagated to the AEM instance and conversely for asset uploaded from Marketing Cloud.
-->

>[!MORELIKETHIS]
>
>* [Assets与Creative Cloud集成最佳实践](/help/assets/aem-cc-integration-best-practices.md)
