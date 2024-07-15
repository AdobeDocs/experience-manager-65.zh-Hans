---
title: 端点类型
description: 了解不同类型的端点。 可以将不同类型的端点（如电子邮件、Watched文件夹等）添加到服务。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 380cab7f-e7f7-4cb7-bd20-ea530a349fac
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 端点类型 {#types-of-endpoints}

必须先配置和启用端点，然后才能使用服务。 终结点指定如何调用服务。

>[!NOTE]
>
>在Workbench中，端点称为起点。

可以将以下类型的端点添加到服务。 并非所有服务都支持所有端点：

**电子邮件：**&#x200B;通过向指定的电子邮件帐户发送一封包含一个或多个文件附件的电子邮件，使用户能够调用服务。 在配置电子邮件端点之前，必须配置所需的电子邮件帐户。 （请参阅配置电子邮件端点。）

**观察文件夹：**&#x200B;使用户可以通过将文件放入文件夹来调用服务，该文件夹以定义的时间间隔扫描。 （请参阅配置观察文件夹端点。）

**任务管理器：**&#x200B;允许Workspace用户调用该服务。

**远程处理：**&#x200B;使使用Flex构建的应用程序能够使用(不推荐用于AEM表单)AEM表单远程处理来调用该服务。 将为每个激活的服务自动创建远程端点。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的远程对象，以调用对相关服务的操作。

**SOAP：**&#x200B;允许使用AEM表单编程API开发的客户端应用程序使用SOAP模式调用该服务。 将为每个激活的服务自动创建SOAP端点。

**注意**：在Adobe Acrobat或Adobe Reader中查看文档时使用SOAP端点时，可以从document security文档中删除&#x200B;*安全性。 有关如何在LCRM文档上禁用SOAP端点的详细信息，请参阅[为文档安全文档禁用SOAP端点](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB：**&#x200B;使使用AEM表单编程API开发的客户端应用程序能够使用Enterprise JavaBeans (EJB)模式调用该服务。 将为每个激活的服务自动创建EJB端点。

**WSDL：**&#x200B;使使用AEM表单编程API开发的客户端应用程序能够使用Web服务定义语言(WSDL)调用该服务。 “核心配置”页包含一个选项，用于为AEM表单中的所有服务启用WSDL生成。 (请参阅配置常规AEM表单设置。)

可以配置在Workbench中创建的&#x200B;**REST：**&#x200B;进程，以便您可以通过代表性状态传输(REST)请求调用它们。 从HTML页发送REST请求。 即，您可以使用REST请求直接从网页调用AEM表单进程。

电子邮件、 TaskManager 、 Watched Folder和Remoting端点仅公开服务的特定操作。 添加这些端点需要执行第二个配置步骤，以选择用于调用服务的方法、设置配置参数以及指定输入和输出参数映射。
