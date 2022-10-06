---
title: 优化Forms服务的性能
seo-title: Optimizing the Performance of theForms Service
description: 在渲染表单时设置运行时选项，并将XDP文件存储在存储库中，以优化Forms服务的性能。
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# 优化Forms服务的性能 {#optimizing-the-performance-of-theforms-service}

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

## 优化Forms服务的性能 {#optimizing-the-performance-of-the-forms-service}

在渲染表单时，您可以设置运行时选项，以优化Forms服务的性能。 您可以执行的另一个任务是将XDP文件存储在存储库中，以提高Forms服务的性能。 但是，本节并未说明如何执行此任务。 (请参阅 [使用Java客户端库调用服务](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>有关Forms服务的更多信息，请参阅 [AEM Forms服务参考](https://www.adobe.com/go/learn_aemforms_services_63).

### 步骤摘要 {#summary-of-steps}

要在渲染表单时优化Forms服务的性能，请执行以下任务：

1. 包括项目文件。
1. 创建Forms客户端API对象。
1. 设置性能运行时选项。
1. 渲染表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms客户端API对象**

您必须先创建Forms服务客户端，然后才能以编程方式执行Forms服务客户端API操作。 如果您使用的是Java API，请创建 `FormsServiceClient` 对象。 如果您使用的是Forms Web服务API，请创建 `FormsService` 对象。

**设置性能运行时选项**

您可以设置以下性能运行时选项以提高Forms服务的性能：

* **表单缓存**:您可以在服务器缓存中缓存呈现为PDF的表单。 每个表单在首次生成后都会缓存。 在后续渲染时，如果缓存的表单比表单设计的时间戳新，则会从缓存中检索表单。 通过缓存表单，可以提高Forms服务的性能，因为它不必从存储库检索表单设计。
* 表单指南（已弃用）的呈现时间可能比其他转换类型要长。 建议您缓存表单指南（已弃用）以提高性能。
* **独立选项**:如果您不需要Forms服务来执行服务器端计算，则可以将“独立”选项设置为 `true`，这会导致表单在渲染时没有状态信息。 如果要向最终用户呈现交互式表单，然后最终用户将信息输入到表单中并将表单提交回Forms服务，则需要提供状态信息。 然后，Forms服务执行计算操作，并将表单呈现回用户，结果显示在表单中。 如果将没有状态信息的表单提交回Forms服务，则只有XML数据可用，且不执行服务器端计算。
* **线性化PDF**:组织线性化PDF文件以在网络环境中实现有效的增量访问。 PDF文件在所有方面都是有效的PDF，并且与所有现有查看器和其他PDF应用程序兼容。 即，在下载时可以查看线性化PDF。
* 当客户端上呈现PDF表单时，此选项不会提高性能。
* **GuideRSL选项**:启用使用运行时共享库生成表单指南（已弃用）。 这意味着第一个请求将下载较小的SWF文件，以及存储在浏览器缓存中的较大共享库。 有关更多信息，请参阅Flex文档中的RSL 。
* 您还可以通过在客户端上渲染表单来提高Forms服务的性能。 (请参阅 [在客户端渲染Forms](/help/forms/developing/rendering-forms-client.md).)

**渲染表单**

要在设置性能选项后渲染表单，请使用与渲染不带性能选项的表单相同的应用程序逻辑。

**将表单数据流写入客户端Web浏览器**

在Forms服务呈现表单后，它将返回一个必须写入客户端Web浏览器的表单数据流。 写入客户端Web浏览器时，用户可以看到该表单。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

### 使用Java API优化性能 {#optimize-the-performance-using-the-java-api}

使用Forms API(Java)渲染性能优化的表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，如adobe-forms-client.jar。

1. 创建Forms客户端API对象

   * 创建 `ServiceClientFactory` 包含连接属性的对象。
   * 创建 `FormsServiceClient` 对象，并使用其构造函数进行传递 `ServiceClientFactory` 对象。

1. 设置性能运行时选项

   * 创建 `PDFFormRenderSpec` 对象。
   * 通过调用 `PDFFormRenderSpec` 对象 `setCacheEnabled` 方法和传递 `true`.
   * 通过调用 `PDFFormRenderSpec` 对象 `setLinearizedPDF` 方法和传递 `true.`

1. 渲染表单

   调用 `FormsServiceClient` 对象 `renderPDFForm` 方法并传递以下值：

   * 指定表单设计名称（包括文件扩展名）的字符串值。
   * A `com.adobe.idp.Document` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递一个空 `com.adobe.idp.Document` 对象。
   * A `PDFFormRenderSpec` 用于存储运行时选项以提高性能的对象。
   * A `URLSpec` 包含Forms服务所需URI值的对象。
   * A `java.util.HashMap` 用于存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。

   的 `renderPDFForm` 方法返回 `FormsResult` 包含必须写入客户端web浏览器的表单数据流的对象。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `javax.servlet.ServletOutputStream` 用于将表单数据流发送到客户端web浏览器的对象。
   * 创建 `com.adobe.idp.Document` 对象 `FormsResult` 对象s `getOutputContent` 方法。
   * 创建 `java.io.InputStream` 对象 `com.adobe.idp.Document` 对象 `getInputStream` 方法。
   * 通过调用 `InputStream` 对象 `read`方法并将字节数组作为参数进行传递。
   * 调用 `javax.servlet.ServletOutputStream` 对象 `write` 将表单数据流发送到客户端web浏览器的方法。 将字节数组传递到 `write` 方法。

**另请参阅**

[快速入门（SOAP模式）：使用Java API优化性能](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Web服务API优化性能 {#optimize-the-performance-using-the-web-service-api}

使用Forms API（Web服务）渲染性能优化的表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 将Java代理类包含到类路径中。

1. 创建Forms客户端API对象

   创建 `FormsService` 对象，并设置身份验证值。

1. 设置性能运行时选项

   * 创建 `PDFFormRenderSpec` 对象。
   * 通过调用 `PDFFormRenderSpec` 对象 `setCacheEnabled` 方法和传递true。
   * 通过调用 `PDFFormRenderSpec` 对象 `setStandAlone` 方法和传递true。
   * 通过调用 `PDFFormRenderSpec` 对象 `setLinearizedPDF` 方法和传递true。

1. 渲染表单

   调用 `FormsService` 对象 `renderPDFForm` 方法并传递以下值：

   * 指定表单设计名称（包括文件扩展名）的字符串值。
   * A `BLOB` 包含要与表单合并的数据的对象。 如果不想合并数据，请传递 `null`.
   * A `PDFFormRenderSpecc` 用于存储运行时选项的对象。
   * A `URLSpec` 包含Forms服务所需URI值的对象。
   * A `java.util.HashMap` 用于存储文件附件的对象。 这是一个可选参数，您可以指定 `null` 如果您不想将文件附加到表单。
   * 空 `com.adobe.idp.services.holders.BLOBHolder` 由方法填充的对象。 用于存储呈现的PDF表单。
   * 空 `javax.xml.rpc.holders.LongHolder` 由方法填充的对象。 （此参数将以表单存储页数）。
   * 空 `javax.xml.rpc.holders.StringHolder` 由方法填充的对象。 （此参数将存储区域设置值）。
   * 空 `com.adobe.idp.services.holders.FormsResultHolder` 包含此操作结果的对象。

   的 `renderPDFForm` 方法填充 `com.adobe.idp.services.holders.FormsResultHolder` 作为最后一个参数值传递的对象，表单数据流必须写入客户端web浏览器。

1. 将表单数据流写入客户端Web浏览器

   * 创建 `FormResult` 对象，方法是获取 `com.adobe.idp.services.holders.FormsResultHolder` 对象 `value` 数据成员。
   * 创建 `javax.servlet.ServletOutputStream` 用于将表单数据流发送到客户端web浏览器的对象。
   * 创建 `BLOB` 通过调用包含表单数据的对象 `FormsResult` 对象 `getOutputContent` 方法。
   * 创建一个字节数组，并通过调用 `BLOB` 对象 `getBinaryData` 方法。 此任务分配 `FormsResult` 对象。
   * 调用 `javax.servlet.http.HttpServletResponse` 对象 `write` 将表单数据流发送到客户端web浏览器的方法。 将字节数组传递到 `write` 方法。

**另请参阅**

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
