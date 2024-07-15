---
title: 将文档传递到FormsService
description: 将包含表单设计的com.adobe.idp.Document对象传递到Forms服务。 Forms服务渲染com.adobe.idp.Document对象中的表单设计。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 0%

---

# 将文档传递到Forms服务 {#passing-documents-to-the-formsservice}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

AEM Forms服务向客户端设备（通常是Web浏览器）呈现交互式PDF forms，以从用户那里收集信息。 交互式PDF表单基于表单设计，该表单设计通常保存为XDP文件并在Designer中创建。 从AEM Forms开始，您可以将包含表单设计的`com.adobe.idp.Document`对象传递到Forms服务。 然后，Forms服务渲染`com.adobe.idp.Document`对象中的表单设计。

将`com.adobe.idp.Document`对象传递到Forms服务的好处是，其他服务操作返回`com.adobe.idp.Document`实例。 也就是说，您可以从另一个服务操作获取`com.adobe.idp.Document`实例并对其进行渲染。 例如，假设XDP文件存储在名为`/Company Home/Form Designs`的Content Services（已弃用）节点中，如下图所示。

您可以以编程方式从内容服务中检索Loan.xdp（已弃用）（已弃用），并将XDP文件传递到`com.adobe.idp.Document`对象中的Forms服务。

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要将从Content Services（已弃用）获得的文档传递到Forms服务，请执行以下任务：

1. 包括项目文件。
1. 创建Forms和文档管理客户端API对象。
1. 从Content Services检索表单设计（已弃用）。
1. 呈现交互式PDF表单。
1. 对表单数据流执行操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请包含代理文件。

**创建Forms和文档管理客户端API对象**

在以编程方式执行Forms服务API操作之前，请先创建Forms客户端API对象。 此外，由于此工作流从内容服务中检索XDP文件（已弃用），因此请创建文档管理API对象。

**从内容服务检索表单设计（已弃用）**

使用Java或Web服务API从内容服务中检索XDP文件（已弃用）。 XDP文件在`com.adobe.idp.Document`实例（或者`BLOB`实例，如果您使用Web服务）中返回。 然后，您可以将`com.adobe.idp.Document`实例传递到Forms服务。

**渲染交互式PDF表单**

要呈现交互式表单，请将从Content Services（已弃用）返回的`com.adobe.idp.Document`实例传递到Forms服务。

>[!NOTE]
>
>您可以将包含表单设计的`com.adobe.idp.Document`传递到Forms服务。 两个名为`renderPDFForm2`和`renderHTMLForm2`的新方法接受包含表单设计的`com.adobe.idp.Document`对象。

**对表单数据流执行操作**

根据客户端应用程序的类型，可以将表单写入客户端Web浏览器或将表单另存为PDF文件。 基于Web的应用程序通常将表单写入Web浏览器。 但是，桌面应用程序通常将表单保存为PDF文件。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## 使用Java API将文档传递到Forms服务 {#pass-documents-to-the-forms-service-using-the-java-api}

使用Forms服务和内容服务（已弃用）API (Java)传递从内容服务（已弃用）获得的文档：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar和adobe-contentservices-client.jar。

1. 创建Forms和Document Management客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）
   * 使用构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`DocumentManagementServiceClientImpl`对象并传递`ServiceClientFactory`对象。

1. 从Content Services检索表单设计（已弃用）

   调用`DocumentManagementServiceClientImpl`对象的`retrieveContent`方法并传递以下值：

   * 一个字符串值，它指定添加内容的存储。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径（例如，`/Company Home/Form Designs/Loan.xdp`）。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。

   `retrieveContent`方法返回包含XDP文件的`CRCResult`对象。 通过调用`CRCResult`对象的`getDocument`方法获取`com.adobe.idp.Document`实例。

1. 呈现交互式PDF表单

   调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

   * 包含从Content Services检索到的表单设计的`com.adobe.idp.Document`对象（已弃用）。
   * 包含要与表单合并的数据的`com.adobe.idp.Document`对象。 如果不想合并数据，请传递一个空的`com.adobe.idp.Document`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 此值是一个可选参数，如果您不想指定运行时选项，则可以指定`null`。
   * 包含URI值的`URLSpec`对象。 此值是可选参数，您可以指定`null`。
   * 存储文件附件的`java.util.HashMap`对象。 此值是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。

   `renderPDFForm`方法返回的`FormsResult`对象包含必须写入客户端Web浏览器的表单数据流。

1. 对表单数据流执行操作

   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用其`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法，创建字节数组并使用表单数据流填充该数组。 将字节数组作为参数传递。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速入门(SOAP模式)：使用Java API将文档传递到Forms服务](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API将文档传递到Forms服务 {#pass-documents-to-the-forms-service-using-the-web-service-api}

使用Forms服务和内容服务（已弃用）API（Web服务）传递从内容服务（已弃用）获得的文档：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 对与Forms服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   对与Document Management服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`。

   由于`BLOB`数据类型对两个服务引用都是通用的，因此使用它时，请完全限定`BLOB`数据类型。 在相应的Web服务快速入门中，所有`BLOB`实例都是完全限定的。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Forms和Document Management客户端API对象

   * 使用默认构造函数创建`FormsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`FormsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/FormsService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`FormsServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`FormsServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`FormsServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。

   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >对`DocumentManagementServiceClient`服务客户端重复这些步骤。

1. 从Content Services检索表单设计（已弃用）

   通过调用`DocumentManagementServiceClient`对象的`retrieveContent`方法并传递以下值来检索内容：

   * 一个字符串值，它指定添加内容的存储。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，它指定要检索的内容的完全限定路径（例如，`/Company Home/Form Designs/Loan.xdp`）。 此值是必需参数。
   * 指定版本的字符串值。 此值是一个可选参数，您可以传递空字符串。 在这种情况下，将检索最新版本。
   * 用于存储浏览链接值的字符串输出参数。
   * 用于存储内容的`BLOB`输出参数。 您可以使用此输出参数检索内容。
   * 用于存储内容属性的`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`输出参数。
   * `CRCResult`输出参数。 您可以使用`BLOB`输出参数来获取内容，而不是使用此对象。

1. 呈现交互式PDF表单

   调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

   * 包含从Content Services检索到的表单设计的`BLOB`对象（已弃用）。
   * 包含要与表单合并的数据的`BLOB`对象。 如果不想合并数据，请传递一个空的`BLOB`对象。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 此值是一个可选参数，如果您不想指定运行时选项，则可以指定`null`。
   * 包含URI值的`URLSpec`对象。 此值是可选参数，您可以指定`null`。
   * 存储文件附件的`Map`对象。 此值是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。
   * 用于存储页数的长输出参数。
   * 用于存储区域设置值的字符串输出参数。
   * 用于存储交互PDF表单`.`的`FormsResult`输出参数

   `renderPDFForm2`方法返回包含交互式PDF表单的`FormsResult`对象。

1. 对表单数据流执行操作

   * 通过获取`FormsResult`对象的`outputContent`字段的值来创建包含表单数据的`BLOB`对象。
   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值表示交互式PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储从`FormsResult`对象检索的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
