---
title: 使用智能内容服务配置资产标记
description: 了解如何在中配置智能标记和增强型智能标记 [!DNL Adobe Experience Manager]，使用智能内容服务。
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: d8d821a64b39b312168733126de8929c04016ff1
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 7%

---

# OAuth凭据的智能标记疑难解答 {#oauth-config}

要接受对的同意，需要打开授权配置 [!DNL Adobe Experience Manager] 应用程序以安全方式与智能内容服务交互。

>[!NOTE]
>
> 从2024年6月起，您无法创建新的JWT凭据。 今后，仅创建OAuth服务器到服务器凭据。
> JWT集成仅对现有AMS和内部部署用户持续工作至2025年1月。

## 新AMS用户的OAuth配置 {#oauth-config-existing-ams-users}

请参阅 [智能内容服务的配置](#integrate-adobe-io) 用于为新用户配置OAuth服务。 完成后，请按照以下步骤操作 [步骤](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>如果需要，您可以按照以下步骤提交支持工单 [支持过程](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

## 现有AMS用户的OAuth配置 {#oauth-config-new-ams-users}

在执行此方法中的任何步骤之前，您需要实施以下内容：

### 先决条件 {#prereqs-config-oauth-onprem}

OAuth配置需要以下先决条件：

* 在中创建新的OAuth集成 [开发人员控制台](https://developer.adobe.com/console/user/servicesandapis). 使用 `ClientID`， `ClientSecret`， `OrgID`，以及以下步骤中的其他属性：
* 以下文件可在此路径中找到 `/apps/system/config in crx/de`：
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### 现有AMS和On Prem用户的OAuth配置 {#steps-config-oauth-onprem}

以下步骤可由系统管理员执行。 AMS客户可以联系Adobe代表或提交支持工单，以遵循 [支持过程](https://experienceleague.adobe.com/?lang=en&amp;support-tab=home#support).

1. 在中添加或更新以下属性 `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`：

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * 更新 `auth.token.provider.client.id` 与新OAuth配置的客户端ID一起使用。
   * 更新 `auth.access.token.request` 到 `"https://ims-na1.adobelogin.com/ims/token/v3"`
1. 将文件重命名为 `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
1. 在中执行以下步骤 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`：
   * 通过新的OAuth集成，使用客户端密钥更新属性auth.ims.client.secret。
   * 将文件重命名为 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
1. 在内容存储库开发控制台（例如，CRXDE）中保存所有更改。
<!--
1. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
1. Delete the old OSGi configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
-->
1. 在 `System/console/configMgr`，删除的旧配置 `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl` 和访问令牌提供程序名称 `adobe-ims-similaritysearch`.
1. 重新启动控制台。

## 验证配置 {#validate-the-configuration}

完成配置后，可以使用JMX MBean来验证配置。 要进行验证，请执行以下步骤。

1. 访问 [!DNL Experience Manager] 服务器位于 `https://[aem_server]:[port]`.

1. 转到 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]** 以打开OSGi控制台。 单击 **[!UICONTROL 主要] > [!UICONTROL JMX]**.

1. 单击 `com.day.cq.dam.similaritysearch.internal.impl`. 它会打开 **[!UICONTROL 相似性搜索其他任务]**.

1. 单击 `validateConfigs()`. 在 **[!UICONTROL 验证配置]** 对话框，请单击 **[!UICONTROL 调用]**.

验证结果将显示在同一对话框中。

## 与Adobe Developer控制台集成 {#integrate-adobe-io}

作为新用户，当您与Adobe Developer Console集成时， [!DNL Experience Manager] 在将您的请求转发到智能内容服务之前，服务器会使用Adobe Developer控制台网关验证您的服务凭据。 要集成，您需要一个拥有组织管理员权限的Adobe ID帐户，以及一个已购买并为您的组织启用的Smart Content Service许可证。

要配置智能内容服务，请按照以下顶级步骤操作：

1. 要生成公钥， [创建智能内容服务](#obtain-public-certificate) 中的配置 [!DNL Experience Manager]. [下载公共证书](#obtain-public-certificate) 用于OAuth集成。

1. *[如果您是现有用户，则不适用]* [在Adobe Developer控制台中创建集成](#create-adobe-i-o-integration).

1. [配置部署](#configure-smart-content-service) 从Adobe Developer控制台使用API密钥和其他凭据。

1. [测试配置](#validate-the-configuration)。

## 通过创建智能内容服务配置下载公共证书 {#download-public-certificate}

公共证书允许您在Adobe Developer控制台上验证配置文件。

1. 在 [!DNL Experience Manager] 用户界面，访问 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧版Cloud Service]**.

1. 在“Cloud Service”页面中，单击 **[!UICONTROL 立即配置]** 下 **[!UICONTROL 资产智能标记]**.

1. 在 **[!UICONTROL 创建配置]** 对话框，请为智能标记配置指定标题和名称。 单击&#x200B;**[!UICONTROL 创建]**。

1. 在 **[!UICONTROL AEM智能内容服务]** 对话框，请使用以下值：

   **[!UICONTROL 服务URL]**： `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   例如，`https://smartcontent.adobe.io/apac`。您可以指定 `na`， `emea`，或， `apac` 作为托管Experience Manager创作实例的地区。

   >[!NOTE]
   >
   >如果Experience Manager托管服务是在2022年9月1日之前配置的，请使用以下服务URL：
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL 授权服务器]**： `https://ims-na1.adobelogin.com`

   其他字段暂时留空（稍后提供）。 单击&#x200B;**[!UICONTROL 确定]**。

   ![Experience Manager智能内容服务对话框以提供内容服务URL](assets/aem_scs12.png)

   *图：用于提供内容服务URL的智能内容服务对话框*

   >[!NOTE]
   >
   >提供的URL为 [!UICONTROL 服务URL] 无法通过浏览器访问，并生成404错误。 如果具有相同值，则配置工作正常。 [!UICONTROL 服务URL] 参数。 有关总体服务状态和维护计划，请参阅 [https://status.adobe.com](https://status.adobe.com).

1. 单击 **[!UICONTROL 下载用于OAuth集成的公共证书]**，并下载公共证书文件 `AEM-SmartTags.crt`. 此外，您不再需要在Adobe开发人员控制台中上传此证书。

   ![为智能标记服务创建的设置的表示形式](assets/smart-tags-download-public-cert1.png)

   *图：智能标记服务的设置。*

## 创建Adobe Developer控制台集成 {#create-adobe-i-o-integration}

要使用Smart Content Service API，请在Adobe Developer控制台中创建集成以获取 [!UICONTROL API密钥] (生成于 [!UICONTROL 客户端ID] 字段(例如Adobe Developer控制台集成字段)， [!UICONTROL 技术帐户ID]， [!UICONTROL 组织ID]、和 [!UICONTROL 客户端密码] 对象 [!UICONTROL 资产智能标记服务设置] 中的云配置 [!DNL Experience Manager].

1. 访问 [https://developer.adobe.com/console/](https://developer.adobe.com/console/) 在浏览器中。 选择相应的帐户并验证关联的组织角色是否为系统管理员。

1. 创建具有任何所需名称的项目。单击&#x200B;**[!UICONTROL 添加 API]**。

1. 在&#x200B;**[!UICONTROL 添加 API]** 页面中，依次选择 **[!UICONTROL Experience Cloud]** 和&#x200B;**[!UICONTROL 智能内容]**。单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择 **[!UICONTROL OAuth服务器到服务器]** 身份验证方法。

1. 添加/修改 **[!UICONTROL 凭据名称]** 根据需要。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 选择产品配置文件 **[!UICONTROL 智能内容服务]**. 单击 **[!UICONTROL 保存配置的API]**. OAuth API会添加到连接的凭据下，以供进一步使用。 您可以复制 [!UICONTROL API密钥（客户端ID）] 或 [!UICONTROL 生成访问令牌] 从它。
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![oauth配置](assets/oauth-config.png)
*图：在Adobe Developer控制台中配置的OAuth服务器到服务器*

## 配置智能内容服务 {#configure-smart-content-service}

要配置集成，请使用 [!UICONTROL 技术帐户ID]， [!UICONTROL 组织ID]， [!UICONTROL 客户端密码]、和 [!UICONTROL 客户端ID] Adobe Developer控制台集成中的字段。 创建智能标记云配置允许对来自的API请求进行身份验证 [!DNL Experience Manager] 部署。

1. 在 [!DNL Experience Manager]，导航到 **[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 旧版Cloud Service]** 以打开 [!UICONTROL Cloud Service] 控制台。

1. 在 **[!UICONTROL 资产智能标记]**，打开上面创建的配置。 在服务设置页面上，单击 **[!UICONTROL 编辑]**.

1. 在 **[!UICONTROL AEM 智能内容服务]**&#x200B;对话框中，为&#x200B;**[!UICONTROL 服务 URL]** 和&#x200B;**[!UICONTROL 授权服务器]**&#x200B;字段使用预填充的值。

1. 对于字段 [!UICONTROL Api密钥]， [!UICONTROL 技术帐户ID]， [!UICONTROL 组织ID]、和 [!UICONTROL 客户端密码]，复制并使用中生成的以下值 [Adobe Developer控制台集成](#create-adobe-i-o-integration).

   | [!UICONTROL 资产智能标记服务设置] | [!DNL Adobe Developer Console] 集成字段 |
   |--- |--- |
   | [!UICONTROL Api密钥] | [!UICONTROL 客户端ID] |
   | [!UICONTROL 技术帐户ID] | [!UICONTROL 技术帐户ID] |
   | [!UICONTROL 组织ID] | [!UICONTROL 组织ID] |
   | [!UICONTROL 客户端密码] | [!UICONTROL 客户端密码] |

>[!MORELIKETHIS]
>
>* [概述以及如何培训智能标记](enhanced-smart-tags.md)
>* [配置智能标记](config-smart-tagging.md)
>* [有关智能标记的视频教程](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
