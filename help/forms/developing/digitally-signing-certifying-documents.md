---
title: 数字签名和认证文档
seo-title: 数字签名和认证文档
description: 使用“签名服务”向PDF文档添加和删除数字签名字段，检索位于PDF文档中的签名字段的名称，修改签名字段，对PDF文档进行数字签名，对PDF文档进行数字签名，验证位于PDF文档中的数字签名，验证位于PDF文档中的所有数字签名，以及从签名字段中删除数字签名。
seo-description: 使用“签名服务”向PDF文档添加和删除数字签名字段，检索位于PDF文档中的签名字段的名称，修改签名字段，对PDF文档进行数字签名，对PDF文档进行数字签名，验证位于PDF文档中的数字签名，验证位于PDF文档中的所有数字签名，以及从签名字段中删除数字签名。
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '17113'
ht-degree: 0%

---

# 数字签名和认证文档{#digitally-signing-and-certifying-documents}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

**关于签名服务**

签名服务允许贵组织保护其分发和接收的Adobe PDF文档的安全和隐私。 此服务使用数字签名和认证来确保只有预期的收件人才能更改文档。 由于安全功能应用于文档本身，因此文档在其整个生命周期中保持安全并受到控制。 文档在防火墙之外、在离线下载以及提交回您的组织时，仍然是安全的。

>[!NOTE]
>
>您可以为签名服务创建自定义签名处理程序，在调用某些操作（如对PDF文档进行签名）时将调用该处理程序。

**签名字段名称**

某些签名服务操作要求您指定在其上执行操作的签名字段的名称。 例如，在对PDF文档进行签名时，您可以指定要签名的签名字段的名称。 假定签名字段的全名为`form1[0].Form1[0].SignatureField1[0]`。 您可以指定`SignatureField1[0]`而不是`form1[0].Form1[0].SignatureField1[0]`。

有时，冲突会导致签名服务在错误的字段上签名（或执行需要签名字段名称的其他操作）。 此冲突是名称`SignatureField1[0]`出现在同一PDF文档中两个或多个位置的结果。 例如，假定PDF文档包含两个名为`form1[0].Form1[0].SignatureField1[0]`和`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`的签名字段，并且您指定了`SignatureField1[0]`。 在这种情况下，签名服务在迭代文档中的所有签名字段时对它找到的第一个签名字段进行签名。

如果PDF文档中有多个签名字段，建议您指定签名字段的全名。 即，指定`form1[0].Form1[0].SignatureField1[0]`而不是`SignatureField1[0]`。

您可以使用签名服务完成以下任务：

* 向PDF文档添加和删除数字签名字段。 （请参阅[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* 检索位于PDF文档中的签名字段的名称。 （请参阅[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。）
* 修改签名字段。 （请参阅[修改签名字段](digitally-signing-certifying-documents.md#modifying-signature-fields)。）
* 对PDF文档进行数字签名。 （请参阅[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。）
* 认证PDF文档。 （请参阅[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）
* 验证位于PDF文档中的数字签名。 （请参阅[验证数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 验证位于PDF文档中的所有数字签名。 （请参阅[验证多个数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。）
* 从签名字段中删除数字签名。 （请参阅[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)。）

>[!NOTE]
>
>有关签名服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 添加签名字段{#adding-signature-fields}

数字签名显示在签名字段中，签名字段是包含签名图形表示的表单字段。 签名字段可以是可见的或不可见的。 签名者可以使用预先存在的签名字段，也可以以编程方式添加签名字段。 无论哪种情况，签名字段都必须存在，然后PDF文档才能签名。

您可以使用签名服务Java API或签名Web服务API以编程方式添加签名字段。 可在PDF文档中添加多个签名字段；但是，每个签名字段名称必须唯一。

>[!NOTE]
>
>某些PDF文档类型不允许您以编程方式添加签名字段。 有关签名服务和添加签名字段的更多信息，请参阅[AEM Forms的服务引用](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary-of-steps}的摘要

要向PDF文档添加签名字段，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取添加了签名字段的PDF文档。
1. 添加签名字段。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取添加了签名字段的PDF文档**

必须获取添加了签名字段的PDF文档。

**添加签名字段**

要成功将签名字段添加到PDF文档，请指定用于标识签名字段位置的坐标值。 （如果添加不可见的签名字段，则不需要这些值。） 此外，您还可以指定在将签名应用于签名字段后，PDF文档中的哪些字段会被锁定。

**将PDF文档另存为PDF文件**

在签名服务将签名字段添加到PDF文档后，您可以将该文档另存为PDF文件，以便用户可以在Acrobat或Adobe Reader中打开它。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#add-signature-fields-using-the-java-api}添加签名字段

使用签名API(Java)添加签名字段：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取添加了签名字段的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示将签名字段添加到的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 添加签名字段

   * 创建一个`PositionRectangle`对象，该对象使用其构造函数指定签名字段位置。 在构造函数中，指定坐标值。
   * 如果需要，请创建一个`FieldMDPOptions`对象，以指定当数字签名应用于签名字段时锁定的字段。
   * 通过调用`SignatureServiceClient`对象的`addSignatureField`方法并传递以下值，向PDF文档添加签名字段：

      * A `com.adobe.idp`. `Document` 表示添加了签名字段的PDF文档的对象。
      * 指定签名字段名称的字符串值。
      * `java.lang.Integer`值，表示将签名字段添加到的页码。
      * 一个`PositionRectangle`对象，用于指定签名字段的位置。
      * `FieldMDPOptions`对象，用于指定在将数字签名应用于签名字段后锁定的PDF文档字段。 此参数值是可选的，您可以传递`null`。
   * 指定各种运行时值的`PDFSeedValueOptions`对象。 此参数值是可选的，您可以传递`null`。

      `addSignatureField`方法返回`com.adobe.idp`。 `Document` 表示包含签名字段的PDF文档的对象。
   >[!NOTE]
   >
   >可以调用`SignatureServiceClient`对象的`addInvisibleSignatureField`方法来添加不可见的签名字段。

1. 将PDF文档另存为PDF文件

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp`。 `Document` 对象的方 `copyToFile` 法，以将对象的内 `Document` 容复制到文件。确保使用`com.adobe.idp`。 `Document` 方法返回的对 `addSignatureField` 象。

**另请参阅**

[签名服务API快速入门](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服务API {#add-signature-fields-using-the-web-service-api}添加签名字段

要使用签名API（Web服务）添加签名字段，请执行以下操作：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取添加了签名字段的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储将包含签名字段的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。

1. 添加签名字段

   调用`SignatureServiceClient`对象的`addSignatureField`方法并传递以下值，以向PDF文档添加签名字段：

   * `BLOB`对象，表示将签名字段添加到的PDF文档。
   * 指定签名字段名称的字符串值。
   * 一个整数值，表示将签名字段添加到的页码。
   * 一个`PositionRect`对象，用于指定签名字段的位置。
   * `FieldMDPOptions`对象，用于指定在将数字签名应用于签名字段后锁定的PDF文档字段。 此参数值是可选的，您可以传递`null`。
   * 指定各种运行时值的`PDFSeedValueOptions`对象。 此参数值是可选的，您可以传递`null`。

   `addSignatureField`方法返回一个`BLOB`对象，该对象表示包含签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示将包含签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`addSignatureField`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`binaryData`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检索签名字段名称{#retrieving-signature-field-names}

您可以检索位于要签名或认证的PDF文档中的所有签名字段的名称。 如果您不确定位于PDF文档中的签名字段名称或要验证这些名称，则可以以编程方式检索它们。 签名服务返回签名字段的完全限定名称，如`form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>有关签名服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤{#summary_of_steps-1}的摘要

要检索签名字段名称，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含签名字段的PDF文档。
1. 检索签名字段名称。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含签名字段的PDF文档**

检索包含签名字段的PDF文档。

**检索签名字段名称**

在检索包含一个或多个签名字段的PDF文档后，可以检索签名字段名称。

**另请参阅**

[使用Java API检索签名字段名称](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服务API检索签名字段](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#retrieve-signature-field-names-using-the-java-api}检索签名字段名称

使用签名API(Java)检索签名字段名称：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar文件。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取包含签名字段的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象使用其构造函数并传递指定PDF文档位置的字符串值来表示包含签名字段的PDF文档。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 检索签名字段名称

   * 调用`SignatureServiceClient`对象的`getSignatureFieldList`方法并传递包含签名字段的PDF文档的`com.adobe.idp.Document`对象，以检索签名字段名称。 此方法返回一个`java.util.List`对象，其中每个元素都包含一个`PDFSignatureField`对象。 使用此对象，您可以获取有关签名字段的其他信息，如签名字段是否可见。
   * 遍历`java.util.List`对象，以确定是否存在签名字段名称。 对于PDF文档中的每个签名字段，您可以获取单独的`PDFSignatureField`对象。 要获取签名字段的名称，请调用`PDFSignatureField`对象的`getName`方法。 此方法将返回一个指定签名字段名称的字符串值。

**另请参阅**

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入门（SOAP模式）：使用Java API检索签名字段名称](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#retrieve-signature-field-using-the-web-service-api}检索签名字段

使用签名API（Web服务）检索签名字段名称：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含签名字段的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储包含签名字段的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`字段分配字节数组内容来填充`BLOB`对象。

1. 检索签名字段名称

   * 调用`SignatureServiceClient`对象的`getSignatureFieldList`方法并传递包含签名字段的PDF文档的`BLOB`对象，以检索签名字段名称。 此方法返回一个`MyArrayOfPDFSignatureField`集合对象，其中每个元素都包含一个`PDFSignatureField`对象。
   * 遍历`MyArrayOfPDFSignatureField`对象以确定是否存在签名字段名称。 对于PDF文档中的每个签名字段，您可以获取`PDFSignatureField`对象。 要获取签名字段的名称，请调用`PDFSignatureField`对象的`getName`方法。 此方法将返回一个指定签名字段名称的字符串值。

**另请参阅**

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改签名字段{#modifying-signature-fields}

您可以使用Java API和Web服务API修改位于PDF文档中的签名字段。 修改签名字段涉及处理其签名字段锁定字典值或种子值字典值。

*字段锁定词典*&#x200B;指定签名字段签名时锁定的字段列表。 锁定的字段可阻止用户更改该字段。 *种子值字典*&#x200B;包含在应用签名时使用的约束信息。 例如，您可以更改权限，以控制可能发生的操作，而无需使签名失效。

通过修改现有签名字段，您可以对PDF文档进行更改以反映不断变化的业务需求。 例如，新业务要求可能要求在文档签署后锁定所有文档字段。

本节介绍如何通过修改字段锁定词典和种子值词典值来修改签名字段。 对签名字段锁定词典所做的更改会导致在签名字段时锁定PDF文档中的所有字段。 对种子值字典所做的更改会禁止对文档进行特定类型的更改。

>[!NOTE]
>
>有关签名服务和修改签名字段的详细信息，请参阅[AEM Forms的服务引用](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-2}的摘要

要修改位于PDF文档中的签名字段，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要修改的签名字段的PDF文档。
1. 设置字典值。
1. 修改签名字段。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括LiveCycleJava库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含要修改的签名字段的PDF文档**

检索包含要修改的签名字段的PDF文档。

**设置字典值**

要修改签名字段，请为其字段锁定字典或种子值字典分配值。 指定签名字段锁定词典值涉及指定签名字段时锁定的PDF文档字段。 （本节将讨论如何锁定所有字段。）

可以设置以下种子值字典值：

* **修订检查**:指定在将签名应用于签名字段时是否执行吊销检查。
* **证书选项**:为证书种子值字典分配值。在指定证书选项之前，建议您熟悉证书种子值字典。 （请参阅[PDF参考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **摘要选项**:分配用于签名的摘要算法。有效值为SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **过滤器**:指定与签名字段一起使用的过滤器。例如，您可以使用Adobe.PPKLite过滤器。 （请参阅[PDF参考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。）
* **标记选项**:指定与此签名字段关联的标记值。值1表示签名者必须仅为条目使用指定的值。 值0表示允许使用其他值。 以下是位位置：

   * **1（过滤器）：** 用于对签名字段进行签名的签名处理程序
   * **2(SubFilter):** 一个名称数组，用于指示在签名时使用的可接受编码
   * **3(V)**:用于签名字段的签名处理程序的最低所需版本号
   * **4（原因）：** 一个字符串数组，用于指定签署文档的可能原因
   * **5(PDFLegalWarnings):** 指定可能合法证明的字符串数组

* **法律证明**:文档经认证后，会自动扫描特定类型的内容，这些内容可能会使文档的可见内容模糊或具有误导性。例如，注释可能会掩盖对了解认证内容非常重要的文本。 扫描过程会生成指示存在此类内容的警告。 它还对可能生成警告的内容提供了额外说明。
* **权限**:指定可在PDF文档上使用的权限，而不使签名失效。
* **原因**:指定必须签署此文档的原因。
* **时间戳**:指定时间戳选项。例如，您可以设置所用时间戳服务器的URL。
* **版本**:指定要用于签名字段的签名处理程序的最低版本号。

**修改签名字段**

在创建签名服务客户端后，检索包含要修改的签名字段的PDF文档，并设置字典值，您可以指示签名服务修改签名字段。 然后，签名服务会返回包含修改后签名字段的PDF文档。 原始PDF文档不受影响。

**将PDF文档另存为PDF文件**

将包含已修改签名字段的PDF文档另存为PDF文件，以便用户在Acrobat或Adobe Reader中打开它。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[签名服务API快速入门](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API {#modify-signature-fields-using-the-java-api}修改签名字段

使用签名API(Java)修改签名字段：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar文件。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取包含要修改的签名字段的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示包含要修改的签名字段的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 设置字典值

   * 使用`PDFSignatureFieldProperties`对象的构造函数创建对象。 `PDFSignatureFieldProperties`对象存储签名字段锁定字典和种子值字典信息。
   * 使用`PDFSeedValueOptionSpec`对象的构造函数创建对象。 此对象允许您设置种子值字典值。
   * 通过调用`PDFSeedValueOptionSpec`对象的`setMdpValue`方法并传递`MDPPermissions.NoChanges`枚举值，禁止更改PDF文档。
   * 使用`FieldMDPOptionSpec`对象的构造函数创建对象。 此对象允许您设置签名字段锁定词典值。
   * 通过调用`FieldMDPOptionSpec`对象的`setMdpValue`方法并传递`FieldMDPAction.ALL`枚举值，锁定PDF文档中的所有字段。
   * 通过调用`PDFSignatureFieldProperties`对象的`setSeedValue`方法并传递`PDFSeedValueOptionSpec`对象来设置种子值字典信息。
   * 通过调用`PDFSignatureFieldProperties`对象的`setFieldMDP`方法并传递`FieldMDPOptionSpec`对象来设置签名字段锁定词典信息。

   >[!NOTE]
   >
   >要查看可设置的所有种子值字典值，请参阅`PDFSeedValueOptionSpec`类引用。 (请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改签名字段

   通过调用`SignatureServiceClient`对象的`modifySignatureField`方法并传递以下值，修改签名字段：

   * 用于存储要修改的包含签名字段的PDF文档的`com.adobe.idp.Document`对象
   * 指定签名字段名称的字符串值
   * 用于存储签名字段锁定字典和种子值字典信息的`PDFSignatureFieldProperties`对象

   `modifySignatureField`方法返回一个`com.adobe.idp.Document`对象，该对象存储包含修改后签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。 确保使用`modifySignatureField`方法返回的`com.adobe.idp.Document`对象。

### 使用Web服务API {#modify-signature-fields-using-the-web-service-api}修改签名字段

使用签名API（Web服务）修改签名字段：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要修改的签名字段的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储包含要修改的签名字段的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。

1. 设置字典值

   * 使用`PDFSignatureFieldProperties`对象的构造函数创建对象。 此对象存储签名字段锁定字典和种子值字典信息。
   * 使用`PDFSeedValueOptionSpec`对象的构造函数创建对象。 此对象允许您设置种子值字典值。
   * 通过将`MDPPermissions.NoChanges`枚举值分配给`PDFSeedValueOptionSpec`对象的`mdpValue`数据成员，禁止更改PDF文档。
   * 使用`FieldMDPOptionSpec`对象的构造函数创建对象。 此对象允许您设置签名字段锁定词典值。
   * 通过将`FieldMDPAction.ALL`枚举值分配给`FieldMDPOptionSpec`对象的`mdpValue`数据成员，锁定PDF文档中的所有字段。
   * 通过将`PDFSeedValueOptionSpec`对象分配给`PDFSignatureFieldProperties`对象的`seedValue`数据成员来设置种子值字典信息。
   * 通过将`FieldMDPOptionSpec`对象分配给`PDFSignatureFieldProperties`对象的`fieldMDP`数据成员来设置签名字段锁定字典信息。

   >[!NOTE]
   >
   >要查看可设置的所有种子值字典值，请参阅`PDFSeedValueOptionSpec`类引用。 (请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改签名字段

   通过调用`SignatureServiceClient`对象的`modifySignatureField`方法并传递以下值，修改签名字段：

   * 用于存储要修改的包含签名字段的PDF文档的`BLOB`对象
   * 指定签名字段名称的字符串值
   * 用于存储签名字段锁定字典和种子值字典信息的`PDFSignatureFieldProperties`对象

   `modifySignatureField`方法返回一个`BLOB`对象，该对象存储包含修改后签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示将包含签名字段的PDF文档的文件位置以及打开文件的模式，来创建对象。
   * 创建一个字节数组，用于存储`addSignatureField`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`MTOM`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对PDF文档进行数字签名{#digitally-signing-pdf-documents}

数字签名可应用于PDF文档，以提供一定程度的安全性。 数字签名（如手写签名）提供了一种手段，使签名者能够识别自己并对文档进行陈述。 用于对文档进行数字签名的技术有助于确保签名者和收件人都清楚已签名的内容，并确信文档自签名后没有被更改。

PDF文档采用公钥技术进行签名。 签名者有两个密钥：公钥和私钥。 私钥存储在用户的凭据中，在签名时必须可用。 公钥存储在用户的证书中，收件人必须可以使用该证书来验证签名。 有关已吊销证书的信息可在由证书颁发机构(CA)分发的证书吊销列表(CRL)和在线证书状态协议(OCSP)响应中找到。 签名时间可以从称为时间戳颁发机构的可信来源获得。

>[!NOTE]
>
>在对PDF文档进行数字签名之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用信任管理器API以编程方式添加的。 （请参阅[使用信任管理器API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)导入凭据。）

您可以以编程方式对PDF文档进行数字签名。 对PDF文档进行数字签名时，必须引用AEM Forms中存在的安全凭据。 凭据是用于签名的私钥。

签名服务在对PDF文档进行签名时执行以下步骤：

1. 签名服务通过传递请求中指定的别名从Truststore中检索凭据。
1. 信任存储会搜索指定的凭据。
1. 凭据将返回到签名服务，并用于对文档进行签名。 此外，还会根据将来请求的别名缓存凭据。

有关处理安全凭据的信息，请参阅应用程序服务器的&#x200B;*安装和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>签名和认证文档之间存在差异。 （请参阅[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)。）

>[!NOTE]
>
>并非所有PDF文档都支持签名。 有关签名服务和数字签名文档的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>签名服务不支持将嵌入了PDF数据的XDP文件作为操作的输入，例如验证文档。 此操作会导致签名服务引发`PDFOperationException`。 要解决此问题，请使用“PDF实用程序”服务将XDP文件转换为PDF文件，然后将转换后的PDF文件传递到签名服务操作。 （请参阅[使用PDF实用程序](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。）

**nShield HSM凭据**

使用nCipher nShield HSM凭据对PDF文档进行签名或认证时，只有在重新启动部署了AEM Forms的J2EE应用程序服务器后，才能使用新凭据。 但是，您可以设置一个配置值，从而在不重新启动J2EE应用程序服务器的情况下使用符号或验证操作。

您可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

**签名不可信**

在对同一PDF文档进行认证和签名时，如果认证签名不可信，则在Acrobat或Adobe Reader中打开该PDF文档时，第一个签名将显示一个黄色三角形。 为避免这种情况，认证签名必须可信。

**对基于XFA的表单的文档进行签名**

如果您尝试使用签名服务API来签署基于XFA的表单，则位于Acrobat的`View` `Signed` `Version`中可能缺少数据。 例如，请考虑以下工作流：

* 使用使用Designer创建的XDP文件，可以合并包含签名字段和包含表单数据的XML数据的表单设计。 您可以使用Forms服务生成交互式PDF文档。
* 您使用签名服务API对PDF文档进行签名。

### 步骤{#summary_of_steps-3}的摘要

要对PDF文档进行数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名服务客户端。
1. 获取要签名的PDF文档。
1. 签署PDF文档。
1. 将签名的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取要签名的PDF文档**

要对PDF文档进行签名，必须获取包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行签名。 可以使用Designer或以编程方式添加签名字段。

**签署PDF文档**

在对PDF文档进行签名时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

使用`PDFSignatureAppearanceOptionSpec`对象设置外观选项。 例如，您可以通过调用`PDFSignatureAppearanceOptionSpec`对象的`setShowDate`方法并传递`true`来显示签名中的日期。

您还可以指定是否执行吊销检查，该检查可确定用于对PDF文档进行数字签名的证书是否已被吊销。 要执行撤销检查，您可以指定以下值之一：

* **无检查**:不执行吊销检查。
* **最佳工作**:始终尝试检查是否吊销链中的所有证书。如果检查中出现任何问题，则假定撤销有效。 如果发生任何失败，请假定证书未被吊销。
* **CheckIfAvailable:** 如果吊销信息可用，请检查是否吊销链中的所有证书。如果检查中出现任何问题，则假定撤销无效。 如果发生任何失败，请假定证书已吊销且无效。 （这是默认值。）
* **始终检查**:检查是否吊销链中的所有证书。如果任何证书中不存在吊销信息，则假定吊销无效。

要对证书执行吊销检查，可以使用`CRLOptionSpec`对象指定到证书吊销列表(CRL)服务器的URL。 但是，如果要执行吊销检查，并且您没有指定到CRL服务器的URL，则签名服务将从证书中获取该URL。

在执行撤销检查时，您可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，在与CRL服务器相对使用OCSP服务器时，会更快地执行撤销检查。 (请参阅[https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)上的“联机证书状态协议”。)

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在Adobe应用程序和服务中设置OCSP服务器，则检查OCSP服务器，然后检查CRL服务器。 （请参阅AAC帮助中的“使用信任存储管理证书和凭据”）。

如果您指定不执行吊销检查，则签名服务不会检查用于对文档进行签名或认证的证书是否已被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>虽然可以在证书中指定CRL或OCSP服务器，但您可以使用`CRLOptionSpec`和`OCSPOptionSpec`对象覆盖证书中指定的URL。 例如，要覆盖CRL服务器，可以调用`CRLOptionSpec`对象的`setLocalURI`方法。

时间戳是指跟踪修改已签名或已验证文档的时间的过程。 文档一旦签名，即使文档所有者也不应修改它。 时间戳有助于加强已签名或已认证文档的有效性。 可以使用`TSPOptionSpec`对象设置时间戳选项。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务中浏览各个部分和相应的快速启动，使用撤销检查。 由于未指定CRL或OCSP服务器信息，因此服务器信息是从用于对PDF文档进行数字签名的证书中获取的。

要成功对PDF文档进行签名，您可以指定将包含数字签名的签名字段的完全限定名称，如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表单字段时，还可以使用签名字段的部分名称：`SignatureField3[3]`。

您还必须引用安全凭据来对PDF文档进行数字签名。 要引用安全凭据，请指定别名。 别名是对实际凭据的引用，实际凭据可能位于PKCS#12文件（具有.pfx扩展名）或硬件安全模块(HSM)中。 有关安全凭据的信息，请参阅应用程序服务器的&#x200B;*安装和部署AEM Forms*&#x200B;指南。

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件，以便用户在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服务API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API {#digitally-sign-pdf-documents-using-the-java-api}对PDF文档进行数字签名

使用签名API(Java)对PDF文档进行数字签名：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取要签名的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示要使用其构造函数进行数字签名的PDF文档，并传递指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 签署PDF文档

   通过调用`SignatureServiceClient`对象的`sign`方法并传递以下值来对PDF文档进行签名：

   * 表示要签名的PDF文档的`com.adobe.idp.Document`对象。
   * 表示将包含数字签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于对PDF文档进行数字签名的凭据。 通过调用`Credential`对象的静态`getInstance`方法并传递一个字符串值来创建`Credential`对象，该字符串值指定与安全凭据对应的别名值。
   * `HashAlgorithm`对象，指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 表示PDF文档进行数字签名的原因的字符串值。
   * 表示签名者联系信息的字符串值。
   * 控制数字签名外观的`PDFSignatureAppearanceOptions`对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * `java.lang.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。
   * `OCSPOptionSpec`对象，用于存储联机证书状态协议(OCSP)支持的首选项。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 此参数是可选的，可以是`null`。 有关更多信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

   `sign`方法返回表示已签名PDF文档的`com.adobe.idp.Document`对象。

1. 保存已签名的PDF文档

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`，以将`Document`对象的内容复制到文件。 确保使用`sign`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入门（SOAP模式）：使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#digitally-signing-pdf-documents-using-the-web-service-api}对PDF文档进行数字签名

要使用签名API（Web服务）对PDF文档进行数字签名，请执行以下操作：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取要签名的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储已签名的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。

1. 签署PDF文档

   通过调用`SignatureServiceClient`对象的`sign`方法并传递以下值来对PDF文档进行签名：

   * 表示要签名的PDF文档的`BLOB`对象。
   * 表示将包含数字签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于对PDF文档进行数字签名的凭据。 使用`Credential`对象的构造函数创建一个对象，并通过为`Credential`对象的`alias`属性分配值来指定别名。
   * `HashAlgorithm`对象，指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 一个布尔值，用于指定是否使用哈希算法。
   * 表示PDF文档进行数字签名的原因的字符串值。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * 控制数字签名外观的`PDFSignatureAppearanceOptions`对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * `System.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。 如果此撤销检查已完成，则会将其嵌入签名中。 默认为 `false`.
   * `OCSPOptionSpec`对象，用于存储联机证书状态协议(OCSP)支持的首选项。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。 有关此对象的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 此参数是可选的，可以是`null`。

   `sign`方法返回表示已签名PDF文档的`BLOB`对象。

1. 保存已签名的PDF文档

   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`sign`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`MTOM`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对交互式Forms进行数字签名{#digitally-signing-interactive-forms}

您可以签署由Forms服务创建的交互式表单。 例如，请考虑以下工作流：

* 您可以合并基于XFA的PDF表单（使用Designer创建），以及使用Forms服务在XML文档中找到的表单数据。 Forms服务器呈现交互式表单。
* 您可以使用签名服务API对交互式表单进行签名。

结果会生成一个数字签名的交互式PDF表单。 在签署基于XFA表单的PDF表单时，请确保将PDF文件另存为Adobe静态PDF表单。 如果您尝试对另存为Adobe动态PDF表单的PDF表单进行签名，则会出现异常。 由于您正在对从Forms服务返回的表单进行签名，因此请确保表单包含签名字段。

>[!NOTE]
>
>在对交互式表单进行数字签名之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用信任管理器API以编程方式添加的。 （请参阅[使用信任管理器API](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)导入凭据。）

使用Forms服务API时，将`GenerateServerAppearance`运行时选项设置为`true`。 此运行时选项可确保在Acrobat或Adobe Reader中打开时，服务器上生成的表单外观仍然有效。 建议在使用Forms API生成要签名的交互式表单时设置此运行时选项。

>[!NOTE]
>
>在阅读交互式Forms的数字签名之前，建议您熟悉PDF文档的签名。 （请参阅[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。）

### 步骤{#summary_of_steps-4}的摘要

要对Forms服务返回的交互式表单进行数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建Forms和签名客户端。
1. 使用Forms服务获取交互式表单。
1. 签署交互式表单。
1. 将签名的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建Forms和签名客户端**

由于此工作流同时调用Forms和签名服务，因此请同时创建Forms服务客户端和签名服务客户端。

**使用Forms服务获取交互式表单**

您可以使用Forms服务获取要签名的交互式PDF表单。 自AEM Forms开始，您可以将`com.adobe.idp.Document`对象传递到包含要渲染的表单的Forms服务。 此方法的名称为`renderPDFForm2`。 此方法会返回一个`com.adobe.idp.Document`对象，其中包含要签名的表单。 您可以将此`com.adobe.idp.Document`实例传递到签名服务。

同样，如果您使用Web服务，则可以将Forms服务返回的`BLOB`实例传递到签名服务。

>[!NOTE]
>
>与交互式Forms部分进行数字签名关联的快速入门会调用`renderPDFForm2`方法。

**对交互式表单进行签名**

在对PDF文档进行签名时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

使用`PDFSignatureAppearanceOptionSpec`对象设置外观选项。 例如，您可以通过调用`PDFSignatureAppearanceOptionSpec`对象的`setShowDate`方法并传递`true`来显示签名中的日期。

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件。 可以在Acrobat或Adobe Reader中打开PDF文件。

**另请参阅**

[使用Java API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用Web服务API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[呈现交互式PDF forms](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API {#digitally-sign-an-interactive-form-using-the-java-api}对交互式表单进行数字签名

使用Forms和签名API(Java)对交互式表单进行数字签名：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 创建Forms和签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。
   * 使用其构造函数创建`FormsServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 使用Forms服务获取交互式表单

   * 创建一个`java.io.FileInputStream`对象，该对象表示要使用其构造函数传递到Forms服务的PDF文档。 传递指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。
   * 创建一个`java.io.FileInputStream`对象，该对象表示包含要使用其构造函数传递到Forms服务的表单数据的XML文档。 传递指定XML文件位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。
   * 创建用于设置运行时选项的`PDFFormRenderSpec`对象。 调用`PDFFormRenderSpec`对象的`setGenerateServerAppearance`方法并传递`true`。
   * 调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

      * 包含要渲染的PDF表单的`com.adobe.idp.Document`对象。
      * `com.adobe.idp.Document`对象，其中包含要与表单合并的数据。
      * 存储运行时选项的`PDFFormRenderSpec`对象。
      * `URLSpec`对象，其中包含Forms服务所需的URI值。 可以为此参数值指定`null`。
      * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。

      `renderPDFForm2`方法返回包含表单数据流的`FormsResult`对象

   * 通过调用`FormsResult`对象的`getOutputContent`方法来检索PDF表单。 此方法会返回表示交互式表单的`com.adobe.idp.Document`对象。


1. 对交互式表单进行签名

   通过调用`SignatureServiceClient`对象的`sign`方法并传递以下值来对PDF文档进行签名：

   * 表示要签名的PDF文档的`com.adobe.idp.Document`对象。 确保此对象是从Forms服务获取的`com.adobe.idp.Document`对象。
   * 表示已签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于对PDF文档进行数字签名的凭据。 通过调用`Credential`对象的静态`getInstance`方法创建`Credential`对象。 传递一个字符串值，以指定与安全凭据对应的别名值。
   * `HashAlgorithm`对象，指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 表示PDF文档进行数字签名的原因的字符串值。
   * 表示签名者联系信息的字符串值。
   * 控制数字签名外观的`PDFSignatureAppearanceOptions`对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * `java.lang.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。
   * `OCSPPreferences`对象，用于存储联机证书状态协议(OCSP)支持的首选项。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 此参数是可选的，可以是`null`。

   `sign`方法返回表示已签名PDF文档的`com.adobe.idp.Document`对象。

1. 保存已签名的PDF文档

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法并传递`java.io.File`，以将`Document`对象的内容复制到文件。 确保使用`sign`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[以数字方式签名交互式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入门（SOAP模式）：使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#digitally-sign-an-interactive-form-using-the-web-service-api}对交互式表单进行数字签名

使用Forms和签名API（Web服务）对交互式表单进行数字签名：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 对与签名服务关联的服务引用使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   对与Forms服务关联的服务引用使用以下WSDL定义：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   由于`BLOB`数据类型对于两个服务引用都是通用的，因此在使用`BLOB`数据类型时，可以完全限定该数据类型。 在相应的Web服务快速启动中，所有`BLOB`实例都完全限定。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建Forms和签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

   >[!NOTE]
   >
   >为Forms服务客户端重复这些步骤。

1. 使用Forms服务获取交互式表单

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储已签名的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。
   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储表单数据。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示包含表单数据的XML文件的文件位置以及打开文件的模式，来创建对象。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。
   * 创建用于设置运行时选项的`PDFFormRenderSpec`对象。 将值`true`分配给`PDFFormRenderSpec`对象的`generateServerAppearance`字段。
   * 调用`FormsServiceClient`对象的`renderPDFForm2`方法并传递以下值：

      * 包含要渲染的PDF表单的`BLOB`对象。
      * `BLOB`对象，其中包含要与表单合并的数据。
      * 存储运行时选项的`PDFFormRenderSpec`对象。
      * `URLSpec`对象，其中包含Forms服务所需的URI值。 可以为此参数值指定`null`。
      * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。
      * 用于存储表单中页数的长输出参数。
      * 用于区域设置值的字符串输出参数。
      * `FormResult`值，是用于存储交互式表单的输出参数。
   * 通过调用`FormsResult`对象的`outputContent`字段来检索PDF表单。 此字段存储表示交互式表单的`BLOB`对象。


1. 对交互式表单进行签名

   通过调用`SignatureServiceClient`对象的`sign`方法并传递以下值来对PDF文档进行签名：

   * 表示要签名的PDF文档的`BLOB`对象。 使用Forms服务返回的`BLOB`实例。
   * 表示已签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于对PDF文档进行数字签名的凭据。 使用`Credential`对象的构造函数创建一个对象，并通过为`Credential`对象的`alias`属性分配值来指定别名。
   * `HashAlgorithm`对象，指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 一个布尔值，用于指定是否使用哈希算法。
   * 表示PDF文档进行数字签名的原因的字符串值。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * 控制数字签名外观的`PDFSignatureAppearanceOptions`对象。 例如，您可以使用此对象向数字签名添加自定义徽标。
   * `System.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。 如果此撤销检查已完成，则会将其嵌入签名中。 默认为 `false`.
   * `OCSPPreferences`对象，用于存储联机证书状态协议(OCSP)支持的首选项。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。 有关此对象的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 此参数是可选的，可以是`null`。

   `sign`方法返回表示已签名PDF文档的`BLOB`对象。

1. 保存已签名的PDF文档

   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`sign`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`MTOM`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[以数字方式签名交互式Forms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF文档{#certifying-pdf-documents}认证

您可以通过使用称为认证签名的特定类型的签名来验证PDF文档，从而保护它。 认证签名与数字签名在以下方面有所区别：

* 它必须是应用于PDF文档的第一个签名；也就是说，在应用经认证的签名时，文档中的任何其他签名字段都必须是无符号的。 在PDF文档中只允许使用一个经认证的签名。 如果要对PDF文档进行签名和认证，则必须在对其签名之前对其进行认证。 验证PDF文档后，您可以对其他签名字段进行数字签名。
* 文档的作者或创作者可以指定文档可以以某些方式修改，而不会使经认证的签名失效。 例如，文档可以允许填写表单或注释。 如果作者指定不允许进行某种修改，则Acrobat会限制用户以这种方式修改文档。 如果进行了此类修改（如使用其他应用程序），则经认证的签名无效，当用户打开文档时，Acrobat会发出警告。 （如果签名未经认证，则不会阻止修改，且常规编辑操作不会使原始签名失效。）
* 在签名时，将扫描文档以查找可能使文档内容含糊或具有误导性的特定类型的内容。 例如，注释可能会模糊页面上一些对于了解正在认证的内容非常重要的文本。 可以对此类内容提供说明（法律证明）。

您可以使用签名服务Java API或签名Web服务API以编程方式认证PDF文档。 验证PDF文档时，必须引用凭据服务中存在的安全凭据。 有关安全凭据的信息，请参阅应用程序服务器的&#x200B;*安装和部署AEM Forms*&#x200B;指南。

>[!NOTE]
>
>在验证和签署同一PDF文档时，如果不信任该认证签名，则当您在Acrobat或Adobe Reader中打开该PDF文档时，第一个签名旁边会显示一个黄色三角形。 必须信任认证签名才能避免这种情况。

>[!NOTE]
>
>使用nCipher nShield HSM凭据对PDF文档进行签名或认证时，新凭据只有在部署了AEM Forms的J2EE应用程序服务器重新启动后才能使用。 但是，您可以设置一个配置值，从而在不重新启动J2EE应用程序服务器的情况下使用符号或验证操作。

您可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

>[!NOTE]
>
>有关签名服务和文档认证的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-5}的摘要

要验证PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取PDF文档以进行认证。
1. 认证PDF文档。
1. 将经认证的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名操作之前，必须创建签名客户端。

**获取PDF文档以进行认证**

要验证PDF文档，必须获取包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行认证。 可以使用Designer或以编程方式添加签名字段。 有关以编程方式添加签名字段的信息，请参阅[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。

**认证PDF文档**

要成功认证PDF文档，您需要签名服务使用的以下输入值来认证PDF文档：

* **PDF文档**:包含签名字段的PDF文档，该字段是包含经认证签名的图形表示的表单字段。PDF文档必须包含签名字段才能进行认证。 可以使用Designer或以编程方式添加签名字段。 （请参阅[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。）
* **签名字段名称**:经认证的签名字段的完全限定名称。以下值是一个示例：`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表单字段时，还可以使用签名字段的部分名称：`SignatureField3[3]`。 如果为字段名称传递了空值，则会动态创建并验证不可见的签名字段。
* **安全凭据**:用于验证PDF文档的凭据。此安全凭据包含密码和别名，该密码和别名必须与位于凭据服务内的凭据中显示的别名相匹配。 别名是对实际凭据的引用，实际凭据可能位于PKCS#12文件（具有.pfx扩展名）或硬件安全模块(HSM)中。
* **哈希算法**:用于摘要PDF文档的哈希算法。
* **签名原因**:一个值，显示在Acrobat或Adobe Reader中，以便其他用户了解PDF文档获得认证的原因。
* **签名者的位置**:由凭据指定的签名者的位置。
* **联系信息**:签名者的联系信息，如地址和电话号码。
* **权限信息**:控制最终用户可对文档执行的操作的权限，而不会导致认证签名无效。例如，您可以设置权限，以便对PDF文档进行任何更改都会导致认证的签名无效。
* **法律解释**:文档经认证后，会自动扫描特定类型的内容，这些内容可能会使文档的内容含糊或具有误导性。例如，注释可能会模糊页面上一些对于了解正在认证的内容非常重要的文本。 扫描过程会生成有关这些类型内容的警告。 此值对可能生成警告的内容提供了额外说明。
* **外观选项**:控制认证签名外观的选项。例如，认证签名可显示日期信息。
* **吊销检查**:此值指定是否对签名者的证书执行吊销检查。默认设置`false`表示未完成吊销检查。
* **OCSP设置**:联机证书状态协议(OCSP)支持的设置，该设置提供有关用于验证PDF文档的凭据状态的信息。例如，您可以指定服务器的URL，以提供有关您用于登录到PDF文档的凭据的信息。
* **CRL设置**:完成吊销检查时，证书吊销列表(CRL)首选项的设置。例如，您可以指定始终检查凭据是否被吊销。
* **时间戳**:定义应用于认证签名的时间戳信息的设置。时间戳表示特定数据是在特定时间之前建立的。 此知识有助于在签名者和验证者之间建立信任关系。

**将经认证的PDF文档另存为PDF文件**

签名服务对PDF文档进行认证后，您可以将其另存为PDF文件，以便用户在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API认证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服务API认证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#certify-pdf-documents-using-the-java-api}验证PDF文档

使用签名API(Java)验证PDF文档：

1. 包含项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在您Java项目的类路径中。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取PDF文档以进行认证

   * 创建一个`java.io.FileInputStream`对象，该对象表示要使用其构造函数进行验证的PDF文档，并传递指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 认证PDF文档

   通过调用`SignatureServiceClient`对象的`certify`方法并传递以下值来验证PDF文档：

   * 表示要认证的PDF文档的`com.adobe.idp.Document`对象。
   * 表示将包含签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于验证PDF文档的凭据。 通过调用`Credential`对象的静态`getInstance`方法并传递一个字符串值来创建`Credential`对象，该字符串值指定与安全凭据对应的别名值。
   * `HashAlgorithm`对象，用于指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 表示PDF文档获得认证的原因的字符串值。
   * 表示签名者联系信息的字符串值。
   * `MDPPermissions`对象，用于指定可对使签名失效的PDF文档执行的操作。
   * 控制认证签名外观的`PDFSignatureAppearanceOptions`对象。 如果需要，请通过调用方法（如`setShowDate`）来修改签名的外观。
   * 一个字符串值，用于解释使签名失效的操作。
   * `java.lang.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。 如果此撤销检查已完成，则会将其嵌入签名中。 默认为 `false`.
   * 一个`java.lang.Boolean`对象，用于指定是否锁定正在认证的签名字段。 如果字段已锁定，则签名字段将标记为只读，其属性将无法修改，并且没有所需权限的任何人都无法清除该字段。 默认为 `false`.
   * `OCSPPreferences`对象，用于存储联机证书状态协议(OCSP)支持的首选项。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。 有关此对象的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 例如，创建`TSPPreferences`对象后，可以通过调用`TSPPreferences`对象的`setTspServerURL`方法来设置TSP服务器的URL。 此参数是可选的，可以是`null`。 有关更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

   `certify`方法返回表示经认证的PDF文档的`com.adobe.idp.Document`对象。

1. 将经认证的PDF文档另存为PDF文件

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法，将`com.adobe.idp.Document`对象的内容复制到文件。

**另请参阅**

[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入门（SOAP模式）：使用Java API验证PDF文档](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#certify-pdf-documents-using-the-web-service-api}验证PDF文档

使用签名API（Web服务）验证PDF文档：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取PDF文档以进行认证

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储经过认证的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值，该字符串值表示要认证的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、开始位置和流长度，用流数据填充字节数组。
   * 通过为`MTOM`数据成员分配字节数组的内容来填充`BLOB`对象。

1. 认证PDF文档

   通过调用`SignatureServiceClient`对象的`certify`方法并传递以下值来验证PDF文档：

   * 表示要认证的PDF文档的`BLOB`对象。
   * 表示将包含签名的签名字段名称的字符串值。
   * `Credential`对象，表示用于验证PDF文档的凭据。 使用`Credential`对象的构造函数创建一个对象，并通过为`Credential`对象的`alias`属性分配值来指定别名。
   * `HashAlgorithm`对象，用于指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，您可以指定`HashAlgorithm.SHA1`以使用SHA1算法。
   * 一个布尔值，用于指定是否使用哈希算法。
   * 表示PDF文档获得认证的原因的字符串值。
   * 表示签名者位置的字符串值。
   * 表示签名者联系信息的字符串值。
   * `MDPPermissions`对象的静态数据成员，用于指定可对PDF文档执行的使签名失效的操作。
   * 一个布尔值，用于指定是否使用作为上一个参数值传递的`MDPPermissions`对象。
   * 一个字符串值，用于解释使签名失效的操作。
   * 控制认证签名外观的`PDFSignatureAppearanceOptions`对象。 使用`PDFSignatureAppearanceOptions`对象的构造函数创建对象。 您可以通过设置签名的一个数据成员来修改其外观。
   * `System.Boolean`对象，用于指定是否对签名者的证书执行吊销检查。 如果此撤销检查已完成，则会将其嵌入签名中。 默认为 `false`.
   * 一个`System.Boolean`对象，用于指定是否锁定正在认证的签名字段。 如果字段已锁定，则签名字段将标记为只读，其属性将无法修改，并且没有所需权限的任何人都无法清除该字段。 默认为 `false`.
   * 一个`System.Boolean`对象，用于指定签名字段是否已锁定。 也就是说，如果将`true`传递到上一个参数，则将`true`传递到此参数。
   * `OCSPPreferences`对象，用于存储联机证书状态协议(OCSP)支持的首选项，该对象提供有关用于验证PDF文档的凭据状态的信息。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * 存储证书吊销列表(CRL)首选项的`CRLPreferences`对象。 如果未完成吊销检查，则不会使用此参数，您可以指定`null`。
   * `TSPPreferences`对象，用于存储时间戳提供程序(TSP)支持的首选项。 例如，在创建`TSPPreferences`对象后，可以通过设置`TSPPreferences`对象的`tspServerURL`数据成员来设置TSP的URL。 此参数是可选的，可以是`null`。

   `certify`方法返回表示经认证的PDF文档的`BLOB`对象。

1. 将经认证的PDF文档另存为PDF文件

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示将包含经认证的PDF文档的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`certify`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`binaryData`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证数字签名{#verifying-digital-signatures}

可以验证数字签名以确保已签名的PDF文档未被修改，并且数字签名有效。 验证数字签名时，您可以检查签名的状态和签名的属性，如签名者的身份。 在信任数字签名之前，建议您验证数字签名。 验证数字签名时，请引用包含数字签名的PDF文档。

假设签名者的身份未知。 在Acrobat中打开PDF文档时，会出现一条警告消息，指出签名者的身份未知，如下图所示。

![vd_vd_verifsig](assets/vd_vd_verifysig.png)

同样，当您以编程方式验证数字签名时，您可以确定签名者身份的状态。 例如，如果验证上图所示文档中的数字签名，则结果是签名者的身份未知。

>[!NOTE]
>
>有关签名服务和验证数字签名的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-6}的摘要

要验证数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 验证数字签名。
1. 确定签名的状态。
1. 确定签名者的身份。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，请创建签名服务客户端。

**获取包含要验证的签名的PDF文档**

要验证用于对PDF文档进行数字签名或认证的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置签名服务在PDF文档中验证签名时使用的以下PKI运行时选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证器计算机上的时间），该时间指示使用当前时间。 有关不同时间值的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`枚举值。

您还可以指定是否在验证过程中执行吊销检查。 例如，您可以执行吊销检查以确定证书是否被吊销。 有关吊销检查选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`枚举值。

要对证书执行吊销检查，请使用`CRLOptionSpec`对象指定到证书吊销列表(CRL)服务器的URL。 但是，如果您没有指定到CRL服务器的URL，签名服务将从证书中获取该URL。

在执行撤销检查时，您可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，与CRL服务器相比，使用OCSP服务器时，撤销检查的执行速度会更快。 （请参阅[联机证书状态协议](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在Adobe应用程序和服务中设置OCSP服务器，则检查OCSP服务器，然后检查CRL服务器。

如果不执行吊销检查，则签名服务不检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`对象覆盖证书中指定的URL。 例如，要覆盖CRL服务器，可以调用`CRLOptionSpec`对象的`setLocalURI`方法。

时间戳是跟踪修改已签名或已验证文档的时间的过程。 文档签名后，任何人都无法修改它。 时间戳有助于加强已签名或已认证文档的有效性。 可以使用`TSPOptionSpec`对象设置时间戳选项。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间设置为`VerificationTime.CURRENT_TIME`，吊销检查设置为`RevocationCheckStyle.BestEffort`。 由于未指定CRL或OCSP服务器信息，因此从证书中获取服务器信息。

**验证数字签名**

要成功验证签名，请指定包含签名的签名字段的完全限定名称，如`form1[0].#subform[1].SignatureField3[3]`。 使用XFA表单字段时，您还可以使用签名字段的部分名称：`SignatureField3`。

默认情况下，签名服务将文档在验证后可签名的时间限制为65分钟。 如果用户尝试在当前时间验证签名，并且签名时间晚于当前时间并且在65分钟内，则签名服务不会创建验证错误。

>[!NOTE]
>
>有关验证签名时需要的其他值，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**确定签名的状态**

在验证数字签名时，您可以检查签名的状态。

**确定签名者的身份**

您可以确定签名者的身份，该身份可以是以下值之一：

* **未知**:此签名者未知，因为无法执行签名者验证。
* **受信任**:此签名者是可信的。
* **不可信**:此签名者不可信。

**另请参阅**

[使用Java API验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#verify-digital-signatures-using-the-java-api}验证数字签名

使用签名服务API(Java)验证数字签名：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取包含要验证的签名的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示包含要使用其构造函数验证的签名的PDF文档。 传递指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 设置PKI运行时选项

   * 使用`PKIOptions`对象的构造函数创建对象。
   * 通过调用`PKIOptions`对象的`setVerificationTime`方法并传递指定验证时间的`VerificationTime`枚举值来设置验证时间。
   * 通过调用`PKIOptions`对象的`setRevocationCheckStyle`方法并传递指定是否执行吊销检查的`RevocationCheckStyle`枚举值来设置吊销检查选项。

1. 验证数字签名

   通过调用`SignatureServiceClient`对象的`verify2`方法并传递以下值来验证签名：

   * `com.adobe.idp.Document`对象，其中包含经过数字签名或认证的PDF文档。
   * 表示包含要验证的签名的签名字段名称的字符串值。
   * 包含PKI运行时选项的`PKIOptions`对象。
   * 包含SPI信息的`VerifySPIOptions`实例。 可以为此参数指定`null`。

   `verify2`方法返回一个`PDFSignatureVerificationInfo`对象，其中包含可用于验证数字签名的信息。

1. 确定签名的状态

   * 通过调用`PDFSignatureVerificationInfo`对象的`getStatus`方法确定签名的状态。 此方法返回一个指定签名状态的`SignatureStatus`对象。 例如，如果未修改带签名的PDF文档，此方法将返回`SignatureStatus.DocumentSigNoChanges`。

1. 确定签名者的身份

   * 通过调用`PDFSignatureVerificationInfo`对象的`getSigner`方法来确定签名者的身份。 此方法返回一个`IdentityInformation`对象。
   * 调用`IdentityInformation`对象的`getStatus`方法来确定签名者的身份。 此方法会返回一个指定标识的`IdentityStatus`枚举值。 例如，如果签名者受信任，此方法将返回`IdentityStatus.TRUSTED`。

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[快速入门（SOAP模式）：使用Java API验证数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#verify-digital-signatures-using-the-web-service-api}验证数字签名

使用签名服务API（Web服务）验证数字签名：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要验证的签名的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储包含要验证的数字或认证签名的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。

1. 设置PKI运行时选项

   * 使用`PKIOptions`对象的构造函数创建对象。
   * 通过为`PKIOptions`对象的`verificationTime`数据成员分配指定验证时间的`VerificationTime`枚举值来设置验证时间。
   * 通过为`PKIOptions`对象的`revocationCheckStyle`数据成员分配指定是否执行吊销检查的`RevocationCheckStyle`枚举值来设置吊销检查选项。

1. 验证数字签名

   通过调用`SignatureServiceClient`对象的`verify2`方法并传递以下值来验证签名：

   * `BLOB`对象，其中包含经过数字签名或认证的PDF文档。
   * 表示包含要验证的签名的签名字段名称的字符串值。
   * 包含PKI运行时选项的`PKIOptions`对象。
   * 包含SPI信息的`VerifySPIOptions`实例。 可以为此参数指定`null`。

   `verify2`方法返回一个`PDFSignatureVerificationInfo`对象，其中包含可用于验证数字签名的信息。

1. 确定签名的状态

   通过获取`PDFSignatureVerificationInfo`对象`status`数据成员的值来确定签名的状态。 此数据成员存储一个指定签名状态的`SignatureStatus`对象。 例如，如果修改了带签名的PDF文档，`status`数据成员将存储值`SignatureStatus.DocumentSigNoChanges`。

1. 确定签名者的身份

   * 通过检索`PDFSignatureVerificationInfo`对象`signer`数据成员的值来确定签名者的身份。 此成员返回一个`IdentityInformation`对象。
   * 检索`IdentityInformation`对象的`status`数据成员，以确定签名者的身份。 此数据成员返回一个指定标识的`IdentityStatus`枚举值。 例如，如果签名者受信任，则此成员将返回`IdentityStatus.TRUSTED`。

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证多个数字签名{#verifying-multiple-digital-signatures}

AEM Forms提供了验证位于PDF文档中的所有数字签名的方法。 假设PDF文档包含多个数字签名，这是业务流程的结果，该业务流程需要多个签名者的签名。 例如，假设一项金融交易要求贷款官员和经理签名。 您可以使用签名服务Java API或Web服务API来验证PDF文档中的所有签名。 验证多个数字签名时，您可以检查每个签名的状态和属性。 在您信任数字签名之前，建议您对其进行验证。 建议您熟悉验证单个数字签名。

>[!NOTE]
>
>有关签名服务和验证数字签名的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-7}的摘要

要验证多个数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 检索所有数字签名。
1. 遍历所有签名。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，请创建签名服务客户端。

**获取包含要验证的签名的PDF文档**

要验证用于对PDF文档进行数字签名或认证的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置签名服务在验证PDF文档中的所有签名时使用的以下PKI运行时选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证器计算机上的时间），该时间指示使用当前时间。 有关不同时间值的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`VerificationTime`枚举值。

您还可以指定是否在验证过程中执行吊销检查。 例如，您可以执行吊销检查以确定证书是否被吊销。 有关吊销检查选项的信息，请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)中的`RevocationCheckStyle`枚举值。

要对证书执行吊销检查，请使用`CRLOptionSpec`对象指定到证书吊销列表(CRL)服务器的URL。 但是，如果您没有指定指向CRL服务器的URL，则签名服务将从证书中获取该URL。

在执行撤销检查时，您可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，使用OCSP服务器而不是CRL服务器时，执行撤销检查的速度会更快。 （请参阅[联机证书状态协议](https://tools.ietf.org/html/rfc2560)。）

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果OCSP服务器是在Adobe应用程序和服务中首先设置的，则检查OCSP服务器，然后检查CRL服务器。

如果不执行吊销检查，则签名服务不检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>您可以使用`CRLOptionSpec`和`OCSPOptionSpec`对象覆盖证书中指定的URL。 例如，要覆盖CRL服务器，可以调用`CRLOptionSpec`对象的`setLocalURI`方法。

时间戳是跟踪修改已签名或已验证文档的时间的过程。 文档签名后，任何人都无法修改它。 时间戳有助于加强已签名或已认证文档的有效性。 可以使用`TSPOptionSpec`对象设置时间戳选项。 例如，您可以指定时间戳提供程序(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间设置为`VerificationTime.CURRENT_TIME`，吊销检查设置为`RevocationCheckStyle.BestEffort`。 由于未指定CRL或OCSP服务器信息，因此从证书中获取服务器信息。

**检索所有数字签名**

要验证位于PDF文档中的所有数字签名，请从PDF文档中检索数字签名。 所有签名都将在列表中返回。 在验证数字签名时，请检查签名的状态。

>[!NOTE]
>
>与验证单个数字签名不同，验证多个签名时，您无需指定签名字段名称。

**遍历所有签名**

遍历每个签名。 即，对于每个签名，验证数字签名，并检查签名者的身份和每个签名的状态。 （请参阅[验证数字签名](#verify-digital-signatures-using-the-java-api)。）

>[!NOTE]
>
>如果要求是整个文档，则无需遍历所有签名。

**另请参阅**

[使用Java API验证多个数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证多个数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#verify-multiple-digital-signatures-using-the-java-api}验证多个数字签名

使用签名服务API(Java)验证多个数字签名：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取包含要验证的签名的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示包含多个数字签名的PDF文档，以便使用其构造函数进行验证。 传递指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 设置PKI运行时选项

   * 使用`PKIOptions`对象的构造函数创建对象。
   * 通过调用`PKIOptions`对象的`setVerificationTime`方法并传递指定验证时间的`VerificationTime`枚举值来设置验证时间。
   * 通过调用`PKIOptions`对象的`setRevocationCheckStyle`方法并传递指定是否执行吊销检查的`RevocationCheckStyle`枚举值来设置吊销检查选项。

1. 检索所有数字签名

   调用`SignatureServiceClient`对象的`verifyPDFDocument`方法并传递以下值：

   * `com.adobe.idp.Document`对象，其中包含包含多个数字签名的PDF文档。
   * 包含PKI运行时选项的`PKIOptions`对象。
   * 包含SPI信息的`VerifySPIOptions`实例。 可以为此参数指定`null`。

   `verifyPDFDocument`方法返回一个`PDFDocumentVerificationInfo`对象，其中包含有关位于PDF文档中的所有数字签名的信息。

1. 遍历所有签名

   * 通过调用`PDFDocumentVerificationInfo`对象的`getVerificationInfos`方法来迭代所有签名。 此方法返回一个`java.util.List`对象，其中每个元素都是一个`PDFSignatureVerificationInfo`对象。 使用`java.util.Iterator`对象遍历签名列表。
   * 使用`PDFSignatureVerificationInfo`对象，可以通过调用`PDFSignatureVerificationInfo`对象的`getStatus`方法来执行诸如确定签名状态的任务。 此方法返回一个`SignatureStatus`对象，其静态数据成员会通知您签名的状态。 例如，如果签名未知，则此方法将返回`SignatureStatus.DocumentSignatureUnknown`。

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[快速入门（SOAP模式）：使用Java API验证多个数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#verifying-multiple-digital-signatures-using-the-web-service-api}验证多个数字签名

使用签名服务API（Web服务）验证多个数字签名：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要验证的签名的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象存储包含多个要验证的数字签名的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数创建对象。 传递一个字符串值，该值表示PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`MTOM`对象的字节数组内容分配其属性来填充`BLOB`对象。

1. 设置PKI运行时选项

   * 使用`PKIOptions`对象的构造函数创建对象。
   * 通过为`PKIOptions`对象的`verificationTime`数据成员分配指定验证时间的`VerificationTime`枚举值来设置验证时间。
   * 通过为`PKIOptions`对象的`revocationCheckStyle`数据成员分配指定是否执行吊销检查的`RevocationCheckStyle`枚举值来设置吊销检查选项。

1. 检索所有数字签名

   调用`SignatureServiceClient`对象的`verifyPDFDocument`方法并传递以下值：

   * `BLOB`对象，其中包含包含多个数字签名的PDF文档。
   * 包含PKI运行时选项的`PKIOptions`对象。
   * 包含SPI信息的`VerifySPIOptions`实例。 可以为此参数指定null。

   `verifyPDFDocument`方法返回一个`PDFDocumentVerificationInfo`对象，其中包含有关位于PDF文档中的所有数字签名的信息。

1. 遍历所有签名

   * 通过获取`PDFDocumentVerificationInfo`对象的`verificationInfos`数据成员，遍历所有签名。 此数据成员返回一个`Object`数组，其中每个元素都是一个`PDFSignatureVerificationInfo`对象。
   * 使用`PDFSignatureVerificationInfo`对象，您可以通过获取`PDFSignatureVerificationInfo`对象的`status`数据成员来执行诸如确定签名状态之类的任务。 此数据成员返回一个`SignatureStatus`对象，其静态数据成员会通知您签名的状态。 例如，如果签名未知，则此方法将返回`SignatureStatus.DocumentSignatureUnknown`。

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除数字签名{#removing-digital-signatures}

必须先从签名字段中删除数字签名，然后才能应用较新的数字签名。 数字签名无法覆盖。 如果尝试将数字签名应用于包含签名的签名字段，则会出现异常。

>[!NOTE]
>
>有关签名服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤{#summary_of_steps-8}的摘要

要从签名字段中删除数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要删除的签名的PDF文档。
1. 从签名字段中删除数字签名。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(在JBoss上部署AEM Forms时必需)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此变量为必需变量)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含要删除的签名的PDF文档**

要从PDF文档中删除签名，必须获取包含签名的PDF文档。

**从签名字段中删除数字签名**

要成功从PDF文档中删除数字签名，必须指定包含数字签名的签名字段的名称。 此外，您必须拥有删除数字签名的权限；否则，会出现异常。

**将PDF文档另存为PDF文件**

在签名服务从签名字段中删除数字签名后，您可以将PDF文档另存为PDF文件，以便用户可以在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服务API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API {#remove-digital-signatures-using-the-java-api}删除数字签名

使用签名API(Java)删除数字签名：

1. 包含项目文件

   将客户端JAR文件（如adobe-signatures-client.jar）包含在您Java项目的类路径中。

1. 创建签名客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`SignatureServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 获取包含要删除的签名的PDF文档

   * 创建一个`java.io.FileInputStream`对象，该对象表示包含要删除的签名的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 从签名字段中删除数字签名

   通过调用`SignatureServiceClient`对象的`clearSignatureField`方法并传递以下值，从签名字段中删除数字签名：

   * `com.adobe.idp.Document`对象，表示包含要删除的签名的PDF文档。
   * 一个字符串值，用于指定包含数字签名的签名字段的名称。

   `clearSignatureField`方法返回一个`com.adobe.idp.Document`对象，该对象表示从中删除数字签名的PDF文档。

1. 将PDF文档另存为PDF文件

   * 创建`java.io.File`对象，并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法。 传递`java.io.File`对象，以将`com.adobe.idp.Document`对象的内容复制到文件。 确保使用`clearSignatureField`方法返回的`Document`对象。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入门（SOAP模式）：使用Java API删除数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API {#remove-digital-signatures-using-the-web-service-api}删除数字签名

使用签名API（Web服务）删除数字签名：

1. 包含项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为托管AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用其默认构造函数创建`SignatureServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`SignatureServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如`http://localhost:8080/soap/services/SignatureService?WSDL`）。 您无需使用`lc_version`属性。 在创建服务引用时，会使用此属性。)
   * 通过获取`SignatureServiceClient.Endpoint.Binding`字段的值，创建`System.ServiceModel.BasicHttpBinding`对象。 将返回值转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务，启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段`SignatureServiceClient.ClientCredentials.UserName.Password`分配相应的密码值。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要删除的签名的PDF文档

   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储包含要删除的数字签名的PDF文档。
   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、开始位置和流长度以读取。
   * 通过为`BLOB`对象的`MTOM`属性分配字节数组的内容来填充该对象。

1. 从签名字段中删除数字签名

   通过调用`SignatureServiceClient`对象的`clearSignatureField`方法并传递以下值来删除数字签名：

   * 包含已签名PDF文档的`BLOB`对象。
   * 表示包含要删除的数字签名的签名字段名称的字符串值。

   `clearSignatureField`方法返回一个`BLOB`对象，该对象表示从中删除数字签名的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调用`System.IO.FileStream`对象的构造函数并传递一个字符串值来创建对象，该字符串值表示包含空签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，用于存储`sign`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象`MTOM`数据成员的值来填充字节数组。
   * 通过调用`System.IO.BinaryWriter`对象的构造函数并传递`System.IO.FileStream`对象来创建该对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
