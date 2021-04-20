---
title: Microsoft Dynamics OData配置
seo-title: Microsoft Dynamics ODta配置
description: 通过表单数据模型利用、集成和使用在线和内部部署的Microsoft Dynamics服务。
seo-description: 了解如何通过表单数据模型利用集成并与在线和内部部署的Microsoft Dynamics服务一起使用。
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---


# Microsoft Dynamics OData配置{#microsoft-dynamics-odata-configuration}

![数据整合](assets/data-integeration.png)

Microsoft Dynamics是一款客户关系管理(CRM)和企业资源规划(ERP)软件，为创建和管理客户帐户、联系人、潜在客户、机会和案例提供企业解决方案。 [AEM Forms Data ](../../forms/using/data-integration.md) Integration提供OData云服务配置，以将Forms与联机和本地Microsoft Dynamics服务器集成。它使您能够基于Microsoft Dynamics服务中定义的实体、属性和服务创建表单数据模型。 表单数据模型可用于创建与Microsoft Dynamics服务器交互的自适应表单，以支持业务工作流。 例如：

* 查询Microsoft Dynamics Server以获取数据并预填充自适应表单
* 在自适应表单提交时将数据写入Microsoft Dynamics
* 通过表单数据模型中定义的自定义实体在Microsoft Dynamics中写入数据，反之亦然

AEM Forms加载项包还包含参考OData配置，您可以利用这些配置将Microsoft Dynamics与AEM Forms快速集成。

安装包后，您的AEM Forms实例上提供以下实体和服务：

* MS Dynamics ODataCloud Service（OData服务）
* 使用预配置的Microsoft Dynamics实体和服务表单数据模型。

仅在AEM实例的运行模式设置为`samplecontent`（默认）时，表单数据模型中预配置的Microsoft Dynamics实体和服务才可用于您的AEM Forms实例。 MS Dynamics ODataCloud Service（OData服务）也可用于其他运行模式。 有关为AEM实例配置运行模式的详细信息，请参阅[运行模式](/help/sites-deploying/configure-runmodes.md)。

## 前提条件 {#prerequisites}

在开始设置和配置Microsoft Dynamics之前，请确保您拥有：

* 已安装[AEM Forms加载项包](../../forms/using/installing-configuring-aem-forms-osgi.md)
* 已联机配置Microsoft Dynamics 365，或已安装下列Microsoft Dynamics版本之一的实例：

   * Microsoft Dynamics 365内部部署
   * Microsoft Dynamics 2016内部部署

* [已向Microsoft Azure Active Directory注册Microsoft Dynamics在线服务的应用程序](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)。记下注册服务的客户端ID(也称为应用程序 ID)和客户端密码的值。 这些值在[配置Microsoft Dynamics服务](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service)的云服务时使用。

## 为已注册的Microsoft Dynamics应用程序{#set-reply-url-for-registered-microsoft-dynamics-application}设置回复URL

请执行以下操作，为注册的Microsoft Dynamics应用程序设置回复URL:

>[!NOTE]
>
>仅在将AEM Forms与联机Microsoft Dynamics服务器集成时使用此过程。

1. 转到Microsoft Azure Active Directory帐户，在注册应用程序的&#x200B;**回复URL**&#x200B;设置中添加以下云服务配置URL:

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure目录](assets/azure_directory_new.png)

1. 保存配置。

## 为IFD {#configure-microsoft-dynamics-for-ifd}配置Microsoft Dynamics

Microsoft Dynamics使用基于声明的身份验证向外部用户提供对Microsoft Dynamics CRM服务器上数据的访问。 要启用此功能，请执行以下操作，为面向Internet的部署(IFD)配置Microsoft Dynamics并配置声明设置。

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时使用此过程。

1. 如[为Microsoft Dynamics](https://technet.microsoft.com/en-us/library/dn609803.aspx)配置IFD中所述，为IFD配置Microsoft Dynamics本地实例。
1. 使用Windows PowerShell运行以下命令，在启用IFD的Microsoft Dynamics上配置声明设置：

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   有关详细信息，请参阅[CRM本地(IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd)的应用程序注册。

## 在AD FS计算机{#configure-oauth-client-on-ad-fs-machine}上配置OAuth客户端

执行以下操作，在Active Directory联合身份验证服务(AD FS)计算机上注册一个OAuth客户端并授予对AD FS计算机的访问权限：

>[!NOTE]
>
>仅在将AEM Forms与本地Microsoft Dynamics服务器集成时使用此过程。

1. 运行以下命令：

   `Add-AdfsClient -ClientId “<Client-ID>” -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   地点：

   * `Client-ID` 是您可以使用任何GUID生成器生成的客户端ID。
   * `redirect-uri` 是AEM Forms上Microsoft Dynamics OData云服务的URL。随AEM Forms包一起安装的默认云服务将部署在以下URL:
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. 运行以下命令以授予对AD FS计算机的访问权限：

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier “<Client-ID>” -ServerRoleIdentifier <resource> -ScopeNames openid`

   地点：

   * `resource` 是Microsoft Dynamics组织URL。

1. Microsoft Dynamics使用HTTPS协议。 要从Forms服务器调用AD FS终结点，请使用运行AEM Forms的计算机上的`keytool`命令将Microsoft Dynamics站点证书安装到Java证书存储区。

## 为Microsoft Dynamics服务{#configure-cloud-service-for-your-microsoft-dynamics-service}配置云服务

**MS Dynamics ODataCloud Service（OData服务）**&#x200B;配置随默认OData配置一起提供。 要将其配置为与Microsoft Dynamics服务连接，请执行以下操作。

1. 导航到&#x200B;**[!UICONTROL 工具>Cloud Services>数据源]**，然后点按`global`配置文件夹。
1. 选择&#x200B;**MS Dynamics ODataCloud Service（OData服务）**&#x200B;配置，然后点按&#x200B;**[!UICONTROL 属性]**。 将打开云服务配置属性对话框。

   在&#x200B;**身份验证设置**&#x200B;选项卡中：

   1. 输入&#x200B;**服务根**&#x200B;字段的值。 转到Dynamics实例，然后导航到&#x200B;**Developer Resources**&#x200B;以视图“服务根”字段的值。 例如，https://&lt;tenant-name>/api/data/v9.1/

   1. 替换&#x200B;**客户端ID**(也称为&#x200B;**应用程序 ID**)、**客户端机密**、**OAuth URL**、**刷新令牌URL**、**中的默认值访问令牌URL**&#x200B;和&#x200B;**资源**&#x200B;字段，其值来自您的Microsoft Dynamics服务配置。 必须在&#x200B;**资源**&#x200B;字段中指定dynamics实例URL，才能使用表单数据模型配置Microsoft Dynamics。 使用服务根URL派生Dynamics实例URL。 例如，[https://org.crm.dynamics.com](https://org.crm.dynamics.com/)。

   1. 在&#x200B;**授权范围**&#x200B;字段中指定&#x200B;**openid**，以便在Microsoft Dynamics上进行授权过程。

   ![身份验证设置](assets/dynamics_authentication_settings_new.png)

1. 单击&#x200B;**[!UICONTROL 连接到OAuth]**。 您将被重定向到Microsoft Dynamics登录页面。
1. 使用您的Microsoft Dynamics凭据登录并接受，以允许云服务配置连接到Microsoft Dynamics服务。 在云服务与服务之间建立连接是一次性任务。

   然后，您将被重定向到云服务配置页，该页显示一条消息，显示OData配置已成功保存。

MS Dynamics ODataCloud Service（OData服务）云服务已配置并与您的Dynamics服务连接。

## 创建表单数据模型{#create-form-data-model}

安装AEM Forms包时，将在AEM实例上部署表单数据模型&#x200B;**Microsoft Dynamics FDM**。 默认情况下，表单数据模型使用在MS Dynamics ODataCloud Service（OData服务）中配置的Microsoft Dynamics服务作为其数据源。

首次打开表单数据模型时，它将连接到已配置的Microsoft Dynamics服务，并从Microsoft Dynamics实例中提取实体。 Microsoft Dynamics的“联系人”和“潜在客户”实体已添加到表单数据模型中。

要查看表单数据模型，请转到&#x200B;**[!UICONTROL Forms >数据集成]**。 选择&#x200B;**Microsoft Dynamics FDM**&#x200B;并单击&#x200B;**编辑**&#x200B;以在编辑模式下打开表单数据模型。 或者，您也可以从以下URL直接打开表单数据模型：

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

接下来，您可以基于表单数据模型创建一个自适应表单并将其用于各种自适应表单用例，例如：

* 通过从Microsoft Dynamics实体和服务查询信息预填自适应表单
* 使用自适应表单规则调用在表单数据模型中定义的Microsoft Dynamics服务器操作
* 将提交的表单数据写入Microsoft Dynamics实体

建议创建随AEM Forms包提供的表单数据模型副本，并配置数据模型和服务以满足您的要求。 它将确保将来对程序包的任何更新不会覆盖表单数据模型。

有关在业务工作流中创建和使用表单数据模型的详细信息，请参阅[数据集成](../../forms/using/data-integration.md)。
