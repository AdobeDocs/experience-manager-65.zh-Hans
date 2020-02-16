---
title: 汇编加密的PDF文档
seo-title: 汇编加密的PDF文档
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 汇编加密的PDF文档 {#assembling-encrypted-pdf-documents}

您可以使用Assembler服务使用口令加密PDF文档。 在用密码加密PDF文档后，用户必须指定密码才能在Adobe reader或Acrobat中查看PDF文档。 要使用口令加密PDF文档，DDX文档必须包含加密PDF文档所需的加密元素值。

在本讨论中，请假定使用以下DDX文档。

```as3
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

在此DDX文档中，请注意为源属性分配了值 `inDoc`。 如果仅将一个输入的PDF文档传递给Assembler服务，并返回一个PDF文档，并调用该操作，请将该值赋给PDF源属 `invokeOneDocument``inDoc` 性。 调用操 `invokeOneDocument` 作时，值 `inDoc` 是预定义的键，必须在DDX文档中指定。

相反，将两个或两个以上输入的PDF文档传递到Assembler服务时，可以调用该操 `invokeDDX` 作。 在这种情况下，将输入PDF文档的文件名指定到属 `source` 性。

加密服务不必成为AEM表单安装的一部分，即可使用口令加密PDF文档。 请参 [阅加密和解密PDF文档](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅 [AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的详细信息，请参 [阅Assembler service和DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建PDF Assembler客户端。
1. 引用现有DDX文档。
1. 引用一个不安全的PDF文档。
1. 设置运行时选项。
1. 加密文档。
1. 保存加密的PDF文档。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

如果AEM Forms部署在JBoss以外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms部署在上的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参 [阅包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Assembler客户端**

在以编程方式执行Assembler操作之前，必须创建Assembler服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDF文档。 例如，请考虑本节中引入的DDX文档。 要加密PDF文档，DDX文档必须包含该元 `PasswordEncryptionProfile` 素。

**引用不安全的PDF文档**

必须引用一个不安全的PDF文档，并将其传递给Assembler服务以加密它。 如果引用的PDF文档已加密，则会引发异常。

**设置运行时选项**

您可以设置运行时选项，这些选项控制Assembler服务在执行作业时的行为。 例如，您可以设置一个选项，指示Assembler服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` AEM Forms API参考 [中的类引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**加密文档**

在创建Assembler服务客户端后，请引用包含加密信息的DDX文档、引用不安全的PDF文档并设置运行时选项，您可以调用该操 `invokeOneDocument` 作。 由于只有一个输入的PDF文档被传递给Assembler服务（并且一个文档被返回），因此您可以使用该 `invokeOneDocument` 操作而不是该操 `invokeDDX` 作。

**保存加密的PDF文档**

如果只有一个PDF文档被传递给Assembler服务，则Assembler服务将返回一个文档而不是集合对象。 即，在调用操作时， `invokeOneDocument` 将返回单个文档。 由于本节中引用的DDX文档包含加密信息，因此Assembler服务会返回一个使用密码加密的PDF文档。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合加密的PDF文档 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建Assembler客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `AssemblerServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 引用现有DDX文档。

   * 使用 `java.io.FileInputStream` DDX文档的构造函数并传递一个指定DDX文件位置的字符串值，创建一个表示该文档的对象。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 引用一个不安全的PDF文档。

   * 使用对 `java.io.FileInputStream` 象的构造函数并传递不安全的PDF文档的位置，从而创建对象。
   * 创建一 `com.adobe.idp.Document` 个对象，并传递 `java.io.FileInputStream` 包含PDF文档的对象。 此对 `com.adobe.idp.Document` 象将传递给该方 `invokeOneDocument` 法。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过调用属于对象的方法，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用对 `AssemblerOptionSpec` 象的方 `setFailOnError` 法并传递 `false`。

1. 加密文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeOneDocument` 法并传递以下值：

   * 表示 `com.adobe.idp.Document` DDX文档的对象。 确保此DDX文档包含PDF `inDoc` 源元素的值。
   * 包 `com.adobe.idp.Document` 含不安全PDF文档的对象。
   * 一个 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 对象，它指定运行时选项，包括默认字体和作业日志级别。
   该方 `invokeOneDocument` 法返回一个 `com.adobe.idp.Document` 包含密码加密的PDF文档的对象。

1. 保存加密的PDF文档。

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `Document` 象的方 `copyToFile` 法，将对象的内容复 `Document` 制到文件。 确保使用方 `Document` 法返回的 `invokeOneDocument` 对象。

**另请参阅**

[快速入门（SOAP模式）:使用Java API组合加密的PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 使用Web服务API组合加密的PDF文档 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建Assembler客户端。

   * 使用对 `AssemblerServiceClient` 象的默认构造函数创建对象。
   * 使用构 `AssemblerServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `AssemblerServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `AssemblerServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 引用现有DDX文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储DDX文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 引用一个不安全的PDF文档。

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储输入的PDF文档。 此对 `BLOB` 象作为参数传递给 `invokeOneDocument` 该对象。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的字段指定 `MTOM` 字节数组的内容来填充该对象。

1. 设置运行时选项。

   * 使用 `AssemblerOptionSpec` 其构造函数创建存储运行时选项的对象。
   * 通过为属于该对象的数据成员分配一个值，设置运行时选项以满足您的业务 `AssemblerOptionSpec` 要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请为对 `false` 象的数 `AssemblerOptionSpec` 据成员分 `failOnError` 配。

1. 加密文档。

   调用对 `AssemblerServiceClient` 象的方 `invokeOneDocument` 法并传递以下值：

   * 表示 `BLOB` DDX文档的对象
   * 表示 `BLOB` 不安全的PDF文档的对象
   * 指定 `AssemblerOptionSpec` 运行时选项的对象
   该方 `invokeOneDocument` 法返回包 `BLOB` 含加密PDF文档的对象。

1. 保存加密的PDF文档。

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示加密的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象 `invokeOneDocument` 的内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
