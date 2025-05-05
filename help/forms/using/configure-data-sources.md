---
title: 配置数据源
description: 了解如何配置不同类型的数据源，以便创建表单数据模型。
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 1%

---

# 配置数据源{#configure-data-sources}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |


![数据集成](do-not-localize/data-integeration.png)

通过AEM Forms数据集成，您可以配置并连接到不同的数据源。 支持开箱即用的以下类型。 但是，只需少量自定义，您也可以集成其他数据源。

* 关系数据库 — MySQL、Microsoft SQL Server、IBM DB2、OracleRDBMS、postgreSQL和Sybase
* AEM用户配置文件
* RESTful Web服务
* 基于SOAP的Web服务
* OData服务

数据集成支持现成的OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证和API密钥身份验证类型，并允许实施自定义身份验证以访问Web服务。 虽然在AEMCloud Service中配置了RESTful、基于SOAP和OData服务，但在AEM Web控制台中配置了关系数据库的JDBC和AEM用户配置文件的连接器。

## 配置关系数据库 {#configure-relational-database}

可以使用AEM Web Console配置来配置关系数据库。 执行以下操作：

1. 转到位于`https://server:host/system/console/configMgr`的AEM Web控制台。
1. 查找&#x200B;**[!UICONTROL Apache Sling Connection Pooled DataSource]**&#x200B;配置。 选择以在编辑模式下打开配置。
1. 在配置对话框中，指定要配置的数据库的详细信息，例如：

   * 数据源的名称
   * 存储数据源名称的数据源服务属性
   * JDBC驱动程序的Java类名
   * JDBC连接URI
   * 用于与JDBC驱动程序建立连接的用户名和密码

   >[!NOTE]
   >
   >在配置数据源之前，请确保对密码等敏感信息进行加密。 要加密：
   >
   > 1. 转到https://&#39;[服务器]：[端口]&#39;/system/console/crypto。
   > 1. 在&#x200B;**[!UICONTROL 纯文本]**&#x200B;字段中，指定要加密的密码或任何字符串，然后选择&#x200B;**[!UICONTROL Protect]**。
   >
   >加密文本将显示在可在配置中指定的受保护文本字段中。

1. 启用&#x200B;**[!UICONTROL 借入时测试]**&#x200B;或&#x200B;**[!UICONTROL 返回时测试]**，以指定在分别从池借入或返回池之前，验证对象。
1. 在&#x200B;**[!UICONTROL 验证查询]**&#x200B;字段中指定SQL SELECT查询以验证来自池的连接。 查询必须至少返回一行。 根据您的数据库，指定以下选项之一：

   * SELECT 1 （MySQL和MS SQL）
   * 从双选件中选择1(Oracle)

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

   >[!NOTE]
   >
   > 如果Forms数据模型包含的对象是关系数据库的保留关键字，则可能会导致数据添加、更新或检索问题。 因此，请避免在表单数据模型中使用此类对象。

## 配置AEM用户配置文件 {#configure-aem-user-profile}

您可以使用AEM Web Console中的用户配置文件连接器配置来配置AEM用户配置文件。 执行以下操作：

1. 转到https://&#39;[server]：[port]&#39;system/console/configMgr上的AEM Web控制台。
1. 查找&#x200B;**[!UICONTROL AEM Forms数据集成 — 用户配置文件连接器配置]**，然后选择以在编辑模式下打开该配置。
1. 在“用户配置文件连接器配置”对话框中，可以添加、删除或更新用户配置文件属性。 指定的属性可用于表单数据模型。 使用以下格式指定用户配置文件属性：

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   示例：

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >上例中的&#x200B;**&#42;**&#x200B;表示CRXDE结构中AEM用户配置文件中`profile/empLocation/`节点下的所有节点。 这意味着表单数据模型可以访问`profile/empLocation/`节点下的任何节点中存在的类型为`string`的`city`属性。 但是，包含指定属性的节点必须遵循一致结构。

1. 选择&#x200B;**[!UICONTROL 保存]**&#x200B;以保存配置。

## 为云服务配置配置文件夹 {#cloud-folder}

>[!NOTE]
>
>配置RESTful、SOAP和OData服务的云服务需要配置云服务文件夹。

AEM中的所有云服务配置都已合并到AEM存储库的`/conf`文件夹中。 默认情况下，`conf`文件夹包含`global`文件夹，您可以在其中创建云服务配置。 但是，您需要为云配置手动启用它。 您还可以在`conf`中创建其他文件夹以创建和组织Cloud Service配置。

要为云服务配置配置文件夹，请执行以下操作：

1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   * 有关详细信息，请参阅[配置浏览器](/help/sites-administering/configurations.md)文档。
1. 执行以下操作可为云配置启用全局文件夹，或跳过此步骤为云服务配置创建和配置其他文件夹。

   1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，选择`global`文件夹并选择&#x200B;**[!UICONTROL 属性]**。

   1. 在&#x200B;**[!UICONTROL 配置属性]**&#x200B;对话框中，启用&#x200B;**[!UICONTROL 云配置]**。

   1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置并退出对话框。

1. 在&#x200B;**[!UICONTROL 配置浏览器]**&#x200B;中，选择&#x200B;**[!UICONTROL 创建]**。
1. 在&#x200B;**[!UICONTROL 创建配置]**&#x200B;对话框中，指定文件夹的标题并启用&#x200B;**[!UICONTROL 云配置]**。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建为云服务配置启用的文件夹。

## 配置RESTful Web服务 {#configure-restful-web-services}

在Swagger定义文件中，可以使用JSON或YAML格式的[Swagger规范](https://swagger.io/specification/)来描述RESTful Web服务。 要在AEM云服务中配置RESTful Web服务，请确保您的文件系统上有Swagger文件或托管该文件的URL。

执行以下操作以配置RESTful服务：

1. 转到&#x200B;**[!UICONTROL 工具>Cloud Service>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL RESTful服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为RESTful服务指定以下详细信息：

   * 从Swagger Source下拉列表中选择URL或文件，并相应地指定Swagger定义文件的Swagger URL或从本地文件系统上传Swagger文件。
   * 根据Swagger Source输入，以下字段已预填充值：

      * 方案：REST API使用的传输协议。 下拉列表中显示的方案类型数取决于Swagger源中定义的方案。
      * 主机：提供REST API的主机的域名或IP地址。 它是必填字段。
      * 基本路径：所有API路径的URL前缀。 它是一个可选字段。\
        如有必要，请编辑这些字段的预填充值。

   * 选择身份验证类型 — None、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证、API密钥、自定义身份验证或相互身份验证 — 以访问RESTful服务，并相应地提供身份验证的详细信息。

   如果选择&#x200B;**[!UICONTROL API密钥]**&#x200B;作为身份验证类型，请指定API密钥的值。 API密钥可作为请求标头或查询参数发送。 从&#x200B;**[!UICONTROL 位置]**&#x200B;下拉列表中选择其中一个选项，并在&#x200B;**[!UICONTROL 参数名称]**&#x200B;字段中相应地指定标头名称或查询参数。

   如果选择&#x200B;**[!UICONTROL 相互身份验证]**&#x200B;作为身份验证类型，请参阅[RESTful和SOAP Web服务的基于证书的相互身份验证](#mutual-authentication)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建RESTful服务的云配置。

### 表单数据模型HTTP客户端配置可优化性能 {#fdm-http-client-configuration}

由于数据源包括用于性能优化的HTTP客户端配置，因此，在与RESTful Web服务集成时，[!DNL Experience Manager Forms]会形成数据模型。
执行以下步骤以配置表单数据模型HTTP客户端：

1. 以管理员身份登录到[!DNL Experience Manager Forms]创作实例并转到[!DNL Experience Manager] Web控制台包。 默认URL为[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)。

1. 为REST数据源&#x200B;**选择**&#x200B;表单数据模型Http客户端配置。

1. 在[!UICONTROL REST数据源]的表单数据模型HTTP客户端配置对话框中：

   * 在&#x200B;**[!UICONTROL 连接限制的]**&#x200B;字段中指定表单数据模型和RESTful Web服务之间允许的连接的最大数目。 默认值为20个连接。

   * 在&#x200B;**[!UICONTROL 每个路由的连接限制]**&#x200B;字段中为每个路由指定允许的最大连接数。 默认值为2个连接。

   * 在&#x200B;**[!UICONTROL 保持活动]**&#x200B;字段中指定持续HTTP连接保持活动状态的持续时间。 默认值为15秒。

   * 在&#x200B;**[!UICONTROL 连接超时]**&#x200B;字段中指定[!DNL Experience Manager Forms]服务器等待连接建立的持续时间。 默认值为10秒。

   * 在&#x200B;**[!UICONTROL 套接字超时]**&#x200B;字段中指定两个数据包之间的最长不活动时间段。 默认值为30秒。

## 配置SOAP Web服务 {#configure-soap-web-services}

基于SOAP的Web服务使用[Web服务描述语言(WSDL)规范](https://www.w3.org/TR/wsdl)进行描述。 要在AEM云服务中配置基于SOAP的Web服务，请确保您具有Web服务的WSDL URL，并执行以下操作：

1. 转到&#x200B;**[!UICONTROL 工具>Cloud Service>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL SOAP Web服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为SOAP Web服务指定以下内容：

   * Web服务的WSDL URL。
   * 服务端点。 在此字段中指定一个值以覆盖WSDL中提到的服务端点。
   * 选择身份验证类型 — None、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、Basic Authentication、Custom Authentication、X509令牌或Mutual Authentication — 以访问SOAP服务，并相应地提供身份验证的详细信息。

     如果选择&#x200B;**[!UICONTROL X509 Token]**&#x200B;作为身份验证类型，请配置X509证书。 有关详细信息，请参阅[设置证书](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service)。
在&#x200B;**[!UICONTROL 密钥别名]**&#x200B;字段中指定X509证书的KeyStore别名。 在&#x200B;**[!UICONTROL 生存时间]**&#x200B;字段中指定身份验证请求保持有效的时间（秒）。 （可选）选择对消息正文或时间戳标头签名或同时选择两者。

     如果选择&#x200B;**[!UICONTROL 相互身份验证]**&#x200B;作为身份验证类型，请参阅[RESTful和SOAP Web服务的基于证书的相互身份验证](#mutual-authentication)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以创建SOAP Web服务的云配置。

## 配置OData服务 {#config-odata}

OData服务由其服务根URL标识。 要在AEM云服务中配置OData服务，请确保您拥有该服务的服务根URL，并执行以下操作：

>[!NOTE]
>
>表单数据模型支持[OData版本4](https://www.odata.org/documentation/)。
>有关配置Microsoft Dynamics 365（在线或本地）的分步指南，请参阅[Microsoft Dynamics OData配置](/help/forms/using/ms-dynamics-odata-configuration.md)。

1. 转到&#x200B;**[!UICONTROL 工具>Cloud Service>数据源]**。 选择以选择要创建云配置的文件夹。

   有关为云服务配置创建和配置文件夹的信息，请参阅[为云服务配置文件夹](../../forms/using/configure-data-sources.md#cloud-folder)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以打开&#x200B;**[!UICONTROL 创建数据Source配置向导]**。 指定配置的名称和标题，从&#x200B;**[!UICONTROL 服务类型]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL OData服务]**，浏览并选择配置的缩略图图像，然后选择&#x200B;**[!UICONTROL 下一步]**。
1. 为OData服务指定以下详细信息：

   * 要配置的OData服务的服务根URL。
   * 选择身份验证类型 — 无、OAuth2.0（[授权代码](https://oauth.net/2/grant-types/authorization-code/)、[客户端凭据](https://oauth.net/2/grant-types/client-credentials/)）、基本身份验证或自定义身份验证 — 以访问OData服务，并相应地提供身份验证的详细信息。

   >[!NOTE]
   >
   >选择OAuth 2.0身份验证类型以使用OData端点作为服务根连接到Microsoft Dynamics服务。

1. 选择&#x200B;**创建**&#x200B;以创建OData服务的云配置。

## RESTful和SOAP Web服务的基于证书的双向身份验证 {#mutual-authentication}

为表单数据模型启用相互身份验证后，数据源和运行表单数据模型的AEM Server在共享任何数据之前都会验证彼此的身份。 您可以对基于REST和SOAP的连接（数据源）使用相互身份验证。 要在AEM Forms环境中为表单数据模型配置双向身份验证，请执行以下操作：

1. 将私钥（证书）上载到[!DNL AEM Forms]服务器。 要上传私钥，请执行以下操作：
   1. 以管理员身份登录[!DNL AEM Forms]服务器。
   1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**。 选择`fd-cloudservice`用户并选择&#x200B;**[!UICONTROL 属性]**。
   1. 打开&#x200B;**[!UICONTROL 密钥库]**&#x200B;选项卡，展开&#x200B;**[!UICONTROL 从KeyStore文件添加私钥]**&#x200B;选项，上传KeyStore文件，指定别名、密码，然后选择&#x200B;**[!UICONTROL 提交]**。 证书已上传。  私钥别名在证书中提及，并在创建证书时设置。
1. 将信任证书上载到全局信任存储区。 要上传证书，请执行以下操作：
   1. 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 信任存储区]**。
   1. 展开&#x200B;**[!UICONTROL 从CER文件添加证书]**&#x200B;选项，选择&#x200B;**[!UICONTROL 选择证书文件]**，上载证书，然后选择&#x200B;**[!UICONTROL 提交]**。
1. 将[SOAP](#configure-soap-web-services)或[RESTful](#configure-restful-web-services) Web服务配置为数据源，并选择&#x200B;**[!UICONTROL 相互身份验证]**&#x200B;作为身份验证类型。 如果为`fd-cloudservice`用户配置多个自签名证书，请指定证书的密钥别名。

## 后续步骤 {#next-steps}

您已配置数据源。 接下来，您可以创建一个表单数据模型，或者，如果您已在不使用数据源的情况下创建了表单数据模型，则可以将其与您配置的数据源相关联。 有关详细信息，请参阅[创建表单数据模型](/help/forms/using/create-form-data-models.md)。
