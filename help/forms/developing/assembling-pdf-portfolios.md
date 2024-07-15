---
title: 组合PDFPortfolio
description: 组合一个PDF组合以组合多个不同类型的文档，包括word文件、图像文件和PDF文档。 您可以使用Java API和Web服务API组合PDF组合。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# 组合PDFPortfolio {#assembling-pdf-portfolios}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

您可以使用Assembler Java和Web服务API来组合PDFPortfolio。 组合可以组合多种类型的文档，包括word文件、图像文件（例如jpeg文件）和PDF文档。 项目组合的布局可设置为不同的样式，如带有预览的&#x200B;*网格*、图像上的&#x200B;*On an Image*&#x200B;布局，甚至&#x200B;*旋转*。

下图是图像&#x200B;*样式布局上具有*&#x200B;的项目组合屏幕截图。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

创建PDFPortfolio是传递文档集合的无纸化替代方法。 使用AEM Forms，您可以通过使用结构化DDX文档调用Assembler服务来创建项目组合。 以下DDX文档是创建PDFPortfolio的DDX文档的示例。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX文档必须包含带有嵌套`Navigator`标记的`Portfolio`标记。 请注意，只有在将`myNavigator`分配为onImage布局导航器时，才需要标记`<Resource name="navigator/image.xxx" source="myImage.png"/>`： `AdobeOnImage.nav`。 此标记允许汇编程序服务选择要用作项目组合背景的图像。 包含`PackageFiles`和`File`标记以定义打包文件的文件名和MIME类型。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要创建PDFPortfolio，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 引用所需的文档。
1. 设置运行时选项。
1. 组合项目组合。
1. 保存组合的项目组合。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建PDF汇编程序客户端**

在以编程方式执行汇编程序操作之前，请先创建汇编程序服务客户端。

**引用现有DDX文档**

必须引用DDX文档才能组合PDFPortfolio。 此DDX文档必须包含`Portfolio`、`Navigator`和`PackageFiles`元素。

**引用所需文档**

要组合PDFPortfolio，请引用表示要组合文档的所有文件。 例如，将DDX文档中指定的所有图像文件传递到Assembler服务。 请注意，以下部分指定的DDX文档引用了这些文件： *myImage.png*&#x200B;和&#x200B;*saint_bernard.jpg*。

在组合PDFPortfolio时，将NAV文件（导航文件）传递给Assembler服务。 您传递到Assembler服务的NAV文件取决于要创建的PDFPortfolio类型。 例如，若要在图像&#x200B;*布局上创建*，请传递AdobeOnImage.nav文件。 您可以在以下文件夹中找到NAV文件：

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

从Acrobat 9（或更高版本）安装目录复制NAV文件。 将NAV文件放置在客户端应用程序可以访问它的位置。 所有文件都传递到Map集合对象中的Assembler服务。

>[!NOTE]
>
>与组装PDFPortfolio关联的快速入门使用AdobeOnImage.nav。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。

**组合项目组合**

要组合PDFPortfolio，请调用`invokeDDX`操作。 Assembler服务返回集合对象中的PDFPortfolio。

**保存组合的项目组合**

PDFPortfolio在集合对象中返回。 循环访问收藏集对象并将PDFPortfolio另存为PDF文件。

**另请参阅**

[使用Java API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-java-api)

[使用Web服务API组合PDFPortfolio](#assemble-a-pdf-portfolio-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## 使用Java API组合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-java-api}

使用Assembler服务API (Java)组合PDFPortfolio：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`AssemblerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用其构造函数并传递指定DDX文件位置的字符串值，创建表示DDX文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 引用所需的文档。

   * 使用`HashMap`构造函数创建用于存储输入PDF文档的`java.util.Map`对象。
   * 使用构造函数创建`java.io.FileInputStream`对象。 传递所需NAV文件的位置（对创建项目组合所需的每个文件重复此任务）。
   * 创建一个`com.adobe.idp.Document`对象并传递包含NAV文件的`java.io.FileInputStream`对象（对创建项目组合所需的每个文件重复此任务）。
   * 通过调用其`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的源元素的值匹配。 （对创建项目组合所需的每个文件重复此任务）。
      * 包含PDF文档的`com.adobe.idp.Document`对象。 （对创建项目组合所需的每个文件重复此任务）。

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合项目组合。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * 包含构建PDFPortfolio所需文件的`java.util.Map`对象。
   * 指定运行时选项（包括默认字体和作业日志级别）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象

   `invokeDDX`方法返回一个`com.adobe.livecycle.assembler.client.AssemblerResult`对象，该对象包含组合的PDFPortfolio和发生的任何异常。

1. 保存组合的项目组合。

   要获取PDFPortfolio，请执行以下步骤：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此方法返回`java.util.Map`对象。
   * 反复查找`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取PDFPortfolio。

**另请参阅**

[快速入门(SOAP模式)：使用Java API组合PDFPortfolio](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合PDFPortfolio {#assemble-a-pdf-portfolio-using-the-web-service-api}

使用Assembler服务API（Web服务）组合PDFPortfolio：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保在设置服务引用时使用以下WSDL定义： `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`。

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
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 引用所需的文档。

   * 对于每个输入文件，使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入文件。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储创建PDFPortfolio所需的输入文件。
   * 对于每个输入文件，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将表示键名的字符串值分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段。 此值必须匹配DDX文档中指定元素的值。 （为每个输入文件执行此任务。）
   * 将存储输入文件的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 (为每个输入PDF文档执行此任务。)
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 (为每个输入PDF文档执行此任务。)

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合项目组合。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含所需文件的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回包含作业结果和发生的任何异常的`AssemblerResult`对象。

1. 保存组合的项目组合。

   要获取新创建的PDFPortfolio，请执行以下步骤：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含生成PDF文档的`Map`对象。
   * 对`Map`对象进行迭代以获取每个结果文档。 然后，将该数组成员的`value`强制转换为`BLOB`。
   * 通过访问其`BLOB`对象的`MTOM`属性，提取表示PDF文档的二进制数据。 这会返回一个字节数组，您可以将该字节写出到PDF文件中。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
