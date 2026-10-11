---
title: 启用 AEM 来搜索受文档安全功能保护的 PDF 和 Microsoft Office 文档
description: 了解如何启用本机AEM搜索，以对受DRM保护的PDF文档执行全文搜索。
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 9%
---
# 启用 AEM 来搜索受文档安全功能保护的 PDF 和 Microsoft Office 文档{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager提供了一个用户界面，用于搜索和查找存储在AEM中的各种资源。 本机搜索能够搜索和定位AEM资源，并对各种常用的文档格式（如纯文本文件、Microsoft Office文档和PDF文档）执行文本搜索。 您还可以扩展和启用本机搜索，以对受DRM保护的PDF和Microsoft Office文档执行全文搜索。

执行以下步骤以允许AEM搜索受Document Security保护的PDF和Microsoft Office文档：

## 开始之前 {#before-you-start}

* 安装和配置AEM Forms Document Security。
* 将包sun.util.calendar添加到&#x200B;**反序列化防火墙配置的中。** 该配置列在`https://'[server]:[port]'/system/console/configMgr`中。
* 确保所有AEM捆绑包均已启动并正在运行。 捆绑包在`https://'[server]:[port]'/system/console/bundles`中列出。 如果所有捆绑包都未处于活动状态，请等待几分钟，然后检查捆绑包的状态。

## 在AEM Forms工作流程（JEE上的AEM Forms）中建立安全连接 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

通过安全连接，可实现JEE上的AEM Forms与同一服务器上运行的OSGi服务之间的无缝信息流。 使用以下方法之一建立安全连接：

* 使用AEM Forms通过JEE管理员凭据配置AEM Forms客户端SDK捆绑包
* 使用相互身份验证配置AEM Forms客户端SDK捆绑包

### 使用AEM Forms通过JEE管理员凭据配置AEM Forms客户端SDK捆绑包 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>：&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK捆绑包。 指定以下属性的值：

   * **服务器URL：**&#x200B;指定JEE服务器上AEM Forms的HTTP URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE keystore file>参数重新启动JEE服务器上的AEM Forms。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。
   * **用户名：**&#x200B;指定AEM Forms on JEE帐户的用户名，用于启动来自AEM Forms on JEE服务器的调用。 指定的帐户必须具有在JEE服务器的AEM Forms上调用文档服务的权限。
   * **密码**：指定用户名字段中提及的AEM Forms on JEE帐户的密码。

   单击&#x200B;**保存**。 启用AEM以搜索受document security保护的PDF和Microsoft Office文档。

### 使用相互身份验证配置AEM Forms客户端SDK捆绑包 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. 为JEE上的AEM Forms启用双向身份验证。 有关详细信息，请参阅[CAC和相互身份验证](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)。
1. 打开AEM配置管理器并以管理员身份登录。 默认URL为https://&lt;serverName>：&lt;port>/lc/system/console/configMgr。
1. 搜索并打开AEM Forms客户端SDK捆绑包。 指定以下属性的值：

   * **服务器URL：**&#x200B;指定JEE服务器上AEM Forms的HTTPS URL。 要启用通过https的通信，请使用-Djavax.net.ssl.trustStore=&lt;JEE keystore file>参数重新启动JEE服务器上的AEM Forms。
   * **启用双向SSL**：启用“启用双向SSL”选项。
   * **KeyStore文件URL**：指定密钥库文件的URL。
   * **TrustStore文件URL**：指定truststore文件的URL。
   * **KeyStore密码**：指定密钥库文件的密码。
   * **TrustStorePassword**：指定truststore文件的密码。
   * **服务名称**：将RightsManagementService添加到指定服务的列表。

   单击&#x200B;**保存**。 AEM能够搜索受document security保护的PDF和Microsoft Office文档

   >[!NOTE]
   >
   > 建议使用 “Ctrl + C” 命令重新启动 SDK。 如果使用其他方式（例如停止 Java 进程）重新启动 AEM SDK，则可能会导致 AEM 开发环境出现不一致情况。

## 为受策略保护的PDF或Microsoft Office示例文档编制索引 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 以管理员身份登录到AEM Assets。
1. 在AEM Digital Asset Manager中创建文件夹，并将受策略保护的PDF或Microsoft Office文档上传到新创建的文件夹。 现在，使用AEM搜索功能搜索受策略保护文档的内容。 必须返回包含搜索文本的文档。
