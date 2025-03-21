---
title: 在客户端渲染Forms
description: 通过使用Forms或Adobe Reader的客户端渲染功能，优化PDF内容的投放，并提高Acrobat服务处理网络负载的能力
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 0%

---

# 在客户端渲染Forms {#rendering-forms-at-the-client}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

## 在客户端渲染Forms {#rendering-forms-at-the-client-inner}

您可以优化PDF内容的投放，并通过使用Forms或Acrobat的客户端渲染功能来提高Adobe Reader服务处理网络负载的能力。 此过程称为在客户端渲染表单。 要在客户端呈现表单，客户端设备（通常为Web浏览器）必须使用Acrobat 7.0或Adobe Reader 7.0或更高版本。

除非根子表单包含设置为`auto`的`restoreState`属性，否则由服务器端脚本执行产生的对表单的更改不会反映在客户端渲染的表单中。 有关此属性的更多信息，请参阅[Forms Designer。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

### 步骤摘要 {#summary-of-steps}

要在客户端呈现表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置客户端渲染运行时选项。
1. 在客户端渲染表单。
1. 将表单写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。 如果您使用的是Java API，请创建一个`FormsServiceClient`对象。 如果您使用的是Forms Web服务API，请创建一个`FormsService`对象。

**设置客户端渲染运行时选项**

通过将`RenderAtClient`运行时选项设置为`true`，将客户端渲染运行时选项设置为在客户端渲染表单。 这会导致表单被传送到呈现该表单的客户端设备。 如果`RenderAtClient`为`auto`（默认值），则窗体设计将确定是否在客户端呈现窗体。 窗体设计必须是具有可流动布局的窗体设计。

您可以设置的可选运行时选项是`SeedPDF`选项。 `SeedPDF`选项将PDF容器(种子PDF文档)与表单设计和XML数据相结合。 表单设计和XML数据都会交付到Acrobat或Adobe Reader，表单会在该位置渲染。 当客户端计算机没有表单中使用的字体时，例如，当最终用户未获得使用表单所有者已获得许可使用的字体的许可时，可以使用`SeedPDF`选项。

您可以使用Designer创建一个简单的动态PDF文件用作种子PDF文件。 要执行此任务，需要执行以下步骤：

1. 确定是否需要在种子PDF文件中嵌入任何字体。 种子PDF文件必须包含渲染的表单所需的其他字体。 将字体嵌入种子PDF文件时，请确保不违反任何字体许可协议。 在Designer中，您可以确定是否可合法嵌入字体。 保存后，如果存在无法嵌入表单中的字体，Designer会显示一条消息，列出无法嵌入的字体。 对于静态PDF文档，此消息不会显示在Designer中。
1. 如果要在Designer中创建种子PDF文件，建议至少添加包含消息的文本字段。 该消息应发送给早期版本的Adobe Reader用户，声明他们需要Acrobat 7.0或更高版本或者Adobe Reader 7.0或更高版本才能查看文档。
1. 将种子PDF文件另存为具有PDF文件扩展名的动态PDF文件。

>[!NOTE]
>
>在客户端上渲染表单不需要定义种子PDF运行时选项。 如果您未指定种子PDF，Forms服务将创建一个shell pdf，其中将不包含COS对象，但将包含嵌入了实际XDPPDF的内容包装器。 本节中的步骤不设置种子PDF运行时选项。 有关COS对象的信息，请参阅《Adobe PDF参考指南》。

**在客户端渲染表单**

要在客户端渲染表单，您必须确保渲染表单的应用程序逻辑中包含客户端渲染运行时选项。

**将表单数据流写入客户端Web浏览器**

Forms服务会创建一个您必须写入客户端Web浏览器的表单数据流。 在写入客户端Web浏览器时，表单将由Acrobat 7.0或Adobe Reader 7.0或更高版本渲染，并且对用户可见。

**另请参阅**

[使用Java API在客户端渲染表单](#render-a-form-at-the-client-using-the-java-api)

[使用Web服务API在客户端渲染表单](#render-a-form-at-the-client-using-the-web-service-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[将文档传递到Forms服务](/help/forms/developing/passing-documents-forms-service.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API在客户端渲染表单 {#render-a-form-at-the-client-using-the-java-api}

使用Forms API (Java)在客户端渲染表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。

1. 设置客户端渲染运行时选项

   * 使用构造函数创建`PDFFormRenderSpec`对象。
   * 通过调用`PDFFormRenderSpec`对象的`setRenderAtClient`方法并传递枚举值`RenderAtClient.Yes`来设置`RenderAtClient`运行时选项。

1. 在客户端渲染表单

   调用`FormsServiceClient`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是AEM Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含要与表单合并的数据的`com.adobe.idp.Document`对象。 如果不想合并数据，请传递一个空的`com.adobe.idp.Document`对象。
   * `PDFFormRenderSpec`对象，用于存储客户端上呈现表单所需的运行时选项。
   * 包含Forms服务渲染表单所需的URI值的`URLSpec`对象。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。

   `renderPDFForm`方法返回的`FormsResult`对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用其`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建字节数组并使用表单数据流填充该数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[快速入门(SOAP模式)：使用Java API在客户端渲染表单](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API在客户端渲染表单 {#render-a-form-at-the-client-using-the-web-service-api}

使用Forms API（Web服务）在客户端渲染表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含在类路径中。

1. 创建Forms客户端API对象

   创建`FormsService`对象并设置身份验证值。

1. 设置客户端渲染运行时选项

   * 使用构造函数创建`PDFFormRenderSpec`对象。
   * 通过调用`PDFFormRenderSpec`对象的`setRenderAtClient`方法并传递字符串值`RenderAtClient.Yes`来设置`RenderAtClient`运行时选项。

1. 在客户端渲染表单

   调用`FormsService`对象的`renderPDFForm`方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 包含要与表单合并的数据的`BLOB`对象。 如果不想合并数据，请传递`null`。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * `PDFFormRenderSpec`对象，用于存储客户端上呈现表单所需的运行时选项。
   * 包含Forms服务所需URI值的`URLSpec`对象。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。
   * 方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数用于存储渲染的PDF表单。
   * 方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 （此参数将存储表单中的页数）。
   * 方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 （此参数将存储区域设置值）。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `renderPDFForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用其`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`BLOB`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[在客户端渲染Forms](#rendering-forms-at-the-client)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
