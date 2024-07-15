---
title: 使用自定义CSS文件渲染HTMLForms
description: 使用Forms服务引用自定义CSS文件来呈现HTML表单，以响应来自Web浏览器的HTTP请求。 您可以使用Java API和Web服务API呈现使用CSS文件的HTML表单。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 5fa385a7-f030-4c0c-8938-0991d02ef361
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 0%

---

# 使用自定义CSS文件渲染HTMLForms {#rendering-html-forms-using-custom-css-files}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

Forms服务会呈现HTML表单，以响应来自Web浏览器的HTTP请求。 呈现HTML表单时，Forms服务可以引用自定义CSS文件。 您可以创建一个自定义CSS文件以满足您的业务要求，并在使用Forms服务渲染HTML表单时引用该CSS文件。

Forms服务可静默解析自定义CSS文件。 也就是说，Forms服务不会报告在自定义CSS文件不符合CSS标准时可能遇到的错误。 在这种情况下，Forms服务会忽略样式，继续处理CSS文件中的其余样式。

以下列表指定了自定义CSS文件中支持的样式：

* **类级别选择器样式对**：如果存在于自定义CSS文件中，则使用在HTML表单中用作类样式的选择器。 未使用的类样式将被忽略。
* **标识符级别选择器样式对**：如果在HTML表单中使用所有标识符样式，则使用这些样式。
* **元素级别选择器样式对**：所有元素样式在HTML表单中都使用。
* **样式优先级**：支持样式优先级（如重要），可在自定义CSS文件中使用。
* **媒体类型**：一个或多个选择器样式对可以封装在@media样式中以定义媒体类型。 Forms服务不检查指定的媒体类型是否受支持。 自定义CSS文件中指定的媒体类型将合并到HTML表单中。

您可以使用FormsIVS应用程序检索示例CSS文件。 上传表单，在“测试表单设计”页面中选择它，然后单击“生成CSS”。 在单击该按钮之前，您不需要设置HTML转换类型。 接下来，选择“保存”。 您可以编辑此CSS文件以满足您的业务要求。

>[!NOTE]
>
>在呈现使用自定义CSS文件的HTML表单之前，请务必充分了解如何呈现HTML表单。 (请参阅[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)。)

>[!NOTE]
>
>有关Forms服务的详细信息，请参阅[AEM Forms的服务参考](https://www.adobe.com/go/learn_aemforms_services_63)。

## 步骤摘要 {#summary-of-steps}

要呈现使用CSS文件的HTML表单，请执行以下任务：

1. 包括项目文件。
1. 创建Forms Java API对象。
1. 引用CSS文件。
1. 呈现HTML表单。
1. 将表单数据流写入客户端Web浏览器。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

**创建Forms Java API对象**

您必须先创建Forms客户端对象，然后才能以编程方式执行Forms服务支持的操作。

**引用CSS文件**

要呈现使用自定义CSS文件的HTML表单，请确保引用现有的CSS文件。

**呈现HTML表单**

要呈现HTML表单，请指定在Designer中创建并另存为XDP文件的表单设计。 选择HTML转换类型。 例如，您可以指定用于呈现Internet Explorer 5.0或更高版本的动态HTML的HTML转换类型。

呈现HTML表单还需要值，例如呈现其他表单类型所需的URI值。

**将表单数据流写入客户端Web浏览器**

当Forms服务渲染HTML表单时，它会返回一个表单数据流，您必须将该数据流写入客户端Web浏览器，才能使用户看到HTML表单。

**另请参阅**

[渲染使用CSS文件的HTML表单（使用Java API）](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms服务API快速启动](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[呈现交互式PDF forms](/help/forms/developing/rendering-interactive-pdf-forms.md)

[将Forms渲染为HTML](/help/forms/developing/rendering-forms-html.md)

[创建可渲染Forms的Web应用程序](/help/forms/developing/creating-web-applications-renders-forms.md)

## 渲染使用CSS文件的HTML表单（使用Java API） {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

使用Forms API (Java)呈现使用自定义CSS文件的HTML表单：

1. 包含项目文件

   在Java项目的类路径中包含客户端JAR文件，例如adobe-forms-client.jar。

1. 创建Forms Java API对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`FormsServiceClient`对象并传递`ServiceClientFactory`对象。

1. 引用CSS文件

   * 使用构造函数创建`HTMLRenderSpec`对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用`HTMLRenderSpec`对象的`setCustomCSSURI`方法，并传递一个指定CSS文件位置和名称的字符串值。

1. 呈现HTML表单

   调用`FormsServiceClient`对象的`(Deprecated) (Deprecated) renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首选项类型的`TransformTo`枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * 包含要与表单合并的数据的`com.adobe.idp.Document`对象。 如果不想合并数据，请传递一个空的`com.adobe.idp.Document`对象。
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`标头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。

   `(Deprecated) renderHTMLForm`方法返回的`FormsResult`对象包含必须写入客户端Web浏览器的表单数据流。

1. 将表单数据流写入客户端Web浏览器

   * 通过调用`FormsResult`对象的`getOutputContent`方法创建`com.adobe.idp.Document`对象。
   * 通过调用其`getContentType`方法获取`com.adobe.idp.Document`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`com.adobe.idp.Document`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.h\ttp.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 通过调用`com.adobe.idp.Document`对象的`getInputStream`方法创建`java.io.InputStream`对象。
   * 通过调用`InputStream`对象的`read`方法并将字节数组作为参数传递，创建字节数组并使用表单数据流填充该数组。
   * 调用`javax.servlet.ServletOutputStream`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[快速入门(SOAP模式)：渲染使用CSS文件的HTML表单（使用Java API）](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 渲染使用CSS文件的HTML表单（使用Web服务API） {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

使用Forms API（Web服务）呈现使用自定义CSS文件的HTML表单：

1. 包含项目文件

   * 创建使用Forms服务WSDL的Java代理类。
   * 在类路径中包含Java代理类。

1. 创建Forms Java API对象

   创建`FormsService`对象并设置身份验证值。

1. 引用CSS文件

   * 使用构造函数创建`HTMLRenderSpec`对象。
   * 要呈现使用自定义CSS文件的HTML表单，请调用`HTMLRenderSpec`对象的`setCustomCSSURI`方法，并传递一个指定CSS文件位置和名称的字符串值。

1. 呈现HTML表单

   调用`FormsService`对象的`(Deprecated) renderHTMLForm`方法并传递以下值：

   * 一个字符串值，它指定窗体设计名称，包括文件扩展名。 如果您引用的表单设计是Forms应用程序的一部分，请确保指定完整路径，如`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * 指定HTML首选项类型的`TransformTo`枚举值。 例如，要渲染与Internet Explorer 5.0或更高版本的动态HTML兼容的HTML表单，请指定`TransformTo.MSDHTML`。
   * 包含要与表单合并的数据的`BLOB`对象。 如果不想合并数据，请传递`null`。 (请参阅[使用可流动布局预填充Forms](/help/forms/developing/prepopulating-forms-flowable-layouts.md)。)
   * 存储HTML运行时选项的`HTMLRenderSpec`对象。
   * 指定`HTTP_USER_AGENT`标头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 如果您不想设置此值，则可以传递空字符串。
   * 一个`URLSpec`对象，用于存储呈现HTML表单所需的URI值。
   * 存储文件附件的`java.util.HashMap`对象。 这是一个可选参数，如果您不想将文件附加到表单，则可以指定`null`。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数值存储渲染的表单。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`com.adobe.idp.services.holders.BLOBHolder`对象。 此参数存储输出XML数据。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.LongHolder`对象。 此参数存储表单中的页数。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数存储区域设置值。
   * 由`(Deprecated) renderHTMLForm`方法填充的空`javax.xml.rpc.holders.StringHolder`对象。 此参数用于存储使用的HTML渲染值。
   * 将包含此操作结果的空`com.adobe.idp.services.holders.FormsResultHolder`对象。

   `(Deprecated) renderHTMLForm`方法使用必须写入客户端Web浏览器的表单数据流填充作为最后一个参数值传递的`com.adobe.idp.services.holders.FormsResultHolder`对象。

1. 将表单数据流写入客户端Web浏览器

   * 通过获取`com.adobe.idp.services.holders.FormsResultHolder`对象的`value`数据成员的值创建`FormResult`对象。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建包含表单数据的`BLOB`对象。
   * 通过调用其`getContentType`方法获取`BLOB`对象的内容类型。
   * 通过调用其`setContentType`方法并传递`BLOB`对象的内容类型来设置`javax.servlet.http.HttpServletResponse`对象的内容类型。
   * 通过调用`javax.servlet.http.HttpServletResponse`对象的`getOutputStream`方法，创建用于将表单数据流写入客户端Web浏览器的`javax.servlet.ServletOutputStream`对象。
   * 创建字节数组，并通过调用`BLOB`对象的`getBinaryData`方法填充该数组。 此任务将`FormsResult`对象的内容分配给字节数组。
   * 调用`javax.servlet.http.HttpServletResponse`对象的`write`方法将表单数据流发送到客户端Web浏览器。 将字节数组传递给`write`方法。

**另请参阅**

[使用自定义CSS文件渲染HTMLForms](#rendering-html-forms-using-custom-css-files)

[使用Base64编码调用AEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
