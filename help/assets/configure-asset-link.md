---
title: 为AdobeAsset Link配置Experience Manager Assets
description: 配置Experience Manager Assets以与用于Creative Cloud应用程序的AdobeAsset Link扩展一起使用。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3060'
ht-degree: 0%

---

# 为AdobeAsset Link配置Experience Manager Assets {#adobe-asset-link}

[AdobeAsset Link (AAL)](https://www.adobe.com/cn/creativecloud/business/enterprise/adobe-asset-link.html)简化了内容创建过程中创意专业人士与营销人员之间的协作。 它将Adobe Experience Manager Assets与Creative Cloud桌面应用程序Adobe InDesign、Adobe Photoshop和Adobe Illustrator连接起来。 AdobeAsset Link面板允许创意人员访问和修改存储在AEM Assets中的内容，而无需离开他们最熟悉的创意应用程序。

要配置要与Asset Link一起使用的Experience Manager Assets，请实施以下任务。 使用Experience Manager管理员帐户进行配置：

1. 根据需要安装包。 详细信息位于[先决条件](#prerequisites)中。

1. 手动配置[Experience Manager](#manual-configuration)，或使用[包](#configure-using-package)配置应用程序。

1. 若要将Creative Cloud授权用户与Experience Manager用户进行映射，请管理[用户访问控制](#user-access)。

1. 创建[自定义查询索引](#create-custom-index)，为InDesign配置[FPO呈现版本](/help/assets/configure-fpo-renditions.md)，配置[Adobe Stock集成](/help/assets/aem-assets-adobe-stock.md)，并配置[视觉或相似性搜索](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 各种功能的先决条件和支持 {#prerequisites}

确保根据需要安装适当的Service Pack和包。 有关每个Experience Manager版本和特定功能，请参阅以下要求。

| Assets功能 | Experience Manager版本和支持要求 |
|--- |--- |
| 默认情况下，Asset Link有效 | Experience Manager6.5和6.5.2或更高版本。 </br>Experience Manager6.4.4和6.4.6或更高版本。 </br>Adobe建议在使用AAL之前安装最新的[Experience ManagerService Pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)。 |
| Asset Link在安装包后工作 | 对于Experience Manager6.4.0 - 6.4.3，请安装[adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)包。 |
| Adobe Stock集成 | Experience Manager6.4.2或更高版本 |
| 视觉或相似性搜索 | Experience Manager6.5.0或更高版本 |


## 使用配置包配置Experience Manager {#configure-using-package}

Adobe建议您安装[adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config)配置包以自动执行大多数配置任务，然后再执行一些手动任务。 或者，您也可以[手动](#manual-configuration)配置。

>[!CAUTION]
>
>如果您的Experience Manager实例配置为使用Adobe IMS帐户进行用户登录，请不要使用配置包。 相反，[手动配置](#manual-configuration)Experience Manager实例。

1. 若要打开包管理器，请在Experience ManagerWeb界面中访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 包共享]**。 安装`adobe-asset-link-config`包。

1. 访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 找到&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供程序]**&#x200B;配置，然后单击以编辑它。

   设置以下属性并保存更改。

   * [!UICONTROL 组映射]：除非需要，否则留空。 有关详细信息，请参阅[组映射](#group-mapping)。
   * [!UICONTROL 组织]：输入您在Adobe Admin Console中使用的组织ID。 有关组织ID的详细信息，请参阅[创建用户组](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html)。

1. 找到&#x200B;**[!UICONTROL AdobeGranite Bearer身份验证处理程序]**&#x200B;配置，然后单击以进行编辑。

   将&#x200B;**[!UICONTROL InDesignAem2]**&#x200B;客户端ID添加到&#x200B;**[!UICONTROL 允许的OAuth客户端ID]**&#x200B;配置属性。


## 手动配置Experience Manager {#manual-configuration}

如果您选择不使用配置包，或者如果您的Experience Manager部署配置为支持使用Adobe IMS帐户进行用户登录，请手动配置Experience Manager。

要手动配置Experience Manager，请执行以下操作：

1. 要访问配置管理器，请访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 从顶部的菜单中选择&#x200B;**[!UICONTROL OSGi]** > **[!UICONTROL 配置]**。

1. 找到&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供程序]**&#x200B;配置，然后单击以编辑它。

   设置以下配置并单击&#x200B;**[!UICONTROL 保存]**。

   * [!UICONTROL 授权终结点]： ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 令牌终结点]： ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 配置文件终结点]： ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 验证URL]： ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 组织]：在[Adobe Admin Console](https://adminconsole.adobe.com/)中设置为组织ID。
   * [!UICONTROL 组映射]：除非您有特殊情况，否则留空。 有关详细信息，请参阅[组映射](#group-mapping)。

1. 找到&#x200B;**[!UICONTROL AdobeGranite Bearer身份验证处理程序]**&#x200B;配置，然后单击以进行编辑。

   将以下客户端ID添加到&#x200B;**[!UICONTROL 允许的OAuth客户端ID]**&#x200B;配置属性： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`。

   若要添加每个`Client ID`，请单击`+`。 添加所有ID后，单击&#x200B;**[!UICONTROL 保存]**。

1. 在&#x200B;**[!UICONTROL AdobeGranite OAuth应用程序和提供程序]**&#x200B;配置中，检查现有&#x200B;**[!UICONTROL AdobeGranite OAuth身份验证处理程序]**&#x200B;实例。 如果找到值为`ims`的`Config ID`实例，请将其用于此过程中的说明。 否则，请单击`+`创建配置实例。 设置以下属性值，然后单击&#x200B;**[!UICONTROL 保存]**。

   * [!UICONTROL 客户端ID]：不更改
   * [!UICONTROL 客户端密钥]：不更改
   * [!UICONTROL 配置ID]： ` ims`
   * [!UICONTROL 作用域]： `AdobeID, OpenID, read_organizations` （其他值可能也在配置中）
   * [!UICONTROL 提供程序ID]： ` ims`
   * [!UICONTROL 创建用户]： ` Checked`
   * 新创建的配置的[!UICONTROL 用户ID属性]： `Email`。 否则，请勿更改。

1. 找到具有&#x200B;**[!UICONTROL 同步处理程序名称]** `ims`的&#x200B;**[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**&#x200B;配置，然后单击以进行编辑。

   设置以下配置属性，然后单击&#x200B;**[!UICONTROL 保存]**。

   * [!UICONTROL 用户过期时间和用户成员资格过期]：“m”后面没有空格的时间（以分钟为单位）。 例如，`15m`持续15分钟。 有关详细信息，请参阅[组映射](#group-mapping)。
   * [!UICONTROL 用户自动成员资格]：不更改
   * [!UICONTROL 用户动态成员资格]： ` Deslect`

1. 找到&#x200B;**[!UICONTROL AdobeGranite OAuth身份验证处理程序]**&#x200B;配置，然后单击以进行编辑。 不进行任何更改，单击&#x200B;**[!UICONTROL 保存]**。

1. 要调整持有者身份验证处理程序的相对优先级，请在CRXDE中导航到`/apps/system/config`。 找到`com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config`并打开其配置。 最后，添加`service.ranking=I"-10"`。 保存更改。

   >[!NOTE]
   >
   >使用持有者令牌进行身份验证的每个请求都会产生对Adobe IMS的三次调用、Experience Manager同步以及创建登录令牌的开销。 为了克服此开销，AdobeAsset Link会捕获在来自Experience Manager的响应中返回的登录令牌，并将其与后续请求一起发送。 要使此进程正常工作，必须调整载体身份验证处理程序的相对优先级。

1. （可选）如果Experience Manager用户的电子邮件ID中包含大写或混合大小写的域名，请在Experience ManagerWeb控制台的&#x200B;**[!UICONTROL AdobeGranite ACP平台配置]**&#x200B;中选择&#x200B;**[!UICONTROL 将锁定用户更改为小写]**。

## 迁移到企业配置文件后的其他配置 {#configure-migration-activity}

AdobeAsset Link用户能够连接到Experience Manager，以允许从企业(CCE)组织的主Creative Cloud进行IMS登录。 Experience Manager使用客户端ID标识允许的IMS组织。 迁移到Business Profiles后，需要为IMS组织配置客户端ID和密钥，以Experience Manager持有者身份验证处理程序。 有关企业个人资料的详细信息，请参阅[Adobe个人资料简介](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html)。

仅当您使用其他Adobe IMS组织进行Experience Manager和企业Creative Cloud(CCE)并在这两个组织之间建立域信任关系时，才需要额外配置。

>[!NOTE]
>
>* Experience Manager6.5.11.0中提供了对Business Profiles的修复。
>* 如果您使用具有Experience Manager和CCE的相同Adobe IMS组织，则现有配置将继续有效。


**前提条件**

1. 为AAL配置了持有者身份验证且正在运行的Experience Manager实例。
1. 在Experience Manager6.5实例上安装以下包(Service Pack 11)。

   [下载Experience Manager6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 联系[!UICONTROL 客户支持]以获取IMS组织的持有者身份验证的客户端ID和密钥。

以下是迁移到Business Profiles后所需的其他配置：

1. 在&#x200B;**[!UICONTROL Adobe的Granite OAuth IMS配置提供程序]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)中，设置：

   * OAuth配置ID (`oauth.configmanager.ims.configid`)： `ims` （验证一次，您可能已配置它）

   * IMS所属实体(`ims.owningEntity`)：您的IMS组织ID

   ![IMS配置ID](assets/bearer-authentication1.png)

1. 打开&#x200B;**[!UICONTROL 持有者身份验证处理程序]**&#x200B;配置，并将从[!UICONTROL 客户支持]获得的客户端ID添加到&#x200B;**[!UICONTROL 允许的OAuth客户端ID]**&#x200B;的列表。

   ![添加客户端ID](assets/add-clientid-bearer-auth.png)

1. 打开&#x200B;**[!UICONTROL AdobeGranite OAuth应用程序和提供程序]**&#x200B;配置，并添加从客户支持获得的&#x200B;**[!UICONTROL 客户端ID]**&#x200B;和&#x200B;**[!UICONTROL 客户端密钥]**（密钥）。

   确保&#x200B;**[!UICONTROL 配置ID]**&#x200B;字段(`oauth.config.id`)包含的值与上面&#x200B;**[!UICONTROL OAuth配置ID]**&#x200B;字段(`oauth.configmanager.ims.configid`)中提供的值相同。

   ![验证客户端ID](assets/clientid-secretkey.png)

1. 打开&#x200B;**[!UICONTROL AdobeGranite IMS群集Exchange令牌预处理器]**&#x200B;配置并将其设置为`enable`。

## 管理用户访问控制 {#user-access}

本节介绍如何管理Experience Manager及其对“用户”存储库的访问权限。

### 组映射 {#group-mapping}

组映射确定Experience Manager中的组如何与Adobe IMS中的组相对应。 在授予AdobeAsset Link用户访问Experience Manager Assets的权限时，它起着重要作用。

与AdobeAsset Link一起使用时，Experience Manager将用户管理功能委派给Adobe IMS。 它会自动创建与Adobe IMS中的用户和组对应的用户和组。 此外，它还同步Experience Manager中的用户、组和组成员资格，以匹配Adobe IMS中的用户、组和组成员资格。

例如，考虑一个方案，其中AdobeAsset Link用户是Adobe IMS组assetlink-users的成员。 在这种情况下，当该Adobe IMS组中的用户首次连接到Experience Manager Asset Link时，将在Adobe中创建名为assetlink-users的同步组。 Adobe IMS组中的每个新用户在首次通过AdobeAsset Link连接到Experience Manager时，都会添加到Experience Manager中的相应组。

Experience Manager中与Adobe IMS中的组对应并同步的组可以直接被授予访问权限，也可以通过使其成为另一个组的成员。 下面是如何管理权限的示例。

![组示例](assets/group-examples.png)

以下规则适用于Experience Manager中的组映射：

* 确保&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供程序]**&#x200B;配置中的&#x200B;**[!UICONTROL 组映射]**&#x200B;属性为空。
* 在&#x200B;**[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**&#x200B;配置中的&#x200B;**[!UICONTROL Adobe过期时间]**&#x200B;属性中经过用户身份验证且经过一段时间后，将评估Asset Link用户组成员资格。 目前，可以在Experience Manager中的组中添加和删除用户，以与Adobe IMS中的内容同步。
* 避免组名冲突。 确保在Adobe IMS中创建的组(用于管理Experience Manager)的名称不同于所有用户系统组名称。

  例如，确保它们不同于`dam-users`组和Experience Manager管理员创建的组。

  如果某个Adobe IMS组的名称与Experience Manager系统组的名称或手动创建的组的名称冲突，则不会使用该IMS组来控制用户权限。
* 如果Adobe IMS用户连接到Experience Manager实例，并且在该实例中，用户的名称与之前创建的Experience Manager用户冲突，则会为Adobe IMS用户指定另一个名称，并添加编号以使其唯一。

**设置首次访问控制**

通过AdobeAsset Link连接的用户在获得所需的权限后，只能查看资源并与之交互。 上面[组映射](#group-mapping)部分讨论如何在Experience Manager中创建用户组，这些用户组对应于Adobe IMS中您组织中的用户组并与之同步。 建议Experience Manager管理员使用这些组来管理AdobeAsset Link用户的访问控制。

对于与Adobe IMS组(用于管理Experience Manager访问控制)同步的每个用户组：

1. 确保组具有可用于从AdobeAsset Link进行初始连接的成员。
1. 使用该用户登录到AdobeAsset Link，然后连接到Experience Manager。 此连接预期会失败。
1. 在Experience Manager中，找到与Adobe IMS中的组对应的组，并授予其所需的访问控制。 例如，新组成为dam-users组的成员。
1. 关闭AdobeAsset Link并重新启动Creative Cloud应用程序。
1. 要验证用户是否具有预期的访问权限，请重新打开AdobeAsset Link。

执行这些步骤后，同一组中的其他用户可以在第一次尝试时通过AdobeAsset Link连接到Experience Manager。 这些用户自动拥有与组中其他用户相同的权限。

## 管理Experience Manager用户以使用AdobeAsset Link {#manage-users}

AdobeAsset Link用户登录其Creative Cloud应用程序后，即可连接到Experience Manager。 此身份验证使用Adobe IMS技术，并在Experience Manager中创建用户信息（如果不存在）。 Experience Manager企业客户通常使用与Experience Manager集成的外部身份提供程序来管理其用户。 身份提供程序包括Adobe IMS以及使用SAML和LDAP协议的其他产品。 或者，也可以在Experience Manager中本地创建和管理用户。

如果符合以下条件，从AdobeAsset Link连接到Experience Manager的用户不会与上次直接登录时存储在Experience Manager中的现有用户信息发生冲突：

* 用于直接登录Experience Manager的所有用户名与Adobe IMS中用于Creative Cloud登录的用户名不同。
* Adobe IMS用作直接Experience Manager登录的身份提供程序。
* 用户先从AdobeAsset Link连接到Experience Manager，然后再使用同一帐户直接Experience Manager登录。


另一方面，在以下情形中，必须更新作为直接Experience Manager登录结果而创建的用户信息，才能与AdobeAsset Link一起使用：

* 相同的用户名（例如用户的电子邮件地址）会用于两者 — 使用Adobe IMS的Creative Cloud中的帐户，以及Adobe IMS以外的外部身份提供商中的帐户。
* 相同的用户名同时用于两者 — Creative Cloud中的帐户和本地Experience Manager帐户。
* Adobe IMS中的Creative Cloud帐户是Federated ID，它们由与Experience Manager集成以便直接登录的同一外部身份提供程序提供。

通过这些方案创建的用户没有与Adobe IMS同步的用户所需的属性。

要在Experience Manager更新此类用户以使用AdobeAsset Link，请执行以下操作：

1. 在Experience ManagerWeb控制台中，找到&#x200B;**[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]**&#x200B;配置，然后单击以进行编辑。 取消选中&#x200B;**[!UICONTROL 外部身份保护]**&#x200B;复选框，然后单击&#x200B;**[!UICONTROL 保存]**。
1. 若要在Experience Manager中访问“用户管理”界面，请导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**。 选择要更新的用户，然后记下该用户的浏览器URL路径末尾，从`/home/users`开始。 或者，您可以在CRXDE中搜索用户名。 示例用户路径： `/home/users/x/xTac082TDh-guJzzG7WM`。
1. 在CRXDE中，导航到用户路径，选择用户节点，并通过选择中下区域的&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡查看节点的属性。 此节点的`jcr:primaryType`属性值是`rep:User`。
1. 在&#x200B;**[!UICONTROL 属性]**&#x200B;选项卡区域的底部，输入`rep:externalId`的`Name`值、`String`的`Type`值和`rep:authorizableId`；`ims`的`Value`值，其中`rep:authorizableId`是节点的`rep:authorizableId`属性的值。 (使用分号（不带空格）将`rep:authorizableId`值与`ims`隔开。)
1. 单击新条目右侧的&#x200B;**[!UICONTROL 添加]**&#x200B;按钮，然后单击&#x200B;**[!UICONTROL 全部保存]**。
1. 对要升级以使用Asset Link的任何其他Adobe重复步骤2至5。
1. 在Experience ManagerWeb控制台中，找到&#x200B;**[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]**&#x200B;配置，然后单击以进行编辑。 取消选中&#x200B;**[!UICONTROL 外部身份保护]**&#x200B;复选框，然后单击&#x200B;**[!UICONTROL 保存]**。

>[!NOTE]
>
>如果服务在几分钟内未恢复，请重新启动Experience Manager以允许成功进行身份验证。

进行此更改后，更新的Experience Manager用户可以连接到AdobeAsset Link，并继续使用直接登录方法登录在更新之前使用的Experience Manager。 成功通过Adobe IMS身份验证后，Experience Manager用户配置文件信息将与Adobe IMS中的用户配置文件同步。

通过有一种方法，可以执行多个Experience Manager用户的批量迁移，以便他们能够使用AdobeAsset Link。 请联系Adobe关怀团队，了解有关启用此选项的更多信息和帮助。

作为这些步骤的替代方法，在某些情况下，可能会向AdobeAsset Link用户提供对Experience Manager的快速访问。 在这种情况下，预先存在的用户信息在与AdobeAsset Link建立连接之前通过Experience Manager用户管理或Experience ManagerCRXDE查找和删除。 新用户信息在连接之后在Experience Manager中创建。 只有在您确定没有重要数据添加为用户节点的子项时，才使用此方法。 此类额外数据是除`tokens`、`preferences`、`profile`、`profiles`、`profiles/public`和`rep:policy/*`节点之外的任何用户节点的子节点。

## 自动启动工作流以有条件地处理资产 {#auto-start-workflow}

在Experience Manager6.4和Experience Manager6.5中，管理员可以配置工作流以根据预定义条件自动执行和处理资源。

配置对于业务线用户和营销人员非常有用，例如在几个特定文件夹上创建自定义工作流。 假设某个机构照片拍摄的所有资产都可以添加水印，或者自由职业者上传的所有资产都可以经过处理以创建特定演绎版。

有关详细信息和Experience Manager配置，请参阅[对资源自动执行工作流](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets)。


## 在Experience Manager6.4.x版本中创建自定义索引 {#create-custom-index}

Experience Manager包含用于查询的索引。 为指定版本创建以下自定义索引。 默认情况下，Experience Manager6.5.0包含此索引。 AdobeAsset Link需要此索引来确定用户已签出的资产。

1. 在CRXDE中，找到`/oak:index`节点。 创建名为`cqDrivelock`的节点并将其`Type`设置为`oak:QueryIndexDefinition`。

1. 将以下属性添加到新节点并保存更改：

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 配置视觉或相似性搜索 {#configure-visual-similarity-search}

可视化搜索功能允许您使用Adobe资源链接面板，在AEM Assets存储库中搜索视觉上类似的资源。 该功能在6.5.0或更高版本中可用，并且只搜索索引资产。 有关详细信息，请参阅[如何配置可视化搜索](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 为Adobe InDesign生成“仅用于置入”演绎版 {#fpo-renditions}

Experience Manager提供仅用于置入(FPO)的演绎版。 这些FPO呈现版本的文件大小较小，但纵横比相同。 如果FPO演绎版不可用于某个资源，Adobe InDesign将改用原始资源。 此回退机制可确保创意工作流不间断地进行。 有关详细信息，请参阅[生成FPO演绎版](/help/assets/configure-fpo-renditions.md)。


## 与Adobe Stock集成 {#adobe-stock-integration}

组织将其Adobe Stock帐户与Experience Manager Assets集成。 它可帮助营销人员为其创意和营销项目提供授权的高质量、免版税的照片、矢量、插图、视频、模板和3D资产。 创意专业人士可以使用Asset Link面板来使用这些资源。

要与Adobe Stock集成，请参阅Experience Manager Assets中的[Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md)。 要与Adobe Stock集成，需要Experience Manager6.4.2或更高版本。


## Experience Manager相关问题疑难解答 {#troubleshoot}


如果您在配置或使用AdobeAsset Link时遇到问题，请尝试以下操作：

* 确保您的部署满足先决条件。 具体来说，请确保安装了相应的功能包或软件包。
* 联系贵组织的合作伙伴或系统集成商。
* 如果您的Creative Cloud用户无法在已签出的资产中进行验证，请检查电子邮件ID中域名的大小写。 若要修复，请参阅[手动配置](#manual-configuration)。
* 有关详细信息，请参阅[Asset Link疑难解答](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html)。


>[!MORELIKETHIS]
>
>* [关于 Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)
>* [在Creative Cloud桌面应用程序中使用Asset Link并管理资源](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [配置Adobe Experience Manager Assetsas a Cloud Service](https://helpx.adobe.com/cn/enterprise/using/configure-aem-assets-for-asset-link.html)。
