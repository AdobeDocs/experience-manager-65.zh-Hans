---
title: 验证DX文档
seo-title: 验证DX文档
description: 使用Java API和Web服务API以编程方式验证DDX文档。
seo-description: 使用Java API和Web服务API以编程方式验证DDX文档。
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 0%

---

# 验证DDX文档{#validating-ddx-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

您可以以编程方式验证汇编程序服务使用的DDX文档。 即，使用汇编程序服务API，可以确定DDX文档是否有效。 例如，如果您从以前的AEM Forms版本升级，并且希望确保DDX文档有效，则可以使用汇编程序服务API验证它。

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要验证DDX文档，请执行以下任务：

1. 包括项目文件。
1. 创建汇编程序客户端。
1. 引用现有DDX文档。
1. 设置运行时选项以验证DDX文档。
1. 执行验证。
1. 将验证结果保存在日志文件中。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

要验证DDX文档，必须引用现有DDX文档。

**设置运行时选项以验证DDX文档**

验证DDX文档时，必须设置特定的运行时选项，这些选项指示汇编程序服务验证DDX文档，而不是执行它。 此外，您还可以增加汇编程序服务写入日志文件的信息量。

**执行验证**

在创建汇编程序服务客户端、引用DDX文档并设置运行时选项后，可以调用`invokeDDX`操作来验证DDX文档。 验证DDX文档时，可以传递`null`作为映射参数（此参数通常存储汇编程序执行DDX文档中指定的操作所需的PDF文档）。

如果验证失败，则会引发异常，并且日志文件包含详细信息，说明DDX文档无效的原因，可以从`OperationException`实例获取。 在经过基本XML解析和模式检查后，将执行针对DDX规范的验证。 位于DDX文档中的所有错误都在日志中指定。

**将验证结果保存在日志文件中**

汇编程序服务返回可写入XML日志文件的验证结果。 汇编程序服务写入日志文件的详细信息量取决于您设置的运行时选项。

**另请参阅**

[使用Java API验证DDX文档](#validate-a-ddx-document-using-the-java-api)

[使用Web服务API验证DDX文档](#validate-a-ddx-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#validate-a-ddx-document-using-the-java-api}验证DDX文档

使用汇编程序服务API(Java)验证DDX文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 设置运行时选项以验证DDX文档。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 设置运行时选项，该选项指示汇编程序服务通过调用`AssemblerOptionSpec`对象的setValidateOnly方法并传递`true`来验证DDX文档。
   * 通过调用`AssemblerOptionSpec`对象的`getLogLevel`方法并传递字符串值来设置汇编程序服务写入日志文件的信息量，这些信息符合您的要求。 验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以传递值`FINE`或`FINER`。

1. 执行验证。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。
   * java.io.Map对象的值`null`，通常用于存储PDF文档。
   * 指定运行时选项的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象。

   `invokeDDX`方法返回一个`AssemblerResult`对象，该对象包含指定DDX文档是否有效的信息。

1. 将验证结果保存在日志文件中。

   * 创建`java.io.File`对象，并确保文件扩展名为.xml。
   * 调用`AssemblerResult`对象的`getJobLog`方法。 此方法会返回一个包含验证信息的`com.adobe.idp.Document`实例。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。

   >[!NOTE]
   >
   >如果DDX文档无效，则会引发`OperationException`。 在catch语句中，可以调用`OperationException`对象的`getJobLog`方法。

**另请参阅**

[验证DX文档](#validating-ddx-documents)

[快速入门（SOAP模式）：使用Java API（SOAP模式）验证DDX文](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) 档

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#validate-a-ddx-document-using-the-web-service-api}验证DDX文档

使用汇编程序服务API（Web服务）验证DDX文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将localhost替换为Forms服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 使用`AssemblerServiceClient`对象的默认构造函数创建对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`AssemblerServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式，可创建对象。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。

1. 设置运行时选项以验证DDX文档。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 设置运行时选项，该选项指示汇编程序服务通过将值true分配给`AssemblerOptionSpec`对象的`validateOnly`数据成员来验证DDX文档。
   * 通过为`AssemblerOptionSpec`对象的`logLevel`数据成员分配字符串值来设置汇编程序服务写入日志文件的信息量。 方法验证DDX文档时，您希望将更多信息写入日志文件，以协助验证过程。 因此，您可以指定值`FINE`或`FINER`。 有关可设置的运行时选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

1. 执行验证。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象。
   * 通常存储PDF文档的`Map`对象的值`null`。
   * 指定运行时选项的`AssemblerOptionSpec`对象。

   `invokeDDX`方法返回一个`AssemblerResult`对象，该对象包含指定DDX文档是否有效的信息。

1. 将验证结果保存在日志文件中。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示日志文件的文件位置以及在中打开该文件的模式，可创建对象。 确保文件扩展名为.xml。
   * 通过获取`AssemblerResult`对象`jobLog`数据成员的值，创建用于存储日志信息的`BLOB`对象。
   * 创建用于存储`BLOB`对象内容的字节数组。 通过获取`BLOB`对象`MTOM`字段的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

   >[!NOTE]
   >
   >如果DDX文档无效，则会引发`OperationException`。 在catch语句中，可以获取`OperationException`对象`jobLog`成员的值。

**另请参阅**

[验证DX文档](#validating-ddx-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
