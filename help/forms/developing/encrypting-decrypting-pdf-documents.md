---
title: 加密和解密PDF文档
description: 使用加密服务加密和解密文档。 加密服务任务包括：使用密码对PDF文档进行加密；使用证书对PDF文档进行加密；从PDF文档中删除基于密码的加密；从PDF文档中删除基于证书的加密；解锁PDF文档以便可以执行其他服务操作；以及确定安全PDF文档的加密类型。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d3cbca7f-9277-4d61-b198-abf4bb008f15
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '8133'
ht-degree: 0%

---

# 加密和解密PDF文档 {#encrypting-and-decrypting-pdf-documents}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于加密服务**

加密服务允许您加密和解密文档。 文档加密后，其内容将变得不可读。 授权用户可以解密文档以获得对内容的访问权限。 如果使用密码对PDF文档进行加密，则必须先指定打开密码，然后才能在Adobe Reader或Adobe Acrobat中查看文档。 同样，如果PDF文档使用证书加密，则用户必须使用与用于加密PDF文档的证书（私钥）对应的公钥对PDF文档进行解密。

您可以使用加密服务完成以下任务：

* 使用密码加密PDF文档。 (请参阅[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)
* 使用证书加密PDF文档。 (请参阅[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。)
* 从PDF文档中删除基于密码的加密。 （请参阅[删除密码加密](encrypting-decrypting-pdf-documents.md#removing-password-encryption)。）
* 从PDF文档中删除基于证书的加密。 （请参阅[删除基于证书的加密](encrypting-decrypting-pdf-documents.md#removing-certificate-based-encryption)。）
* 解锁PDF文档，以便执行其他服务操作。 例如，在解锁密码加密的PDF文档后，您可以对其应用数字签名。 (请参阅[解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlocking-encrypted-pdf-documents)。)
* 确定受保护PDF文档的加密类型。 （请参阅[确定加密类型](encrypting-decrypting-pdf-documents.md#determining-encryption-type)。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 使用密码加密PDF文档 {#encrypting-pdf-documents-with-a-password}

使用密码加密PDF文档时，用户必须指定密码才能在Adobe Reader或Acrobat中打开PDF文档。 此外，在对文档执行另一AEM Forms操作(如对PDF文档进行数字签名)之前，必须解锁密码加密的PDF文档。

>[!NOTE]
>
>如果您将加密的PDF文档上传到AEM Forms存储库，它将无法对PDF文档进行解密并提取XDP内容。 建议您在将文档上传到AEM Forms存储库之前不要对其进行加密。 （请参阅[正在写入资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要使用口令加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密客户端API对象。
1. 获取要加密的PDF文档。
1. 设置加密运行时选项。
1. 添加密码。
1. 将加密的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。

**获取要加密的PDF文档**

获取未加密的PDF文档，以使用密码加密文档。 如果试图保护已加密的PDF文档，则会导致异常。

**设置加密运行时选项**

要使用口令加密PDF文档，可以指定四个值，包括两个口令值。 第一个密码值用于加密PDF文档，并且必须在打开PDF文档时指定。 第二个口令值（称为主口令值）用于从PDF文档中删除加密。 密码值区分大小写，且这两个密码值不能相同。

指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据之外的所有内容，或者仅加密文档的附件。 如果只加密文档的附件，则当用户尝试访问文件附件时，系统会提示用户输入密码。

加密PDF文档时，您可以指定与受保护文档关联的权限。 通过指定权限，您可以控制允许打开密码加密PDF文档的用户执行的操作。 例如，要成功提取表单数据，您必须设置以下权限：

* PASSWORD_EDIT_ADD
* PASSWORD_EDIT_MODIFY

>[!NOTE]
>
>权限指定为`PasswordEncryptionPermission`枚举值。

**添加密码**

检索不安全的PDF文档并设置加密运行时值后，可以向PDF文档添加口令。

**将加密的PDF文档另存为PDF文件**

您可以将密码加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-using-the-java-api)

[使用Web服务API加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-a-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)

### 使用Java API加密PDF文档 {#encrypt-a-pdf-document-using-the-java-api}

使用加密API (Java)对PDF文档进行密码加密：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建加密客户端API。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取要加密的PDF文档。

   * 创建表示要加密的PDF文档的`java.io.FileInputStream`对象，该对象使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 设置加密运行时选项。

   * 通过调用其构造函数创建`PasswordEncryptionOptionSpec`对象。
   * 通过调用`PasswordEncryptionOptionSpec`对象的`setEncryptOption`方法并传递指定要加密的PDF资源的`PasswordEncryptionOption`枚举值，来指定要加密的文档资源。 例如，要加密整个PDF文档，包括其元数据和附件，请指定`PasswordEncryptionOption.ALL`。
   * 使用`ArrayList`构造函数创建存储加密权限的`java.util.List`对象。
   * 通过调用`java.util.List`对象的`add`方法并传递与要设置的权限对应的枚举值来指定权限。 例如，要设置允许用户复制PDF文档中的数据的权限，请指定`PasswordEncryptionPermission.PASSWORD_EDIT_COPY`。 （对每个要设置的权限重复此步骤）。
   * 通过调用`PasswordEncryptionOptionSpec`对象的`setCompatability`方法并传递指定Acrobat兼容性级别的枚举值来指定Acrobat兼容性选项。 例如，您可以指定`PasswordEncryptionCompatability.ACRO_7`。
   * 指定密码值，以允许用户通过调用`PasswordEncryptionOptionSpec`对象的`setDocumentOpenPassword`方法并传递表示打开密码的字符串值来打开加密的PDF文档。
   * 指定主密码值，以允许用户通过调用`PasswordEncryptionOptionSpec`对象的`setPermissionPassword`方法并传递表示主密码的字符串值，从PDF文档中删除加密。

1. 添加密码。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingPassword`方法并传递以下值来加密PDF文档：

   * 包含要用密码加密的PDF文档的`com.adobe.idp.Document`对象。
   * 包含加密运行时选项的`PasswordEncryptionOptionSpec`对象。

   `encryptPDFUsingPassword`方法返回包含密码加密PDF文档的`com.adobe.idp.Document`对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`com.adobe.idp.Document`对象的内容复制到文件中。 确保使用`encryptPDFUsingPassword`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)


[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API加密PDF文档 {#encrypting-a-pdf-document-using-the-web-service-api}

使用加密API（Web服务）对PDF文档进行密码加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密客户端API对象。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已用密码加密的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。

1. 设置加密运行时选项。

   * 使用构造函数创建`PasswordEncryptionOptionSpec`对象。
   * 通过将`PasswordEncryptionOption`枚举值分配给`PasswordEncryptionOptionSpec`对象的`encryptOption`数据成员，指定要加密的PDF文档资源。 要加密整个PDF，包括其元数据和附件，请将`PasswordEncryptionOption.ALL`分配给此数据成员。
   * 通过将`PasswordEncryptionCompatability`枚举值分配给`PasswordEncryptionOptionSpec`对象的`compatability`数据成员来指定Acrobat兼容性选项。 例如，将`PasswordEncryptionCompatability.ACRO_7`分配给此数据成员。
   * 通过为`PasswordEncryptionOptionSpec`对象的`documentOpenPassword`数据成员分配一个表示打开密码的字符串值，指定允许用户打开加密的PDF文档的密码值。
   * 通过为`PasswordEncryptionOptionSpec`对象的`permissionPassword`数据成员分配一个表示主密码的字符串值，指定允许用户从PDF文档中删除加密的密码值。

1. 添加密码。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingPassword`方法并传递以下值来加密PDF文档：

   * 包含要用密码加密的PDF文档的`BLOB`对象。
   * 包含加密运行时选项的`PasswordEncryptionOptionSpec`对象。

   `encryptPDFUsingPassword`方法返回包含密码加密PDF文档的`BLOB`对象。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调用其构造函数并传递表示受保护PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`encryptPDFUsingPassword`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 使用证书加密PDF文档 {#encrypting-pdf-documents-with-certificates}

基于证书的加密允许您通过公钥技术为特定收件人加密文档。 可以为各种收件人授予该文档的不同权限。 公钥技术使加密的许多方面成为可能。 算法用于生成两个大数字，称为&#x200B;*键*，它们具有以下属性：

* 一个密钥用于加密一组数据。 随后，只能使用另一个密钥来解密数据。
* 一个键和另一个键无法区分。

其中一个密钥充当用户的私钥。 仅用户有权访问此键很重要。 另一个密钥是用户的公钥，可以与其他用户共享。

公钥证书包含用户的公钥和标识信息。 X.509格式用于存储证书。 证书通常由证书颁发机构(CA)颁发并进行数字签名，CA是一个公认的实体，提供对证书有效性的信任度量。 证书有过期日期，过期后不再有效。 此外，证书吊销列表(CRL)提供在证书过期日期之前被吊销的证书的相关信息。 证书颁发机构定期发布CRL。 证书吊销状态也可以通过网络上的联机证书状态协议(OCSP)进行检索。

>[!NOTE]
>
>如果您将加密的PDF文档上传到AEM Forms存储库，它将无法对PDF文档进行解密并提取XDP内容。 建议您在将文档上传到AEM Forms存储库之前不要对其进行加密。 （请参阅[正在写入资源](/help/forms/developing/aem-forms-repository.md#writing-resources)。）

>[!NOTE]
>
>使用证书加密PDF文档之前，必须确保将证书添加到AEM Forms。 使用管理控制台或以编程方式使用信任管理器API添加证书。 （请参阅[使用信任管理器API导入凭据](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)。）

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-1}

要使用证书加密PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密客户端API对象。
1. 获取要加密的PDF文档。
1. 引用证书。
1. 设置加密运行时选项。
1. 创建证书加密的PDF文档。
1. 将加密的PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

**创建加密客户端API对象**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建一个`EncrytionServiceClient`对象。 如果您使用的是Web服务加密服务API，请创建一个`EncryptionServiceService`对象。

**获取要加密的PDF文档**

获取要加密的未加密PDF文档。 如果尝试保护已加密的PDF文档，则会引发异常。

**引用证书**

要使用证书加密PDF文档，请引用用于加密PDF文档的证书。 证书是.cer文件、.crt文件或.pem文件。 PKCS#12文件用于存储具有相应证书的私钥。

使用证书加密PDF文档时，指定与受保护文档关联的权限。 通过指定权限，您可以控制打开证书加密PDF文档的用户可以执行的操作。

**设置加密运行时选项**

指定要加密的PDF文档资源。 您可以加密整个PDF文档，除文档元数据之外的所有内容，或者仅加密文档的附件。

**创建证书加密的PDF文档**

在检索不安全的PDF文档、引用证书并设置运行时选项后，可以创建证书加密的PDF文档。 PDF文档加密后，您需要相应的公钥才能将其解密。

**将加密的PDF文档另存为PDF文件**

您可以将加密的PDF文档另存为PDF文件。

**另请参阅**

[使用Java API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-java-api)

[使用Web服务API使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-java-api}

使用加密API (Java)使用证书加密PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建加密客户端API对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取要加密的PDF文档。

   * 创建表示要加密的PDF文档的`java.io.FileInputStream`对象，该对象使用其构造函数并传递一个指定PDF文档位置的字符串值。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 引用证书。

   * 使用它的构造函数创建存储权限信息的`java.util.List`对象。
   * 通过调用`java.util.List`对象的`add`方法并传递表示向打开受保护PDF文档的用户授予权限的`CertificateEncryptionPermissions`枚举值，指定与加密文档关联的权限。 例如，若要指定所有权限，请传递`CertificateEncryptionPermissions.PKI_ALL_PERM`。
   * 使用构造函数创建`Recipient`对象。
   * 创建一个`java.io.FileInputStream`对象，该对象表示用于加密PDF文档的证书，该证书使用其构造函数并传递指定证书位置的字符串值。
   * 使用构造函数创建`com.adobe.idp.Document`对象，并传递表示证书的`java.io.FileInputStream`对象。
   * 调用`Recipient`对象的`setX509Cert`方法并传递包含证书的`com.adobe.idp.Document`对象。 （此外，`Recipient`对象可以具有Truststore证书别名或LDAP URL作为证书源。）
   * 使用构造函数创建存储权限和证书信息的`CertificateEncryptionIdentity`对象。
   * 调用`CertificateEncryptionIdentity`对象的`setPerms`方法并传递存储权限信息的`java.util.List`对象。
   * 调用`CertificateEncryptionIdentity`对象的`setRecipient`方法并传递存储证书信息的`Recipient`对象。
   * 使用构造函数创建存储证书信息的`java.util.List`对象。
   * 调用`java.util.List`对象的添加方法并传递`CertificateEncryptionIdentity`对象。 （此`java.util.List`对象作为参数传递到`encryptPDFUsingCertificates`方法。）

1. 设置加密运行时选项。

   * 通过调用其构造函数创建`CertificateEncryptionOptionSpec`对象。
   * 通过调用`CertificateEncryptionOptionSpec`对象的`setOption`方法并传递指定要加密的PDF资源的`CertificateEncryptionOption`枚举值，来指定要加密的文档资源。 例如，要加密整个PDF文档，包括其元数据和附件，请指定`CertificateEncryptionOption.ALL`。
   * 通过调用`CertificateEncryptionOptionSpec`对象的`setCompat`方法并传递指定Acrobat兼容性级别的`CertificateEncryptionCompatibility`枚举值来指定Acrobat兼容性选项。 例如，您可以指定`CertificateEncryptionCompatibility.ACRO_7`。

1. 创建证书加密的PDF文档。

   通过调用`EncryptionServiceClient`对象的`encryptPDFUsingCertificates`方法并传递以下值，使用证书加密PDF文档：

   * 包含要加密的PDF文档的`com.adobe.idp.Document`对象。
   * 存储证书信息的`java.util.List`对象。
   * 包含加密运行时选项的`CertificateEncryptionOptionSpec`对象。

   `encryptPDFUsingCertificates`方法返回包含证书加密PDF文档的`com.adobe.idp.Document`对象。

1. 将加密的PDF文档另存为PDF文件。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`com.adobe.idp.Document`对象的内容复制到文件中。 确保使用`encryptPDFUsingCertificates`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API使用证书加密PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-encrypting-a-pdf-document-with-a-certificate-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API使用证书加密PDF文档 {#encrypt-a-pdf-document-with-a-certificate-using-the-web-service-api}

使用加密API（Web服务）使用证书加密PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密客户端API对象。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取要加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储已使用证书加密的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示要加密的PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 引用证书。

   * 使用构造函数创建`Recipient`对象。 此对象将存储证书信息。
   * 使用构造函数创建`BLOB`对象。 此`BLOB`对象将存储加密PDF文档的证书。
   * 通过调用其构造函数并传递一个表示证书文件位置和文件打开模式的字符串值，创建`System.IO.FileStream`对象。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。
   * 将存储证书的`BLOB`对象分配给`Recipient`对象的`x509Cert`数据成员。
   * 使用构造函数创建存储证书信息的`CertificateEncryptionIdentity`对象。
   * 将存储证书的`Recipient`对象分配给`CertificateEncryptionIdentity`对象的收件人数据成员。
   * 创建`Object`数组并将`CertificateEncryptionIdentity`对象分配给`Object`数组的第一个元素。 此`Object`数组作为参数传递到`encryptPDFUsingCertificates`方法。

1. 设置加密运行时选项。

   * 使用构造函数创建`CertificateEncryptionOptionSpec`对象。
   * 通过将`CertificateEncryptionOption`枚举值分配给`CertificateEncryptionOptionSpec`对象的`option`数据成员，指定要加密的PDF文档资源。 要加密整个PDF文档，包括其元数据和附件，请将`CertificateEncryptionOption.ALL`分配给此数据成员。
   * 通过将`CertificateEncryptionCompatibility`枚举值分配给`CertificateEncryptionOptionSpec`对象的`compat`数据成员来指定Acrobat兼容性选项。 例如，将`CertificateEncryptionCompatibility.ACRO_7`分配给此数据成员。

1. 创建证书加密的PDF文档。

   通过调用`EncryptionServiceService`对象的`encryptPDFUsingCertificates`方法并传递以下值，使用证书加密PDF文档：

   * 包含要加密的PDF文档的`BLOB`对象。
   * 存储证书信息的`Object`数组。
   * 包含加密运行时选项的`CertificateEncryptionOptionSpec`对象。

   `encryptPDFUsingCertificates`方法返回包含证书加密PDF文档的`BLOB`对象。

1. 将加密的PDF文档另存为PDF文件。

   * 通过调用其构造函数并传递表示受保护PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`encryptPDFUsingCertificates`方法返回的`BLOB`对象的数据内容。 通过获取`BLOB`对象的`binaryData`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除基于证书的加密 {#removing-certificate-based-encryption}

可以从PDF文档中删除基于证书的加密，以便用户可以在Adobe Reader或Acrobat中打开PDF文档。 要从使用证书加密的PDF文档中删除加密，必须引用公共密钥。 从PDF文档中删除加密后，该加密不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-2}

要从PDF文档中删除基于证书的加密，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除加密。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建一个`EncrytionServiceClient`对象。 如果您使用的是Web服务加密服务API，请创建一个`EncryptionServiceService`对象。

**获取加密的PDF文档**

获取加密的PDF文档，以删除基于证书的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。 同样，如果尝试从密码加密的文档中删除基于证书的加密，则会引发异常。

**删除加密**

要从已加密的PDF文档中删除基于证书的加密，您需要已加密的PDF文档以及与用于加密PDF文档的密钥对应的私钥。 从加密的PDF文档中删除基于证书的加密时，将指定私钥的别名值。 有关公钥的信息，请参阅[使用证书加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-certificates)。

>[!NOTE]
>
>私钥存储在AEM Forms信任存储区中。 将证书放在其中时，指定别名值。

**保存PDF文档**

从加密的PDF文档中删除基于证书的加密后，可以将PDF文档另存为PDF文件。 用户可以在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[使用Java API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-java-api)

[使用Web服务API删除基于证书的加密](encrypting-decrypting-pdf-documents.md#remove-certificate-based-encryption-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-java-api}

使用加密API (Java)从PDF文档中删除基于证书的加密：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用加密PDF文档的构造函数并传递指定加密PDF文档位置的字符串值，创建表示该加密文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 删除加密。

   通过调用`EncryptionServiceClient`对象的`removePDFCertificateSecurity`方法并传递以下值，从PDF文档中删除基于证书的加密：

   * 包含加密PDF文档的`com.adobe.idp.Document`对象。
   * 一个字符串值，指定与用于加密PDf文档的密钥对应的私钥的别名。

   `removePDFCertificateSecurity`方法返回包含不安全PDF文档的`com.adobe.idp.Document`对象。

1. 保存PDF文档。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中。 确保使用`removePDFCredentialSecurity`方法返回的`com.adobe.idp.Document`对象。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API删除基于证书的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-certificate-based-encryption-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API删除基于证书的加密 {#remove-certificate-based-encryption-using-the-web-service-api}

使用加密API（Web服务）删除基于证书的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储加密的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。

1. 删除加密。

   调用`EncryptionServiceClient`对象的`removePDFCertificateSecurity`方法并传递以下值：

   * 包含表示加密PDF文档的文件流数据的`BLOB`对象。
   * 一个字符串值，指定与用于加密PDf文档的私钥对应的公钥的别名。

   `removePDFCredentialSecurity`方法返回包含不安全PDF文档的`BLOB`对象。

1. 保存PDF文档。

   * 通过调用其构造函数并传递表示无保护PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`removePDFPasswordSecurity`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 删除密码加密 {#removing-password-encryption}

可以从PDF文档中删除基于密码的加密，以便用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。 从PDF文档中删除基于密码的加密后，文档不再安全。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-3}

要从PDF文档中删除基于密码的加密，请执行以下步骤：

1. 包含项目文件
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 删除密码。
1. 将PDF文档另存为PDF文件。

**包含项目文件**

将必要的文件包含在开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果在JBoss上部署了AEM Forms，则此为必填字段)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建一个`EncrytionServiceClient`对象。 如果您使用的是Web服务加密服务API，请创建一个`EncryptionServiceService`对象。

**获取加密的PDF文档**

获取加密的PDF文档以删除基于密码的加密。 如果尝试从未加密的PDF文档中删除加密，则会引发异常。

**删除密码**

要从已加密的PDF文档中删除基于密码的加密，您需要一个已加密的PDF文档和一个用于从PDF文档中删除加密的主密码值。 用于打开密码加密的PDF文档的密码不能用于删除加密。 使用密码对PDF文档进行加密时，指定主密码。 (请参阅[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

**保存PDF文档**

在Encryption服务从PDF文档中删除基于密码的加密后，您可以将PDF文档另存为PDF文件。 用户无需指定密码即可在Adobe Reader或Acrobat中打开PDF文档。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### 使用Java API删除基于密码的加密 {#remove-password-based-encryption-using-the-java-api}

使用加密API (Java)从PDF文档中删除基于密码的加密：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 通过使用加密的PDF文档的构造函数并传递指定PDF文档位置的字符串值，创建表示该文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 删除密码。

   通过调用`EncryptionServiceClient`对象的`removePDFPasswordSecurity`方法并传递以下值，从PDF文档中删除基于密码的加密：

   * 包含加密PDF文档的`com.adobe.idp.Document`对象。
   * 一个字符串值，它指定用于从PDF文档中删除加密的主口令值。

   `removePDFPasswordSecurity`方法返回包含不安全PDF文档的`com.adobe.idp.Document`对象。

1. 保存PDF文档。

   * 创建`java.io.File`对象并确保文件扩展名为.pdf。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以将`Document`对象的内容复制到文件中。 确保使用`removePDFPasswordSecurity`方法返回的`Document`对象。

**另请参阅**

[快速入门(SOAP模式)：使用Java API删除基于密码的加密](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-removing-password-based-encryption-using-the-java-api)

### 使用Web服务API删除基于密码的加密 {#remove-password-based-encryption-using-the-web-service-api}

使用加密API（Web服务）删除基于密码的加密：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储密码加密的PDF文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。

1. 删除密码。

   调用`EncryptionServiceService`对象的`removePDFPasswordSecurity`方法并传递以下值：

   * 包含表示加密PDF文档的文件流数据的`BLOB`对象。
   * 一个字符串值，它指定用于从PDF文档中删除加密的口令值。 使用密码加密PDF文档时指定此值。

   `removePDFPasswordSecurity`方法返回包含不安全PDF文档的`BLOB`对象。

1. 保存PDF文档。

   * 通过调用其构造函数并传递表示无保护PDF文档的文件位置的字符串值来创建`System.IO.FileStream`对象。
   * 创建一个字节数组，用于存储`removePDFPasswordSecurity`方法返回的`BLOB`对象的内容。 通过获取`BLOB`对象的`MTOM`数据成员的值填充字节数组。
   * 通过调用其构造函数并传递`System.IO.FileStream`对象来创建`System.IO.BinaryWriter`对象。
   * 通过调用`System.IO.BinaryWriter`对象的`Write`方法并传递字节数组，将字节数组的内容写入PDF文件。

**另请参阅**

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 解锁加密的PDF文档 {#unlocking-encrypted-pdf-documents}

必须先解锁密码加密或证书加密的PDF文档，然后才能对其执行其他AEM Forms操作。 如果尝试对加密的PDF文档执行操作，将生成异常。 解锁加密的PDF文档后，可以对其执行一个或多个操作。 这些操作可以属于其他服务，例如Acrobat Reader DC扩展服务。

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-4}

要解锁已加密的PDF文档，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 解锁文档。
1. 执行AEM Forms操作。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

**创建加密服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建一个`EncrytionServiceClient`对象。 如果您使用的是Web服务加密服务API，请创建一个`EncryptionServiceService`对象。

**获取加密的PDF文档**

获取加密的PDF文档以将其解锁。 如果尝试解锁未加密的PDF文档，则会引发异常。

**解锁文档**

要解除对密码加密的PDF文档的锁定，您需要一个加密的PDF文档和一个用于打开密码加密的PDF文档的密码值。 使用密码加密PDF文档时指定此值。 (请参阅[使用密码加密PDF文档](encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)。)

要解锁证书加密的PDF文档，您需要加密的PDF文档以及对应于用于加密PDF文档的私钥的公共密钥的别名值。

**执行AEM Forms操作**

解锁加密的PDF文档后，您可以对其执行其他服务操作，例如对其应用使用权限。 此操作属于Acrobat Reader DC扩展服务。

**另请参阅**

[使用Java API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-java-api)

[使用Web服务API解锁加密的PDF文档](encrypting-decrypting-pdf-documents.md#unlock-an-encrypted-pdf-document-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

### 使用Java API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-java-api}

使用加密API (Java)解锁加密的PDF文档：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建加密服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 使用加密PDF文档的构造函数并传递指定加密PDF文档位置的字符串值，创建表示该加密文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 解锁文档。

   通过调用`EncryptionServiceClient`对象的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法解锁已加密的PDF文档。

   要解锁使用密码加密的PDF文档，请调用`unlockPDFUsingPassword`方法并传递以下值：

   * 包含密码加密PDF文档的`com.adobe.idp.Document`对象。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用密码加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用`unlockPDFUsingCredential`方法并传递以下值：

   * 包含证书加密PDF文档的`com.adobe.idp.Document`对象。
   * 一个字符串值，指定与用于加密PDF文档的私钥对应的公钥的别名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都返回了您传递给另一个AEM Forms Java方法以执行操作的`com.adobe.idp.Document`对象。

1. 执行AEM Forms操作。

   对解锁的PDF文档执行AEM Forms操作，以满足您的业务要求。 例如，假设您要将使用权限应用到已解锁的PDF文档，请将`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`com.adobe.idp.Document`对象传递到`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速入门(SOAP模式)：使用Java API解锁加密的PDF文档](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-unlocking-an-encrypted-pdf-document-using-the-java-api)(SOAP模式)

[将使用权限应用于PDF文档](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API解锁加密的PDF文档 {#unlock-an-encrypted-pdf-document-using-the-web-service-api}

使用加密API（Web服务）解锁加密的PDF文档：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建加密服务客户端。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。

1. 解锁文档。

   通过调用`EncryptionServiceClient`对象的`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法解锁已加密的PDF文档。

   要解锁使用密码加密的PDF文档，请调用`unlockPDFUsingPassword`方法并传递以下值：

   * 包含密码加密PDF文档的`BLOB`对象。
   * 一个字符串值，它指定用于打开密码加密的PDF文档的密码值。 使用密码加密PDF文档时指定此值。

   要解锁使用证书加密的PDF文档，请调用`unlockPDFUsingCredential`方法并传递以下值：

   * 包含证书加密PDF文档的`BLOB`对象。
   * 一个字符串值，指定与用于加密PDf文档的私钥对应的公钥的别名。

   `unlockPDFUsingPassword`和`unlockPDFUsingCredential`方法都返回了您传递给其他AEM Forms方法以执行操作的`com.adobe.idp.Document`对象。

1. 执行AEM Forms操作。

   对解锁的PDF文档执行AEM Forms操作，以满足您的业务要求。 例如，假定您要对已解锁的PDF文档应用使用权限，请将`unlockPDFUsingPassword`或`unlockPDFUsingCredential`方法返回的`BLOB`对象传递到`ReaderExtensionsServiceClient`对象的`applyUsageRights`方法。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 确定加密类型 {#determining-encryption-type}

您可以使用Java加密服务API或Web服务加密服务API以编程方式确定保护PDF文档的加密类型。 有时需要动态确定PDF文档是否已加密，如果是，则确定加密类型。 例如，您可以确定PDF文档是使用基于密码的加密还是使用Rights Management策略进行保护。

PDF文档可通过以下加密类型进行保护：

* 基于密码的加密
* 基于证书的加密
* Rights Management服务创建的策略
* 另一种加密

>[!NOTE]
>
>有关加密服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary_of_steps-5}

要确定保护PDF文档的加密类型，请执行以下步骤：

1. 包括项目文件。
1. 创建加密服务客户端。
1. 获取加密的PDF文档。
1. 确定加密类型。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-encryption-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

**创建服务客户端**

要以编程方式执行加密服务操作，必须创建加密服务客户端。 如果您使用的是Java加密服务API，请创建一个`EncrytionServiceClient`对象。 如果您使用的是Web服务加密服务API，请创建一个`EncryptionServiceService`对象。

**获取加密的PDF文档**

获取PDF文档以确定保护它的加密类型。

**确定加密类型**

您可以确定保护PDF文档的加密类型。 如果PDF文档未受保护，则加密服务会通知您PDF文档未受保护。

**另请参阅**

[使用Java API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-java-api)

[使用Web服务API确定加密类型](encrypting-decrypting-pdf-documents.md#determine-the-encryption-type-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[加密服务API快速启动](/help/forms/developing/encryption-service-java-api-quick.md#encryption-service-java-api-quick-start-soap)

[使用策略保护文档](/help/forms/developing/protecting-documents-policies.md#protecting-documents-with-policies)

### 使用Java API确定加密类型 {#determine-the-encryption-type-using-the-java-api}

确定使用加密API (Java)保护PDF文档的加密类型：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-encryption-client.jar。

1. 创建服务客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EncryptionServiceClient`对象并传递`ServiceClientFactory`对象。

1. 获取加密的PDF文档。

   * 通过使用其构造函数并传递指定PDF文档位置的字符串值，创建表示PDF文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 确定加密类型。

   * 通过调用`EncryptionServiceClient`对象的`getPDFEncryption`方法并传递包含PDF文档的`com.adobe.idp.Document`对象来确定加密类型。 此方法返回`EncryptionTypeResult`对象。
   * 调用`EncryptionTypeResult`对象的`getEncryptionType`方法。 此方法返回指定加密类型的`EncryptionType`枚举值。 例如，如果PDF文档受基于密码的加密保护，此方法将返回`EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[快速启动(SOAP模式)：使用Java API确定加密类型](/help/forms/developing/encryption-service-java-api-quick.md#quick-start-soap-mode-determining-encryption-type-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API确定加密类型 {#determine-the-encryption-type-using-the-web-service-api}

确定使用加密API（Web服务）保护PDF文档的加密类型：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 确保使用以下WSDL定义： `http://localhost:8080/soap/services/EncryptionService?WSDL&lc_version=9.0.1`。

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建服务客户端。

   * 使用默认构造函数创建`EncryptionServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`EncryptionServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务（例如，`http://localhost:8080/soap/services/EncryptionService?WSDL`）。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。)
   * 通过获取`EncryptionServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给字段`EncryptionServiceClient.ClientCredentials.UserName.UserName`。
      * 将相应的密码值分配给字段`EncryptionServiceClient.ClientCredentials.UserName.Password`。
      * 将常量值`HttpClientCredentialType.Basic`分配给字段`BasicHttpBindingSecurity.Transport.ClientCredentialType`。
      * 将常量值`BasicHttpSecurityMode.TransportCredentialOnly`分配给字段`BasicHttpBindingSecurity.Security.Mode`。

1. 获取加密的PDF文档。

   * 使用构造函数创建`BLOB`对象。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示加密PDF文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法并传递要读取的字节数组、起始位置和流长度，使用流数据填充字节数组。
   * 通过将字节数组的内容分配给`BLOB`对象的`MTOM`数据成员来填充`BLOB`对象。

1. 确定加密类型。

   * 调用`EncryptionServiceClient`对象的`getPDFEncryption`方法并传递包含PDF文档的`BLOB`对象。 此方法返回`EncryptionTypeResult`对象。
   * 获取`EncryptionTypeResult`对象的`encryptionType`数据方法的值。 例如，如果PDF文档受基于密码的加密保护，则此数据成员的值为`EncryptionType.PASSWORD`。

**另请参阅**

[步骤摘要](encrypting-decrypting-pdf-documents.md#summary-of-steps)

[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[使用SwaRef调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
