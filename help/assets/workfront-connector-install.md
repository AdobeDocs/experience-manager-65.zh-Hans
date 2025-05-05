---
title: 安装 [!DNL Workfront for Experience Manager enhanced connector]
description: 安装 [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
exl-id: 087bc811-e8f8-4db5-b066-627a9b082f57
hide: true
solution: Experience Manager, Workfront
source-git-commit: 5ccac0aadce3971e66da052d393cbd33b61e94f7
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# 安装[!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

在[!DNL Adobe Experience Manager]中具有管理员访问权限的用户安装增强型连接器。 安装之前，请查看平台支持以及连接器[&#128279;](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience)的其他先决条件。

>[!IMPORTANT]
>
>* Adobe仅需要通过认证合作伙伴或[!DNL Adobe Professional Services]来部署和配置[!DNL Adobe Workfront for Experience Manager enhanced connector]。 如果未使用认证合作伙伴或[!DNL Adobe Professional Services]进行部署和配置，则Adobe不支持该功能。
>
>* Adobe可能会发布使此连接器冗余的[!DNL Adobe Workfront]和[!DNL Adobe Experience Manager]更新；如果发生这种情况，客户可能需要从使用此连接器过渡。
>
>* Adobe支持增强型连接器版本1.7.4及更高版本。 不支持以前的预发行版和自定义版本。 要检查增强型连接器版本，请导航到[包管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=zh-Hans)的左窗格中可用的`digital.hoodoo`组。
>
>* 查看Experience Manager Assets增强型连接器的[Workfront合作伙伴认证考试](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html)。 有关考试的信息，请参阅[考试指南](https://express.adobe.com/page/Tc7Mq6zLbPFy8/)。

要安装连接器，请执行以下步骤：

1. 从[[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下载连接器。
1. [配置防火墙](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html)。
1. 在Dispatcher上，允许名为`authorization`、`username`和`apikey`的HTTP标头。 允许`GET`、`POST`和`PUT`请求发送给`/bin/workfront-tools`。
1. 确保[!DNL Experience Manager]存储库中不存在以下路径：

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. 使用[!UICONTROL 包管理器]安装包。 要了解如何安装包，请参阅[包管理器文档](/help/sites-administering/package-manager.md)。
1. 在[!DNL Experience Manager]用户组中创建`wf-workfront-users`并将权限`jcr:all`分配给`/content/dam`。
1. 向&#x200B;**`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**&#x200B;的开箱即用索引定义添加自定义属性。 执行以下步骤：
   * 将名为&#x200B;**`wfReferenceNumber`**&#x200B;的&#x200B;**`nt:unstructured`**&#x200B;属性添加到：

     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`。
   * 通过将重新索引标志翻转到`true`来重新索引`index /oak:index/ntFolderDamLucene`。

自动创建系统用户`workfront-tools`，并自动管理所需的权限。 [!DNL Workfront]中使用连接器的所有用户都自动添加为该组的一部分。

## 配置[!DNL Experience Manager]和[!DNL Workfront]之间的连接 {#configure-connection}

要创建与Workfront的连接，请执行以下步骤：

1. 在[!DNL Experience Manager]中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Workfront工具配置]**。

1. 在左侧面板中选择`workfront-tools`，然后在页面的右上角区域中选择&#x200B;**[!UICONTROL 创建]**&#x200B;选项。

1. 在&#x200B;**[!UICONTROL Workfront连接]**&#x200B;对话框中，提供[!DNL Workfront]部署所需的详细信息，然后选择&#x200B;**[!UICONTROL 连接到Workfront]**&#x200B;选项。 成功连接后，将在[!DNL Workfront]环境中自动创建[!DNL Workfront]文档自定义集成。

   ![连接[!DNL Experience Manager]和[!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. 要验证连接，请在[!DNL Workfront]中访问它，并验证API密钥是否相同，以及连接是否为&#x200B;**[!UICONTROL 已启用]**。 为此，请在[!DNL Workfront]中选择&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 文档]** > **[!UICONTROL 自定义集成]**。

## 更新[!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets允许您将[!DNL Workfront for Experience Manager enhanced connector]从以前的版本更新到最新的版本。

要将[!DNL Workfront for Experience Manager enhanced connector]更新到最新版本，请执行以下操作：

1. 从[[!DNL Software Distribution] 链接](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip)下载增强型连接器的最新版本。
1. 使用[!UICONTROL 包管理器]安装包。 要了解如何安装包，请参阅[包管理器文档](/help/sites-administering/package-manager.md)。
