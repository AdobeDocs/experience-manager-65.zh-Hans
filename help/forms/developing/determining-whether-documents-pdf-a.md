---
title: 确定文档是否符合PDF/A
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: 使用汇编程序服务来使用Java API和Web服务API确定PDF文档是否符合PDF/A规范。
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2082'
ht-degree: 0%

---

# 确定文档是否符合PDF/A {#determining-whether-documents-are-pdf-a-compliant}

您可以使用汇编程序服务确定PDF文档是否符合PDF/A规范。 PDF/文档作为存档格式存在，用于长期保存文档的内容。 字体嵌入在文档中，且文件未压缩。 因此，PDF/A文档通常比标准PDF文档大。 此外，PDF/文档不包含音频和视频内容。

PDF/A-1规范由两个符合性级别组成，即A和B。两个级别之间的主要区别在于逻辑结构（无障碍）支持，这是符合性级别B不需要的。无论符合性级别如何，PDF/A-1都指示所有字体都嵌入在生成的PDF/A文档中。 目前，验证（和转换）仅支持PDF/A-1b。

在本讨论中，假定使用了以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

在此DDX文档中， `DocumentInformation` 元素指示汇编程序服务返回有关输入PDF文档的信息。 在 `DocumentInformation` 元素， `PDFAValidation` 元素指示汇编程序服务指示输入PDF文档是否符合PDF/A规范。

汇编程序服务返回信息，该信息指定输入PDF文档在包含PDF的XML文档中是否与汇编/A兼容 `PDFAConformance` 元素。 如果输入PDF文档符合PDF/A规范，则 `PDFAConformance` 元素 `isCompliant` 属性为 `true`. 如果PDF文档与PDF/A不兼容，则 `PDFAConformance` 元素 `isCompliant` 属性为 `false`.

>[!NOTE]
>
>因为在此部分中指定的DDX文档包含 `DocumentInformation` 元素，汇编程序服务会返回XML数据而不是PDF文档。 即汇编程序服务不会汇编或拆解PDF文档；它返回有关XML文档中输入PDF文档的信息。

>[!NOTE]
>
>有关汇编程序服务的详细信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅 [汇编程序服务和DDX参考](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 步骤摘要 {#summary-of-steps}

要确定PDF文档是否符合PDF/A，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用用于确定PDF/A符合性的PDF文档。
1. 设置运行时选项。
1. 检索有关PDF文档的信息。
1. 保存返回的XML文档。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为特定于AEM Forms所部署的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件的位置的信息，请参阅 [包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，必须创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能执行汇编程序服务操作。 要确定输入PDF文档是否符合PDF/A，请确保DDX文档包含 `PDFAValidation` 元素 `DocumentInformation` 元素。 的 `PDFAValidation` 元素指示汇编程序服务返回一个XML文档，该文档指定输入PDF文档是否与PDF/A兼容。

**引用用于确定PDF/A符合性的PDF文档**

必须引用PDF文档并将其传递到汇编程序服务，以确定PDF文档是否符合PDF/A。

**设置运行时选项**

您可以设置运行时选项，以在汇编程序服务执行作业时控制其行为。 例如，您可以设置一个选项，指示汇编程序服务在遇到错误时继续处理作业。 有关可设置的运行时选项的信息，请参阅 `AssemblerOptionSpec` 类引用 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**检索有关PDF文档的信息**

在创建汇编程序服务客户端、引用DDX文档、引用交互式PDF文档并设置运行时选项后，可以调用 `invokeDDX` 操作。 因为DDX文档包含 `DocumentInformation` 元素，汇编程序服务会返回XML数据而不是PDF文档。

**保存返回的XML文档**

汇编程序服务返回的XML文档指定输入PDF文档是否与PDF/A兼容。 例如，如果输入PDF文档不符合PDF/A规范，汇编程序服务将返回包含以下元素的XML文档：

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

将XML文档另存为XML文件，以便打开该文件并查看结果。

**另请参阅**

[使用Java API确定文档是否符合PDF/A规范](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[使用Web服务API确定文档是否符合PDF/A规范](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API确定文档是否符合PDF/A规范 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

使用汇编程序服务API(Java)确定PDF文档是否符合PDF/A规范：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `AssemblerServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 引用现有DDX文档。

   * 创建 `java.io.FileInputStream` 使用其构造函数并传递指定DDX文件位置的字符串值来表示DDX文档的对象。 要确定PDF文档是否符合PDF/A，请确保DDX文档包含 `PDFAValidation` 包含在 `DocumentInformation` 元素。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 对象。

1. 引用用于确定PDF/A符合性的PDF文档。

   * 创建 `java.io.FileInputStream` 对象，并传递用于确定PDF/A合规性的PDF文档的位置。
   * 创建 `com.adobe.idp.Document` 对象，并使用其构造函数进行传递 `java.io.FileInputStream` 包含PDF文档的对象。
   * 创建 `java.util.Map` 用于通过使用 `HashMap` 构造函数。
   * 在 `java.util.Map` 通过调用对象 `put` 方法和传递以下参数：

      * 表示键名称的字符串值。 此值必须匹配DDX文档中指定的源元素值。 例如，本节介绍的DDX文档中的源元素值为Loan.pdf。
      * A `com.adobe.idp.Document` 包含输入PDF文档的对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过调用属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请调用 `AssemblerOptionSpec` 对象 `setFailOnError` 方法和传递 `false`.

1. 检索有关PDF文档的信息。

   调用 `AssemblerServiceClient` 对象 `invokeDDX` 方法，并传递以下必需值：

   * A `com.adobe.idp.Document` 表示要使用的DDX文档的对象
   * A `java.util.Map` 包含用于确定PDF/A符合性的输入PDF文件的对象
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 指定运行时选项的对象

   的 `invokeDDX` 方法返回 `com.adobe.livecycle.assembler.client.AssemblerResult` 包含XML数据的对象，该数据指定输入PDF文档是否与PDF/A兼容。

1. 保存返回的XML文档。

   要获取指定输入PDF文档是否为PDF/A文档的XML数据，请执行以下操作：

   * 调用 `AssemblerResult` 对象 `getDocuments` 方法。 这会返回 `java.util.Map` 对象。
   * 循环访问 `java.util.Map` 对象，直到找到结果 `com.adobe.idp.Document` 对象。
   * 调用 `com.adobe.idp.Document` 对象 `copyToFile` 方法提取XML文档。 确保将XML数据另存为XML文件。

**另请参阅**

[快速入门（SOAP模式）：使用Java API确定文档是否符合PDF/A规范](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAP模式）

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API确定文档是否符合PDF/A规范 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

通过使用汇编程序服务API（Web服务）确定PDF文档是否符合PDF/A规范：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 具有托管AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 创建 `AssemblerServiceClient` 对象。
   * 创建 `AssemblerServiceClient.Endpoint.Address` 对象 `System.ServiceModel.EndpointAddress` 构造函数。 将指定WSDL的字符串值传递到AEM Forms服务(例如， `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)。 您无需使用 `lc_version` 属性。 在创建服务引用时，会使用此属性。)
   * 创建 `System.ServiceModel.BasicHttpBinding` 对象，方法是获取 `AssemblerServiceClient.Endpoint.Binding` 字段。 将返回值转换为 `BasicHttpBinding`.
   * 设置 `System.ServiceModel.BasicHttpBinding` 对象 `MessageEncoding` 字段 `WSMessageEncoding.Mtom`. 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 为字段分配相应的密码值 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 指定常量值 `HttpClientCredentialType.Basic` 到字段 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 指定常量值 `BasicHttpSecurityMode.TransportCredentialOnly` 到字段 `BasicHttpBindingSecurity.Security.Mode`.

1. 引用现有DDX文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储DDX文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示DDX文档的文件位置以及在中打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 字段中，显示字节数组的内容。

1. 引用用于确定PDF/A符合性的PDF文档。

   * 创建 `BLOB` 对象。 的 `BLOB` 对象用于存储输入PDF文档。
   * 创建 `System.IO.FileStream` 对象，方法是调用其构造函数并传递一个字符串值，该字符串值表示输入PDF文档的文件位置和打开文件的模式。
   * 创建用于存储 `System.IO.FileStream` 对象。 您可以通过获取 `System.IO.FileStream` 对象 `Length` 属性。
   * 通过调用 `System.IO.FileStream` 对象 `Read` 方法及传递要读取的字节数组、起始位置及流长度。
   * 填充 `BLOB` 通过指定对象 `MTOM` 属性。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 此集合对象用于存储PDF文档。
   * 创建 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象。
   * 为分配表示键名称的字符串值 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `key` 字段。 此值必须匹配DDX文档中指定的PDF源元素的值。
   * 分配 `BLOB` 将PDF文档存储到 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `value` 字段。
   * 添加 `MyMapOf_xsd_string_To_xsd_anyType_Item` 对象 `MyMapOf_xsd_string_To_xsd_anyType` 对象。 调用 `MyMapOf_xsd_string_To_xsd_anyType` 对象&#39; `Add` 方法和通过 `MyMapOf_xsd_string_To_xsd_anyType` 对象。

1. 设置运行时选项。

   * 创建 `AssemblerOptionSpec` 使用其构造函数存储运行时选项的对象。
   * 通过为属于 `AssemblerOptionSpec` 对象。 例如，要指示汇编程序服务在发生错误时继续处理作业，请指定 `false` 到 `AssemblerOptionSpec` 对象 `failOnError` 数据成员。

1. 检索有关PDF文档的信息。

   调用 `AssemblerServiceService` 对象 `invoke` 方法并传递以下值：

   * A `BLOB` 表示DDX文档的对象。
   * 的 `MyMapOf_xsd_string_To_xsd_anyType` 包含输入PDF文档的对象。 其键必须匹配PDF源文件的名称，并且其值必须为 `BLOB` 对应于输入PDF文件的对象。
   * 安 `AssemblerOptionSpec` 指定运行时选项的对象。

   的 `invoke` 方法返回 `AssemblerResult` 包含XML数据的对象，该数据指定输入PDF文档是否为PDF/A文档。

1. 保存返回的XML文档。

   要获取指定输入PDF文档是否为PDF/A文档的XML数据，请执行以下操作：

   * 访问 `AssemblerResult` 对象 `documents` 字段， `Map` 包含XML数据的对象，该数据指定输入PDF文档是否为PDF/A文档。
   * 循环访问 `Map` 对象来获取每个生成文档。 然后，将该数组成员的值转换为 `BLOB`.
   * 通过访问表示XML数据的二进制数据 `BLOB` 对象 `MTOM` 字段。 此字段存储一个字节数组，您可以将其作为XML文件写出。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
