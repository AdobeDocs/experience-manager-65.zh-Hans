---
title: 按值呈现Forms
seo-title: 按值呈现Forms
description: 使用Forms API(Java)通过Java API和Web服务API来按值呈现表单。
seo-description: 使用Forms API(Java)通过Java API和Web服务API来按值呈现表单。
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---

# 按值{#rendering-forms-by-value}呈现Forms

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

通常，在Designer中创建的表单设计会通过引用Forms服务来传递。 表单设计可能较大，因此，通过引用传递它们更为有效，从而避免必须按值封送表单设计字节。 Forms服务还可以缓存表单设计，以便在缓存时，不必持续读取表单设计。

如果表单设计包含UUID属性，则会缓存该属性。 对于所有表单设计，UUID值都是唯一的，可用于唯一标识表单。 按值呈现表单时，只有在表单重复使用时才应缓存该表单。 但是，如果表单没有重复使用且必须是唯一的，则可以避免使用使用使用AEM Forms API设置的缓存选项来缓存表单。

Forms服务还可以解析表单设计中链接内容的位置。 例如，从表单设计中引用的链接图像是相对URL。 链接的内容始终被假定为相对于表单设计位置。 因此，解析链接内容是通过将相对路径应用到绝对表单设计位置来确定其位置的问题。

您可以按值传递表单设计，而不是按引用传递表单设计。 在动态创建表单设计时，按值传递表单设计非常有效；也就是说，当客户端应用程序在运行时生成创建表单设计的XML时。 在这种情况下，表单设计不会存储在物理存储库中，因为它存储在内存中。 在运行时动态创建表单设计并按值传递该设计时，您可以缓存该表单并提高Forms服务的性能。

**按值传递表单的限制**

按值传递表单设计时，将受到以下限制：

* 表单设计中不能包含任何相对链接的内容。 所有图像和片段必须嵌入到表单设计中，或绝对引用。
* 表单呈现后，无法执行服务器端计算。 如果表单已提交回Forms服务，则无需任何服务器端计算，即可提取并返回数据。
* 由于HTML在运行时只能使用链接的图像，因此无法生成包含嵌入图像的HTML。 这是因为Forms服务通过从引用的表单设计中检索图像来支持带有HTML的嵌入图像。 由于按值传递的表单设计没有引用位置，因此在显示HTML页面时无法提取嵌入的图像。 因此，图像引用必须是要以HTML呈现的绝对路径。

>[!NOTE]
>
>尽管您可以按值呈现不同类型的表单（例如，包含使用权限的HTML表单或表单），但本节将讨论渲染交互式PDF forms。

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤{#summary-of-steps}的摘要

要按值渲染表单，请执行以下步骤：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 引用表单设计。
1. 按值呈现表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

在以编程方式将数据导入PDF表单客户端API之前，您必须创建数据集成服务客户端。 在创建服务客户端时，您可以定义调用服务所需的连接设置。

**引用表单设计**

按值呈现表单时，必须创建一个`com.adobe.idp.Document`对象，其中包含要渲染的表单设计。 您可以引用现有的XDP文件，也可以在运行时动态创建表单设计，并使用该数据填充`com.adobe.idp.Document`。

>[!NOTE]
>
>此部分和相应的快速启动会引用现有的XDP文件。

**按值呈现表单**

要按值渲染表单，请将包含表单设计的`com.adobe.idp.Document`实例传递到渲染方法的`inDataDoc`参数（可以是`FormsServiceClient`对象的任何渲染方法，如`renderPDFForm`、`(Deprecated) renderHTMLForm`等）。 此参数值通常为与表单合并的数据保留。 同样，将空字符串值传递到`formQuery`参数。 通常，此参数需要一个字符串值来指定表单设计的名称。

>[!NOTE]
>
>如果要在表单中显示数据，必须在`xfa:datasets`元素中指定数据。 有关XFA架构的信息，请转到[https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**将表单数据流写入客户端Web浏览器**

当Forms服务按值呈现表单时，它会返回一个必须写入客户端Web浏览器的表单数据流。 写入客户端Web浏览器时，用户可以看到该表单。

**另请参阅**

[使用Java API按值呈现表单](#render-a-form-by-value-using-the-java-api)

[使用Web服务API按值呈现表单](#render-a-form-by-value-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 使用Java API {#render-a-form-by-value-using-the-java-api}按值呈现表单

使用Forms API(Java)按值呈现表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`FormsServiceClient`对象，并传递`ServiceClientFactory`对象。

1. 引用表单设计

   * 创建一个`java.io.FileInputStream`对象，该对象通过使用其构造函数并传递指定XDP文件位置的字符串值来表示要呈现的表单设计。
   * 使用其构造函数创建`com.adobe.idp.Document`对象，并传递`java.io.FileInputStream`对象。

1. 按值呈现表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个指定表单设计名称的字符串值。）
   * 包含表单设计的`com.adobe.idp.Document`对象。 通常，此参数值是为与表单合并的数据保留的。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是一个可选参数，如果不想指定运行时选项，可以指定`null`。
   * `URLSpec`对象，其中包含Forms服务所需的URI值。
   * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。

   `renderPDFForm`方法返回一个`FormsResult`对象，该对象包含可写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象“s `getOutputContent`”方法创建`com.adobe.idp.Document`对象。
   * 通过调用`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 创建字节数组并分配`InputStream`对象的大小。 调用`InputStream`对象的`available`方法以获取`InputStream`对象的大小。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数进行传递，使用表单数据流填充字节数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递到`write`方法。

**另请参阅**

[按值呈现Forms](/help/forms/developing/rendering-forms.md)

[快速入门（SOAP模式）：使用Java API按值呈现](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 使用Web服务API {#render-a-form-by-value-using-the-web-service-api}按值呈现表单

使用Forms API（Web服务）按值呈现表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 引用表单设计

   * 使用`java.io.FileInputStream`对象的构造函数创建对象。 传递指定XDP文件位置的字符串值。
   * 使用`BLOB`对象的构造函数创建对象。 `BLOB`对象用于存储使用密码加密的PDF文档。
   * 创建用于存储`java.io.FileInputStream`对象内容的字节数组。 您可以通过使用`available`方法获取`java.io.FileInputStream`对象的大小来确定字节数组的大小。
   * 通过调用`java.io.FileInputStream`对象的`read`方法并传递字节数组，用流数据填充字节数组。
   * 通过调用`setBinaryData`方法并传递字节数组来填充`BLOB`对象。

1. 按值呈现表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 空字符串值。 （通常，此参数需要一个指定表单设计名称的字符串值。）
   * 包含表单设计的`BLOB`对象。 通常，此参数值是为与表单合并的数据保留的。
   * 存储运行时选项的`PDFFormRenderSpec`对象。 这是一个可选参数，如果不想指定运行时选项，可以指定`null`。
   * `URLSpec`对象，其中包含Forms服务所需的URI值。
   * 用于存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，可以指定`null`。
   * 由方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 用于存储渲染的PDF表单。
   * 由方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数以表单形式存储页数。）
   * 由方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数存储区域设置值。）
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象`value`数据成员的值，创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用`setContentType`方法并传递`BLOB`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建一个`javax.servlet.ServletOutputStream`对象，用于将表单数据流写入客户端Web浏览器。
   * 创建一个字节数组，并通过调用`BLOB`对象的`getBinaryData`方法来填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法，将表单数据流发送到客户端Web浏览器。 将字节数组传递到`write`方法。

**另请参阅**

[按值呈现Forms](#rendering-forms-by-value)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
