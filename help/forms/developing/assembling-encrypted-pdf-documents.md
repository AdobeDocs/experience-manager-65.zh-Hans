---
title: 汇编加密的PDF文档
description: 使用Java API和Web服务API汇编加密的PDF文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# 汇编加密的PDF文档 {#assembling-encrypted-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms 。**

您可以使用Assembler服务用密码加密PDF文档。 使用密码加密PDF文档后，用户必须指定密码才能在Adobe Reader或Acrobat中查看PDF文档。 要使用口令加密PDF文档，DDX文档必须包含加密PDF文档所需的加密元素值。

为了进行此讨论，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

在此DDX文档中，请注意已将值指定给源属性 `inDoc`. 如果只有一个输入PDF文档被传递到Assembler服务，并且返回了一个PDF文档，则调用 `invokeOneDocument` 操作，分配值 `inDoc` 到PDF源属性。 调用时 `invokeOneDocument` 操作， `inDoc` value是必须在DDX文档中指定的预定义键。

相反，在将两个或多个输入PDF文档传递到Assembler服务时，您可以调用 `invokeDDX` 操作。 在这种情况下，将输入PDF文档的文件名分配给 `source` 属性。

加密服务不必是AEM Forms安装的一部分，也可以使用密码对PDF文档进行加密。 请参阅 [加密和解密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参见 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的详细信息，请参见 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要汇编加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用不安全的PDF文档。
1. 设置运行时选项。
1. 加密文档。
1. 保存加密的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为JAR文件，这些文件特定于部署AEM Forms的J2EE应用程序服务器。 有关所有AEM Forms JAR文件的位置的信息，请参见 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要组合PDF文档，必须引用DDX文档。 例如，考虑本节介绍的DDX文档。 要加密PDF文档，DDX文档必须包含 `PasswordEncryptionProfile` 元素。

**引用不安全的PDF单据**

必须引用不安全的PDF文档并将其传递给Assembler服务才能对其进行加密。 如果引用已加密的PDF文档，则会引发异常。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。 有关可设置的运行时选项的信息，请参见 `AssemblerOptionSpec` 中的类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**加密文档**

创建Assembler服务客户端、引用包含加密信息的DDX文档、引用不安全的PDF文档并设置运行时选项后，可以调用 `invokeOneDocument` 操作。 由于只有一个输入PDF文档被传递到Assembler服务（并且返回了一个文档），因此您可以使用 `invokeOneDocument` 操作而非 `invokeDDX` 操作。

**保存加密的PDF文档**

如果只有一个PDF文档传递到Assembler服务，则Assembler服务返回单个文档，而不是集合对象。 也就是说，调用 `invokeOneDocument` 操作，则返回单个文档。 由于此节中引用的DDX文档包含加密信息，因此Assembler服务会返回使用口令加密的PDF文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API汇编加密的PDF文档 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，使用它的构造函数传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 通过使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。
   * 创建 `com.adobe.idp.Document` 对象，使用它的构造函数传递 `java.io.FileInputStream` 对象。

1. 引用不安全的PDF文档。

   * 创建 `java.io.FileInputStream` 对象通过使用该对象的构造函数并传递不安全PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 对象并传递 `java.io.FileInputStream` 包含PDF文档的对象。 此 `com.adobe.idp.Document` 对象被传递到 `invokeOneDocument` 方法。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象的 `setFailOnError` 方法和路径 `false`.

1. 加密文档。

   调用 `AssemblerServiceClient` 对象的 `invokeOneDocument` 方法并传递以下值：

   * A `com.adobe.idp.Document` 表示DDX文档的对象。 确保此DDX文档包含值 `inDoc` (对于PDF源元素)。
   * A `com.adobe.idp.Document` 包含不安全PDF文档的对象。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项（包括默认字体和作业日志级别）的对象。

   此 `invokeOneDocument` 方法返回 `com.adobe.idp.Document` 包含密码加密PDF文档的对象。

1. 保存加密的PDF文档。

   * 创建 `java.io.File` 对象并确保文件扩展名为.pdf。
   * 调用 `Document` 对象的 `copyToFile` 用于复制 `Document` 对象到文件。 确保您使用 `Document` 对象 `invokeOneDocument` 方法已返回。

**另请参阅**

[快速入门（SOAP模式）：使用Java API汇编加密的PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用Web服务API汇编加密的PDF文档 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` ，其中包含托管AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

   * 创建 `AssemblerServiceClient` 对象使用默认构造函数。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 此属性在创建服务引用时使用。
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值强制转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象的 `MessageEncoding` 字段至 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 将相应的密码值分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 分配常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 分配常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是：调用其构造函数，并传递一个字符串值，该值表示DDX文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 引用不安全的PDF文档。

   * 创建 `BLOB` 对象。 此 `BLOB` 对象用于存储输入PDF文档。 此 `BLOB` 对象被传递到 `invokeOneDocument` 作为论据。
   * 创建 `System.IO.FileStream` 对象，方法是：调用其构造函数，并传递一个字符串值，该值表示输入PDF文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象的 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象的 `Read` 方法，并传递字节数组、起始位置和要读取的流长度。
   * 填充 `BLOB` 对象，通过指定其 `MTOM` 包含字节数组内容的字段。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用构造函数存储运行时选项的对象。
   * 通过为属于以下对象的数据成员分配值，设置运行时选项以满足您的业务要求 `AssemblerOptionSpec` 对象。 例如，要指示Assembler服务在发生错误时继续处理作业，请分配 `false` 到 `AssemblerOptionSpec` 对象的 `failOnError` 数据成员。

1. 加密文档。

   调用 `AssemblerServiceClient` 对象的 `invokeOneDocument` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象
   * A `BLOB` 表示无保护PDF单据的对象
   * An `AssemblerOptionSpec` 指定运行时选项的对象

   此 `invokeOneDocument` 方法返回 `BLOB` 包含加密PDF文档的对象。

1. 保存加密的PDF文档。

   * 创建 `System.IO.FileStream` 对象，方法是：调用其构造函数，并传递一个字符串值，该值表示加密PDF文档的文件位置以及用于打开文件的模式。
   * 创建一个字节数组，用于存储 `BLOB` 对象 `invokeOneDocument` 方法已返回。 通过获取的值，填充字节数组 `BLOB` 对象的 `MTOM` 数据成员。
   * 创建 `System.IO.BinaryWriter` 对象通过调用其构造函数并传递 `System.IO.FileStream` 对象。
   * PDF通过调用 `System.IO.BinaryWriter` 对象的 `Write` 和传递字节数组。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
