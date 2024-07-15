---
title: 启用AEM以搜索受Document Security保护的PDF文档
description: 了解如何启用本机AEM搜索，以对受DRM保护的PDF文档执行全文搜索。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 启用AEM以搜索受Document Security保护的PDF文档{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM search能够搜索和定位AEM资源，并对各种常用的文档格式(如纯文本文件、Microsoft Office文档和PDF文档)执行文本搜索。 您还可以扩展本机搜索，以便对受AEM Document Security保护的[PDF文档执行全文搜索](../../forms/using/admin-help/document-security.md)。 要使AEM能够对此类文档执行全文搜索，请执行以下步骤：

1. 建立安全连接
1. 为受策略保护的PDF示例文档编制索引

## 先决条件 {#prerequisites}

* 如果您在OSGi上使用AEM Forms：

   * 在AEM Forms服务器上安装[AEM Forms Document Security Indexer包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)。

   * 确保JEE服务器上的AEM Forms已启动并正在运行，并且JEE服务器上的相应AEM Forms上安装了Document Security。 需要JEE服务器上的AEM表单才能对受保护文档编制索引。

* 如果您在JEE服务器上只使用AEM Forms，则表示已安装了索引器包。
* 确保所有捆绑包都已启动并正在运行。 如果所有捆绑包都未处于活动状态，请等待所有捆绑包都启动并运行。

   * 对于OSGi上的AEM Forms，捆绑包位于https://&#39;[server]：[port]&#39;/system/console/bundles。
   * 对于JEE上的AEM Forms，捆绑包位于https://&#39;[server]：[port]&#39;/[context-path]/system/console/bundles。 例如，https://localhost:8080/lc/system/console/bundles。

* 将&#x200B;*sun.util.calendar*&#x200B;程序包添加到允许列表。 要将软件包添加到允许列表，请执行以下步骤：

   1. 打开AEM Web控制台。 URL是https://&#39;[服务器]：[端口]&#39;/system/console/configMgr。
   1. 找到并打开&#x200B;**反序列化防火墙配置**。

   1. 列入允许列表将sun.util.calendar包添加到类或包前缀字段，然后单击&#x200B;**保存**。

### 在AEM Forms JEE和OSGi栈栈之间建立安全连接 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

您可以使用以下方法之一来建立安全连接：

* 使用AEM Forms通过JEE管理员凭据配置AdobeLiveCycle客户端SDK包
* 使用相互身份验证配置AdobeLiveCycle客户端SDK捆绑包

#### 使用AEM Forms通过JEE管理员凭据配置AdobeLiveCycle客户端SDK包 {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM Web控制台。 URL是https://&#39;[服务器]：[端口]&#39;/system/console/configMgr。
1. 找到并打开&#x200B;**AdobeLiveCycle客户端SDK包**。 指定以下字段的值：

   * **服务器URL：**&#x200B;指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>参数重新启动服务器。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。
   * **用户名：**&#x200B;指定AEM Forms on JEE帐户的用户名以启动来自AEM服务器的调用。 指定的帐户必须具有在JEE服务器的AEM Forms上启动文档服务的权限。
   * **密码**：指定用户名字段中提及的AEM Forms on JEE帐户的密码。

   单击&#x200B;**保存**。启用AEM以搜索受Document Security保护的PDF文档。

#### 使用相互身份验证配置AdobeLiveCycle客户端SDK捆绑包 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. 为JEE上的AEM Forms启用双向身份验证。 有关详细信息，请参阅[CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM Web控制台。 URL是https://&#39;[服务器]：[端口]&#39;/system/console/configMgr。
1. 找到并打开&#x200B;**AdobeLiveCycle客户端SDK**&#x200B;包。 指定以下属性的值：

   * **服务器URL**：指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE keystore file>参数上的AEM Forms的路径>重新启动AEM服务器。
   * **启用双向SSL**：启用“启用双向SSL”选项。
   * **KeyStore文件URL**：指定密钥库文件的URL。
   * **TrustStore文件URL**：指定truststore文件的URL。
   * **KeyStore密码**：指定密钥库文件的密码。
   * **TrustStorePassword**：指定truststore文件的密码。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。启用AEM以搜索受Document Security保护的PDF文档

### 为受策略保护的PDF示例文档编制索引 {#index-a-sample-policy-protected-pdf-document}

1. 以管理员身份登录到AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF文档上传到新创建的文件夹。

   现在，您可以使用AEM搜索功能搜索受策略保护的文档。

   >[!NOTE]
   >
   > 建议使用“Ctrl + C”命令重新启动SDK。 使用替代方法（例如，停止Java进程）重新启动AEM SDK可能会导致AEM开发环境不一致。
