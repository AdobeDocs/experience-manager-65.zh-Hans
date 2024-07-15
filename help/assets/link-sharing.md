---
title: 使用链接共享资源
description: 将资源、文件夹和收藏集共享为URL。
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 6%

---

# 将资产作为链接共享 {#asset-link-sharing}

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | 本文 |

[!DNL Adobe Experience Manager Assets]允许您将资产、文件夹和收藏集作为URL与您的组织成员和外部实体（包括合作伙伴和供应商）共享。 通过链接共享资产是一种便利的方法，使外部参与方无需先登录[!DNL Assets]即可使用资源。

>[!PREREQUISITES]
>
>* 您需要对要作为链接共享的文件夹或资产具有`Edit ACL`权限。
>* 若要向用户发送电子邮件，请在[Day CQ邮件服务](#configmailservice)中配置SMTP服务器详细信息。

## 共享资源 {#share-assets}

要生成要与用户共享的资源URL，请使用[!UICONTROL 链接共享]对话框。

* 具有管理员权限或在`/var/dam/share`位置具有读取权限的用户可以查看与其共享的链接。
* 在`/var/dam/jobs/download`位置具有读取权限的用户可以从共享链接下载资产。

1. 在[!DNL Assets]用户界面中，选择要作为链接共享的资产。

1. 在工具栏中，单击&#x200B;**[!UICONTROL 共享链接]** ![共享资产图标](assets/do-not-localize/assets_share.png)。 单击&#x200B;**[!UICONTROL 共享]**&#x200B;后创建的链接预先显示在[!UICONTROL 共享链接]字段中。 选择&#x200B;**[!UICONTROL 提交]**&#x200B;后才会创建链接。

   ![与链接共享对话](assets/share-assets-as-link.png)

   *图：将资源共享为链接的对话框。*

1. 在&#x200B;**[!UICONTROL 链接共享]**&#x200B;对话框的电子邮件地址框中，键入要与其共享链接的用户的电子邮件 ID。您可以添加一个或多个用户。

   >[!NOTE]
   >
   >如果您输入的电子邮件ID不是您组织的成员，则单词[!UICONTROL 外部用户]将带有该用户的电子邮件ID前缀。

1. 在&#x200B;**[!UICONTROL 主题]**&#x200B;框中，输入要共享的资源的主题。

1. 在&#x200B;**[!UICONTROL 消息]**&#x200B;框中，输入可选消息。

1. 在&#x200B;**[!UICONTROL 过期]**&#x200B;字段中，指定链接停止工作的过期日期和时间。 链接的默认过期时间为一天。

   ![设置共享链接的过期日期](assets/Set-shared-link-expiration.png)

1. 要允许用户下载原始资源，请选择&#x200B;**[!UICONTROL 允许下载原始文件]**。 要允许用户仅下载共享资源的演绎版，请选择&#x200B;**[!UICONTROL 允许下载文件的演绎版]**。

1. 单击&#x200B;**[!UICONTROL 共享]**。 将显示一条消息，确认通过电子邮件将该链接与用户共享。

1. 要查看共享资产，请单击发送给用户的电子邮件中的链接。 要生成资源的预览，请单击共享资源。 要关闭预览，请单击&#x200B;**[!UICONTROL 上一步]**。 如果已共享文件夹，请单击&#x200B;**[!UICONTROL 父文件夹]**&#x200B;以返回到父文件夹。

   ![共享资源的预览](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager]仅支持生成[支持的文件类型](/help/assets/assets-formats.md)的资源预览。 如果共享其他MIME类型，则只能下载资源且无法预览。

1. 要下载共享资源，请单击工具栏中的&#x200B;**[!UICONTROL 选择]**，单击该资源，然后单击工具栏中的&#x200B;**[!UICONTROL 下载]**。

   用于下载共享资源的![工具栏选项](assets/chlimage_1-547.png)

1. 要查看您作为链接共享的资源，请转到[!DNL Assets]用户界面并单击[!DNL Experience Manager]徽标。 选择&#x200B;**[!UICONTROL 导航]**。 在“导航”窗格中，选择&#x200B;**[!UICONTROL 共享链接]**&#x200B;以显示共享资源列表。

1. 要取消共享资产，请选择该资产并单击工具栏中的&#x200B;**[!UICONTROL 取消共享]**。 随后将显示确认消息。 资源的条目将从列表中删除。

## 配置Day CQ邮件服务 {#configure-day-cq-mail-service}

1. 在[!DNL Experience Manager]主页上，导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 在服务列表中，找到&#x200B;**[!UICONTROL 天CQ邮件服务]**。
1. 单击服务旁边的&#x200B;**[!UICONTROL 编辑]**，并为&#x200B;**[!UICONTROL Day CQ Mail Service]**&#x200B;配置以下参数，并针对其名称提供详细信息：

   * SMTP服务器主机名：电子邮件服务器主机名
   * SMTP服务器端口：电子邮件服务器端口
   * SMTP用户：电子邮件服务器用户名
   * SMTP密码：电子邮件服务器密码

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. 单击&#x200B;**[!UICONTROL 保存]**。

## 配置最大数据大小 {#configure-maximum-data-size}

当您从使用链接共享功能共享的链接下载资产时，[!DNL Experience Manager]会从存储库压缩资产层次结构，然后以ZIP文件返回该资产。 但是，由于ZIP文件中可以压缩的数据量没有限制，因此会压缩大量数据，这会导致JVM中出现内存不足错误。 为了保护系统免受由于此情况而导致的潜在拒绝服务攻击，请在Configuration Manager中使用&#x200B;**[!UICONTROL Day CQ DAM临时资产共享代理Servlet]**&#x200B;的&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数配置最大大小。 如果资产的未压缩大小超过配置值，则会拒绝资产下载请求。 默认值为100 MB。

1. 单击[!DNL Experience Manager]徽标，然后转到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。
1. 从Web控制台中，找到&#x200B;**[!UICONTROL Day CQ DAM临时资产共享代理Servlet]**&#x200B;配置。
1. 在编辑模式下打开 **[!UICONTROL Day CQ DAM 临时资产共享代理 Servlet]** 配置，并修改&#x200B;**[!UICONTROL 最大内容大小（未压缩）]**&#x200B;参数的值。

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. 保存更改。

## 最佳实践和疑难解答 {#best-practices-and-troubleshooting}

* 名称中包含空格的资产文件夹或收藏集可能无法共享。
* 如果用户无法下载共享资源，请与[!DNL Experience Manager]管理员确认[下载限制](#configure-maximum-data-size)是什么。
* 如果您无法发送包含共享资源链接的电子邮件，或者其他用户无法接收您的电子邮件，请向您的[!DNL Experience Manager]管理员确认是否配置了[电子邮件服务](#configure-day-cq-mail-service)。
* 如果您无法使用链接共享功能共享资源，请确保您拥有适当的权限。 请参阅[共享资源](#share-assets)。
* 如果将共享资源移动到其他位置，则其链接将停止工作。 重新创建链接并与用户重新共享。

* 如果要将来自[!DNL Experience Manager]创作部署的链接共享到外部实体，请确保仅针对`GET`请求公开以下用于链接共享的URL。 出于安全原因，阻止其他URL。

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  在[!DNL Experience Manager]界面中，访问&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 打开&#x200B;**[!UICONTROL Day CQ Link Externalizer]**&#x200B;配置，并在&#x200B;**[!UICONTROL Domains]**&#x200B;字段中修改以下属性，这些属性的值针对`local`、`author`和`publish`提及。 对于`local`和`author`属性，请分别提供本地实例和创作实例的URL。 如果您运行单个[!DNL Experience Manager]创作实例，请为`local`和`author`属性使用相同的值。 对于Publish实例，请提供[!DNL Experience Manager] Publish实例的URL。
