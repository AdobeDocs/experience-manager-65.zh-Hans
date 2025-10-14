---
title: 文档安全产品
description: 了解AEM Document Security的各种工具和功能。
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# 文档安全产品{#document-security-offerings}

Adobe Experience Manager Forms document security确保只有授权用户才能使用您的文档。 使用Document Security，您可以安全地分发以支持的格式保存的任何信息。 支持的文件格式包括Adobe可移植文档格式(PDF)和Microsoft®Word、Excel和PowerPoint文件。

您可以使用策略保护文档。 您在策略中指定的机密性设置确定收件人如何使用您应用策略的文档。 例如，您可以指定收件人是否可以打印或复制文本、编辑文本或者向受保护文档添加签名和注释。

策略存储在Document Security服务器上；您可以通过客户端应用程序将策略应用到文档。 将策略应用到文档时，策略中指定的机密性设置保护文档包含的信息。 您可以将受策略保护的文档分发给策略授权的收件人。

下图显示了AEM Forms Document Security的典型架构：

![Document Security — 建议的架构](do-not-localize/document_security_architecture.png)

## Document Security客户端 {#document-security-clients}

Document Security提供各种客户端来保护文档，查看和编辑受保护的文档，并提供索引器以启用对受保护文档的全文搜索。 您可以根据您的要求和客户端的功能选择客户端。

Document Security Server是Document Security执行事务（如用户身份验证、实时策略管理和机密性应用）的中心组件。 该服务器还为策略、审计记录和其他相关信息提供了一个中央存储库。

Document Security服务器提供了一个基于Web的界面（网页），用于创建策略、管理受策略保护的文档以及监控与受策略保护文档关联的事件。 管理员还可以为受邀用户配置全局选项，如用户身份验证、审核和消息传送，以及管理受邀用户帐户。

该服务器包含在AEM Forms Document Security附加产品中。 您可以联系AEM Forms [销售团队](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG)以购买Document Security加载项。

### Protect文档 {#protect-documents}

AEM Forms Document Security提供了多种应用安全策略的工具。 您可以根据要求和规格选择工具。

![document-security-offers](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Document Security Extension for Microsoft®Office或可移植保护库来应用和跟踪安全策略：

* **Document Security SDK：**&#x200B;该SDK是功能丰富的客户端。 您可以使用Document Security SDK访问文档服务器功能，打开受策略保护的文档，以及开发自定义扩展、插件或应用程序。 例如，您可以开发扩展以保护自定义文件格式，或将SDK与数据丢失防护(DLP)解决方案集成。 使用Document Security SDK开发的扩展、应用程序和插件可将文档发送到指定的AEM Forms服务器，并且策略会应用于该服务器。 AEM Forms Document Security客户端SDK (CSDK)无法取消保护使用可移植保护库(PPL)保护的文档，反之亦然。

  Document Security SDK适用于Java™和C++。 Java™ SDK包含在AEM Forms Document Security产品中，并安装在在JEE上部署AEM Forms时。 联系[AEM客户支持](https://experienceleague.adobe.com/zh-hans?support-solution=General&support-tab=home#support)以获取C++ SDK。 C++ SDK可以使用Microsoft® Visual Studio 2013进行编译。 访问[Document Security API文档](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html)网站，您可以在其中学习和使用SDK的功能。

* **Adobe Acrobat：**&#x200B;您可以使用Adobe Acrobat将安全策略应用于PDF使用常用桌面应用程序(如Microsoft®Office、Web浏览器或任何支持PDF打印的应用程序)创建的文档。

  您可以从[Adobe网站](https://www.adobe.com/acrobat/free-trial-download.html)购买并下载Adobe Acrobat。 Adobe Acrobat文章[为PDF设置安全策略](https://helpx.adobe.com/cn/acrobat/using/setting-security-policies-pdfs.html)提供了有关在Adobe Acrobat中创建和应用策略的详细信息。

* **Document Security Extension for Microsoft® Office**：您可以使用Document Security Extension for Microsoft® Office，在Microsoft® Office程序中将预定义策略应用于Microsoft® Office文件。 该扩展可确保只有授权人员才能使用受策略保护的Microsoft®Word、Excel和PowerPoint文件。 只有安装了此插件的授权用户才能使用受策略保护的文件。

  Document Security Extension可作为Microsoft® Office插件使用。 联系[AEM客户支持](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html)以获取扩展。 稍后，您可以访问[Document Security Extension for Microsoft® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=zh-Hans)帮助，了解有关安装、配置和使用该扩展的信息。

* **可移植保护库：** PPL在本地保护文档，而不将文档发送到AEM Forms服务器。 只有安全凭据和策略详细信息通过网络传递。 PPL还允许您将策略检索访问权限限制为仅登录用户。 您可以根据已登录AEM用户的上下文来获取策略。

  除上述功能外，PPL还具有Document Security SDK的所有功能。 您可以使用Document Security SDK访问文档服务器功能，打开受策略保护的文档，以及开发自定义扩展、插件或应用程序。 PPL无法取消保护使用AEM Forms Document Security客户端SDK (CSDK)或相反方式保护的文档。

  PPL可用于32位和64位版本的Java™和C++语言。 它还作为OSGi上AEM Forms的OSGi包提供。 C++ PPL可以使用Microsoft® Visual Studio 2013进行编译。 如果您已许可AEM Forms Document Security加载项，则可以联系[AEM Forms Document Security](https://experienceleague.adobe.com/zh-hans?support-solution=General&support-tab=home#support)支持团队以获取PPL。 之后，您可以使用PPL帮助（与库捆绑在一起）来设置和使用PPL。

### 查看或编辑受保护的文档 {#view-or-edit-protected-documents}

* 对于&#x200B;**PDF文档**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile查看受保护的PDF文档。 大多数用户在其设备上已安装Acrobat Reader，因此他们无需获取或学习其他软件即可查看受保护的文档。 您还可以从[Acrobat Reader下载网站](https://get.adobe.com/reader/)下载Acrobat Reader。

* 对于&#x200B;**Microsoft® Office文档**，您需要使用Microsoft® Office和AEM Forms Document Security Extension for Microsoft® Office。 Document Security Extension可作为Microsoft® Office插件使用。 您可以从Adobe网站下载扩展。

### 索引受保护的文档 {#index-protected-documents}

Microsoft® Windows全文搜索引擎(SharePoint Index server)和Adobe Experience Manager (AEM)可以对常用的文档格式(如纯文本文件、Microsoft® Office文档和PDF文档)执行全文搜索。 您可以使用Document Security索引器启用全文搜索引擎来搜索受保护的PDF文档：

* **iFilter索引器：**&#x200B;您可以使用iFilter索引器为受保护的PDF文档编制索引，并使Microsoft® Windows全文搜索引擎(Desktop Indexing Service和SharePoint Index Server)能够搜索受保护的PDF文档。 有关详细信息，请参阅受保护文档的[AEM SharePoint IFilter](assets/sharepoint-ifilter-doc-security.pdf)。

* **AEM Forms Document Security Indexer：**&#x200B;您可以使用AEM Forms Document Security indexer为受保护的PDF文档编制索引，并使Adobe Experience Manager能够搜索受保护的PDF文档。 索引器是AEM Forms Document Security产品的一部分。 JEE安装程序上的AEM Forms中包含这些组件。
