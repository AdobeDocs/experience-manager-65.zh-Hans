---
title: 将Adobe Sign与AEM Forms集成
description: 了解如何为AEM自适应Forms配置Adobe Sign。 Adobe Sign改进了法律、销售、工资单、人力资源管理和其他许多领域的工作流程和处理文档。
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components,Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 16%

---

# 集成 [!DNL Adobe Sign] 使用AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | 本文 |

[!DNL Adobe Sign] 支持自适应表单的电子签名工作流。 电子签名改进了法律、销售、工资单、人力资源管理和其他许多方面的文档的处理工作流。

在典型的 [!DNL Adobe Acrobat Sign] 和自适应表单方案中，用户需填写自适应表单来申请服务。例如，信用卡申请表和公民权益表。在用户填写、签署和提交申请表后，该表将发送给服务提供商以执行后续操作。服务提供商将审核申请，并使用 [!DNL Adobe Acrobat Sign] 将申请标记为已批准。AEM Forms支持Adobe Acrobat Sign和Adobe Acrobat Sign Solutions政府版。 根据您的许可证和要求，您可以将AEM Forms与以下任一解决方案集成或连接：

* [将AEM Forms与Adobe Acrobat Sign连接](#adobe-sign)
* [将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接](#adobe-acrobat-sign-for-government)

## 将AEM Forms与Adobe Acrobat Sign连接 {#adobe-sign}

连接 **[!DNL AEM Forms]** 替换为 **[!DNL Adobe Acrobat Sign]**，设置先决条件部分中列出的软件和帐户，并将Adobe Sign连接到您的所有AEM Forms创作实例和Publish实例：

## 先决条件 {#prerequisites}

要集成，您需要以下项 [!DNL Adobe Sign] 使用AEM [!DNL Forms]：

* 活动 [Adobe Sign开发人员帐户。](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* An [已启用SSL](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] 服务器。
* [Adobe Sign API 应用程序](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)。
* [!DNL Adobe Sign] API 应用程序的凭据（客户端 ID 和客户端密码）。
* 重新配置时，删除现有的 [!DNL Adobe Sign] 来自创作实例和发布实例的配置。
* 针对创作实例和发布实例，使用[相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed)。

## 配置 [!DNL Adobe Sign] 使用AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

满足前提条件后，执行以下步骤以配置 [!DNL Adobe Sign] 使用AEM [!DNL Forms] 在创作实例上：

1. 在AEM上 [!DNL Forms] 创作实例，导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，选择 **[!UICONTROL 创建]**.
   * 请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档，以了解更多信息。
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，并选择 **[!UICONTROL 创建]**. 它会创建一个配置容器。
1. 导航到 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** 并选择您在上一步中创建的配置容器。

   >[!NOTE]
   >
   >您可以执行步骤1-4以创建配置容器并创建 [!DNL Adobe Sign] 在容器中进行配置或使用现有的 `global` 文件夹位置 **工具** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. 如果您在新配置容器中创建配置，请确保在 **[!UICONTROL 配置容器]** 创建自适应表单时显示的字段。

   >[!NOTE]
   >
   确保“Cloud Service配置”页面的URL开头为 **HTTPS**. 如果不能， [启用SSL](/help/sites-administering/ssl-by-default.md) 适用于AEM的 [!DNL Forms] 服务器。


1. 在配置页面上，点击 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] AEM中的配置 [!DNL Forms].
1. 在 **[!UICONTROL 常规]** 选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** 有关配置，请点击 **[!UICONTROL 下一个]**. 您可以选择指定标题并浏览以选择配置的缩略图。
1. 现在您可以 **[!UICONTROL 选择解决方案]** 以选择 [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. 将当前浏览器窗口中的URL复制到记事本并移除部分/`ui#/aem` 从URL访问。 然后，需要修改的URL才能配置 [!DNL Adobe Acrobat Sign] 应用程序 [!DNL AEM Forms]，在后续步骤中。 点按 [!UICONTROL 下一个].

1. 在 **[!UICONTROL 设置]** 选项卡，
   * 该 **[!UICONTROL OAuth URL]** 字段包含默认URL，其中包含Adobe Sign数据库分片。 URL 的格式为：

     `https://<shard>/public/oauth/v2`

     例如：
     `https://secure.na1.echosign.com/public/oauth/v2`

   * 该 **[!UICONTROL 访问令牌URL]** 字段包含默认URL，其中包含Adobe Sign数据库分片。 URL 的格式为：

     `https://<shard>/oauth/v2/token`

     例如：
     `https://api.na1.echosign.com/oauth/v2/token`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Acrobat Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   * 保留 **创建Adobe Acrobat Sign配置** 页面打开。 不要关闭它。 您可以检索 **客户端ID** 和 **客户端密码** 在为配置OAuth设置后 [!DNL Adobe Acrobat Sign] 应用程序（如即将执行的步骤中所述）。
   * 登录Adobe Sign帐户后，导航至 **[!UICONTROL ACROBAT SIGN API]** > **[!UICONTROL API信息]** > **[!UICONTROL REST API方法文档]** > **[!UICONTROL Oauth访问令牌]** 访问与Adobe Sign OAuth URL和访问令牌URL相关的信息。

1. 配置 [!DNL Adobe Sign] 应用程序的 OAuth 设置：

   1. 打开浏览器窗口并登录到 [!DNL Adobe Sign] 开发人员帐户。
   1. 选择为AEM配置的应用程序 [!DNL Forms]，并选择 **[!UICONTROL 为应用程序配置OAuth]**.
   1. 复制 **[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]** 记事本。
   1. 在 **[!UICONTROL 重定向URL]** 框中，添加在上一步中复制的HTTPS URL。
   1. 为启用以下OAuth设置 [!DNL Adobe Sign] 应用程序并单击 **[!UICONTROL 保存]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   有关为 [!DNL Adobe Sign] 应用程序配置 OAuth 设置并获取密钥的分步信息，请参阅[为应用程序配置 OAuth 设置](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md)开发人员文档。

   ![OAuth 配置](assets/oauthconfig_new.png)

<!--
1. Go back to the **[!UICONTROL Create Adobe Sign Configuration]** page. In the **[!UICONTROL Settings]** tab, the **[!UICONTROL OAuth URL]** field mentions the  default URL. The format of the URL is:

   `https://<shard>/public/oAuth/v2`

   For example: 
   `https://secure.na1.echosign.com/public/oauth/v2`

   where:

   **na1** refers to the default database shard.

   You can modify the value for the database shard. Restart the server to be able to use the new value for the database shard.

   >[!NOTE]
   >
   >Ensure that your author and publish instance configurations point to the same shard. If you create multiple Adobe Sign configurations for an organization, ensure all the configurations utilize the same shard. -->

1. 返回 **[!UICONTROL 创建Adobe Sign配置]** 页面。 在 **[!UICONTROL 设置]** 选项卡，指定 **客户端ID** （也称为应用程序ID）和 **客户端密码**. 使用 [Adobe Sign应用程序的客户端ID和客户端密码](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) 为AEM Forms创建。

1. 选择 **[!UICONTROL 另为附件启用Adobe Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Sign] 文档已发送供签名。

1. 选择 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供创建时使用的帐户的用户名和密码 [!DNL Adobe Sign] 应用程序。

   ![Adobe Acrobat Sign云配置成功](assets/adobe-sign-cloud-configuration-success.png)

1. 点按 **[!UICONTROL 创建]** 创建 [!DNL Adobe Sign] 配置。
1. 打开AEM Web控制台。 URL为 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **[!UICONTROL Forms通用配置服务].**
1. 在 **[!UICONTROL 允许]** 字段， **选择** 所有用户 — 所有用户（匿名或已登录）都可以预览附件、验证和签署表单，然后单击 **[!UICONTROL 保存].** 创作实例配置为使用 [!DNL Adobe Sign].
1. Publish配置。
1. 使用 [复制](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) 以在相应的发布实例上创建相同的配置。

现在， [!DNL Adobe Sign] 与AEM集成 [!DNL Forms] 并准备用于自适应表单。 至 [在自适应表单中使用Adobe Sign服务](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)，指定上文在自适应表单属性中创建的配置容器。

>[!NOTE]
>
要配置Adobe Sign沙盒，您可以按照中所述的相同配置步骤进行操作 [Adobe Sign](#adobe-sign).

## 将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接 {#adobe-acrobat-sign-for-government}

将AEM Forms与面向政府的Adobe Acrobat Sign Solutions连接是一个多步骤过程。 它涉及：

* 为您的AEM实例创建重定向URL
* 与面向政府团队的Adobe Sign解决方案共享重定向URL和范围
* 从Adobe Sign团队接收凭据
* 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### 开始之前 {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

在开始将AEM Forms与Adobe Acrobat Sign解决方案连接之前，

* 确保 [Adobe Acrobat Sign Solutions政府版](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) 已设置帐户。
* 您的AEM [!DNL Forms] 服务器是 [已启用SSL](/help/sites-administering/ssl-by-default.md) .
* 您的AEM [!DNL Forms] 服务器正在使用 [相同的加密密钥](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) 用于创作和发布实例。

### 将AEM Forms连接到适用于政府的Adobe Acrobat Sign Solutions {#connect-adobe-acrobat-sign-for-government}

#### 为您的AEM实例创建重定向URL

1. 在您的AEM Forms实例上，导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL 常规]** > **[!UICONTROL 配置浏览器]**.
1. 在 **[!UICONTROL 配置浏览器]** 页面，选择 **[!UICONTROL 创建]**.
1. 在 **[!UICONTROL 创建配置]** 对话框，请指定 **[!UICONTROL 标题]** 对于配置，启用 **[!UICONTROL 云配置]**，并选择 **[!UICONTROL 创建]**. 它会创建一个配置容器。 请确保容器/文件夹名称不包含任何空格。

1. 导航到 **[!UICONTROL 工具]** ![锤子](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** ，然后打开您在上一步中创建的配置容器。 在创建自适应表单时，请在 **[!UICONTROL 配置容器]** 字段。
1. 在配置页面上，选择 **[!UICONTROL 创建]** 创建 [!DNL Adobe Acrobat Sign] AEM Forms配置。
1. 将当前浏览器窗口的URL从URL复制到记事本。 此URL称为 `re-direct URL`. 在下一部分中，您共享 `re-direct URL` 和 `Scopes` 包含Adobe Sign团队和请求凭据（客户端ID和客户端密钥）。

>[!NOTE]
>
>
* A `re-direct URL` 应包含 [顶级](https://en.wikipedia.org/wiki/Top-level_domain) 域。 例如，`https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* 请勿将本地URL用作 `re-direct URL`. 例如：`https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`。


#### 与Adobe Sign团队共享重定向URL和作用域并接收凭据

Adobe Acrobat Sign政府解决方案团队要求 `re-direct URL` 以及要为您的Adobe Acrobat Sign应用程序启用的某些范围（如下所列），用于生成凭据（客户端ID和客户端密钥），从而让您将AEM Forms与面向政府的Adobe Acrobat Sign Solutions连接。

共享 `scopes` （如下所列）及 `re-direct URL` 与您的Adobe Acrobat Sign政府解决方案代表一起创建并记下上一节的最后一步 [Adobe Professional Services团队成员](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_范围_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

该代表会生成凭据并与您共享。 在下一部分中，您使用凭据（客户端ID和客户端密钥）将AEM Forms与用于政府的Adobe Acrobat Sign Solutions连接。

#### 使用收到的凭据将AEM Forms与适用于政府的Adobe Acrobat Sign Solutions连接

1. 打开 `re-direct URL` 在浏览器中。 您创建并记下了 `re-direct URL` 在 [在您的AEM实例上创建重定向URL](#create-redirect-url) 部分。

1. 在 **[!UICONTROL 常规]** 选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，指定 **[!UICONTROL 名称]** 对于配置，并选择 **[!UICONTROL 下一个]**. 您可以选择指定 **[!UICONTROL 标题]** 并浏览以选择 **[!UICONTROL 缩略图]** 用于配置。 单击&#x200B;**[!UICONTROL 下一步]**。

1. 在 **[!UICONTROL 设置]** 选项卡 **[!UICONTROL 创建Adobe Sign配置]** 页面，用于 **[!UICONTROL 选择解决方案]** 选项，选择 [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions政府版](/help/forms/using/assets/adobe-sign-for-govt.png)

1. 在 **[!UICONTROL 电子邮件]** 字段中，为政府帐户指定与Adobe Acrobat Sign Solutions关联的电子邮件地址。

1. 在 **[!UICONTROL 设置]** 选项卡，
   * 该 **[!UICONTROL OAuth URL]** 字段包含默认URL，其中包含Adobe Sign数据库分片。 URL 的格式为：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * 该 **[!UICONTROL 访问令牌URL]** 字段包含默认URL，其中包含Adobe Sign数据库分片。 URL 的格式为：

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     例如：
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   其中：

   **na1** 指默认数据库分片。您可以修改数据库分片的值。确保 [!DNL  Adobe Acrobat Sign] 云配置指向[正确分片](https://helpx.adobe.com/sign/using/identify-account-shard.html)。

   >[!NOTE]
   >
   * 登录Adobe Sign帐户后，导航至 **[!UICONTROL ACROBAT SIGN API]** > **[!UICONTROL API信息]** > **[!UICONTROL REST API方法文档]** > **[!UICONTROL Oauth访问令牌]** 访问与Adobe Sign oAuth URL和访问令牌URL相关的信息。

1. 使用Adobe Acrobat Sign为政府解决方案代表共享的凭据([Adobe Professional Services团队成员])在上一部分中，显示为[**[!UICONTROL 客户端ID]** 和 **[!UICONTROL 客户端密码]**]。

1. 选择 **[!UICONTROL 为附件启用Adobe Acrobat Sign]** 用于将附加到自适应表单的文件追加到相应表单的选项 [!DNL Adobe Acrobat Sign] 文档已发送供签名。

1. 选择 **[!UICONTROL 连接到Adobe Sign]**. 在系统提示输入凭据时，提供在创建 [!DNL Adobe Acrobat Sign] 应用程序时所用帐户的用户名和密码。当要求确认访问时 `Adobe Acrobat Sign for Government Solutions` 和，单击 **[!UICONTROL 允许访问]**. 如果凭据正确，并且您允许 [!DNL AEM Forms] 访问您的 [!DNL Adobe Acrobat Sign] 开发人员帐户，系统会显示一条与以下内容类似的成功消息。

   ![Adobe Acrobat Sign云配置成功](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   在系统提示输入凭据时，提供在创建 [!DNL Adobe Acrobat Sign] 应用程序时所用帐户的用户名和密码。当要求确认访问时 `your account`，然后单击 **[!UICONTROL 允许访问]**.

1. 选择 **[!UICONTROL 创建]** 以创建配置。
1. 打开AEM Web控制台。 URL为 `https://'[server]:[port]'/system/console/configMgr`
1. 打开 **[!UICONTROL Forms通用配置服务].**
1. 在 **[!UICONTROL 允许]** 字段， **选择** 所有用户 — 所有用户（匿名或已登录）都可以预览附件、验证和签署表单，然后单击 **[!UICONTROL 保存].** 创作实例配置为使用 [!DNL Adobe Sign].

1. Publish配置。
1. 使用 [复制](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) 以在相应的发布实例上创建相同的配置。

现在，您可以 [在自适应表单中使用添加Adobe Acrobat Sign字段](working-with-adobe-sign.md) 或 [AEM Workflow](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). 确保将用于Cloud Service配置的配置容器添加到启用的所有自适应Forms [!DNL Adobe Acrobat Sign]. 您可以从自适应表单的属性中指定配置容器。


## 配置 [!DNL Adobe Sign] 用于同步签名状态的计划程序 {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

An [!DNL Adobe Sign] 仅在所有签名者完成签名过程后提交启用的自适应表单。 默认情况下， [!DNL Adobe Sign] 计划程序服务被安排在每24小时检查（轮询）签名者响应。 您可以更改环境的默认间隔。 执行以下步骤以更改默认间隔：

1. 登录到AEM [!DNL Forms] 具有管理员凭据的服务器，并导航到 **工具** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**.

   您还可以在浏览器窗口中打开以下URL：
   `https://[localhost]:'port'/system/console/configMgr`

1. 找到并打开 **[!UICONTROL Adobe Sign配置服务]** 选项。 指定 [cron表达式](https://en.wikipedia.org/wiki/Cron#CRON_expression) 在 **[!UICONTROL 状态更新计划程序表达式]** 字段并单击 **[!UICONTROL 保存]**. 例如，要在每天凌晨00:00运行配置服务，请指定 `0 0 0 1/1 * ? *` 在 **[!UICONTROL 状态更新计划程序表达式]** 字段。

同步状态的默认间隔 [!DNL Adobe Sign] 现已更改。

## 相关文章 {#related-articles}

* [在自适应表单中使用Adobe Sign](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign具有以表单为中心的工作流](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [将Adobe Sign与AEM Forms结合使用（视频）](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
