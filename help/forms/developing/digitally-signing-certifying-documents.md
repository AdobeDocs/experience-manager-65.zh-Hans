---
title: 对文档进行数字签名和认证
seo-title: 对文档进行数字签名和认证
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 对文档进行数字签名和认证 {#digitally-signing-and-certifying-documents}

**关于签名服务**

通过签名服务，您的组织可以保护其分发和接收的Adobe PDF文档的安全性和隐私。 此服务使用数字签名和认证来确保只有预期收件人才能更改文档。 由于安全功能应用于文档本身，因此文档在整个生命周期内都保持安全并受到控制。 文档在离线下载和提交回您的组织时，在防火墙之外保持安全。

>[!NOTE]
>
>您可以为签名服务创建自定义签名处理程序，该处理程序在调用某些操作（如对PDF文档进行签名）时被调用。

**签名字段名称**

某些签名服务操作要求您指定执行操作的签名字段的名称。 例如，在对PDF文档进行签名时，您指定要签名的签名字段的名称。 假定签名字段的全名为 `form1[0].Form1[0].SignatureField1[0]`。 您可以指 `SignatureField1[0]` 定而不是 `form1[0].Form1[0].SignatureField1[0]`。

有时，冲突会导致签名服务在错误的字段上签名（或执行另一个需要签名字段名称的操作）。 此冲突是同一PDF文档中两 `SignatureField1[0]` 个或多个位置显示的名称的结果。 例如，考虑一个PDF文档，它包含两个名为和且您指 `form1[0].Form1[0].SignatureField1[0]` 定的 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` 签名字段 `SignatureField1[0]`。 在这种情况下，签名服务会在对文档中所有签名字段进行迭代时对它找到的第一个签名字段进行签名。

如果PDF文档中有多个签名字段，建议您指定签名字段的全名。 即指定而 `form1[0].Form1[0].SignatureField1[0]`不是指 `SignatureField1[0]`定。

您可以使用签名服务完成以下任务：

* 向PDF文档添加和删除数字签名字段。 (请参阅 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* 检索PDF文档中的签名字段的名称。 (请参阅 [检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)。)
* 修改签名字段。 (请参阅 [修改签名字段](digitally-signing-certifying-documents.md#modifying-signature-fields)。)
* 对PDF文档进行数字签名。 (请参阅 [对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)
* 验证PDF文档。 (请参阅 [认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)
* 验证PDF文档中的数字签名。 (请参阅 [验证数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 验证PDF文档中的所有数字签名。 (请参阅 [验证多个数字签名](digitally-signing-certifying-documents.md#verifying-digital-signatures)。)
* 从签名字段中删除数字签名。 (请参阅 [删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)。)

   ***注意&#x200B;**:有关签名服务的详细信息，请参[阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。*

## 添加签名字段 {#adding-signature-fields}

数字签名显示在签名字段中，签名字段是包含签名图形表示形式的表单字段。 签名字段可以是可见的或不可见的。 签名者可以使用预先存在的签名字段，或以编程方式添加签名字段。 无论哪种情况，签名字段都必须存在，才能对PDF文档进行签名。

您可以使用签名服务Java API或签名Web服务API以编程方式添加签名字段。 可向PDF文档添加多个签名字段；但是，每个签名字段名称必须是唯一的。

>[!NOTE]
>
>某些PDF文档类型不允许以编程方式添加签名字段。 有关签名服务和添加签名字段的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要向PDF文档添加签名字段，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取添加了签名字段的PDF文档。
1. 添加签名字段。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取添加了签名字段的PDF文档**

您必须获取要添加签名字段的PDF文档。

**添加签名字段**

要成功地向PDF文档添加签名字段，请指定用于标识签名字段位置的坐标值。 （如果添加了不可见的签名字段，则这些值不是必需的。）此外，您还可以指定在将签名应用到签名字段后，PDF文档中的哪些字段将被锁定。

**将PDF文档另存为PDF文件**

在签名服务向PDF文档添加签名字段后，您可以将该文档另存为PDF文件，以便用户可以在Acrobat或Adobe reader中打开它。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API添加签名字段 {#add-signature-fields-using-the-java-api}

使用签名API(Java)添加签名字段：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取添加了签名字段的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，它使用其构造函数并传递一个指定PDF文档位置的字符串值，来表示要向其添加签名字段的PDF文档。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 添加签名字段

   * 创建一个 `PositionRectangle` 对象，该对象使用其构造函数指定签名字段的位置。 在构造函数中，指定坐标值。
   * 如果需要，请创建一 `FieldMDPOptions` 个对象，该对象指定将数字签名应用到签名字段时锁定的字段。
   * 通过调用对象的方法并传递以下值，将签 `SignatureServiceClient` 名字段添 `addSignatureField` 加到PDF文档：

      * A `com.adobe.idp`. `Document` 对象，它表示添加了签名字段的PDF文档。
      * 指定签名字段名称的字符串值。
      * 一个 `java.lang.Integer` 值，它表示添加签名字段的页码。
      * 一个 `PositionRectangle` 对象，它指定签名字段的位置。
      * 一个 `FieldMDPOptions` 对象，它指定在将数字签名应用到签名字段后锁定的PDF文档中的字段。 此参数值是可选的，您可以传递 `null`。
   * 指定 `PDFSeedValueOptions` 各种运行时值的对象。 此参数值是可选的，您可以传递 `null`。

      该 `addSignatureField` 方法返回 `com.adobe.idp`。 `Document` 表示包含签名字段的PDF文档的对象。
   >[!NOTE]
   >
   >可以调用对 `SignatureServiceClient` 象的方法来 `addInvisibleSignatureField` 添加不可见的签名字段。

1. 将PDF文档另存为PDF文件

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用 `com.adobe.idp`。 `Document` 对象的方 `copyToFile` 法将对象的内容复 `Document` 制到文件。 确保使用 `com.adobe.idp`。 `Document` 由方法返回的对 `addSignatureField` 象。

**另请参阅**

[签名服务API快速入门](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### 使用Web服务API添加签名字段 {#add-signature-fields-using-the-web-service-api}

要使用签名API（Web服务）添加签名字段，请执行以下操作：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取添加了签名字段的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储将包含签名字段的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 添加签名字段

   通过调用对象的方法并传递以下值，向PDF `SignatureServiceClient` 文档添 `addSignatureField` 加一个签名字段：

   * 一个 `BLOB` 对象，它表示向其添加签名字段的PDF文档。
   * 指定签名字段名称的字符串值。
   * 一个整数值，它表示要向其添加签名字段的页码。
   * 一个 `PositionRect` 对象，它指定签名字段的位置。
   * 一个 `FieldMDPOptions` 对象，它指定在将数字签名应用到签名字段后锁定的PDF文档中的字段。 此参数值是可选的，您可以传递 `null`。
   * 指定 `PDFSeedValueOptions` 各种运行时值的对象。 此参数值是可选的，您可以传递 `null`。
   该方 `addSignatureField` 法返回一个对 `BLOB` 象，该对象表示包含签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示将包含签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `addSignatureField` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 检索签名字段名称 {#retrieving-signature-field-names}

您可以检索位于要签名或验证的PDF文档中的所有签名字段的名称。 如果不确定PDF文档中的签名字段名称或要验证这些名称，可以通过编程方式检索它们。 签名服务返回签名字段的完全限定名称，如 `form1[0].grantApplication[0].page1[0].SignatureField1[0]`。

>[!NOTE]
>
>有关签名服务的详细信息，请参阅AEM [表单的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)

### 步骤摘要 {#summary_of_steps-1}

要检索签名字段名称，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含签名字段的PDF文档。
1. 检索签名字段名称。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含签名字段的PDF文档**

检索包含签名字段的PDF文档。

**检索签名字段名称**

在检索包含一个或多个签名字段的PDF文档后，可以检索签名字段名称。

**另请参阅**

[使用Java API检索签名字段名称](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[使用Web服务API检索签名字段](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API检索签名字段名称 {#retrieve-signature-field-names-using-the-java-api}

使用签名API(Java)检索签名字段名称：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取包含签名字段的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，它使用其构造函数并传递一个指定PDF文档位置的字符串值，来表示包含签名字段的PDF文档。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 检索签名字段名称

   * 通过调用对象的方法并传 `SignatureServiceClient` 递包含签名字 `getSignatureFieldList` 段的PDF文 `com.adobe.idp.Document` 档的对象，检索签名字段名称。 此方法返回一 `java.util.List` 个对象，其中每个元素都包含一个 `PDFSignatureField` 对象。 使用此对象，您可以获取有关签名字段的其他信息，如签名字段是否可见。
   * 遍历对象 `java.util.List` 以确定是否存在签名字段名称。 对于PDF文档中的每个签名字段，您可以获得单独的 `PDFSignatureField` 对象。 要获取签名字段的名称，请调用对 `PDFSignatureField` 象的方 `getName` 法。 此方法返回指定签名字段名称的字符串值。

**另请参阅**

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[快速入门（SOAP模式）:使用Java API检索签名字段名称](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API检索签名字段 {#retrieve-signature-field-using-the-web-service-api}

使用签名API（Web服务）检索签名字段名称：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含签名字段的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储包含签名字段的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过为 `BLOB` 对象的字段分配字 `MTOM` 节数组内容来填充对象。

1. 检索签名字段名称

   * 通过调用对象的方法并传 `SignatureServiceClient` 递包含签名字 `getSignatureFieldList` 段的PDF文档的 `BLOB` 对象，检索签名字段名称。 此方法返回一个 `MyArrayOfPDFSignatureField` 集合对象，其中每个元素都包含一个 `PDFSignatureField` 对象。
   * 遍历对象 `MyArrayOfPDFSignatureField` 以确定是否存在签名字段名称。 对于PDF文档中的每个签名字段，您可以获得一个 `PDFSignatureField` 对象。 要获取签名字段的名称，请调用对 `PDFSignatureField` 象的方 `getName` 法。 此方法返回指定签名字段名称的字符串值。

**另请参阅**

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 修改签名字段 {#modifying-signature-fields}

您可以使用Java API和Web服务API修改位于PDF文档中的签名字段。 修改签名字段涉及操作其签名字段锁定词典值或种子值词典值。

字 *段锁定词典* ，指定签名字段签名时锁定的字段列表。 锁定的字段会阻止用户对字段进行更改。 种 *子值词典* ，包含在应用签名时使用的约束信息。 例如，您可以更改权限，以控制在签名不失效的情况下可能执行的操作。

通过修改现有签名字段，您可以对PDF文档进行更改，以反映不断变化的业务要求。 例如，新业务要求可能要求在文档签名后锁定所有文档字段。

本节介绍如何通过修改字段锁定词典和种子值词典值来修改签名字段。 对签名字段所做的更改锁定词典导致签名字段时PDF文档中的所有字段都被锁定。 对种子值字典所做的更改会禁止对文档进行特定类型的更改。

>[!NOTE]
>
>有关签名服务和修改签名字段的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要修改PDF文档中的签名字段，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要修改的签名字段的PDF文档。
1. 设置词典值。
1. 修改签名字段。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括LiveCycle java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含要修改的签名字段的PDF文档**

检索包含要修改的签名字段的PDF文档。

**设置词典值**

要修改签名字段，请为其字段锁词典或种子值词典指定值。 指定签名字段锁定词典值涉及指定签名字段时锁定的PDF文档字段。 （本节讨论如何锁定所有字段。）

可以设置以下种子值字典值：

* **修订检查**:指定在将签名应用到签名字段时是否执行吊销检查。
* **证书选项**:为证书种子值字典赋值。 在指定证书选项之前，建议您熟悉证书种子值词典。 (请参阅 [PDF参考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **摘要选项**:指定用于签名的摘要算法。 有效值为SHA1、SHA256、SHA384、SHA512和RIPEMD160。
* **筛选**:指定与签名字段一起使用的过滤器。 例如，您可以使用Adobe.PPKLite滤镜。 (请参阅 [PDF参考](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)。)
* **标记选项**:指定与此签名字段关联的标记值。 值1表示签署方只能为条目使用指定的值。 值0表示允许其他值。 下面是位位置：

   * **** 1（过滤器）:用于签名字段的签名处理程序
   * **** 2（子过滤器）:指示在签名时使用的可接受编码的名称数组
   * **3(V)**:用于签署签名字段的签名处理程序的最低版本号
   * **** 4（理由）:一组字符串，它指定对文档进行签名的可能原因
   * **** 5(PDFegalWarnings):指定可能合法证明的字符串数组

* **法律证明**:当文档经过认证时，会自动扫描其是否有特定类型的内容，这些内容会使文档的可见内容变得模糊或具有误导性。 例如，注释可以模糊文本，这对于了解正在验证的内容很重要。 扫描过程生成指示存在这种类型的内容的警告。 它还提供了可能生成警告的内容的附加说明。
* **权限**:指定可在PDF文档上使用的权限，而不使签名失效。
* **原因**:指定必须签署此文档的原因。
* **时间戳**:指定时间戳选项。 例如，可以设置所使用的时间戳服务器的URL。
* **版本**:指定用于签署签名字段的签名处理程序的最低版本号。

**修改签名字段**

在创建签名服务客户端后，检索包含要修改的签名字段的PDF文档，并设置词典值，您可以指示签名服务修改签名字段。 然后，签名服务将返回包含修改后的签名字段的PDF文档。 原始PDF文档不受影响。

**将PDF文档另存为PDF文件**

将包含修改后的签名字段的PDF文档另存为PDF文件，以便用户可以在Acrobat或Adobe reader中打开它。

**另请参阅**

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[签名服务API快速入门](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### 使用Java API修改签名字段 {#modify-signature-fields-using-the-java-api}

使用签名API(Java)修改签名字段：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取包含要修改的签名字段的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，它表示包含要修改的签名字段的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置词典值

   * 使用对 `PDFSignatureFieldProperties` 象的构造函数创建对象。 对象 `PDFSignatureFieldProperties` 存储签名字段锁定词典和种子值词典信息。
   * 使用对 `PDFSeedValueOptionSpec` 象的构造函数创建对象。 通过此对象可设置种子值字典值。
   * 通过调用对象的方法并传递枚举值， `PDFSeedValueOptionSpec` 禁止对 `setMdpValue` PDF文档 `MDPPermissions.NoChanges` 进行更改。
   * 使用对 `FieldMDPOptionSpec` 象的构造函数创建对象。 此对象允许您设置签名字段锁定词典值。
   * 通过调用对象的方法并传递枚举值，锁 `FieldMDPOptionSpec` 定PDF文档 `setMdpValue` 中的所有 `FieldMDPAction.ALL` 字段。
   * 通过调用对象的方法并传递对 `PDFSignatureFieldProperties` 象来设置 `setSeedValue` 种子值字典 `PDFSeedValueOptionSpec` 信息。
   * 通过调用对象的方法并传递对 `PDFSignatureFieldProperties`象来设置签 `setFieldMDP` 名字段锁定词典 `FieldMDPOptionSpec` 信息。
   >[!NOTE]
   >
   >要查看可设置的所有种子值字典值，请参阅类 `PDFSeedValueOptionSpec` 引用。 (请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

1. 修改签名字段

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值来修 `modifySignatureField` 改签名字段：

   * 存储 `com.adobe.idp.Document` 包含要修改的签名字段的PDF文档的对象
   * 指定签名字段名称的字符串值
   * 存储 `PDFSignatureFieldProperties` 签名字段锁词典和种子值词典信息的对象
   该方 `modifySignatureField` 法返回一个对 `com.adobe.idp.Document` 象，该对象存储包含修改后的签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。 确保使用方 `com.adobe.idp.Document` 法返回的 `modifySignatureField` 对象。

### 使用Web服务API修改签名字段 {#modify-signature-fields-using-the-web-service-api}

使用签名API（Web服务）修改签名字段：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要修改的签名字段的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 对 `BLOB` 象用于存储包含要修改的签名字段的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。

1. 设置词典值

   * 使用对 `PDFSignatureFieldProperties` 象的构造函数创建对象。 该对象存储签名字段锁词典和种子值词典信息。
   * 使用对 `PDFSeedValueOptionSpec` 象的构造函数创建对象。 通过此对象可设置种子值字典值。
   * 通过将枚举值指定给对象的数 `MDPPermissions.NoChanges` 据成员，禁止对PDF `PDFSeedValueOptionSpec` 文档进 `mdpValue` 行更改。
   * 使用对 `FieldMDPOptionSpec` 象的构造函数创建对象。 此对象允许您设置签名字段锁定词典值。
   * 通过将枚举值指定给对象的数据 `FieldMDPAction.ALL` 成员，锁定PDF文 `FieldMDPOptionSpec` 档中的所 `mdpValue` 有字段。
   * 通过将对象指定给对象的数 `PDFSeedValueOptionSpec` 据成员来设置 `PDFSignatureFieldProperties` 种子值字 `seedValue` 典信息。
   * 通过将对象分配给对象的数据成 `FieldMDPOptionSpec` 员来设置签 `PDFSignatureFieldProperties` 名字段锁定词 `fieldMDP` 典信息。
   >[!NOTE]
   >
   >要查看可设置的所有种子值字典值，请参阅类 `PDFSeedValueOptionSpec` 引用。 (请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 修改签名字段

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值来修 `modifySignatureField` 改签名字段：

   * 存储 `BLOB` 包含要修改的签名字段的PDF文档的对象
   * 指定签名字段名称的字符串值
   * 存储 `PDFSignatureFieldProperties` 签名字段锁词典和种子值词典信息的对象
   该方 `modifySignatureField` 法返回一个对 `BLOB` 象，该对象存储包含修改后的签名字段的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示将包含签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方法返 `BLOB` 回的对象的 `addSignatureField` 内容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对PDF文档进行数字签名 {#digitally-signing-pdf-documents}

数字签名可以应用于PDF文档，从而提供更高的安全性。 数字签名（如手写签名）提供了一种方法，让签名者识别自己并对文档做出声明。 用于对文档进行数字签名的技术有助于确保签署方和接收方都清楚已签名的内容，并确信文档自签名后没有更改。

PDF文档通过公钥技术进行签名。 签署方有两个密钥：公钥和私钥。 私钥存储在用户凭据中，签名时该凭据必须可用。 公钥存储在用户的证书中，收件人必须可以使用该证书才能验证签名。 有关已吊销证书的信息，请参阅由证书颁发机构(CA)分发的证书撤销列表(CRL)和在线证书状态协议(OCSP)响应。 签名时间可从称为时间戳颁发机构的可信来源获得。

>[!NOTE]
>
>在对PDF文档进行数字签名之前，必须确保将证书添加到AEM Forms。 证书是使用管理控制台添加的，或使用Trust Manager API以编程方式添加的。 (请参 [阅使用Trust Manager API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

您可以以编程方式对PDF文档进行数字签名。 对PDF文档进行数字签名时，必须引用AEM Forms中存在的安全凭证。 凭据是用于签名的私钥。

签名服务在对PDF文档进行签名时执行以下步骤：

1. 签名服务通过传递请求中指定的别名从Truststore检索凭据。
1. Truststore将搜索指定的凭证。
1. 凭据将返回给签名服务并用于对文档进行签名。 此外，还会根据别名缓存凭据，以备将来请求。

有关处理安全凭据的信息，请参阅适 *用于应用程序服务器的安装和部署AEM Forms* 指南。

>[!NOTE]
>
>签署文档与认证文档之间存在差异。 (请参阅 [认证PDF文档](digitally-signing-certifying-documents.md#certifying-pdf-documents)。)

>[!NOTE]
>
>并非所有PDF文档都支持签名。 有关签名服务和对文档进行数字签名的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>签名服务不支持将嵌入的PDF数据作为操作输入的XDP文件，如文档认证。 此操作导致签名服务引发错误 `PDFOperationException`。 要解决此问题，请使用“PDF实用程序”服务将XDP文件转换为PDF文件，然后将转换后的PDF文件传递给签名服务操作。 (请参 [阅使用PDF实用程序](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)。)

**nCypher nShield HSM凭证**

当使用nCypher nShield HSM凭证对PDF文档进行签名或认证时，只有在重新启动部署AEM Forms的J2EE应用程序服务器后，才能使用新凭证。 但是，您可以设置一个配置值，这样，签名或验证操作就可以正常工作，而无需重新启动J2EE应用程序服务器。

您可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

在将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

**签名不可信**

在认证和签署同一PDF文档时，如果认证签名不可信，则在Acrobat或Adobe reader中打开PDF文档时，第一个签名旁会显示一个黄色三角形。 为避免这种情况，认证签名必须受信任。

**对基于XFA的表单的文档进行签名**

如果您尝试使用签名服务API对基于XFA的表单进行签名，则Acrobat中的数据可 `View` 能 `Signed``Version` 会丢失。 例如，请考虑以下工作流：

* 使用使用Designer创建的XDP文件，可以合并一个包含签名字段的表单设计和包含表单数据的XML数据。 您可以使用Forms服务生成交互式PDF文档。
* 使用签名服务API对PDF文档进行签名。

### 步骤摘要 {#summary_of_steps-3}

要对PDF文档进行数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名服务客户端。
1. 获取要签名的PDF文档。
1. 签署PDF文档。
1. 将签名的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取要签名的PDF文档**

要对PDF文档进行签名，您必须获得包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行签名。 签名字段可以使用Designer或通过编程方式添加。

**对PDF文档进行签名**

对PDF文档进行签名时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

可使用对象设置外观 `PDFSignatureAppearanceOptionSpec` 选项。 例如，可以通过调用对象的方法并传递来显示签 `PDFSignatureAppearanceOptionSpec` 名中的 `setShowDate` 日期 `true`。

您还可以指定是否执行撤消检查，该检查确定用于对PDF文档进行数字签名的证书是否已被撤销。 要执行撤销检查，可指定以下值之一：

* **不检查**:请勿执行撤销检查。
* **BestEffort**:始终尝试检查是否吊销链中的所有证书。 如果检查中出现任何问题，则假定撤销有效。 如果发生任何故障，请假定证书未被吊销。
* **** CheckIfAvailable:如果撤销信息可用，请检查是否撤销链中的所有证书。 如果检查中出现任何问题，则假定撤销无效。 如果发生任何故障，则假定证书已吊销且无效。 （这是默认值。）
* **始终检查**:检查是否撤销链中的所有证书。 如果任何证书中都不存在撤销信息，则假定撤销无效。

要对证书执行撤销检查，可使用对象指定证书撤销列表(CRL)服务器的URL。 `CRLOptionSpec` 但是，如果要执行撤销检查，但不指定CRL服务器的URL，则签名服务将从证书获取该URL。

在执行撤销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，与CRL服务器相比，使用OCSP服务器时，执行吊销检查的速度更快。 (请参阅https://tools.ietf.org/html/rfc2560上的“联机证书状态协 [议](https://tools.ietf.org/html/rfc2560)”。)

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在“Adobe Applications and Services”（Adobe应用程序和服务）中设置OCSP服务器，则会检查OCSP服务器，然后检查CRL服务器。 （请参阅AAC帮助中的“使用信任存储管理证书和凭据”）。

如果指定不执行撤销检查，则签名服务不会检查用于签署或验证文档的证书是否已被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>虽然可以在证书中指定CRL或OCSP服务器，但可以使用和对象覆盖证书中指定 `CRLOptionSpec` 的URL `OCSPOptionSpec` 。 例如，要覆盖CRL服务器，可调用对 `CRLOptionSpec` 象的方 `setLocalURI` 法。

时间戳是指跟踪已签名或已验证文档被修改的时间的过程。 文档一旦签名，即使文档所有者也不应修改它。 时间戳有助于增强已签名或已验证文档的有效性。 可以使用对象设置时间戳 `TSPOptionSpec` 选项。 例如，可指定时间戳提供者(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务中，遍历各个部分和相应的快速启动，使用撤销检查。 由于未指定CRL或OCSP服务器信息，因此服务器信息是从用于对PDF文档进行数字签名的证书中获取的。

要成功签署PDF文档，您可以指定将包含数字签名的签名字段的完全限定名称，例如 `form1[0].#subform[1].SignatureField3[3]`。 使用XFA表单字段时，签名字段的部分名称也可以使用： `SignatureField3[3]`.

您还必须引用安全凭证才能对PDF文档进行数字签名。 要引用安全凭证，请指定别名。 别名是对实际凭证的引用，该凭证可能位于PKCS#12文件（扩展名为。pfx）或硬件安全模块(HSM)中。 有关安全凭据的信息，请参阅适 *用于应用程序服务器的安装和部署AEM Forms* 指南。

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件，以便用户可以在Acrobat或Adobe reader中打开它。

**另请参阅**

[使用Java API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[使用Web服务API对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

[检索签名字段名称](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### 使用Java API对PDF文档进行数字签名 {#digitally-sign-pdf-documents-using-the-java-api}

使用签名API(Java)对PDF文档进行数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取要签名的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，它表示PDF文档，并使用其构造函数传递一个指定PDF文档位置的字符串值进行数字签名。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 对PDF文档进行签名

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值 `sign` 对PDF文档进行签名：

   * 表示 `com.adobe.idp.Document` 要签名的PDF文档的对象。
   * 一个字符串值，它表示将包含数字签名的签名字段的名称。
   * 表示 `Credential` 用于对PDF文档进行数字签名的凭证的对象。 通过调 `Credential` 用对象的静态方 `Credential``getInstance` 法并传递一个字符串值，该字符串值指定与安全凭证对应的别名值，来创建对象。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个字符串值，它表示PDF文档进行数字签名的原因。
   * 表示签署方联系信息的字符串值。
   * 控 `PDFSignatureAppearanceOptions` 制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义标志。
   * 一个 `java.lang.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。
   * 存储 `OCSPOptionSpec` “联机证书状态协议”(OCSP)支持首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 此参数是可选的，可以是可 `null`选的。 有关详细信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   该方 `sign` 法返回一个 `com.adobe.idp.Document` 表示已签名PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法并传递， `java.io.File`以将对象的内容 `Document` 复制到文件。 确保使用由 `com.adobe.idp.Document` 该方法返回的对 `sign` 象。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[快速入门（SOAP模式）:使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对PDF文档进行数字签名 {#digitally-signing-pdf-documents-using-the-web-service-api}

要使用签名API（Web服务）对PDF文档进行数字签名，请执行以下操作：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取要签名的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储已签名的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。

1. 对PDF文档进行签名

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值 `sign` 对PDF文档进行签名：

   * 表示 `BLOB` 要签名的PDF文档的对象。
   * 一个字符串值，它表示将包含数字签名的签名字段的名称。
   * 表示 `Credential` 用于对PDF文档进行数字签名的凭证的对象。 使用对 `Credential` 象的构造函数创建对象，并通过为对象的属性指定一个值 `Credential` 来指定别 `alias` 名。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个布尔值，它指定是否使用哈希算法。
   * 一个字符串值，它表示PDF文档进行数字签名的原因。
   * 表示签署方位置的字符串值。
   * 表示签署方联系信息的字符串值。
   * 控 `PDFSignatureAppearanceOptions` 制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义标志。
   * 一个 `System.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。 如果执行了此撤销检查，则它将嵌入签名中。 默认为 `false`.
   * 存储 `OCSPOptionSpec` “联机证书状态协议”(OCSP)支持首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。 有关此对象的信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 此参数是可选的，可以是可 `null`选的。
   该方 `sign` 法返回一个 `BLOB` 表示已签名PDF文档的对象。

1. 保存已签名的PDF文档

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `sign` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 对交互式表单进行数字签名 {#digitally-signing-interactive-forms}

您可以对Forms服务创建的交互式表单进行签名。 例如，请考虑以下工作流：

* 您可以合并使用设计器创建的基于XFA的PDF表单和使用Forms服务的XML文档中的表单数据。 Forms服务器呈现交互式表单。
* 您可以使用签名服务API对交互式表单进行签名。

结果是一个数字签名的交互式PDF表单。 对基于XFA表单的PDF表单进行签名时，请确保将PDF文件另存为Adobe静态PDF表单。 如果您尝试对另存为Adobe动态PDF表单的PDF表单进行签名，则会出现异常。 由于您正在对从表单服务返回的表单进行签名，请确保表单包含签名字段。

>[!NOTE]
>
>在对交互式表单进行数字签名之前，必须确保将证书添加到AEM表单。 证书是使用管理控制台添加的，或使用Trust Manager API以编程方式添加的。 (请参 [阅使用Trust Manager API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。)

使用Forms Service API时，将运行 `GenerateServerAppearance` 时选项设置为 `true`。 此运行时选项可确保在Acrobat或Adobe reader中打开时在服务器上生成的表单的外观仍然有效。 建议在生成交互式表单以使用Forms API进行签名时设置此运行时选项。

>[!NOTE]
>
>在阅读“对交互式表单进行数字签名”之前，建议您熟悉对PDF文档的签名。 (请参阅 [对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)。)

### 步骤摘要 {#summary_of_steps-4}

要以数字方式对Forms服务返回的交互式表单进行签名，请执行以下任务：

1. 包括项目文件。
1. 创建表单和签名客户端。
1. 使用Forms服务获取交互式表单。
1. 对交互式表单进行签名。
1. 将签名的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建表单和签名客户端**

由于此工作流同时调用表单和签名服务，因此请创建Forms服务客户端和签名服务客户端。

**使用Forms服务获取交互式表单**

您可以使用表单服务获取要签名的交互式PDF表单。 从AEM Forms开始，您可以将对象传 `com.adobe.idp.Document` 递给包含要渲染的表单的Forms服务。 此方法的名称为 `renderPDFForm2`。 此方法返回 `com.adobe.idp.Document` 包含要签名的表单的对象。 您可以将此实 `com.adobe.idp.Document` 例传递给签名服务。

同样，如果您使用Web服务，则可以将Forms `BLOB` 服务返回的实例传递给签名服务。

>[!NOTE]
>
>与“对交互式表单进行数字签名”部分关联的快速入门调用该 `renderPDFForm2` 方法。

**对交互式表单进行签名**

对PDF文档进行签名时，您可以设置签名服务使用的运行时选项。 您可以设置以下选项：

* 外观选项
* 吊销检查
* 时间戳值

可使用对象设置外观 `PDFSignatureAppearanceOptionSpec` 选项。 例如，可以通过调用对象的方法并传递来显示签 `PDFSignatureAppearanceOptionSpec` 名中的 `setShowDate` 日期 `true`。

**保存已签名的PDF文档**

签名服务对PDF文档进行数字签名后，您可以将其另存为PDF文件。 可以在Acrobat或Adobe reader中打开PDF文件。

**另请参阅**

[使用Java API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[使用Web服务API对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[对PDF文档进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[渲染交互式PDF表单](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### 使用Java API对交互式表单进行数字签名 {#digitally-sign-an-interactive-form-using-the-java-api}

使用表单和签名API(Java)对交互式表单进行数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar和adobe-forms-client.jar。

1. 创建表单和签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。
   * 使用对 `FormsServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 使用Forms服务获取交互式表单

   * 创建一 `java.io.FileInputStream` 个对象，它表示要通过使用其构造函数传递到Forms服务的PDF文档。 传递指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。
   * 创建一 `java.io.FileInputStream` 个对象，它表示包含表单数据的XML文档，以便通过使用其构造函数传递到Forms服务。 传递一个指定XML文件位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对 `java.io.FileInputStream` 象。
   * 创建 `PDFFormRenderSpec` 用于设置运行时选项的对象。 调用对 `PDFFormRenderSpec` 象的方 `setGenerateServerAppearance` 法并传递 `true`。
   * 调用对 `FormsServiceClient` 象的方 `renderPDFForm2` 法并传递以下值：

      * 包含 `com.adobe.idp.Document` 要渲染的PDF表单的对象。
      * 包含 `com.adobe.idp.Document` 要与表单合并的数据的对象。
      * 存 `PDFFormRenderSpec` 储运行时选项的对象。
      * 包 `URLSpec` 含Forms服务所需的URI值的对象。 您可以为 `null` 此参数值指定。
      * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
      该方 `renderPDFForm2` 法返回包 `FormsResult` 含表单数据流的对象

   * 通过调用对象的方法 `FormsResult` 检索PDF表 `getOutputContent` 单。 此方法返回一 `com.adobe.idp.Document` 个表示交互式表单的对象。


1. 对交互式表单进行签名

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值 `sign` 对PDF文档进行签名：

   * 表示 `com.adobe.idp.Document` 要签名的PDF文档的对象。 确保此对象是从Forms `com.adobe.idp.Document` 服务获取的对象。
   * 一个字符串值，它表示已签名的签名字段的名称。
   * 表示 `Credential` 用于对PDF文档进行数字签名的凭证的对象。 通过 `Credential` 调用对象的静态 `Credential` 方法创建对 `getInstance` 象。 传递一个字符串值，它指定与安全凭证对应的别名值。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个字符串值，它表示PDF文档进行数字签名的原因。
   * 表示签署方联系信息的字符串值。
   * 控 `PDFSignatureAppearanceOptions` 制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义标志。
   * 一个 `java.lang.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。
   * 存储 `OCSPPreferences` “联机证书状态协议”(OCSP)支持首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 此参数是可选的，可以是可 `null`选的。
   该方 `sign` 法返回一个 `com.adobe.idp.Document` 表示已签名PDF文档的对象。

1. 保存已签名的PDF文档

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法并传递， `java.io.File`以将对象的内容 `Document` 复制到文件。 确保使用方 `com.adobe.idp.Document` 法返回的 `sign` 对象。

**另请参阅**

[对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[快速入门（SOAP模式）:使用Java API对PDF文档进行数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API对交互式表单进行数字签名 {#digitally-sign-an-interactive-form-using-the-web-service-api}

使用表单和签名API（Web服务）对交互式表单进行数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 由于此客户端应用程序调用两个AEM Forms服务，因此请创建两个服务引用。 对与签名服务关联的服务引用使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   对于与Forms服务关联的服务引用，请使用以下WSDL定义： `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   由于两 `BLOB` 种服务引用都使用数据类型，因此在使用数据类 `BLOB` 型时完全限定数据类型。 在相应的Web服务快速启动中，所有实 `BLOB` 例都完全限定。

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建表单和签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
   * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。
   >[!NOTE]
   >
   >为Forms服务客户端重复这些步骤。

1. 使用Forms服务获取交互式表单

   * 使用对 `BLOB` 象的构造函数创建对象。 该 `BLOB` 对象用于存储已签名的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要签名的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。
   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储表单数据。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示包含表单数据的XML文件的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。
   * 创建 `PDFFormRenderSpec` 用于设置运行时选项的对象。 将值指 `true` 定到对 `PDFFormRenderSpec` 象的字 `generateServerAppearance` 段。
   * 调用对 `FormsServiceClient` 象的方 `renderPDFForm2` 法并传递以下值：

      * 包含 `BLOB` 要渲染的PDF表单的对象。
      * 包含 `BLOB` 要与表单合并的数据的对象。
      * 存 `PDFFormRenderSpec` 储运行时选项的对象。
      * 包 `URLSpec` 含Forms服务所需的URI值的对象。 您可以为 `null` 此参数值指定。
      * 存储 `java.util.HashMap` 文件附件的对象。 这是一个可选参数，您可 `null` 以指定是否不想将文件附加到表单。
      * 用于存储表单中页数的长输出参数。
      * 用于区域设置值的字符串输出参数。
      * 一 `FormResult` 个值，它是用于存储交互式表单的输出参数。
   * 通过调用对象的字段 `FormsResult` 来检索PDF表 `outputContent` 单。 此字段存储一 `BLOB` 个表示交互式表单的对象。


1. 对交互式表单进行签名

   通过调用对象的方法并传 `SignatureServiceClient` 递以下值 `sign` 对PDF文档进行签名：

   * 表示 `BLOB` 要签名的PDF文档的对象。 使用Forms `BLOB` 服务返回的实例。
   * 一个字符串值，它表示已签名的签名字段的名称。
   * 表示 `Credential` 用于对PDF文档进行数字签名的凭证的对象。 使用对 `Credential` 象的构造函数创建对象，并通过为对象的属性指定一个值 `Credential` 来指定别 `alias` 名。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个布尔值，它指定是否使用哈希算法。
   * 一个字符串值，它表示PDF文档进行数字签名的原因。
   * 表示签署方位置的字符串值。
   * 表示签署方联系信息的字符串值。
   * 控 `PDFSignatureAppearanceOptions` 制数字签名外观的对象。 例如，您可以使用此对象向数字签名添加自定义标志。
   * 一个 `System.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。 如果执行了此撤销检查，则它将嵌入签名中。 默认为 `false`.
   * 存储 `OCSPPreferences` “联机证书状态协议”(OCSP)支持首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。 有关此对象的信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 此参数是可选的，可以是可 `null`选的。
   该方 `sign` 法返回一个 `BLOB` 表示已签名PDF文档的对象。

1. 保存已签名的PDF文档

   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `sign` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[对交互式表单进行数字签名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF文档认证 {#certifying-pdf-documents}

您可以通过使用称为认证签名的特定类型的签名对PDF文档进行认证来保护它。 通过以下方式将认证签名与数字签名区分开：

* 它必须是应用于PDF文档的第一个签名；即，在应用认证签名时，文档中的任何其他签名字段都必须未签名。 PDF文档中仅允许一个认证签名。 如果要对PDF文档进行签名和验证，则必须在对其进行签名之前对其进行验证。 验证PDF文档后，您可以对其他签名字段进行数字签名。
* 文档的作者或作者可以指定以某些方式修改文档，而不会使已验证的签名失效。 例如，文档可能允许填写表单或添加注释。 如果作者指定不允许进行某些修改，则Acrobat会限制用户以这种方式修改文档。 如果进行了此类修改（如使用其他应用程序），则认证签名无效，并且当用户打开文档时，Acrobat会发出警告。 （对于未经认证的签名，不会阻止修改，并且正常的编辑操作不会使原始签名失效。）
* 在签名时，将扫描文档以查找可能使文档内容含糊或具有误导性的特定类型的内容。 例如，注释可能会模糊页面上的某些文本，这些文本对于了解正在验证的内容很重要。 可以提供有关此类内容的说明（法律证明）。

您可以使用签名服务Java API或签名Web服务API以编程方式验证PDF文档。 在验证PDF文档时，必须引用凭证服务中存在的安全凭证。 有关安全凭据的信息，请参阅适 *用于应用程序服务器的安装和部署AEM Forms* 指南。

>[!NOTE]
>
>在验证和签署同一PDF文档时，如果验证签名不可信，则在Acrobat或Adobe reader中打开PDF文档时，第一个签名旁边将显示一个黄色的三角形。 要避免这种情况，必须信任认证签名。

>[!NOTE]
>
>当使用nCypher nShield HSM凭证对PDF文档进行签名或认证时，只有在部署AEM Forms的J2EE应用程序服务器重新启动之前，才能使用新凭证。 但是，您可以设置一个配置值，这样，签名或验证操作就可以正常工作，而无需重新启动J2EE应用程序服务器。

您可以在cknfastrc文件中添加以下配置值，该文件位于/opt/nfast/cknfastrc(或c:\nfast\cknfastrc):

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

在将此配置值添加到cknfastrc文件后，无需重新启动J2EE应用程序服务器即可使用新凭据。

>[!NOTE]
>
>有关签名服务和文档认证的详细信息，请参阅AEM [表单服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要验证PDF文档，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取要认证的PDF文档。
1. 验证PDF文档。
1. 将认证的PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名操作之前，必须创建签名客户端。

**获取PDF文档以验证**

要验证PDF文档，您必须获得包含签名字段的PDF文档。 如果PDF文档不包含签名字段，则无法对其进行认证。 签名字段可以使用Designer或通过编程方式添加。 有关以编程方式添加签名字段的信息，请参阅 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。

**验证PDF文档**

要成功验证PDF文档，您需要以下由签名服务用来验证PDF文档的输入值：

* **PDF文档**:包含签名字段的PDF文档，该字段是包含已验证签名的图形表示形式的表单字段。 PDF文档必须包含签名字段，才能进行认证。 签名字段可以使用Designer或通过编程方式添加。 (请参阅 [添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)。)
* **签名字段名称**:经过认证的签名字段的完全限定名称。 以下值是一个示例： `form1[0].#subform[1].SignatureField3[3]`. 使用XFA表单字段时，签名字段的部分名称也可以使用： `SignatureField3[3]`. 如果为字段名称传递了null值，则会动态创建并验证不可见的签名字段。
* **安全凭证**:用于验证PDF文档的凭证。 此安全凭据包含口令和别名，该口令和别名必须与位于凭据服务中的凭据中显示的别名匹配。 别名是对实际凭证的引用，该凭证可能位于PKCS#12文件（扩展名为。pfx）或硬件安全模块(HSM)中。
* **哈希算法**:用于摘要PDF文档的哈希算法。
* **签名原因**:Acrobat或Adobe Reader中显示的值，以便其他用户了解PDF文档被认证的原因。
* **签署方的位置**:由凭证指定的签署方的位置。
* **联系信息**:签署方的联系信息，如地址和电话号码。
* **权限信息**:控制最终用户在文档上可以执行的操作而不会导致认证签名无效的权限。 例如，您可以设置权限，以便对PDF文档进行任何更改都会导致认证的签名无效。
* **法律解释**:文档经过认证后，会自动扫描其是否有特定类型的内容，这些内容可能会使文档的内容含糊或具有误导性。 例如，注释可能会模糊页面上的某些文本，这些文本对于了解正在验证的内容很重要。 扫描过程生成关于这些类型的内容的警告。 此值提供了可能生成警告的内容的附加说明。
* **外观选项**:控制认证签名外观的选项。 例如，认证签名可显示日期信息。
* **撤销检查**:此值指定是否对签署方的证书执行吊销检查。 默认设置表 `false` 示不执行吊销检查。
* **OCSP设置**:“联机证书状态协议(OCSP)”支持的设置，提供有关用于认证PDF文档的凭证状态的信息。 例如，您可以指定服务器的URL，该URL提供有关您用于登录PDF文档的凭证的信息。
* **CRL设置**:完成吊销检查时证书吊销列表(CRL)首选项的设置。 例如，您可以指定始终检查凭证是否被吊销。
* **时间戳**:定义应用于认证签名的时间戳信息的设置。 时间戳指示特定数据是在特定时间之前建立的。 此知识有助于在签署方和验证方之间建立信任关系。

**将认证的PDF文档另存为PDF文件**

签名服务验证PDF文档后，您可以将其另存为PDF文件，以便用户可以在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API验证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[使用Web服务API验证PDF文档](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API验证PDF文档 {#certify-pdf-documents-using-the-java-api}

使用签名API(Java)验证PDF文档：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取PDF文档以验证

   * 创建一 `java.io.FileInputStream` 个对象，它表示要验证的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 验证PDF文档

   通过调用对象的方法并 `SignatureServiceClient` 传递以下 `certify` 值来验证PDF文档：

   * 表示 `com.adobe.idp.Document` 要认证的PDF文档的对象。
   * 一个字符串值，它表示将包含签名的签名字段的名称。
   * 一个 `Credential` 对象，它表示用于验证PDF文档的凭证。 通过调 `Credential` 用对象的静态方 `Credential``getInstance` 法并传递一个字符串值，该字符串值指定与安全凭证对应的别名值，来创建对象。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个字符串值，它表示PDF文档被认证的原因。
   * 表示签署方联系信息的字符串值。
   * 一个 `MDPPermissions` 对象，它指定可对使签名无效的PDF文档执行的操作。
   * 控 `PDFSignatureAppearanceOptions` 制已验证签名外观的对象。 如果需要，可通过调用方法(例如， `setShowDate`
   * 一个字符串值，它解释使签名失效的操作。
   * 一个 `java.lang.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。 如果执行了此撤销检查，则它将嵌入签名中。 默认为 `false`.
   * 一个 `java.lang.Boolean` 对象，它指定是否锁定了要验证的签名字段。 如果字段已锁定，则签名字段将标记为只读，其属性将无法修改，并且没有必要权限的任何人都无法清除该字段。 默认为 `false`.
   * 存储 `OCSPPreferences` “联机证书状态协议”(OCSP)支持首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。 有关此对象的信息，请参 [阅AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 例如，在创建对象 `TSPPreferences` 后，可以通过调用对象的方法来设置TSP服 `TSPPreferences` 务器的URL `setTspServerURL` 。 此参数是可选的，可以是可 `null`选的。 有关详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。
   该方 `certify` 法返回一个 `com.adobe.idp.Document` 表示已验证PDF文档的对象。

1. 将认证的PDF文档另存为PDF文件

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用对 `com.adobe.idp.Document` 象的方 `copyToFile` 法，将对象的内容复 `com.adobe.idp.Document` 制到文件。

**另请参阅**

[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[快速入门（SOAP模式）:使用Java API认证PDF文档](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API验证PDF文档 {#certify-pdf-documents-using-the-web-service-api}

使用签名API（Web服务）验证PDF文档：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取PDF文档以验证

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储已验证的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示要验证的PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法并传递要读取的字 `System.IO.FileStream` 节数组、开始 `Read` 位置和流长度，用流数据填充字节数组。
   * 通过 `BLOB` 为对象的数据成员分 `MTOM` 配字节数组的内容来填充对象。

1. 验证PDF文档

   通过调用对象的方法并 `SignatureServiceClient` 传递以下 `certify` 值来验证PDF文档：

   * 表示 `BLOB` 要认证的PDF文档的对象。
   * 一个字符串值，它表示将包含签名的签名字段的名称。
   * 一个 `Credential` 对象，它表示用于验证PDF文档的凭证。 使用对 `Credential` 象的构造函数创建对象，通过为对象的属性指定值来 `Credential` 指定别 `alias` 名。
   * 一个 `HashAlgorithm` 对象，它指定表示用于摘要PDF文档的哈希算法的静态数据成员。 例如，可指定 `HashAlgorithm.SHA1` 使用SHA1算法。
   * 一个布尔值，它指定是否使用哈希算法。
   * 一个字符串值，它表示PDF文档被认证的原因。
   * 表示签署方位置的字符串值。
   * 表示签署方联系信息的字符串值。
   * 对 `MDPPermissions` 象的静态数据成员，它指定可对使签名无效的PDF文档执行的操作。
   * 一个布尔值，它指定是否使用 `MDPPermissions` 作为先前参数值传递的对象。
   * 一个字符串值，用于解释使签名失效的操作。
   * 控 `PDFSignatureAppearanceOptions` 制已验证签名外观的对象。 使用对 `PDFSignatureAppearanceOptions` 象的构造函数创建对象。 您可以通过设置签名的一个数据成员来修改签名的外观。
   * 一个 `System.Boolean` 对象，它指定是否对签署方的证书执行撤销检查。 如果执行了此撤销检查，则它将嵌入签名中。 默认为 `false`.
   * 一个 `System.Boolean` 对象，它指定是否锁定了要验证的签名字段。 如果字段已锁定，则签名字段将标记为只读，其属性将无法修改，并且没有必要权限的任何人都无法清除该字段。 默认为 `false`.
   * 指定 `System.Boolean` 签名字段是否已锁定的对象。 即，如果传递到上 `true` 一个参数，则传递 `true` 到此参数。
   * 存储 `OCSPPreferences` “联机证书状态协议”(OCSP)支持首选项的对象，它提供有关用于验证PDF文档的凭证状态的信息。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `CRLPreferences` 证书撤销列表(CRL)首选项的对象。 如果未执行撤销检查，则不使用此参数，您可以指定 `null`。
   * 存储 `TSPPreferences` 时间戳提供者(TSP)支持首选项的对象。 例如，创建对象 `TSPPreferences` 后，可以通过设置对象的数据成员来设置TSP `TSPPreferences` 的 `tspServerURL` URL。 此参数是可选的，可以是可 `null`选的。
   该方 `certify` 法返回一个 `BLOB` 表示已验证PDF文档的对象。

1. 将认证的PDF文档另存为PDF文件

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示将包含已验证的PDF文档的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `certify` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `binaryData` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[PDF文档认证](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证数字签名 {#verifying-digital-signatures}

可以验证数字签名以确保已签名的PDF文档未被修改，且数字签名有效。 验证数字签名时，您可以检查签名的状态和签名的属性，如签名者的身份。 在信任数字签名之前，建议您验证数字签名。 验证数字签名时，请参考包含数字签名的PDF文档。

假设签署方的身份未知。 当您在Acrobat中打开PDF文档时，将显示一条警告消息，指出签署者的身份未知，如下图所示。

![vd_vd_verifisig](assets/vd_vd_verifysig.png)

同样，当您以编程方式验证数字签名时，您可以确定签署方身份的状态。 例如，如果验证上图所示文档中的数字签名，则结果将是签署方的身份未知。

>[!NOTE]
>
>有关签名服务和验证数字签名的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-6}

要验证数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 验证数字签名。
1. 确定签名的状态。
1. 确定签署方的身份。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，请创建签名服务客户端。

**获取包含签名的PDF文档以验证**

要验证用于对PDF文档进行数字签名或认证的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置签名服务在验证PDF文档中的签名时使用的以下PKI运行时选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证程序计算机上的时间），它指示使用当前时间。 有关不同时间值的信息，请参阅 `VerificationTime`[AEM Forms API参考中的枚举值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您还可以指定是否在验证过程中执行撤销检查。 例如，您可以执行撤销检查以确定证书是否被吊销。 有关撤销检查选项的信息，请参阅 `RevocationCheckStyle` AEM Forms API参考中的枚举值 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要对证书执行撤销检查，请使用对象指定证书撤销列表(CRL)服务器的URL。 `CRLOptionSpec` 但是，如果未指定URL到CRL服务器，则签名服务将从证书获取该URL。

在执行撤销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，与CRL服务器相比，使用OCSP服务器时，执行吊销检查的速度会更快。 (请参阅 [联机证书状态协议](https://tools.ietf.org/html/rfc2560)。)

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果首先在“Adobe Applications and Services”（Adobe应用程序和服务）中设置OCSP服务器，则会检查OCSP服务器，然后检查CRL服务器。

如果不执行撤销检查，则签名服务不检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>可以使用和对象覆盖证书中指 `CRLOptionSpec` 定的 `OCSPOptionSpec` URL。 例如，要覆盖CRL服务器，可调用对 `CRLOptionSpec` 象的方 `setLocalURI` 法。

时间戳是跟踪已签名或已验证文档被修改的时间的过程。 文档签名后，任何人都无法修改它。 时间戳有助于增强已签名或已验证文档的有效性。 可以使用对象设置时间戳 `TSPOptionSpec` 选项。 例如，可指定时间戳提供者(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间被设置为， `VerificationTime.CURRENT_TIME` 撤销检查被设置为 `RevocationCheckStyle.BestEffort`。 由于未指定CRL或OCSP服务器信息，因此将从证书获取服务器信息。

**验证数字签名**

要成功验证签名，请指定包含签名的签名字段的完全限定名称，如 `form1[0].#subform[1].SignatureField3[3]`。 在使用XFA表单字段时，您还可以使用签名字段的部分名称： `SignatureField3`.

默认情况下，签名服务将文档在验证时间后的签名时间限制为65分钟。 如果用户尝试在当前时间验证签名，而签名时间晚于当前时间且在65分钟内，则签名服务不会创建验证错误。

>[!NOTE]
>
>有关验证签名时需要的其他值，请参阅 [AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**确定签名的状态**

作为验证数字签名的一部分，您可以检查签名的状态。

**确定签署方的身份**

您可以确定签署方的身份，该身份可以是以下值之一：

* **未知**:此签署方未知，因为无法执行签署方验证。
* **可信**:此签署方是受信任的。
* **不信任**:此签署方不受信任。

**另请参阅**

[使用Java API验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API验证数字签名 {#verify-digital-signatures-using-the-java-api}

使用签名服务API(Java)验证数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取包含签名的PDF文档以验证

   * 创建一 `java.io.FileInputStream` 个对象，它表示包含要使用其构造函数验证的签名的PDF文档。 传递指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置PKI运行时选项

   * 使用对 `PKIOptions` 象的构造函数创建对象。
   * 通过调用对象的方法并 `PKIOptions` 传递指定验 `setVerificationTime` 证时间的 `VerificationTime` 枚举值来设置验证时间。
   * 通过调用对象的方法并传递指定 `PKIOptions` 是否执行撤销 `setRevocationCheckStyle` 检查的枚举值， `RevocationCheckStyle` 设置撤销检查选项。

1. 验证数字签名

   通过调用对象的方 `SignatureServiceClient` 法并传递以 `verify2` 下值来验证签名：

   * 包含 `com.adobe.idp.Document` 已数字签名或已验证的PDF文档的对象。
   * 一个字符串值，它表示包含要验证的签名的签名字段名称。
   * 包 `PKIOptions` 含PKI运行时选项的对象。
   * 包 `VerifySPIOptions` 含SPI信息的实例。 可以为此 `null` 参数指定。
   该方 `verify2` 法返回一 `PDFSignatureVerificationInfo` 个对象，该对象包含可用于验证数字签名的信息。

1. 确定签名的状态

   * 通过调用对象的方法确定 `PDFSignatureVerificationInfo` 签名的状 `getStatus` 态。 此方法返回一 `SignatureStatus` 个指定签名状态的对象。 例如，如果未修改已签名的PDF文档，则此方法将返回 `SignatureStatus.DocumentSigNoChanges`。

1. 确定签署方的身份

   * 通过调用对象的方法确定签 `PDFSignatureVerificationInfo` 署者的身 `getSigner` 份。 此方法返回一个 `IdentityInformation` 对象。
   * 调用对 `IdentityInformation` 象的方 `getStatus` 法以确定签署方的身份。 此方法返回 `IdentityStatus` 指定标识的枚举值。 例如，如果签署方受信任，则此方法将返回 `IdentityStatus.TRUSTED`。

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[快速入门（SOAP模式）:使用Java API验证数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API验证数字签名 {#verify-digital-signatures-using-the-web-service-api}

使用签名服务API（Web服务）验证数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含签名的PDF文档以验证

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储包含要验证的数字或认证签名的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。

1. 设置PKI运行时选项

   * 使用对 `PKIOptions` 象的构造函数创建对象。
   * 通过为对象的数据成员分 `PKIOptions` 配指定验 `verificationTime` 证时间 `VerificationTime` 的枚举值来设置验证时间。
   * 通过为对象的数据成员分配指定是 `PKIOptions` 否执行撤销 `revocationCheckStyle` 检查的 `RevocationCheckStyle` 枚举值来设置撤销检查选项。

1. 验证数字签名

   通过调用对象的方 `SignatureServiceClient` 法并传递以 `verify2` 下值来验证签名：

   * 包含 `BLOB` 已数字签名或已验证的PDF文档的对象。
   * 一个字符串值，它表示包含要验证的签名的签名字段名称。
   * 包 `PKIOptions` 含PKI运行时选项的对象。
   * 包 `VerifySPIOptions` 含SPI信息的实例。 可以为此 `null` 参数指定。
   该方 `verify2` 法返回一 `PDFSignatureVerificationInfo` 个对象，该对象包含可用于验证数字签名的信息。

1. 确定签名的状态

   通过获取对象数据成员的值来确 `PDFSignatureVerificationInfo` 定签名的 `status` 状态。 此数据成员存储一 `SignatureStatus` 个指定签名状态的对象。 例如，如果修改了已签名的PDF文档，则数 `status` 据成员会存储该值 `SignatureStatus.DocumentSigNoChanges`。

1. 确定签署方的身份

   * 通过检索对象数据成员的值来确定签 `PDFSignatureVerificationInfo` 署者的 `signer` 身份。 此成员返回一个 `IdentityInformation` 对象。
   * 检索对 `IdentityInformation` 象的数据 `status` 成员以确定签署方的身份。 此数据成员返回 `IdentityStatus` 指定标识的枚举值。 例如，如果签署方受信任，则此成员将返回 `IdentityStatus.TRUSTED`。

**另请参阅**

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 验证多个数字签名 {#verifying-multiple-digital-signatures}

AEM Forms提供了验证PDF文档中所有数字签名的方法。 假定PDF文档包含多个数字签名，因为业务流程需要多个签名者的签名。 例如，考虑一项金融交易，该交易既需要贷款官签字，又需要经理签字。 您可以使用签名服务Java API或Web服务API验证PDF文档内的所有签名。 验证多个数字签名时，您可以检查每个签名的状态和属性。 在您信任数字签名之前，建议您验证它。 建议您熟悉验证单个数字签名。

>[!NOTE]
>
>有关签名服务和验证数字签名的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-7}

要验证多个数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要验证的签名的PDF文档。
1. 设置PKI运行时选项。
1. 检索所有数字签名。
1. 遍历所有签名。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，请创建签名服务客户端。

**获取包含签名的PDF文档以验证**

要验证用于对PDF文档进行数字签名或认证的签名，请获取包含签名的PDF文档。

**设置PKI运行时选项**

设置签名服务在验证PDF文档中的所有签名时使用的以下PKI运行时选项：

* 验证时间
* 吊销检查
* 时间戳值

在设置这些选项时，您可以指定验证时间。 例如，您可以选择当前时间（验证程序计算机上的时间），它指示使用当前时间。 有关不同时间值的信息，请参阅 `VerificationTime`[AEM Forms API参考中的枚举值](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

您还可以指定是否在验证过程中执行撤销检查。 例如，您可以执行撤销检查以确定证书是否被吊销。 有关撤销检查选项的信息，请参阅 `RevocationCheckStyle` AEM Forms API参考中的枚举值 [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

要对证书执行撤销检查，请使用对象指定证书撤销列表(CRL)服务器的URL。 `CRLOptionSpec` 但是，如果未指定CRL服务器的URL，则签名服务将从证书获取该URL。

在执行撤销检查时，可以使用联机证书状态协议(OCSP)服务器，而不是使用CRL服务器。 通常，使用OCSP服务器而非CRL服务器时，执行吊销检查的速度会更快。 (请参阅 [联机证书状态协议](https://tools.ietf.org/html/rfc2560)。)

您可以使用Adobe应用程序和服务设置签名服务使用的CRL和OCSP服务器顺序。 例如，如果OCSP服务器在Adobe Applications and services中是第一个设置的，则会检查OCSP服务器，然后检查CRL服务器。

如果不执行撤销检查，则签名服务不检查证书是否被吊销。 即，忽略CRL和OCSP服务器信息。

>[!NOTE]
>
>可以使用和对象覆盖证书中指 `CRLOptionSpec` 定的 `OCSPOptionSpec` URL。 例如，要覆盖CRL服务器，可调用对 `CRLOptionSpec` 象的方 `setLocalURI` 法。

时间戳是跟踪已签名或已验证文档被修改的时间的过程。 文档签名后，任何人都无法修改它。 时间戳有助于增强已签名或已验证文档的有效性。 可以使用对象设置时间戳选 `TSPOptionSpec` 项。 例如，可指定时间戳提供者(TSP)服务器的URL。

>[!NOTE]
>
>在Java和Web服务快速启动中，验证时间被设置为， `VerificationTime.CURRENT_TIME` 撤销检查被设置为 `RevocationCheckStyle.BestEffort`。 由于未指定CRL或OCSP服务器信息，因此将从证书获取服务器信息。

**检索所有数字签名**

要验证PDF文档中的所有数字签名，请从PDF文档中检索数字签名。 所有签名都会在列表中返回。 作为验证数字签名的一部分，请检查签名的状态。

>[!NOTE]
>
>与验证单个数字签名不同，验证多个签名时，无需指定签名字段名称。

**遍历所有签名**

遍历每个签名。 即，对于每个签名，验证数字签名，检查签署者的身份和每个签名的状态。 (请参阅 [验证数字签名](#verify-digital-signatures-using-the-java-api)。)

>[!NOTE]
>
>如果要求是整个文档，则无需遍历所有签名。

**另请参阅**

[使用Java API验证多个数字签名](#verify-digital-signatures-using-the-java-api)

[使用Web服务API验证多个数字签名](#verify-digital-signatures-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API验证多个数字签名 {#verify-multiple-digital-signatures-using-the-java-api}

使用Signature Service API(Java)验证多个数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对 `ServiceClientFactory` 象。

1. 获取包含签名的PDF文档以验证

   * 创建一 `java.io.FileInputStream` 个对象，它表示包含多个数字签名的PDF文档，并使用其构造函数进行验证。 传递指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 设置PKI运行时选项

   * 使用对 `PKIOptions` 象的构造函数创建对象。
   * 通过调用对象的方法并 `PKIOptions` 传递指定验 `setVerificationTime` 证时间的 `VerificationTime` 枚举值来设置验证时间。
   * 通过调用对象的方法并传递 `PKIOptions` 指定是否执行 `setRevocationCheckStyle` 撤销检查的 `RevocationCheckStyle` 枚举值来设置撤销检查选项。

1. 检索所有数字签名

   调用对 `SignatureServiceClient` 象的方 `verifyPDFDocument` 法并传递以下值：

   * 包 `com.adobe.idp.Document` 含包含多个数字签名的PDF文档的对象。
   * 包 `PKIOptions` 含PKI运行时选项的对象。
   * 包 `VerifySPIOptions` 含SPI信息的实例。 可以为此 `null` 参数指定。
   该方 `verifyPDFDocument` 法返回一个对 `PDFDocumentVerificationInfo` 象，该对象包含PDF文档中所有数字签名的相关信息。

1. 遍历所有签名

   * 通过调用对象的方法，对所 `PDFDocumentVerificationInfo` 有签名进行 `getVerificationInfos` 迭代。 此方法返回一个 `java.util.List` 对象，其中每个元素都是一个 `PDFSignatureVerificationInfo` 对象。 使用对 `java.util.Iterator` 象在签名列表中循环。
   * 使用对 `PDFSignatureVerificationInfo` 象，您可以执行任务，如通过调用对象的方法确定签 `PDFSignatureVerificationInfo` 名的状 `getStatus` 态。 此方法返回一个对 `SignatureStatus` 象，其静态数据成员会通知您有关签名状态的信息。 例如，如果签名未知，则此方法返回 `SignatureStatus.DocumentSignatureUnknown`。

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[快速入门（SOAP模式）:使用Java API验证多个数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[验证数字签名](#verify-digital-signatures-using-the-java-api)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API验证多个数字签名 {#verifying-multiple-digital-signatures-using-the-web-service-api}

使用Signature Service API（Web服务）验证多个数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含签名的PDF文档以验证

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象存储一个PDF文档，该文档包含多个要验证的数字签名。
   * 通过调 `System.IO.FileStream` 用对象的构造函数创建对象。 传递一个字符串值，它表示PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 将对象的属性指 `MTOM` 定到字节数组的内容来填充对象。

1. 设置PKI运行时选项

   * 使用对 `PKIOptions` 象的构造函数创建对象。
   * 通过为对象的数据成员分 `PKIOptions` 配指定验 `verificationTime` 证时间 `VerificationTime` 的枚举值来设置验证时间。
   * 通过为对象的数据成员分配一个 `PKIOptions` 枚举值来设置 `revocationCheckStyle` 撤销检查 `RevocationCheckStyle` 选项，该枚举值指定是否执行撤销检查。

1. 检索所有数字签名

   调用对 `SignatureServiceClient` 象的方 `verifyPDFDocument` 法并传递以下值：

   * 包 `BLOB` 含包含多个数字签名的PDF文档的对象。
   * 包 `PKIOptions` 含PKI运行时选项的对象。
   * 包 `VerifySPIOptions` 含SPI信息的实例。 可以为此参数指定null。
   该方 `verifyPDFDocument` 法返回一个对 `PDFDocumentVerificationInfo` 象，该对象包含PDF文档中所有数字签名的相关信息。

1. 遍历所有签名

   * 通过获取对象的数据成员 `PDFDocumentVerificationInfo` 来迭代所有 `verificationInfos` 签名。 此数据成员返回一个 `Object` 数组，其中每个元素都是一个 `PDFSignatureVerificationInfo` 对象。
   * 使用对 `PDFSignatureVerificationInfo` 象，您可以通过获取对象的数据成员来执行诸如确定签名 `PDFSignatureVerificationInfo` 状态之类的 `status` 任务。 此数据成员返回一个 `SignatureStatus` 对象，其静态数据成员会通知您有关签名状态的信息。 例如，如果签名未知，则此方法返回 `SignatureStatus.DocumentSignatureUnknown`。

**另请参阅**

[验证多个数字签名](#verifying-multiple-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除数字签名 {#removing-digital-signatures}

必须先从签名字段删除数字签名，然后才能应用较新的数字签名。 无法覆盖数字签名。 如果尝试将数字签名应用到包含签名的签名字段，则会出现异常。

>[!NOTE]
>
>有关签名服务的详细信息，请参 [阅AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-8}

要从签名字段中删除数字签名，请执行以下任务：

1. 包括项目文件。
1. 创建签名客户端。
1. 获取包含要删除的签名的PDF文档。
1. 从签名字段中删除数字签名。
1. 将PDF文档另存为PDF文件。

**包括项目文件**

在开发项目中包含必要的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

以下JAR文件必须添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（在JBoss上部署AEM表单时为必需）
* jbossall-client.jar（在JBoss上部署AEM表单时需要）

有关这些JAR文件的位置的信息，请参 [阅包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建签名客户端**

在以编程方式执行签名服务操作之前，必须创建签名服务客户端。

**获取包含要删除的签名的PDF文档**

要从PDF文档中删除签名，您必须获得包含签名的PDF文档。

**从签名字段中删除数字签名**

要从PDF文档中成功删除数字签名，必须指定包含数字签名的签名字段的名称。 此外，您必须拥有删除数字签名的权限；否则，会出现异常。

**将PDF文档另存为PDF文件**

在签名服务从签名字段删除数字签名后，您可以将PDF文档另存为PDF文件，以便用户可以在Acrobat或Adobe Reader中打开它。

**另请参阅**

[使用Java API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[使用Web服务API删除数字签名](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[添加签名字段](digitally-signing-certifying-documents.md#adding-signature-fields)

### 使用Java API删除数字签名 {#remove-digital-signatures-using-the-java-api}

使用签名API(Java)删除数字签名：

1. 包括项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-signatures-client.jar。

1. 创建签名客户端。

   * 创建包 `ServiceClientFactory` 含连接属性的对象。
   * 使用对 `SignatureServiceClient` 象的构造函数并传递该对象来创建 `ServiceClientFactory` 对象。

1. 获取包含要删除的签名的PDF文档

   * 创建一 `java.io.FileInputStream` 个对象，它表示包含要删除的签名的PDF文档，方法是使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对 `com.adobe.idp.Document` 象的构造函数并传递该对象来创建 `java.io.FileInputStream` 对象。

1. 从签名字段中删除数字签名

   通过调用对象的方法并传递以下值，从 `SignatureServiceClient` 签名字 `clearSignatureField` 段中删除数字签名：

   * 表示 `com.adobe.idp.Document` 包含要删除的签名的PDF文档的对象。
   * 一个字符串值，它指定包含数字签名的签名字段的名称。
   该方 `clearSignatureField` 法返回一个对 `com.adobe.idp.Document` 象，该对象表示从中删除了数字签名的PDF文档。

1. 将PDF文档另存为PDF文件

   * 创建一 `java.io.File` 个对象，并确保文件扩展名为。pdf。
   * 调用 `com.adobe.idp.Document` 对象的方 `copyToFile` 法。 传递对 `java.io.File` 象，将对象的内容复 `com.adobe.idp.Document` 制到文件。 确保使用由 `Document` 该方法返回的对 `clearSignatureField` 象。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[快速入门（SOAP模式）:使用Java API删除数字签名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[包括AEM Forms java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除数字签名 {#remove-digital-signatures-using-the-web-service-api}

使用签名API（Web服务）删除数字签名：

1. 包括项目文件

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >替换 `localhost` 为承载AEM Forms的服务器的IP地址。

1. 创建签名客户端

   * 使用对 `SignatureServiceClient` 象的默认构造函数创建对象。
   * 使用构 `SignatureServiceClient.Endpoint.Address` 造函数创建对 `System.ServiceModel.EndpointAddress` 象。 将指定WSDL的字符串值传递给AEM Forms服务(例如， `http://localhost:8080/soap/services/SignatureService?WSDL`)。 您无需使用该属 `lc_version` 性。 在创建服务引用时，会使用此属性。)
   * 通过 `System.ServiceModel.BasicHttpBinding` 获取字段的值创建对 `SignatureServiceClient.Endpoint.Binding` 象。 将返回值转换为 `BasicHttpBinding`。
   * 将对 `System.ServiceModel.BasicHttpBinding` 象的字段 `MessageEncoding` 设置为 `WSMessageEncoding.Mtom`。 此值确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段 `SignatureServiceClient.ClientCredentials.UserName.UserName`。
      * 为字段分配相应的口令值 `SignatureServiceClient.ClientCredentials.UserName.Password`。
      * 为字段指 `HttpClientCredentialType.Basic` 定常数值 `BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 为字段指 `BasicHttpSecurityMode.TransportCredentialOnly` 定常数值 `BasicHttpBindingSecurity.Security.Mode`。

1. 获取包含要删除的签名的PDF文档

   * 使用对 `BLOB` 象的构造函数创建对象。 该对 `BLOB` 象用于存储包含要删除的数字签名的PDF文档。
   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示已签名PDF文档的文件位置以及打开文件的模式。
   * 创建存储对象内容的字节数 `System.IO.FileStream` 组。 您可以通过获取对象的属性来确定字 `System.IO.FileStream` 节数组的大 `Length` 小。
   * 通过调用对象的方法，用流数据 `System.IO.FileStream` 填充字节数 `Read` 组。 传递要读取的字节数组、开始位置和流长度。
   * 通过 `BLOB` 将对象的属性指定 `MTOM` 为字节数组的内容来填充对象。

1. 从签名字段中删除数字签名

   通过调用对象的方法并 `SignatureServiceClient` 传递以下值 `clearSignatureField` 来删除数字签名：

   * 包 `BLOB` 含已签名PDF文档的对象。
   * 一个字符串值，它表示包含要删除的数字签名的签名字段的名称。
   该方 `clearSignatureField` 法返回一个对 `BLOB` 象，该对象表示从中删除了数字签名的PDF文档。

1. 将PDF文档另存为PDF文件

   * 通过调 `System.IO.FileStream` 用对象的构造函数并传递一个字符串值来创建对象，该字符串值表示包含空签名字段的PDF文档的文件位置以及打开文件的模式。
   * 创建一个字节数组，它存储方 `BLOB` 法返回的对象的内 `sign` 容。 通过获取对象数据成员的值 `BLOB` 填充字节 `MTOM` 数组。
   * 通过调 `System.IO.BinaryWriter` 用对象的构造函数并传递该对 `System.IO.FileStream` 象来创建。
   * 通过调用对象的方法并传递字节数组，将字 `System.IO.BinaryWriter` 节数组的内 `Write` 容写入PDF文件。

**另请参阅**

[删除数字签名](digitally-signing-certifying-documents.md#removing-digital-signatures)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM表单](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
