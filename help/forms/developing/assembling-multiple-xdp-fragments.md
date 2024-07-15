---
title: 组装多个XDP片段
description: 使用Java API和Web服务API将多个XDP片段组合为单个XDP文档。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# 组装多个XDP片段{#assembling-multiple-xdp-fragments}

您可以将多个XDP片段组合到单个XDP文档中。 例如，考虑XDP片段，其中每个XDP文件都包含一个或多个用于创建健康表单的子表单。 下图显示了大纲视图（表示在&#x200B;*汇编多个XDP片段*&#x200B;快速入门中使用的tuc018_template_flowed.xdp文件）：

![am_am_forma](assets/am_am_forma.png)

下图显示了患者部分（表示在&#x200B;*汇编多个XDP片段*&#x200B;快速入门中使用的tuc018_contact.xdp文件）：

![am_am_formb](assets/am_am_formb.png)

下图显示了患者健康部分（表示在&#x200B;*汇编多个XDP片段*&#x200B;快速入门中使用的tuc018_patient.xdp文件）：

![am_am_formc](assets/am_am_formc.png)

此片段包含两个名为&#x200B;*subPatientPhysical*&#x200B;和&#x200B;*subPatientHealth*&#x200B;的子表单。 这两个子表单在传递给Assembler服务的DDX文档中引用。 使用Assembler服务，您可以将所有这些XDP片段组合到单个XDP文档中，如下图所示。

![am_am_formd](assets/am_am_formd.png)

以下DDX文档将多个XDP片段组合到一个XDP文档中。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDX文档包含指定结果名称的XDP `result`标记。 在这种情况下，值为`tuc018result.xdp`。 在Assembler服务返回结果后，在用于检索XDP文档的应用程序逻辑中引用此值。 例如，考虑用于检索已装配XDP文档的以下Java应用程序逻辑（请注意该值为粗体）：

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

`XDP source`标记指定表示完整XDP文档的XDP文件，该文件可用作添加XDP片段的容器，或作为按顺序追加在一起的多个文档之一。 在这种情况下，XDP文档仅用作容器（*组合多个XDP片段*&#x200B;中显示的第一个插图）。 也就是说，其他XDP文件被放置在XDP容器中。

对于每个子表单，您可以添加`XDPContent`元素（此元素是可选的）。 在上例中，请注意有三个子表单： `subPatientContact`、`subPatientPhysical`和`subPatientHealth`。 `subPatientPhysical`子表单和`subPatientHealth`子表单都在相同的XDP文件tuc018_patient.xdp中。 片段元素指定子表单的名称，如Designer中所定义。

>[!NOTE]
>
>有关Assembler服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>有关DDX文档的更多信息，请参阅[汇编程序服务和DDX引用](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 步骤摘要 {#summary-of-steps}

要组合多个XDP片段，请执行以下任务：

1. 包括项目文件。
1. 创建PDF汇编程序客户端。
1. 引用现有DDX文档。
1. 参考XDP文档。
1. 设置运行时选项。
1. 组合多个XDP文档。
1. 检索装配的XDP文档。

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

要组合多个XDP文档，必须引用DDX文档。 此DDX文档必须包含`XDP result`、`XDP source`和`XDPContent`元素。

**引用XDP文档**

要组合多个XDP文档，请引用用于组合结果XDP文档的所有XDP文件。 确保在`fragment`属性中指定了`source`属性引用的XDP文档中包含的子表单的名称。 在Designer中定义子表单。 例如，请考虑以下XML。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

名为&#x200B;*subPatientContact*&#x200B;的子表单必须位于名为&#x200B;*tuc018_contact.xdp*&#x200B;的XDP文件中。

**设置运行时选项**

您可以设置运行时选项，以控制Assembler服务执行作业时的行为。 例如，您可以设置一个选项，在遇到错误时指示Assembler服务继续处理作业。

**汇编多个XDP文档**

要组合多个XDP文件，请调用`invokeDDX`操作。 Assembler服务返回集合对象中的已装配XDP文档。

**检索已装配的XDP文档**

在收集对象中返回已装配的XDP文档。 循环访问收集对象并将XDP文档另存为XDP文件。 您还可以将XDP文档传递到另一个AEM Forms服务，例如输出。

**另请参阅**

[使用Java API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[使用Web服务API组合多个XDP片段](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[以编程方式组合PDF文档](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[使用片段创建PDF文档](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## 使用Java API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-java-api}

使用Assembler服务API (Java)汇编多个XDP片段：

1. 包括项目文件。

   在您的Java项目的类路径中包含客户端JAR文件，例如adobe-assembler-client.jar。

1. 创建PDF汇编程序客户端。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`AssemblerServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用现有DDX文档。

   * 通过使用其构造函数并传递指定DDX文件位置的字符串值，创建表示DDX文档的`java.io.FileInputStream`对象。
   * 使用对象的构造函数创建`com.adobe.idp.Document`对象并传递`java.io.FileInputStream`对象。

1. 参考XDP文档。

   * 使用`HashMap`构造函数创建用于存储输入XDP文档的`java.util.Map`对象。
   * 创建一个`com.adobe.idp.Document`对象并传递包含输入XDP文件的`java.io.FileInputStream`对象（对每个XDP文件重复此任务）。
   * 通过调用其`put`方法并传递以下参数，向`java.util.Map`对象添加一个条目：

      * 表示键名的字符串值。 此值必须与DDX文档中指定的`source`元素值匹配（对每个XDP文件重复此任务）。
      * 包含与`source`元素对应的XDP文档的`com.adobe.idp.Document`对象（对每个XDP文件重复此任务）。

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过调用属于`AssemblerOptionSpec`对象的方法，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请调用`AssemblerOptionSpec`对象的`setFailOnError`方法并传递`false`。

1. 组合多个XDP文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下必需值：

   * 表示要使用的DDX文档的`com.adobe.idp.Document`对象
   * 包含输入XDP文件的`java.util.Map`对象
   * 指定运行时选项（包括默认字体和作业日志级别）的`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`对象

   `invokeDDX`方法返回包含已装配XDP文档的`com.adobe.livecycle.assembler.client.AssemblerResult`对象。

1. 检索装配的XDP文档。

   要获取装配的XDP文档，请执行以下步骤：

   * 调用`AssemblerResult`对象的`getDocuments`方法。 此方法返回`java.util.Map`对象。
   * 反复查找`java.util.Map`对象，直到找到结果`com.adobe.idp.Document`对象。
   * 调用`com.adobe.idp.Document`对象的`copyToFile`方法以提取装配的XDP文档。

**另请参阅**

[组合多个XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[快速入门(SOAP模式)：使用Java API汇编多个XDP片段](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[正在设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API组合多个XDP片段 {#assemble-multiple-xdp-fragments-using-the-web-service-api}

使用Assembler服务API（Web服务）组合多个XDP片段：

1. 包括项目文件。

   创建使用MTOM的Microsoft .NET项目。 在设置服务引用时，请确保使用以下WSDL定义：

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >将`localhost`替换为承载AEM Forms的服务器的IP地址。

1. 创建PDF汇编程序客户端。

   * 使用默认构造函数创建`AssemblerServiceClient`对象。
   * 使用`System.ServiceModel.EndpointAddress`构造函数创建`AssemblerServiceClient.Endpoint.Address`对象。 将指定WSDL的字符串值传递给AEM Forms服务，如`https://localhost:8080/soap/services/AssemblerService?blob=mtom`。 您无需使用`lc_version`属性。 此属性在创建服务引用时使用。
   * 通过获取`AssemblerServiceClient.Endpoint.Binding`字段的值创建一个`System.ServiceModel.BasicHttpBinding`对象。 将返回值强制转换为`BasicHttpBinding`。
   * 将`System.ServiceModel.BasicHttpBinding`对象的`MessageEncoding`字段设置为`WSMessageEncoding.Mtom`。 此值可确保使用MTOM。
   * 通过执行以下任务启用基本HTTP身份验证：

      * 将AEM表单用户名分配给`AssemblerServiceClient.ClientCredentials.UserName.UserName`字段。
      * 将相应的密码值分配给`AssemblerServiceClient.ClientCredentials.UserName.Password`字段。
      * 将`HttpClientCredentialType.Basic`常量值分配给`BasicHttpBindingSecurity.Transport.ClientCredentialType`字段。
      * 将`BasicHttpSecurityMode.TransportCredentialOnly`常量值分配给`BasicHttpBindingSecurity.Security.Mode`字段。

1. 引用现有DDX文档。

   * 使用构造函数创建`BLOB`对象。 `BLOB`对象用于存储DDX文档。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示DDX文档的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和流长度以读取。
   * 使用字节数组的内容指定其`MTOM`属性以填充`BLOB`对象。

1. 参考XDP文档。

   * 对于每个输入XDP文件，使用其构造函数创建一个`BLOB`对象。 `BLOB`对象用于存储输入文件。
   * 通过调用其构造函数并传递一个字符串值来创建一个`System.IO.FileStream`对象，该字符串值表示输入文件的文件位置以及打开文件的模式。
   * 创建用于存储`System.IO.FileStream`对象的内容的字节数组。 您可以通过获取`System.IO.FileStream`对象的`Length`属性来确定字节数组的大小。
   * 通过调用`System.IO.FileStream`对象的`Read`方法，使用流数据填充字节数组。 传递字节数组、起始位置和流长度以读取。
   * 使用字节数组的内容分配其`MTOM`字段以填充`BLOB`对象。
   * 创建`MyMapOf_xsd_string_To_xsd_anyType`对象。 此集合对象用于存储创建组合的XDP文档所需的输入文件。
   * 对于每个输入文件，创建一个`MyMapOf_xsd_string_To_xsd_anyType_Item`对象。
   * 将表示键名的字符串值分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`key`字段。 此值必须匹配DDX文档中指定元素的值。 （为每个输入XDP文件执行此任务。）
   * 将存储输入文件的`BLOB`对象分配给`MyMapOf_xsd_string_To_xsd_anyType_Item`对象的`value`字段。 （为每个输入XDP文件执行此任务。）
   * 将`MyMapOf_xsd_string_To_xsd_anyType_Item`对象添加到`MyMapOf_xsd_string_To_xsd_anyType`对象。 调用`MyMapOf_xsd_string_To_xsd_anyType`对象的`Add`方法并传递`MyMapOf_xsd_string_To_xsd_anyType`对象。 （为每个输入XDP文档执行此任务。）

1. 设置运行时选项。

   * 使用构造函数创建存储运行时选项的`AssemblerOptionSpec`对象。
   * 通过为属于`AssemblerOptionSpec`对象的数据成员分配值，设置运行时选项以满足您的业务要求。 例如，要指示Assembler服务在发生错误时继续处理作业，请将`false`分配给`AssemblerOptionSpec`对象的`failOnError`数据成员。

1. 组合多个XDP文档。

   调用`AssemblerServiceClient`对象的`invokeDDX`方法并传递以下值：

   * 表示DDX文档的`BLOB`对象
   * 包含所需文件的`MyMapOf_xsd_string_To_xsd_anyType`对象
   * 指定运行时选项的`AssemblerOptionSpec`对象

   `invokeDDX`方法返回包含作业结果和发生的任何异常的`AssemblerResult`对象。

1. 检索装配的XDP文档。

   要获取新创建的XDP文档，请执行以下步骤：

   * 访问`AssemblerResult`对象的`documents`字段，该字段是包含生成PDF文档的`Map`对象。
   * 对`Map`对象进行迭代以获取每个结果文档。 然后，将该数组成员的`value`强制转换为`BLOB`。
   * 通过访问其`BLOB`对象的`MTOM`属性，提取表示PDF文档的二进制数据。 这会返回一个字节数组，您可以将其写出到XDP文件。

**另请参阅**

[组合多个XDP片段](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[使用MTOM调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
