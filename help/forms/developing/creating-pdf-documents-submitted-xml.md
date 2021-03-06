---
title: 使用SubmittedXML数据创建PDF文档
seo-title: 使用SubmittedXML数据创建PDF文档
description: 使用Forms服务检索用户在交互式表单中输入的表单数据。 将表单数据传递到另一个AEM Forms服务操作，然后使用该数据创建PDF文档。
seo-description: 使用Forms服务检索用户在交互式表单中输入的表单数据。 将表单数据传递到另一个AEM Forms服务操作，然后使用该数据创建PDF文档。
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# 使用已提交的XML数据{#creating-pdf-documents-with-submittedxml-data}创建PDF文档

**本文档中的示例和示例仅适用于JEE环境中的AEM Forms。**

## 使用已提交的XML数据{#creating-pdf-documents-with-submitted-xml-data}创建PDF文档

使用户能够填写交互式表单的基于Web的应用程序需要将数据提交回服务器。 使用Forms服务，您可以检索用户在交互式表单中输入的表单数据。 然后，您可以将表单数据传递到另一个AEM Forms服务操作，并使用该数据创建PDF文档。

>[!NOTE]
>
>在阅读此内容之前，建议您对处理提交的表单有更深入的了解。 表单设计与提交的XML数据之间的关系等概念在处理提交的Forms中进行了介绍。

请考虑以下涉及三项AEM Forms服务的工作流：

* 用户从基于Web的应用程序向Forms服务提交XML数据。
* Forms服务用于处理提交的表单和提取表单字段。 可以处理表单数据。 例如，数据可提交到企业数据库。
* 表单数据会发送到输出服务以创建非交互式PDF文档。
* 非交互式PDF文档存储在Content Services中（已弃用）。

下图提供了此工作流的可视化表示形式。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

用户从客户端Web浏览器提交表单后，非交互式PDF文档将存储在Content Services中（已弃用）。 下图显示了存储在Content Services中的PDF文档（已弃用）。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 步骤{#summary-of-steps}的摘要

要使用提交的XML数据创建非交互式PDF文档并将其存储在Content Services的PDF文档中（已弃用），请执行以下任务：

1. 包括项目文件。
1. 创建Forms、输出和文档管理对象。
1. 使用Forms服务检索表单数据。
1. 使用输出服务创建非交互式PDF文档。
1. 使用文档管理服务将PDF表单存储在内容服务中（已弃用）。

**包含项目文件**

在开发项目中包含必需的文件。 如果您使用Java创建客户端应用程序，请包含必需的JAR文件。 如果您使用的是Web服务，请确保包含代理文件。

**创建Forms、输出和文档管理对象**

在以编程方式执行Forms服务API操作之前，请先创建Forms客户端API对象。 同样，由于此工作流会调用输出和文档管理服务，因此请创建输出客户端API对象和文档管理客户端API对象。

**使用Forms服务检索表单数据**

检索已提交到Forms服务的表单数据。 您可以处理提交的数据以满足您的业务要求。 例如，您可以将表单数据存储在企业数据库中。 但是，要创建非交互式PDF文档，表单数据将传递到输出服务。

**使用输出服务创建非交互式PDF文档。**

使用输出服务创建基于表单设计和XML表单数据的非交互式PDF文档。 在工作流中，将从Forms服务中检索表单数据。

**使用文档管理服务在内容服务中存储PDF表单（已弃用）**

使用文档管理服务API在Content Services中存储PDF文档（已弃用）。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms Service API快速入门](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### 使用Java API {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}创建包含已提交XML数据的PDF文档

使用Forms、输出和文档管理API(Java)创建包含已提交XML数据的PDF文档：

1. 包含项目文件

   将客户端JAR文件（如adobe-forms-client.jar、adobe-output-client.jar和adobe-contentservices-client.jar）包含到您Java项目的类路径中。

1. 创建Forms、输出和文档管理对象

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用其构造函数创建`FormsServiceClient`对象，并传递`ServiceClientFactory`对象。
   * 使用其构造函数创建`OutputClient`对象，并传递`ServiceClientFactory`对象。
   * 使用其构造函数创建`DocumentManagementServiceClientImpl`对象，并传递`ServiceClientFactory`对象。

1. 使用Forms服务检索表单数据

   * 调用`FormsServiceClient`对象的`processFormSubmission`方法并传递以下值：

      * 包含表单数据的`com.adobe.idp.Document`对象。
      * 一个字符串值，用于指定环境变量，包括所有相关的HTTP标头。 通过为`CONTENT_TYPE`环境变量指定一个或多个值来指定要处理的内容类型。 例如，要处理XML数据，请为此参数指定以下字符串值：`CONTENT_TYPE=text/xml`。
      * 指定`HTTP_USER_AGENT`标头值的字符串值，如`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
      * 存储运行时选项的`RenderOptionsSpec`对象。

      `processFormSubmission`方法返回一个`FormsResult`对象，其中包含表单提交的结果。

   * 通过调用`FormsResult`对象的`getAction`方法，确定Forms服务是否已完成表单数据的处理。 如果此方法返回值`0`，则数据可供处理。
   * 通过调用`FormsResult`对象的`getOutputContent`方法，创建`com.adobe.idp.Document`对象以检索表单数据。 （此对象包含可发送到输出服务的表单数据。）
   * 通过调用`java.io.DataInputStream`构造函数并传递`com.adobe.idp.Document`对象来创建`java.io.InputStream`对象。
   * 通过调用静态`org.w3c.dom.DocumentBuilderFactory`对象的`newInstance`方法创建`org.w3c.dom.DocumentBuilderFactory`对象。
   * 通过调用`org.w3c.dom.DocumentBuilderFactory`对象的`newDocumentBuilder`方法创建`org.w3c.dom.DocumentBuilder`对象。
   * 通过调用`org.w3c.dom.DocumentBuilder`对象的`parse`方法并传递`java.io.InputStream`对象来创建`org.w3c.dom.Document`对象。
   * 检索XML文档中每个节点的值。 完成此任务的一种方法是创建一个接受两个参数的自定义方法：`org.w3c.dom.Document`对象以及要检索其值的节点的名称。 此方法会返回表示节点值的字符串值。 在此过程后面的代码示例中，此自定义方法称为`getNodeText`。 此方法的正文如下。


1. 使用输出服务创建非交互式PDF文档。

   通过调用`OutputClient`对象的`generatePDFOutput`方法并传递以下值来创建PDF文档：

   * `TransformationFormat`枚举值。 要生成PDF文档，请指定`TransformationFormat.PDF`。
   * 指定表单设计名称的字符串值。 确保表单设计与从Forms服务中检索的表单数据兼容。
   * 一个字符串值，用于指定表单设计所在的内容根目录。
   * 包含PDF运行时选项的`PDFOutputOptionsSpec`对象。
   * 包含渲染运行时选项的`RenderOptionsSpec`对象。
   * `com.adobe.idp.Document`对象，其中包含要与表单设计合并的数据的XML数据源。 确保此对象是由`FormsResult`对象的`getOutputContent`方法返回的。
   * `generatePDFOutput`方法返回一个包含操作结果的`OutputResult`对象。
   * 通过调用`OutputResult`对象的`getGeneratedDoc`方法来检索非交互式PDF文档。 此方法会返回一个`com.adobe.idp.Document`实例，该实例表示非交互式PDF文档。

1. 使用文档管理服务在内容服务中存储PDF表单（已弃用）

   通过调用`DocumentManagementServiceClientImpl`对象的`storeContent`方法并传递以下值来添加内容：

   * 一个字符串值，用于指定添加内容的商店。 默认存储为`SpacesStore`。 此值是必需参数。
   * 一个字符串值，用于指定添加内容的空间的完全限定路径（例如，`/Company Home/Test Directory`）。 此值是必需参数。
   * 表示新内容的节点名称（例如，`MortgageForm.pdf`）。 此值是必需参数。
   * 指定节点类型的字符串值。 要添加新内容（如PDF文件），请指定`{https://www.alfresco.org/model/content/1.0}content`。 此值是必需参数。
   * 表示内容的`com.adobe.idp.Document`对象。 此值是必需参数。
   * 指定编码值的字符串值（例如`UTF-8`）。 此值是必需参数。
   * `UpdateVersionType`枚举值，用于指定如何处理版本信息（例如，`UpdateVersionType.INCREMENT_MAJOR_VERSION`）以递增内容版本。 )此值是必需参数。
   * 一个`java.util.List`实例，用于指定与内容相关的方面。 此值是一个可选参数，您可以指定`null`。
   * 存储内容属性的`java.util.Map`对象。

   `storeContent`方法返回描述内容的`CRCResult`对象。 例如，使用`CRCResult`对象，您可以获取内容的唯一标识符值。 要执行此任务，请调用`CRCResult`对象的`getNodeUuid`方法。

**另请参阅**

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
