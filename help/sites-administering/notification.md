---
title: 配置电子邮件通知
description: 了解如何在Adobe Experience Manager中配置电子邮件通知。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: efaff4557aba3557a355ed385a5358cf1108c159
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 8%

---


# 配置电子邮件通知{#configuring-email-notification}

AEM会向符合以下条件的用户发送电子邮件通知：

* 已订阅页面事件，例如，修改或复制。 [通知收件箱](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)部分介绍了如何订阅此类事件。

* 已订阅论坛活动。
* 必须在工作流中执行步骤。 [参与者步骤](/help/sites-developing/workflows-step-ref.md#participant-step)部分介绍了如何在工作流中触发电子邮件通知。

先决条件：

* 用户需要在其个人资料中定义有效的电子邮件地址。
* 需要正确配置&#x200B;**天CQ邮件服务**。

当用户收到通知时，将收到其用户档案中定义的语言版本的电子邮件。 每种语言都有其自己的可自定义的模板。 可以为新语言添加新电子邮件模板。

>[!NOTE]
>
>使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

## 配置邮件服务 {#configuring-the-mail-service}

为了使AEM能够发送电子邮件，需要正确配置&#x200B;**Day CQ邮件服务**。 您可以在Web控制台中查看配置。 使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

以下约束适用：

* **SMTP服务器端口**&#x200B;必须为25或更高。

* **SMTP服务器主机名**&#x200B;不能为空。
* **“发件人”地址**&#x200B;不能为空，并且您必须更改默认值“<noreply@day.com>”。

为了帮助您调试&#x200B;**Day CQ邮件服务**&#x200B;的问题，您可以查看该服务的日志：

`com.day.cq.mailer.DefaultMailService`

该配置在Web控制台中如下所示：

![Day CQ Mail Service OSGi配置窗口](assets/chlimage_1-276.png)

## 配置电子邮件通知渠道 {#configuring-the-email-notification-channel}

当您订阅页面或论坛事件通知时，发件人电子邮件地址默认设置为`no-reply@acme.com`。 您可以通过在Web控制台中配置&#x200B;**通知电子邮件渠道**&#x200B;服务来更改此值。

要配置发件人电子邮件地址，请向存储库添加一个`sling:OsgiConfig`节点。 使用以下过程可使用CRXDE Lite直接添加节点：

1. 在CRXDE Lite中，在应用程序文件夹下添加名为`config`的文件夹。
1. 在配置文件夹中，添加一个名为的节点：

   `sling:OsgiConfig`类型的`com.day.cq.wcm.notification.email.impl.EmailChannel`

1. 将`String`属性添加到名为`email.from`的节点。 对于值，指定要使用的电子邮件地址。

1. 单击&#x200B;**全部保存**。

请按下列步骤在内容包源文件夹中定义节点：

1. 在您的`jcr_root/apps/*app_name*/config folder`中创建名为`com.day.cq.wcm.notification.email.impl.EmailChannel.xml`的文件

1. 添加以下XML以表示节点：

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. 将`email.from`属性的值(`name@server.com`)替换为您的电子邮件地址。

1. 保存文件。

## 配置工作流电子邮件通知服务 {#configuring-the-workflow-email-notification-service}

当您收到工作流电子邮件通知时，发件人电子邮件地址和主机URL前缀都会设置为默认值。 您可以通过在Web控制台中配置&#x200B;**Day CQ工作流电子邮件通知服务**&#x200B;来更改这些值。 如果这样做，您必须在存储库中保留更改。

在Web控制台中，默认配置如下所示：

![Day CQ工作流电子邮件通知服务配置窗口](assets/chlimage_1-277.png)

### 页面通知的电子邮件模板 {#email-templates-for-page-notification}

页面通知的电子邮件模板位于下方：

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

默认英语模板(`en.txt`)的定义如下：

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自定义页面通知的电子邮件模板 {#customizing-email-templates-for-page-notification}

要自定义页面通知的英语电子邮件模板，请执行以下操作：

1. 为[页面通知](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)创建叠加

1. 打开文件：

   `en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

其中，&lt;text_x>可以是静态文本和动态字符串变量的组合。 以下变量可在电子邮件模板中用于页面通知：

* `${time}`，事件的日期和时间。

* `${userFullName}`，触发事件的用户的全名。

* `${userId}`，触发事件的用户的ID。
* `${modifications}`，以格式描述页面事件的类型和页面路径：

  &lt;页面事件类型> => &lt;页面路径>

  例如：

  PageModified => /content/geometrixx/en/products

### 工作流通知的电子邮件模板 {#email-templates-for-workflow-notification}

工作流通知的电子邮件模板（英文）位于：

`/libs/settings/workflow/notification/email/default/en.txt`

其定义如下：

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### 自定义工作流通知的电子邮件模板 {#customizing-email-templates-for-workflow-notification}

要自定义工作流事件通知的英语电子邮件模板，请执行以下操作：

1. 为[工作流通知](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)创建叠加

1. 打开文件：

   `en.txt`

1. 根据需要修改文件。
1. 保存更改。

模板需要具有以下格式：

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>其中`<text_x>`可以是静态文本和动态字符串变量的组合。 `<text_x>`项的每一行都需要以反斜杠(`\`)结尾，但最后一个实例除外，因为缺少反斜杠表示`<text_x>`字符串变量的结尾。
>
>有关模板格式的详细信息，可在Properties.load() [&#128279;](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-)方法的javadocs中找到。

方法`${payload.path.open}`显示工作项的有效负荷的路径。 例如，对于网站中的页面，则`payload.path.open`将类似于`/bin/wcmcommand?cmd=open&path=…`。；这没有服务器名称，因此模板会将此前面加上`${host.prefix}`。

可在电子邮件模板中使用以下变量：

* `${event.EventType}`，事件的类型
* `${event.TimeStamp}`，事件的日期和时间
* `${event.User}`，触发事件的用户
* `${initiator.home}`，启动器节点路径

* `${initiator.name}`，启动器名称

* `${initiator.email}`，发起人的电子邮件地址
* `${item.id}`，工作项的ID
* `${item.node.id}`，与此工作项关联的工作流模型中节点的ID
* `${item.node.title}`，工作项的标题
* `${participant.email}`，参与者的电子邮件地址
* `${participant.name}`，参与者的名称
* `${participant.familyName}`，参与者的姓氏
* `${participant.id}`，参与者的ID
* `${participant.language}`，参与者语言
* `${instance.id}`，工作流ID
* `${instance.state}`，工作流状态
* `${model.title}`，工作流模型的标题
* `${model.id}`，工作流模型的id

* `${model.version}`，工作流模型的版本
* `${payload.data}`，有效负载

* `${payload.type}`，有效负载类型
* `${payload.path}`，有效负载的路径
* `${host.prefix}`，主机前缀，例如： `http://localhost:4502`

### 添加新语言的电子邮件模板 {#adding-an-email-template-for-a-new-language}

要添加新语言的模板，请执行以下操作：

1. 根据需要创建[叠加](/help/sites-developing/overlays.md)。

   * [页面通知](/help/sites-deploying/sites-repository-restructuring-in-aem-6-5.md#page-event-notification-e-mail-template)
   * [工作流通知](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#workflow-notification-email-templates)

1. 添加文件`<language-code>.txt`。
1. 使文件适应语言。
1. 保存更改。

>[!NOTE]
>
>用作电子邮件模板文件名的`<language-code>`必须是AEM可识别的双字母小写语言代码。 对于语言代码，AEM依赖于ISO-639-1。

## 配置AEM Assets电子邮件通知 {#assetsconfig}

在共享或取消共享AEM Assets中的收藏集时，用户可以从AEM接收电子邮件通知。 要配置电子邮件通知，请执行以下步骤。

1. 配置电子邮件服务，如[配置邮件服务](/help/sites-administering/notification.md#configuring-the-mail-service)中所述。
1. 以管理员身份登录AEM。 单击&#x200B;**工具** > **操作** > **Web控制台**&#x200B;以打开Web控制台配置。
1. 编辑&#x200B;**Day CQ DAM资源收集Servlet**。 选择&#x200B;**发送电子邮件**。 单击&#x200B;**保存**。

## 设置OAuth {#setting-up-oauth}

AEM为其集成的邮件程序服务提供OAuth2支持，以允许组织遵守安全电子邮件要求。

您可以为多个电子邮件提供商配置OAuth，如下所述。

>[!NOTE]
>
>此过程是Publish实例的示例。 如果您希望在“作者”实例上启用电子邮件通知，则需要在“作者”上执行相同的步骤。

### Gmail {#gmail}

1. 在`https://console.developers.google.com/projectcreate`创建项目
1. 选择您的项目，然后转到&#x200B;**API和服务** - **仪表板 — 凭据**
1. 根据您的要求配置OAuth同意屏幕
1. 在后续的更新屏幕中，添加这两个范围：
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 添加作用域后，请返回左侧菜单中的&#x200B;**凭据**，然后转到&#x200B;**创建凭据** - **OAuth客户端ID** - **桌面应用程序**
1. 此时将打开一个包含客户端ID和客户端密钥的新窗口。
1. 保存这些凭据。

**AEM端配置**

>[!NOTE]
>
>Adobe托管服务客户可以与其客户服务工程师合作，对生产环境进行这些更改。

首先，配置邮件服务：

1. 转到`http://serveraddress:serverport/system/console/configMgr`打开AEM Web控制台
1. 查找，然后单击&#x200B;**Day CQ邮件服务**
1. 添加以下设置：
   * SMTP服务器主机名： `smtp.gmail.com`
   * SMTP服务器端口： `25`或`587`，具体取决于要求
   * 选中&#x200B;**SMPT的复选框使用StarTLS**，**SMTP需要StarTLS**
   * 检查&#x200B;**OAuth流程**&#x200B;并单击&#x200B;**保存**。

接下来，按照以下过程配置您的SMTP OAuth提供程序：

>[!WARNING]
>
>完成此配置后，如果您曾更改OSGi配置&#x200B;**CQ Mailer SMTP OAuth2 Provide**&#x200B;中的&#x200B;*any*&#x200B;值，则必须按照以下步骤再次重新授权。
>
>如果未执行这些操作，则存储在`/conf/global/settings/mailer/oauth`中的访问令牌将无效，并且与SMTP服务器的OAuth2连接将失败。

1. 转到`http://serveraddress:serverport/system/console/configMgr`打开AEM Web控制台
1. 查找，然后单击&#x200B;**CQ Mailer SMTP OAuth2提供程序**

1. 按如下方式填写所需信息：
   * 授权URL： `https://accounts.google.com/o/oauth2/auth`
   * 令牌URL： `https://accounts.google.com/o/oauth2/token`
   * 范围： `https://www.googleapis.com/auth/gmail.send`和`https://mail.google.com/`。 通过按每个已配置作用域右侧的&#x200B;**+**&#x200B;按钮，可以添加多个作用域。
   * 客户端ID和客户端密码：使用您在上面段落中检索到的值配置这些字段。
   * 刷新令牌URL： `https://accounts.google.com/o/oauth2/token`
   * 刷新令牌过期：从不
1. 单击&#x200B;**保存**。

<!-- clarify refresh token expiry, currently not present in the UI -->

配置完毕后，设置应如下所示：

![CQ邮件程序SMTP Oauth2提供程序配置窗口](assets/oauth-smtpprov2.png)

现在，激活OAuth组件。 您可以执行以下操作来实现此目标：

1. 通过访问以下URL转到组件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下组件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按组件左侧的播放图标

   ![显示OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的组件列表](assets/oauth-components-play.png)

最后，通过以下方式确认配置：

1. 转到发布实例的地址，并以管理员身份登录。
1. 在浏览器中打开新选项卡，然后转到`http://serveraddress:serverport/services/mailer/oauth2/authorize`。 这会将您重定向到SMTP提供商的页面，在本例中为Gmail。
1. 登录并同意授予所需权限
1. 同意后，令牌将存储在存储库中。 您可以通过直接访问发布实例上的此URL在`accessToken`下访问它： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 对每个发布实例重复以上步骤

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. 转至 [https://portal.azure.com/](https://portal.azure.com/) 并登录。
1. 在搜索栏中搜索 **Azure Active Directory**，并单击搜索结果。或者，您可以直接浏览到 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. 单击&#x200B;**应用程序注册** - **新注册**

   ![配置Microsoft Outlook时的新注册按钮](assets/oauth-outlook1.png)

1. 根据您的要求填写信息，然后单击&#x200B;**注册**
1. 转至新创建的应用程序，并选择 **API 权限**
1. 转至&#x200B;**添加权限** - **图表权限** - **委派权限**
1. 为应用程序选择以下权限，然后单击&#x200B;**添加权限**：
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. 转到&#x200B;**身份验证** - **添加平台** - **Web**，然后在&#x200B;**重定向URL**&#x200B;部分中添加以下URL以重定向OAuth代码，然后按&#x200B;**配置**：
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 对每个发布实例重复以上步骤
1. 根据您的要求配置设置
1. 接下来，转到&#x200B;**证书和密码**，单击&#x200B;**新建客户端密码**，并按照屏幕上的步骤创建密码。 请务必记下此密码供以后使用
1. 按左窗格中的&#x200B;**概述**，复制&#x200B;**应用程序（客户端）ID** 和&#x200B;**目录（租户）ID** 的值供以后使用

回顾一下，您必须具有以下信息才能在AEM端为邮件程序服务配置OAuth2：

* 将使用租户 ID 构建的身份验证 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* 将使用租户 ID 构建的令牌 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 将使用租户 ID 构建的刷新 URL。它采用以下形式：`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 客户端 ID
* 客户端密码

**AEM端配置**

接下来，将您的OAuth2设置与AEM集成：

>[!WARNING]
>
>完成此配置后，如果您曾更改OSGi配置&#x200B;**CQ Mailer SMTP OAuth2 Provide**&#x200B;中的&#x200B;*any*&#x200B;值，则必须按照以下步骤再次重新授权。
>
>如果未执行这些操作，则存储在`/conf/global/settings/mailer/oauth`中的访问令牌将无效，并且与SMTP服务器的OAuth2连接将失败。

1. 通过浏览到`http://serveraddress:serverport/system/console/configMgr`转到本地实例的Web控制台
1. 查找并单击&#x200B;**天CQ邮件服务**
1. 添加以下设置：
   * SMTP服务器主机名： `smtp.office365.com`
   * SMTP用户：您的用户名，采用电子邮件格式
   * “发件人”地址：在邮件程序发送的邮件的“发件人：”字段中使用的电子邮件地址
   * SMTP服务器端口： `25`或`587`，具体取决于要求
   * 选中&#x200B;**SMPT的复选框使用StarTLS**，**SMTP需要StarTLS**
   * 检查&#x200B;**OAuth流程**&#x200B;并单击&#x200B;**保存**。
1. 查找，然后单击&#x200B;**CQ Mailer SMTP OAuth2提供程序**
1. 按如下方式填写所需信息：
   * 按照此过程末尾的[处所述，通过构造授权URL、令牌URL和刷新令牌URL来填写它们](#microsoft-outlook)
   * 客户端ID和客户端密钥：使用如上所述检索到的值配置这些字段。
   * 将以下范围添加到配置：
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode重定向Url： `http://localhost:4503/services/mailer/oauth2/token`
   * 刷新令牌URL：其值应与上面的令牌URL的值相同
1. 单击&#x200B;**保存**。

配置完毕后，设置应如下所示：

![已完成的CQ邮件程序SMTP OAuth2配置](assets/oauth-outlook-smptconfig.png)

现在，激活OAuth组件。 您可以执行以下操作来实现此目标：

1. 通过访问以下URL转到组件控制台： `http://serveraddress:serverport/system/console/components`
1. 查找以下组件
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. 按组件左侧的播放图标

![包含OAuthCodeGenerateServlet和OAuthCodeAccessTokenGenerator的组件列表的片段](assets/oauth-components-play.png)

最后，通过以下方式确认配置：

1. 转到发布实例的地址，并以管理员身份登录。
1. 在浏览器中打开新选项卡，然后转到`http://serveraddress:serverport/services/mailer/oauth2/authorize`。 这会将您重定向到SMTP提供商的页面，在本例中为Outlook。
1. 登录并同意授予所需权限
1. 同意后，令牌将存储在存储库中。 您可以通过直接访问发布实例上的此URL在`accessToken`下访问它： `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
