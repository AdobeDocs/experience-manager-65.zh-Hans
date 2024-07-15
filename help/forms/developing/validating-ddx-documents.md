---
title: 验证DDX文档
description: 使用Java API和Web服务API以编程方式验证DDX文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 0%

---

# 验证DDX文档 {#validating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以以编程方式验证汇编程序服务使用的DDX文档。 即，使用Assembler服务API，您可以确定DDX文档是否有效。 例如，如果您从以前的AEM Forms版本升级，并且要确保DDX文档有效，则可以使用汇编程序服务API验证它。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要验证DDX文档，请执行以下任务：

1. 包括项目文件。
1. 创建Assembler客户端。
1. 引用现有DDX文档。
1. 设置运行时选项以验证DDX文档。
1. 执行验证。
1. 将验证结果保存在日志文件中。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为JAR文件，这些文件特定于部署AEM Forms的J2EE应用程序服务器。

**创建PDF汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要验证DDX文档，必须引用现有的DDX文档。

**设置运行时选项以验证DDX文档**

验证DDX文档时，必须设置特定的运行时选项，以指示Assembler服务验证DDX文档，而不是执行文档。 此外，您还可以增加Assembler服务写入日志文件的信息量。

**执行验证**

创建Assembler服务客户端、引用DDX文档并设置运行时选项后，可以调用`invokeDDX`操作来验证DDX文档。 验证DDX文档时，您可以将`null`作为映射参数传递(此参数通常存储汇编程序执行DDX文档中指定的操作所需的PDF文档)。

如果验证失败，则会引发异常，并且日志文件包含详细信息，说明为何可从`OperationException`实例获取DDX文档无效。 一旦通过了基本的XML解析和模式检查，就会执行针对DDX规范的验证。 DDX文档中的所有错误都在日志中指定。

**将验证结果保存在日志文件中**

Assembler服务返回可以写入XML日志文件的验证结果。 Assembler服务写入日志文件的详细信息量取决于您设置的运行时选项。

**另请参阅**

[使用Java API验证DDX文档](#validate-a-ddx-document-using-the-java-api)

[使用Web服务API验证DDX文档](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API验证DDX文档 {#validate-a-ddx-document-using-the-java-api}

使用Assembler服务API (Java)验证DDX文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`AssemblerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用其构造函数并传递指定DDX文件位置的字符串值，创建表示DDX文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 设置运行时选项以验证DDX文档。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用`AssemblerOptionSpec`对象的setValidateOnly方法并传递`true`，设置指示Assembler服务验证DDX文档的运行时选项。
   * 通过调用`AssemblerOptionSpec`对象的`getLogLevel`方法并传递一个符合要求的字符串值，设置Assembler服务写入日志文件的信息量。 验证DDX文档时，您需要将更多信息写入日志文件，以帮助验证过程。 因此，您可以传递值`FINE`或`FINER`。

1. 执行验证。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。
   * java.io.Map对象(通常存储PDF文档)的值`null`。
   * 指定运行时选项的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象。

   `invokeDDX`方法返回包含指定DDX文档是否有效的信息的`AssemblerResult`对象。

1. 将验证结果保存在日志文件中。

   * 创建`java.io.File`对象并确保文件扩展名为.xml。
   * 调用`AssemblerResult`对象的`getJobLog`方法。 此方法返回包含验证信息的`com.adobe.idp.Document`实例。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`com.adobe.idp.Document`对象的内容复制到文件中。

   >[!NOTE]
   >
   >如果DDX文档无效，则抛出`OperationException`。 在catch语句中，您可以调用`OperationException`对象的`getJobLog`方法。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[快速入门(SOAP模式)：使用Java API验证DDX文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)(SOAP模式)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API验证DDX文档 {#validate-a-ddx-document-using-the-web-service-api}

使用Assembler服务API（Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将localhost替换为Forms服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 使用默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示DDX文档的文件位置以及用于打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 设置运行时选项以验证DDX文档。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为`AssemblerOptionSpec`对象的`validateOnly`数据成员分配值true，设置指示Assembler服务验证DDX文档的运行时选项。
   * 通过为`AssemblerOptionSpec`对象的`logLevel`数据成员分配字符串值，设置Assembler服务写入日志文件的信息量。 方法验证DDX文档时，您需要将更多信息写入日志文件，以帮助验证过程。 因此，您可以指定值`FINE`或`FINER`。 有关可设置的运行时选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

1. 执行验证。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 通常存储PDF文档的`Map`对象的值`null`。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invokeDDX`方法返回包含指定DDX文档是否有效的信息的`AssemblerResult`对象。

1. 将验证结果保存在日志文件中。

   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示日志文件的文件位置以及用于打开文件的模式。 确保文件扩展名为.xml。
   * 通过获取`AssemblerResult`对象的`jobLog`数据成员的值，创建存储日志信息的`BLOB`对象。
   * 创建用于存储`BLOB`对象的内容的字节数组。 通过获取`BLOB`对象的`MTOM`字段的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

   >[!NOTE]
   >
   >如果DDX文档无效，则抛出`OperationException`。 在catch语句中，您可以获取`OperationException`对象的`jobLog`成员的值。

**另请参阅**

[验证DDX文档](#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
