---
title: 汇编非交互式PDF文档
seo-title: 汇编非交互式PDF文档
description: 使用非交互式PDF表单作为输入，以使用Java API和Web服务API来组合非交互式PDF文档。
seo-description: 使用非交互式PDF表单作为输入，以使用Java API和Web服务API来组合非交互式PDF文档。
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---

# 汇编非交互式PDF文档{#assembling-non-interactive-pdf-documents}

使用交互式PDF表单作为输入时，可以组合非交互式PDF文档。 也就是说，假定您有一个表单，用户可以使用该表单在其字段中输入数据。 您可以将该表单传递到汇编程序服务，从而汇编程序服务返回PDF文档，该文档阻止用户在其字段中输入数据。 本文档是非交互式PDF表单。 例如，下图显示了一个表示交互式表单的抵押贷款应用程序。

在本讨论中，假定使用了以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

在此DDX文档中，请注意为源属性分配了值`inDoc`。 如果仅将一个输入的PDF文档传递到汇编程序服务，并返回一个PDF文档，并调用`invokeOneDocument`操作，则将值`inDoc`分配给PDF源属性。 调用`invokeOneDocument`操作时，`inDoc`值是必须在DDX文档中指定的预定义键值。

相反，在将两个或更多输入的PDF文档传递到汇编程序服务时，可以调用`invokeDDX`操作。 在这种情况下，将输入PDF文档的文件名分配给`source`属性。

此DDX文档包含`NoXFA`元素，该元素会指示汇编程序服务返回非交互式PDF文档。

如果输入的PDF文档基于Acrobat表单或静态XFA表单，则汇编程序服务可以汇编非交互式PDF文档，而“输出”服务不是AEM表单安装的一部分。 但是，如果输入的PDF文档是动态XFA表单，则输出服务必须包含在AEM表单安装中。 如果组装动态XFA表单时，输出服务未包含在AEM表单安装中，则会引发异常。 请参阅[创建文档输出流](/help/forms/developing/creating-document-output-streams.md)。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用汇编程序服务来汇编PDF文档。 本节不讨论相关概念，例如创建包含输入文档的集合对象，或了解如何从返回的集合对象中提取结果。 （请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)。）

>[!NOTE]
>
>有关汇编程序服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤{#summary-of-steps}的摘要

要组合非交互式PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用交互式PDF文档。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存非交互式PDF文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。

**创建汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档来组合PDF文档。 此DDX文档必须包含`NoXFA`元素，该元素会指示汇编程序服务返回非交互式PDF文档。

**引用交互式PDF文档**

必须引用交互式PDF文档并将其传递到汇编程序服务，才能返回非交互式PDF文档。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。

**组合PDF文档**

在创建汇编程序服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用`invokeOneDocument`操作。 由于只有一个输入的PDF文档被传递到汇编程序服务并且返回了一个文档，因此您可以使用`invokeOneDocument`操作而不是`invokeDDX`操作。

**保存非交互式PDF文档**

如果仅将单个PDF文档传递到汇编程序服务，汇编程序服务将返回单个文档而不是集合对象。 也就是说，调用`invokeOneDocument`操作时，会返回一个文档。 由于本节中引用的DDX文档包含创建非交互式PDF文档的说明，汇编程序服务会返回一个非交互式PDF文档，该文档可以另存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}组合非交互式PDF文档

使用汇编程序服务API(Java)汇编非交互式PDF文档：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`AssemblerServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 使用DDX文档的构造函数并传递指定DDX文件位置的字符串值，创建一个表示该文档的`java.io.FileInputStream`对象。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 引用交互式PDF文档。

   * 使用`java.io.FileInputStream`对象的构造函数创建一个对象，并传递交互式PDF文档的位置。
   * 创建`com.adobe.idp.Document`对象并传递包含PDF文档的`java.io.FileInputStream`对象。 此`com.adobe.idp.Document`对象将传递到`invokeOneDocument`方法。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法来设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`com.adobe.idp.Document`对象。 确保此DDX文档包含PDF源元素的值`inDoc`。
   * 包含交互式PDF文档的`com.adobe.idp.Document`对象。
   * `com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象，用于指定运行时选项，包括默认字体和作业日志级别。

   `invokeOneDocument`方法返回一个包含非交互式PDF文档的`com.adobe.idp.Document`对象。

1. 保存非交互式PDF文档。

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`Document`对象的`copyToFile`方法，将`Document`对象的内容复制到文件。 确保使用`invokeOneDocument`方法返回的`Document`对象。

* “快速入门（SOAP模式）：使用Java API汇编非交互式PDF文档”

## 使用Web服务API {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}组合非交互式PDF文档

使用汇编程序服务API（Web服务）汇编非交互式PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建汇编程序客户端。

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
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 引用交互式PDF文档。

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储输入的PDF文档。 此`BLOB`对象将作为参数传递到`invokeOneDocument`。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置和在中打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`字段分配字节数组的内容来填充该对象。

1. 设置运行时选项。

   * 使用`AssemblerOptionSpec`的构造函数创建一个用于存储运行时选项的对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配一个值，设置运行时选项以满足您的业务要求。 例如，要指示汇编程序服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeOneDocument`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 表示交互式PDF文档的`BLOB`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeOneDocument`方法返回一个包含非交互式PDF文档的`BLOB`对象。

1. 保存非交互式PDF文档。

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示非交互式PDF文档的文件位置以及在中打开文件的模式，来创建对象。
   * 创建一个字节数组，用于存储`invokeOneDocument`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`MTOM`字段的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

* “快速入门(MTOM):使用Web服务API汇编非交互式PDF文档”。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
