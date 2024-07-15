---
title: 使用书签组合PDF文档
description: 使用Assembler服务通过Java API和Web服务API修改包含书签的PDF文档，以包含书签。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 0%

---

# 使用书签组合PDF文档 {#assembling-pdf-documents-with-bookmarks}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以组合包含书签的PDF文档。 例如，假设您有一个不包含书签的PDF文档，并且您想通过提供书签来修改它。 使用Assembler服务，您可以向其传递不包含书签的PDF文档，并取回包含书签的PDF文档。

书签包含以下属性：

* 在屏幕上显示为文本的标题。
* 一个操作，指定用户单击书签时执行的操作。 书签的典型操作是移动到当前文档中的另一个位置或打开另一个PDF文档，但可以指定其他操作。

为了进行此讨论，假定使用以下DDX文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

在此DDX文档中，请注意源属性被分配了值`Loan.pdf`。 此DDX文档指定将单个PDF文档传递到Assembler服务。 在组合带有书签的PDF文档时，必须指定描述结果文档中书签的书签XML文档。 若要指定书签XML文档，请确保在DDX文档中指定了`Bookmarks`元素。

在此示例DDX文档中，`Bookmarks`元素指定`doc2`作为值。 此值表示传递到Assembler服务的输入映射包含名为`doc2`的键。 `doc2`键的值是表示书签XML文档的`com.adobe.idp.Document`值。 （请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“书签语言”。）

本主题使用以下XML书签语言来组合包含书签的PDF文档。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

在此书签XML文档中，请注意定义用户单击书签时执行的操作的操作元素。 在Action元素下是Launch元素，该元素可启动应用程序（如NotePad）并打开文件(如PDF文件)。 要打开PDF文件，必须使用指定要打开的文件的File元素。 例如，在此部分指定的书签XML文件中，打开的文件名为LoanDetails.pdf。

>[!NOTE]
>
>有关支持的操作的完整详细信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“`Action`元素”。

给定本节中指定的DDX文档并将XML文件标记为书签，Assembler服务将组合包含以下书签的PDF文档。

![aw_aw_bmark](assets/aw_aw_bmark.png)

当用户单击&#x200B;*打开贷款详细信息*&#x200B;书签时，将打开LoanDetails.pdf。 同样，当用户单击&#x200B;*Launch NotePad*&#x200B;书签时，NotePad将启动。

>[!NOTE]
>
>在阅读本节之前，建议您熟悉使用Assembler服务组合PDF文档。 本节不讨论相关概念，例如创建包含输入文档的收藏集对象，或者了解如何从返回的收藏集对象中提取结果。 (请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)。)

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合包含书签的PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用添加书签的PDF文档。
1. 引用书签XML文档。
1. 将PDF文档和书签XML文档添加到地图收藏集。
1. 设置运行时选项。
1. 组合PDF文档。
1. 保存包含书签的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

如果AEM Forms部署在除JBoss之外的受支持J2EE应用程序服务器上，则必须将adobe-utilities.jar和jbossall-client.jar文件替换为JAR文件，这些文件特定于部署AEM Forms的J2EE应用程序服务器。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建PDF汇编程序客户端**

您必须先创建一个Assembler服务客户端，然后才能以编程方式执行Assembler操作。

**引用现有DDX文档**

要组合PDF文档，必须引用DDX文档。 此DDX文档必须包含`Bookmarks`元素，该元素指示汇编程序服务汇编包含书签的PDF。 （有关示例，请参阅本节前面显示的DDX文档。）

**引用添加书签的PDF文档**

引用添加书签的PDF文档。 所引用的PDF文档是否已包含书签并不重要。 如果`Bookmarks`元素是PDF源元素的子元素，则书签将替换PDF源中已存在的书签。 但是，如果要保留现有书签，请确保`Bookmarks`是PDF源元素的同级。 例如，请考虑以下示例：

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**引用书签XML文档**

要组合包含新书签的PDF，必须引用书签XML文档。 书签XML文档将传递到Map集合对象中的Assembler服务。 （有关示例，请参阅本节前面显示的书签XML文档。）

>[!NOTE]
>
>请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)中的“书签语言”。

**将PDF文档和书签XML文档添加到地图收藏集**

将添加书签的PDF文档以及书签XML文档添加到映射集合中。 因此，映射集合对象包含两个元素：PDF文档和书签XML文档。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。 有关可设置的运行时选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`AssemblerOptionSpec`类引用。

**汇编PDF文档**

要组合包含新书签的PDF文档，请使用Assembler服务的`invokeDDX`操作。 必须使用`invokeDDX`操作而不是其他Assembler服务操作（如`invokeOneDocument`）的原因是，Assembler服务需要在Map集合对象中传递的书签XML文档。 此对象是`invokeDDX`操作的参数。

**保存包含书签的PDF文档**

从返回的映射对象中提取结果并保存相应的PDF文档。 (请参阅[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)中的“提取结果”。)

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合带有书签的PDF文档 {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

使用Assembler服务API (Java)组合带有书签的PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用构造函数创建`AssemblerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用其构造函数并传递指定DDX文件位置的字符串值，创建表示DDX文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 引用添加书签的PDF文档。

   * 使用构造函数创建`java.io.FileInputStream`对象并传递PDF文档的位置。
   * 使用构造函数创建`com.adobe.idp.Document`对象并传递包含PDF文档的`java.io.FileInputStream`对象。

1. 引用书签XML文档。

   * 通过使用其构造函数并传递表示书签XML文档的XML文件的位置来创建`java.io.FileInputStream`对象。
   * 创建一个`com.adobe.idp.Document`对象并传递包含PDF文档的`java.io.FileInputStream`对象。

1. 将PDF文档和书签XML文档添加到地图收藏集。

   * 创建用于存储输入PDF文档和书签XML文档的`java.util.Map`对象。
   * 通过调用`java.util.Map`对象的`put`方法并传递以下参数来添加输入PDF文档：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的PDF源元素的值匹配。
      * 包含输入PDF文档的`com.adobe.idp.Document`对象。

   * 通过调用`java.util.Map`对象的`put`方法并传递以下参数来添加书签XML文档：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的书签源元素的值匹配。
      * 包含书签XML文档的`com.adobe.idp.Document`对象。

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * 包含输入PDF文档和书签XML文档的`java.util.Map`对象。
   * 指定运行时选项（包括默认字体和作业日志级别）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象

   `invokeDDX`方法返回包含作业结果和发生的任何异常的`com.adobe.livecycle.assembler.client.AssemblerResult`对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行下列操作：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 这将返回`java.util.Map`对象。
   * 反复查找`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。 (可以使用DDX文档中指定的PDF结果元素来获取文档。)
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法来提取PDF文档。

**另请参阅**

[快速入门(SOAP模式)：使用Java API组合带有书签的PDF文档](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合带有书签的PDF文档 {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

使用Assembler服务API（Web服务）组合带有书签的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

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
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 引用添加书签的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储输入PDF。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 引用书签XML文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储书签XML文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示输入PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。

1. 将PDF文档和书签XML文档添加到地图收藏集。

   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储输入的PDF文档和书签XML文档。
   * 对于每个输入PDF文档和书签XML文档，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将表示键名的字符串值分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段。 此值必须与DDX文档中指定的PDF源元素的值匹配。
   * 将存储PDF文档的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 (为每个输入PDF文档和书签XML文档执行此任务。)

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合PDF文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含输入文档的`MyMapOf_xsd_string_To_xsd_anyType`数组
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个包含作业结果和可能已发生的任何异常的`AssemblerResult`对象。

1. 保存包含书签的PDF文档。

   要获取新创建的PDF文档，请执行下列操作：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含结果PDF文档的`Map`对象。
   * 循环访问`Map`对象，直到找到与结果文档名称匹配的键。 然后将该数组成员的`value`强制转换为`BLOB`。
   * 通过访问其`BLOB`对象的`MTOM`字段提取表示PDF文档的二进制数据。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
