---
title: 分配使用权限
description: 使用Acrobat Reader DC扩展Java客户端API和Web服务API来应用和删除PDF文档中的使用权限。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,Reader Extensions
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3897'
ht-degree: 0%

---

# 分配使用权限 {#assigning-usage-rights}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 关于Acrobat Reader DC扩展服务 {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC扩展服务通过扩展Adobe Reader的功能，使您的组织可以轻松共享交互式PDF文档。 Acrobat Reader DC扩展服务完全支持任何PDF文档，直到（包括）PDF1.7。它适用于Adobe Reader 7.0及更高版本。 该服务会向PDF文档添加使用权限，激活在使用Adobe Reader打开PDF文档时通常不可用的功能。 第三方用户无需其他软件或插件即可使用启用了权限的文档。

您可以使用Acrobat Reader DC扩展服务完成这些任务：

* 将使用权限应用于PDF文档。 有关信息，请参阅[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* 从PDF文档中删除使用权限。 有关信息，请参阅[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 检索凭据详细信息。 有关信息，请参阅[检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参阅[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 将使用权限应用于PDF文档 {#applying-usage-rights-to-pdf-documents}

您可以使用Acrobat Reader DC扩展Java客户端API和Web服务向PDF文档应用使用权限。 使用权限与Acrobat中默认提供的功能有关，但在Adobe Reader中不可用，例如向表单添加注释或填写表单字段并保存表单的功能。 已应用使用权限的PDF文档称为启用权限的文档。 在Adobe Reader中打开启用了权限的文档的用户可以执行为该特定文档启用的操作。

>[!NOTE]
>
>当使用属于Java API一部分的`applyUsageRights`方法向PDF文档应用使用权限时，可以将`ReaderExtensionsOptionSpec`对象的`isModeFinal`参数设置为`false`。 这会导致表单处理的计数器未更新并改进性能。 如果您不关心更新已处理的表单计数器，建议将`isModeFinal`参数设置为`false`。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参阅[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要对PDF文档应用使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索PDF文档。
1. 指定要应用的使用权限。
1. 对PDF文档应用使用权限。
1. 保存启用权限的PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

要以编程方式执行Acrobat Reader DC扩展服务操作，您必须创建Acrobat Reader DC扩展服务客户端对象。 如果您使用Acrobat Reader DC扩展Java API，请创建一个`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建一个`ReaderExtensionsServiceService`对象。

**检索PDF文档**

检索PDF文档以应用使用权限。 启用权限的PDF文档包含使用权限字典。 当Adobe Reader打开包含此类词典的文档时，它仅启用词典中为该文档指定的使用权限。 如果文档不包含使用权限词典，则Acrobat Reader DC扩展服务会创建一个使用权限词典。 如果它已经包含字典，则Acrobat Reader DC扩展服务会使用您指定的字典覆盖现有使用权限。 词典指定启用哪些使用权限。 当用户在Adobe Reader中打开文档时，仅允许词典中指定的使用权限。

**指定要应用的使用权限**

您可以设置的使用权限取决于您从Adobe Systems Incorporated购买的凭据。 凭据通常提供设置一组相关使用权限的权限，例如与交互式表单相关的使用权限。 每个凭据都提供了创建特定数量的已启用权限的PDF文档的权利。 评估凭据授权创建无限数量的草稿文档。

>[!NOTE]
>
>如果尝试分配凭据不允许的使用权限，则会导致异常。

**将使用权限应用于PDF文档**

要对PDF文档应用使用权限，请引用用于应用使用权限的凭据的别名(凭据通常在安装AEM Forms期间安装)。 另外，您必须指定应用了使用权限的PDF文档。 有关配置凭据的信息，请参阅应用程序服务器的安装和部署指南。

**保存启用权限的PDF文档**

在Acrobat Reader DC扩展服务将使用权限应用于PDF文档后，您可以将启用权限的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[使用Web服务API应用使用权限](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API应用使用权限 {#apply-usage-rights-using-the-java-api}

使用Acrobat Reader DC扩展API (Java)对PDF文档应用使用权限：

1. 包含项目文件

   将客户端JAR文件（如adobe-reader-extensions-client.jar）包含在Java项目的类路径中。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`ReaderExtensionsServiceClient`对象并传递`ServiceClientFactory`对象。

1. 检索PDF文档。

   * 通过使用其构造函数并传递指定PDF文档位置的字符串值，创建表示PDF文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 指定要应用的使用权限。

   * 使用构造函数创建表示使用权限的`UsageRights`对象。
   * 对于要应用的每个使用权限，调用属于`UsageRights`对象的相应方法。 例如，要添加`enableFormFillIn`使用权限，请调用`UsageRights`对象的`enableFormFillIn`方法并传递`true`。 （对要应用的每个使用权限重复此步骤）。

1. 对PDF文档应用使用权限。

   * 使用构造函数创建`ReaderExtensionsOptionSpec`对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。 调用此构造函数时，必须指定以下值：

      * 包含要应用于文档的使用权限的`UsageRights`对象。
      * 一个字符串值，指定在Adobe Reader 7.x中打开启用了权限的PDF文档时，用户会看到的消息。Adobe Reader 8.0中不显示此消息。

   * 通过调用`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法并传递以下值，将使用权限应用于PDF文档：

      * 包含应用了使用权限的PDF文档的`com.adobe.idp.Document`对象。
      * 一个字符串值，它指定可让您应用使用权限的凭据别名。
      * 指定相应密码值的字符串值。 (当前忽略此参数。 您可以传递`null`。)

   * 包含运行时选项的`ReaderExtensionsOptionSpec`对象。

   `applyUsageRights`方法返回包含启用权限的PDF文档的`com.adobe.idp.Document`对象。

1. 保存启用权限的PDF文档。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`com.adobe.idp.Document`对象的内容复制到文件中（确保您使用`applyUsageRights`方法返回的`com.adobe.idp.Document`对象）。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[快速入门(SOAP模式)：使用Java API应用使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API应用使用权限 {#apply-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务）对PDF文档应用使用权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 使用默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 请确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储应用了使用权限的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和要读取的流长度。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 指定要应用的使用权限。

   * 使用构造函数创建表示使用权限的`UsageRights`对象。
   * 对于要应用的每个使用权限，将值`true`分配给属于`UsageRights`对象的相应数据成员。 例如，要添加`enableFormFillIn`使用权限，请将`true`分配给`UsageRights`对象的`enableFormFillIn`数据成员。 （对要应用的每个使用权限重复此步骤）。

1. 对PDF文档应用使用权限。

   * 使用构造函数创建`ReaderExtensionsOptionSpec`对象。 此对象包含Acrobat Reader DC扩展服务所需的运行时选项。
   * 将`UsageRights`对象分配给`ReaderExtensionsOptionSpec`对象的`usageRights`数据成员。
   * 指定一个字符串值，该值指定在Adobe Reader中打开启用了权限的PDF文档时用户看到的消息到`ReaderExtensionsOptionSpec`对象的`message`数据成员。
   * 通过调用`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法并传递以下值，将使用权限应用于PDF文档：

      * 包含应用了使用权限的PDF文档的`BLOB`对象。
      * 一个字符串值，它指定可让您应用使用权限的凭据别名。
      * 指定相应密码值的字符串值。 (当前忽略此参数。 您可以传递`null`。)

   * 包含运行时选项的`ReaderExtensionsOptionSpec`对象。

   `applyUsageRights`方法返回包含启用权限的PDF文档的`BLOB`对象。

1. 保存启用权限的PDF文档。

   * 通过调用其构造函数创建`System.IO.FileStream`对象。 传递一个字符串值，该值表示启用权限的PDF文档的文件位置。
   * 创建一个字节数组，用于存储`applyUsageRights`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 从PDF文档中删除使用权限 {#removing-usage-rights-from-pdf-documents}

您可以从启用了权限的文档中删除使用权限。 从启用了权限的PDF文档中删除使用权限对于在其上执行其他AEM Forms操作也是必需的。 例如，在设置使用权限之前，必须对PDF文档进行数字签名（或认证）。 因此，如果要对启用权限的文档执行操作，必须从PDF文档中删除使用权限，执行其他操作，如对文档进行数字签名，然后重新将使用权限应用到文档。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参阅[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要从启用权限的PDF文档中删除使用权限，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索启用了权限的PDF文档。
1. 从PDF文档中删除使用权限。
1. 保存PDF文档。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

您必须先创建Acrobat Reader DC扩展服务客户端对象，然后才能以编程方式执行Acrobat Reader DC扩展服务操作。 如果您使用的是Java API，请创建一个`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建一个`ReaderExtensionsServiceService`对象。

**检索启用权限的PDF文档**

检索启用了权限的PDF文档以删除使用权限。

**从PDF文档中删除使用权限**

检索启用了权限的PDF文档后，可以删除使用权限。 删除使用权限后，在Adobe Reader中查看PDF文档时，该文档将没有任何其他功能。

**保存PDF文档**

您可以将不再包含使用权限的PDF文档保存为PDF文件。 保存为PDF文件后，即可在Adobe Reader或Acrobat中查看PDF文档。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[将使用权限应用于PDF文档](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### 使用Java API删除使用权限 {#remove-usage-rights-using-the-java-api}

使用Acrobat Reader DC扩展API (Java)从启用了权限的PDF文档中删除使用权限：

1. 包括项目文件。

   将客户端JAR文件（如adobe-reader-extensions-client.jar）包含在Java项目的类路径中。

1. 创建Acrobat Reader DC扩展客户端对象。

   使用对象的构造函数创建`ReaderExtensionsServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 检索PDF文档。

   * 使用启用权限的PDF文档的构造函数并传递指定PDF文档位置的字符串值，创建表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 从PDF文档中删除使用权限。

   通过调用`ReaderExtensionsServiceClient`对象的`removeUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，从PDF文档中删除使用权限。 此方法返回的`com.adobe.idp.Document`对象包含没有使用权限的PDF文档。

1. 对PDF文档应用使用权限。

   * 创建`java.io.File`对象并确保文件扩展名为。PDF。
   * 调用`Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中（确保您使用`removeUsageRights`方法返回的`Document`对象）。

**另请参阅**

[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[快速入门(SOAP模式)：使用Java API从PDF文档中删除使用权限](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除使用权限 {#remove-usage-rights-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务），从启用了权限的PDF文档中删除使用权限：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 使用默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 请确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已启用权限的PDF文档，该文档中的使用权限已被删除。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 从PDF文档中删除使用权限。

   通过调用`ReaderExtensionsServiceClient`对象的`removeUsageRights`方法并传递包含启用权限的PDF文档的`BLOB`对象，从PDF文档中删除使用权限。 此方法返回的`BLOB`对象包含没有使用权限的PDF文档。

1. 对PDF文档应用使用权限。

   * 通过调用其构造函数并传递表示PDF文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`removeUsageRights`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。

**另请参阅**

[从PDF文档中删除使用权限](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 正在检索凭据信息 {#retrieving-credential-information}

您可以检索有关用于向启用权限的PDF文档应用使用权限的凭据的信息。 通过检索有关凭据的信息，您可以获取信息，例如证书不再有效的日期。

>[!NOTE]
>
>有关Acrobat Reader DC扩展服务的详细信息，请参阅[AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要检索有关用于向PDF文档应用使用权限的凭据的信息，请执行以下步骤：

1. 包括项目文件。
1. 创建Acrobat Reader DC扩展客户端对象。
1. 检索启用了权限的PDF文档。
1. 检索有关凭据的信息。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Acrobat Reader DC扩展客户端对象**

您必须先创建Acrobat Reader DC扩展服务客户端对象，然后才能以编程方式执行Acrobat Reader DC扩展服务操作。 如果您使用的是Java API，请创建一个`ReaderExtensionsServiceClient`对象。 如果您使用Acrobat Reader DC扩展Web服务API，请创建一个`ReaderExtensionsServiceService`对象。

**检索启用权限的PDF文档**

检索启用了权限的PDF文档，以检索有关凭据的信息。 还可以通过指定凭据的别名来检索有关凭据的信息；但是，如果要检索有关用于向特定启用权限的PDF文档应用使用权限的凭据的信息，则必须检索该文档。

**检索有关凭据的信息**

检索启用了权限的PDF文档后，您可以获取有关用于对其应用使用权限的凭据的信息。 您可以获取有关凭据的以下信息：

* 打开启用了权限的PDF文档时，Adobe Reader中显示的消息。
* 凭据不再有效的截止日期。
* 凭据无效的日期。
* 为此启用权限的PDF文档设置的使用权限。
* 凭据已使用的次数。

**另请参阅**

[使用Java API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[使用Web服务API删除使用权限](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC扩展服务API快速入门](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### 使用Java API检索凭据信息 {#retrieve-credential-information-using-the-java-api}

使用Acrobat Reader DC扩展API (Java)检索凭据信息：

1. 包括项目文件。

   将客户端JAR文件（如adobe-reader-extensions-client.jar）包含在Java项目的类路径中。

1. 创建Acrobat Reader DC扩展客户端对象。

   使用对象的构造函数创建`ReaderExtensionsServiceClient`对象，并传递包含连接属性的`ServiceClientFactory`对象。

1. 检索PDF文档。

   * 使用启用权限的PDF文档的构造函数并传递指定启用权限的PDF文档位置的字符串值，创建表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 从PDF文档中删除使用权限。

   * 通过调用`ReaderExtensionsServiceClient`对象的`getDocumentUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，检索有关用于向PDF文档应用使用权限的凭据的信息。 此方法返回包含凭据信息的`GetUsageRightsResult`对象。
   * 通过调用`GetUsageRightsResult`对象的`getNotAfter`方法，检索凭据不再有效的日期。 此方法返回表示凭据不再有效的日期的`java.util.Date`对象。
   * 通过调用`GetUsageRightsResult`对象的`getMessage`方法，检索在启用权限的PDF文档打开时在Adobe Reader中显示的消息。 此方法返回代表消息的字符串值。

**另请参阅**

[正在检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[快速入门(SOAP模式)：使用Java API检索凭据信息](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索凭据信息 {#retrieve-credential-information-using-the-web-service-api}

使用Acrobat Reader DC扩展API（Web服务）检索凭据信息：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建Acrobat Reader DC扩展客户端对象。

   * 使用默认构造函数创建`ReaderExtensionsServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`ReaderExtensionsServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）。 请确保指定`?blob=mtom`。)
   * 通过获取`ReaderExtensionsServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 检索PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储启用权限的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示启用权限的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 从PDF文档中删除使用权限。

   * 通过调用`ReaderExtensionsServiceClient`对象的`getDocumentUsageRights`方法并传递包含启用权限的PDF文档的`com.adobe.idp.Document`对象，检索有关用于向PDF文档应用使用权限的凭据的信息。 此方法返回包含凭据信息的`GetUsageRightsResult`对象。
   * 通过获取`GetUsageRightsResult`对象的`notAfter`数据成员的值，检索凭据不再有效的日期。 此数据成员的数据类型为`System.DateTime`。
   * 通过获取`GetUsageRightsResult`对象的`message`数据成员的值，检索在Adobe Reader中打开启用权限的PDF文档时显示的消息。 此数据成员的数据类型是一个字符串。
   * 通过获取`GetUsageRightsResult`对象的`useCount`数据成员的值检索凭据的使用次数。 此数据成员的数据类型是整数。

**另请参阅**

[正在检索凭据信息](assigning-usage-rights.md#retrieving-credential-information)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
