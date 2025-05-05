---
title: 为Microsoft&reg (Forms JEE OAuth)；Office 365邮件服务器协议配置基于OAuth2的身份验证
description: 为Microsoft&reg (Forms JEE OAuth)；Office 365邮件服务器协议配置基于OAuth2的身份验证
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# 将AEM Forms与Microsoft® Office 365邮件服务器协议集成 {#oauth2-support-for-the-microsoft-mail-server-protocols}

为了让组织遵守安全电子邮件要求，AEM Forms提供了OAuth 2.0支持与Microsoft® Office 365邮件服务器协议集成。 您可以使用Azure Active Directory (Azure AD) OAuth 2.0身份验证服务连接各种协议（如IMAP、POP或SMTP），并访问Office 365用户的电子邮件数据。 以下是配置Microsoft® Office 365邮件服务器协议以通过OAuth 2.0服务进行身份验证的分步说明：

1. 登录到[https://portal.azure.com/](https://portal.azure.com/)并在搜索栏中搜索&#x200B;**Azure Active Directory**，然后单击结果。
或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**添加** > **应用程序注册** > **新注册**。

   ![应用程序注册](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 根据您的要求填写信息，然后单击&#x200B;**注册。**
   ![支持的帐户](/help/forms/using/assets/azure_suuportedaccountype.png)
在上例中，已选择任何组织目录（任何Azure AD目录 — 多租户）中的&#x200B;**帐户和个人Microsoft®帐户（例如，Skype、Xbox）**&#x200B;选项。

   >[!NOTE]
   >
   > * 对于任何组织目录（任何Azure AD目录 — 多租户）**应用程序中的**&#x200B;帐户，Adobe建议您使用工作帐户，而不是个人电子邮件帐户。
   > * **仅个人Microsoft®帐户**&#x200B;应用程序不受支持。
   > * Adobe建议您使用&#x200B;**多租户和个人Microsoft®帐户**&#x200B;应用程序。

1. 接下来，转至&#x200B;**证书和密码**，单击&#x200B;**新建客户端密码**，然后执行屏幕上显示的步骤来创建密码。请务必记下此secret值供以后使用。

   ![密钥](/help/forms/using/assets/azure_secretkey.png)

1. 若要添加权限，请转到新创建的应用程序，然后选择&#x200B;**API权限** > **添加权限** > **Microsoft® Graph** > **委派权限**。
1. 选中应用程序的以下权限对应的复选框，然后单击&#x200B;**添加权限**：

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API权限](/help/forms/using/assets/azure_apipermission.png)

1. 选择&#x200B;**身份验证** > **添加平台** > **Web**，然后在&#x200B;**重定向Url**&#x200B;部分中，添加以下任意URI（通用资源标识符）作为：
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   在这种情况下，`https://login.microsoftonline.com/common/oauth2/nativeclient`被用作重定向URI。

1. 添加每个URL后单击&#x200B;**配置**，并根据您的要求配置设置。
   ![重定向URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 必须选中&#x200B;**访问令牌**&#x200B;和&#x200B;**ID令牌**&#x200B;复选框。

1. 单击左侧窗格中的&#x200B;**概述**，并复制&#x200B;**应用程序（客户端） ID**、**目录（租户） ID**&#x200B;和&#x200B;**客户端密钥**&#x200B;的值供以后使用。

   ![概述](/help/forms/using/assets/azure_overview.png)

## 生成授权码 {#generating-the-authorization-code}

接下来，必须生成授权码，如以下步骤所述：

1. 将`clientID`替换为`<client_id>`并在浏览器中打开以下URL，将`redirect_uri`替换为您的应用程序的重定向URI：

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > 如果存在单个租户应用程序，请在以下URL中将`common`替换为您的`[tenantid]`以生成授权代码： `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. 键入上述URL后，您将被重定向到登录屏幕：
   ![登录屏幕](/help/forms/using/assets/azure_loginscreen.png)

1. 输入电子邮件，单击&#x200B;**下一步**，将显示“应用程序权限”屏幕：

   ![允许权限](/help/forms/using/assets/azure_permission.png)

1. 当您允许权限时，您将被重定向到一个新的URL，如下所示： `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 将上述URL中`<code>`的值从`0.ASY...`复制到上述URL中的`&session_state`。

## 生成刷新令牌 {#generating-the-refresh-token}

接下来，必须生成刷新令牌，如以下步骤所述：

1. 打开命令提示符并使用以下cURL命令获取refreshToken。

1. 将`clientID`、`client_secret`和`redirect_uri`替换为应用程序的值以及`<code>`的值：

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > 在单个租户应用程序中，要生成刷新令牌，请使用以下cURL命令并将`common`替换为中的`[tenantid]`：
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. 记下刷新令牌。

## 使用OAuth 2.0支持配置电子邮件服务 {#configureemailservice}

现在，通过登录到管理员UI在最新的JEE服务器上配置电子邮件服务：

1. 转到&#x200B;**主页** > **服务** > **应用程序和服务** > **服务管理** > **电子邮件服务**，将显示&#x200B;**配置电子邮件服务**&#x200B;窗口，此窗口是为基本身份验证配置的。

   >[!NOTE]
   >
   > 若要启用oAuth 2.0身份验证服务，必须选中&#x200B;**SMTP服务器是否需要身份验证（SMTP身份验证）**&#x200B;复选框。

1. 将&#x200B;**oAuth 2.0身份验证设置**&#x200B;设置为`True`。
1. 从Azure门户复制&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**&#x200B;的值。
1. 复制生成的&#x200B;**刷新令牌**&#x200B;的值。
1. 登录到&#x200B;**Workbench**&#x200B;并从&#x200B;**活动选取器**&#x200B;中搜索&#x200B;**电子邮件1.0**。
1. 电子邮件1.0下提供了三个选项：
   * **随文档一起发送**：发送带有单个附件的电子邮件。
   * **随附件映射一起发送**：发送带有多个附件的电子邮件。
   * **接收**：接收来自IMAP的电子邮件。

   >[!NOTE]
   >
   >* 传输安全协议具有以下有效值：“blank”、“SSL”或“TLS”。 将&#x200B;**SMTP Transport Security**&#x200B;和&#x200B;**Receive Transport Security**&#x200B;的值设置为&#x200B;**TLS**&#x200B;以启用oAuth身份验证服务。
   >* 使用电子邮件端点时，OAuth不支持&#x200B;**POP3协议**。

   ![连接设置](/help/forms/using/assets/oauth_connectionsettings.png)

1. 通过选择&#x200B;**随文档**&#x200B;一起发送，测试应用程序。
1. 提供&#x200B;**TO**&#x200B;和&#x200B;**From**&#x200B;地址。
1. 调用应用程序，并使用0Auth 2.0身份验证发送电子邮件。

   >[!NOTE]
   >
   >如果需要，您可以将Workbench中特定进程的Auth 2.0身份验证设置更改为基本身份验证。 为此，请在&#x200B;**连接设置**&#x200B;选项卡中的&#x200B;**使用全局设置**&#x200B;下将&#x200B;**OAuth 2.0身份验证**&#x200B;值设置为“False”。

## 启用oAuth任务通知 {#enable_oauth_task}

1. 转到&#x200B;**主页** > **服务** > **表单工作流** > **服务器设置** > **电子邮件设置**
1. 要启用oAuth任务通知，请选中&#x200B;**启用oAuth**&#x200B;复选框。
1. 从Azure门户复制&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**&#x200B;的值。
1. 复制生成的&#x200B;**刷新令牌**&#x200B;的值。
1. 单击&#x200B;**保存**&#x200B;以保存详细信息。

   ![任务通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > 若要了解有关任务通知的更多信息，[单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service)。

## 配置电子邮件端点 {#configure_email_endpoint}

1. 转到&#x200B;**主页** > **服务** > **应用程序和服务** > **端点管理**
1. 要配置电子邮件终结点，请将&#x200B;**oAuth 2.0身份验证设置**&#x200B;设置为`True`。
1. 从Azure门户复制&#x200B;**客户端ID**&#x200B;和&#x200B;**客户端密钥**&#x200B;的值。
1. 复制生成的&#x200B;**刷新令牌**&#x200B;的值。
1. 单击&#x200B;**保存**&#x200B;以保存详细信息。

   ![连接设置](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 若要了解有关配置电子邮件端点的详细信息，请单击[配置电子邮件端点](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html)。

## 疑难解答 {#troubleshooting}

* 如果电子邮件服务无法正常工作，请尝试重新生成`Refresh Token`，如上所述。 部署新值需要花费几分钟的时间。

* 使用Workbench在电子邮件端点中配置电子邮件服务器详细信息时出错。 尝试通过Admin UI（而不是Workbench）配置端点。
