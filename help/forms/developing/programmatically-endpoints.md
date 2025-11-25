---
title: 以编程方式管理端点
description: 使用“端点注册”服务可以添加EJB端点、添加SOAP端点、添加Watched Folder端点、添加电子邮件端点、添加远程端点、添加Task Manager端点、修改端点、删除端点以及检索端点连接器信息。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '10799'
ht-degree: 1%

---

# 以编程方式管理端点 {#programmatically-managing-endpoints}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于终结点注册表服务**

Endpoint Registry服务提供了以编程方式管理端点的功能。 例如，您可以将以下类型的端点添加到服务中：

* EJB
* SOAP
* 观察文件夹
* 电子邮件
* (已在AEM表单中弃用)远程处理
* 任务管理器

>[!NOTE]
>
>SOAP、EJB和(不用于JEE上的AEM Forms)远程端点会自动为每个激活的服务创建。 SOAP和EJB端点为所有服务操作启用SOAP和EJB。

远程端点使Flex客户端能够调用对该端点所添加到的AEM Forms服务的操作。 将创建与端点同名的Flex目标，并且Flex客户端可以创建指向此目标的RemoteObjects以调用对相关服务的操作。

电子邮件、任务管理器和“观察文件夹”端点仅公开服务的特定操作。 添加这些端点需要第二个配置步骤来选择要调用的方法、设置配置参数以及指定输入和输出参数映射。

您可以将TaskManager端点组织成名为&#x200B;*类别*&#x200B;的组。 这些类别随后通过TaskManager向Workspace显示，最终用户在分类时看到TaskManager端点。 在Workspace中，最终用户可在导航窗格中看到这些类别。 每个类别中的端点在Workspace的“启动流程”页面上显示为流程卡片。

您可以使用Endpoint Registry服务完成以下任务：

* 添加EJB端点。 （请参阅[添加EJB端点](programmatically-endpoints.md#adding-ejb-endpoints)。）
* 添加SOAP端点。 (请参阅[添加SOAP端点](programmatically-endpoints.md#adding-soap-endpoints)。)
* 添加观察文件夹终结点（请参阅[添加观察文件夹终结点](programmatically-endpoints.md#adding-watched-folder-endpoints)。）
* 添加电子邮件端点。 （请参阅[添加电子邮件终结点](programmatically-endpoints.md#adding-email-endpoints)。）
* 添加远程端点。 （请参阅[添加远程端点](programmatically-endpoints.md#adding-remoting-endpoints)。）
* 添加TaskManager端点（请参阅[添加TaskManager端点](programmatically-endpoints.md#adding-taskmanager-endpoints)。）
* 修改端点（请参阅[修改端点](programmatically-endpoints.md#modifying-endpoints)。）
* 删除终结点（请参阅[删除终结点](programmatically-endpoints.md#removing-endpoints)。）
* 检索终结点连接器信息（请参阅[检索终结点连接器信息](programmatically-endpoints.md#retrieving-endpoint-connector-information)。）

## 添加EJB端点 {#adding-ejb-endpoints}

您可以使用AEM Forms Java API以编程方式将EJB端点添加到服务。 通过将EJB端点添加到服务，可以使客户机应用程序使用EJB模式调用该服务。 即，在设置调用AEM Forms所需的连接属性时，可以选择EJB模式。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>无法使用Web服务添加EJB端点。

>[!NOTE]
>
>通常，EJB端点会默认添加到服务中。但是，EJB端点可以添加到以编程方式部署的进程中，或者在删除了EJB端点且必须再次添加时。

### 步骤摘要 {#summary-of-steps}

要向服务添加EJB端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistry Client`对象。
1. 设置EJB终结点属性。
1. 创建EJB端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加EJB端点。

**设置EJB终结点属性**

要为服务创建EJB端点，请指定以下值：

* **连接器标识符**：指定要创建的终结点类型。 要创建EJB端点，请指定`EJB`。
* **描述**：指定终结点描述。
* **名称**：指定终结点的名称。
* **服务标识符**：指定终结点所属的服务。
* **操作名称**：指定使用终结点调用的操作的名称。 创建EJB端点时，请指定通配符(`*`)。 但是，如果要指定特定操作而不是调用所有服务操作，请指定操作名称，而不是使用通配符(`*`)。

**创建EJB终结点**

设置EJB终结点属性后，可以为服务创建EJB终结点。

**启用终结点**

创建端点后，必须启用它。 启用端点后，便可用于调用服务。 启用该端点后，可在管理控制台中查看它。

**另请参阅**

[使用Java API添加EJB端点](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加EJB端点 {#adding-an-ejb-endpoint-using-the-java-api}

使用Java API添加EJB端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。 (

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 设置EJB终结点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`EJB`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法调用的操作，并传递指定该操作名称的字符串值。 对于SOAP和EJB端点，请指定通配符(`*`)，这表示所有操作。

1. 创建EJB端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示新EJB终结点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的enable方法并传递`Endpoint`方法返回的`createEndpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加EJB端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端点 {#adding-soap-endpoints}

您可以使用AEM Forms Java API以编程方式将SOAP端点添加到服务。 通过添加SOAP端点，您可以使客户端应用程序能够使用SOAP模式调用服务。 也就是说，在设置调用AEM Forms所需的连接属性时，您可以选择SOAP模式。

>[!NOTE]
>
>无法使用Web服务添加SOAP端点。

>[!NOTE]
>
>通常，SOAP端点会默认添加到服务，但是SOAP端点可以添加到以编程方式部署的进程中，或者在删除了SOAP端点且必须再次添加时。

### 步骤摘要 {#summary_of_steps-1}

要将SOAP端点添加到服务，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置SOAP端点属性。
1. 创建SOAP端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

创建SOAP端点需要这些JAR文件。 但是，如果您使用SOAP端点调用服务，则需要添加JAR文件。 有关AEM Forms JAR文件的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式将SOAP端点添加到服务，您必须创建一个`EndpointRegistryClient`对象。

**设置SOAP终结点属性**

要将SOAP端点添加到服务，请指定以下值：

* **连接器标识符值**：指定要创建的终结点的类型。 要创建SOAP端点，请指定`SOAP`。
* **描述**：指定终结点描述。
* **名称**：指定终结点名称。
* **服务标识符值**：指定终结点所属的服务。
* **操作名称**：指定使用终结点调用的操作的名称。 创建SOAP端点时，请指定通配符(`*`)。 但是，如果要指定特定操作而不是调用所有服务操作，请指定操作名称，而不是使用通配符(`*`)。

**创建SOAP终结点**

设置SOAP端点属性后，您可以创建SOAP端点。

**启用终结点**

创建端点后，必须启用它。 启用终结点后，可用于调用服务。 启用该端点后，您可以在管理控制台中查看它。

**另请参阅**

[使用Java API添加SOAP端点](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加SOAP端点 {#add-a-soap-endpoint-using-the-java-api}

使用Java API将SOAP端点添加到服务：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 设置SOAP端点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`SOAP`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名称的字符串值而调用的操作。 对于SOAP和EJB端点，请指定通配符(`*`)，这表示所有操作。

1. 创建SOAP端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示新SOAP端点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的enable方法启用终结点，并传递`Endpoint`方法返回的`createEndpoint`对象。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加SOAP端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加观察文件夹端点 {#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API以编程方式将观察文件夹端点添加到服务。 通过添加Watched Folder端点，用户可以将文件(如PDF文件)放置在文件夹中。 将文件放在文件夹中后，将调用配置的服务并操作文件。 服务执行指定的操作后，将修改的文件保存在指定的输出文件夹中。 观察文件夹配置为按固定速率间隔或按cron时间表进行扫描，例如每周一、周三和周五中午。

为了以编程方式将Watched Folder端点添加到服务，请考虑以下名为&#x200B;*EncryptDocument*&#x200B;的短暂进程。 (请参阅[了解AEM Forms流程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此进程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的`EncryptPDFUsingPassword`操作。 PDF文档使用密码进行加密，并且经过密码加密的PDF文档是此过程的输出值。 输入值(不安全的PDF文档)的名称为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

>[!NOTE]
>
>无法使用Web服务添加Watched文件夹端点。

### 步骤摘要 {#summary_of_steps-2}

要向服务添加Watched文件夹端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置观察文件夹终结点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建观察文件夹端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式添加观察文件夹端点，您必须创建一个`EndpointRegistryClient`对象。

**设置Watched文件夹终结点属性**

要为服务创建Watched文件夹端点，请指定以下值：

* **连接器标识符**：指定已创建的终结点的类型。 要创建Watched文件夹终结点，请指定`WatchedFolder`。
* **描述**：指定终结点的描述。
* **名称**：指定终结点的名称。
* **服务标识符**：指定终结点所属的服务。 例如，要将Watched文件夹端点添加到此部分中介绍的进程（使用Workbench激活时，进程将成为服务），请指定`EncryptDocument`。
* **操作名称**：指定使用终结点调用的操作的名称。 通常，在为源自在Workbench中创建的进程的服务创建观察文件夹端点时，操作的名称为`invoke`。

**指定配置值**

以编程方式将观察文件夹端点添加到服务时，指定观察文件夹端点的配置值。 如果使用管理控制台添加观察文件夹终结点，则这些配置值由管理员指定。

以下列表指定以编程方式将Watched文件夹端点添加到服务时设置的配置值：

* **url**：指定观察文件夹位置。 在群集环境中，此值必须指向可从群集中的每台计算机访问的共享网络文件夹。
* **asynchronous**：将调用类型标识为异步或同步。 瞬态和同步进程只能同步调用。 默认值为true。 建议使用异步。
* **cronExpression**：由Quartz用来安排对输入目录的轮询。
* **purgeDuration**：这是必需属性。 当结果文件夹中的文件和文件夹早于此值时将清除它们。 此值以天为单位。 此属性有助于确保结果文件夹不会填满。 值为–1天表示从不删除结果文件夹。 默认值为 -1。
* **repeatInterval**：扫描Watched文件夹以进行输入的间隔（以秒为单位）。 除非启用了限制，否则该值应大于处理平均作业的时间；否则，系统可能会过载。 默认值为 5。
* **repeatCount**：观察文件夹扫描文件夹或目录的次数。 值–1表示无限扫描。 默认值为 -1。
* **throttleOn**：限制可在任何给定时间处理的观察文件夹作业数。 最大作业数由batchSize值决定。
* **userName**：从Watched文件夹调用目标服务时使用的用户名。 此值是必需的。 默认值为SuperAdmin。
* **domainName**：用户的域。 此值是必需的。 默认值为DefaultDom。
* **batchSize**：每次扫描要提取的文件或文件夹数。 使用此值可防止系统过载；一次扫描太多文件可能会导致崩溃。 默认值为 2。
* **waitTime**：创建文件夹或文件后，在扫描文件夹或文件之前等待的时间（以毫秒为单位）。 例如，如果等待时间为36,000,000毫秒（1小时），文件是在一分钟前创建的，则将在59分钟或更长时间后提取此文件。 此属性对于确保文件或文件夹完全复制到输入文件夹非常有用。 例如，如果处理的文件很大，且下载文件需要10分钟，则将等待时间设置为10&amp;amp；ast；60&amp;amp；ast；1000毫秒。 如果观察文件夹未等待10分钟，则此设置将阻止该文件夹扫描文件。 默认值为 0。
* **excludeFilePattern**： Watched文件夹用于确定要扫描和选取的文件和文件夹的模式。 将不会扫描任何具有此模式的文件或文件夹以进行处理。 当输入是包含多个文件的文件夹时，此设置非常有用。 文件夹的内容可以复制到一个文件夹，该文件夹具有将被监视文件夹拾取的名称。 此步骤可防止观察文件夹在文件夹完全复制到输入文件夹之前拾取文件夹进行处理。 例如，如果excludeFilePattern值为`data*`，则不会选取与`data*`匹配的所有文件和文件夹。 这包括名为`data1`、`data2`等的文件和文件夹。 此外，还可以使用通配符模式对模式进行补充，以指定文件模式。 观察文件夹修改正则表达式以支持通配符模式，如`*.*`和`*.pdf`。 正则表达式不支持这些通配符模式。
* **includeFilePattern**： watched文件夹用于确定扫描和选取哪些文件夹和文件的模式。 例如，如果此值为`*`，则选取与`input*`匹配的所有文件和文件夹。 这包括名为`input1`、`input2`等的文件和文件夹。 默认值为`*`。 此值指示所有文件和文件夹。 此外，还可以使用通配符模式对模式进行补充，以指定文件模式。 观察文件夹修改正则表达式以支持通配符模式，如`*.*`和`*.pdf`。 正则表达式不支持这些通配符模式。 此值为必填项。
* **resultFolderName**：保存结果的文件夹。 此位置可以是绝对或相对目录路径。 如果结果未出现在此文件夹中，请检查失败文件夹。 只读文件不会得到处理，将保存在故障文件夹中。 默认值为`result/%Y/%M/%D/`。 这是watched文件夹中的结果文件夹。
* **preserveFolderName**：成功扫描和提取后存储文件的位置。 此位置可以是绝对、相对或空目录路径。 默认值为 `preserve/%Y/%M/%D/`。
* **failureFolderName**：保存失败文件的文件夹。 此位置始终相对于观察文件夹。 只读文件不会得到处理，将保存在故障文件夹中。 默认值为 `failure/%Y/%M/%D/`。
* **preserveOnFailure**：如果无法对服务运行操作，则保留输入文件。 默认值为true。
* **overwriteDuplicateFilename**：设置为true时，将覆盖结果文件夹和保留文件夹中的文件。 当设置为false时，使用具有数字索引后缀的文件和文件夹作为名称。 默认值为false。

**定义输入参数值**

创建Watched文件夹端点时，必须定义输入参数值。 也就是说，必须描述传递给由watched文件夹调用的操作的输入值。 例如，请考虑本主题中引入的过程。 它有一个名为`InDoc`的输入值，其数据类型是`com.adobe.idp.Document`。 为此进程创建Watched文件夹端点时（激活进程后，该进程将成为服务），必须定义输入参数值。

要定义Watched文件夹端点所需的输入参数值，请指定以下值：

**输入参数名称**：输入参数的名称。 在Workbench中为进程指定输入值的名称。 如果输入值属于服务操作（不是在Workbench中创建的进程的服务），则在component.xml文件中指定输入名称。 例如，此部分引入的进程的输入参数的名称是`InDoc`。

**映射类型**：用于配置调用服务操作所需的输入值。 有两种类型的映射：

* `Literal`： Watched文件夹端点使用在显示的字段中输入的值。 支持所有基本Java类型。 例如，如果API使用字符串、long、int和Boolean等输入，则字符串将转换为正确类型并调用服务。
* `Variable`：输入的值是watched文件夹用于选取输入的文件模式。 例如，如果您为映射类型选择“变量”，并且输入文档必须是PDF文件，则可以指定`*.pdf`作为映射值。

**映射值**：指定映射类型的值。 例如，如果选择`Variable`映射类型，则可以指定`*.pdf`作为文件模式。

**数据类型**：指定输入值的数据类型。 例如，此部分引入的进程的输入值的数据类型为`com.adobe.idp.Document`。

**定义输出参数值**

创建Watched文件夹端点时，必须定义输出参数值。 也就是说，必须描述由Watched文件夹端点调用的服务返回的输出值。 例如，请考虑本主题中引入的过程。 它具有名为`SecuredDoc`的输出值，其数据类型是`com.adobe.idp.Document`。 为此进程创建Watched文件夹端点时（激活进程后，该进程将成为服务），必须定义输出参数值。

要定义Watched文件夹端点所需的输出参数值，请指定以下值：

**输出参数名称**：输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则在component.xml文件中指定输出名称。 例如，此部分引入的进程的输出参数的名称是`SecuredDoc`。

**映射类型**：用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象（单个文档），则模式为`%F.pdf`，源目标为sourcefilename.pdf。 例如，本节介绍的流程返回单个文档。 因此，映射类型可以定义为`%F.pdf` （`%F`表示使用给定的文件名）。 模式`%E`指定输入文档的扩展名。
* 如果服务返回列表，则模式为`Result\%F\`，源目标为Result\sourcefilename\source1 （输出1）和Result\sourcefilename\source2 （输出2）。
* 如果服务返回映射，则模式为`Result\%F\`，源目标为Result\sourcefilename\file1和Result\sourcefilename\file2。 如果映射有多个对象，则模式为`Result\%F.pdf`，源目标为Result\sourcefilename1.pdf （输出1）、Result\sourcefilenam2.pdf （输出2）等。

**数据类型**：指定返回值的数据类型。 例如，此部分引入的进程的返回值的数据类型为`com.adobe.idp.Document`。

**创建观察文件夹终结点**

在设置端点的属性、配置值并定义输入和输出参数值后，必须创建Watched文件夹端点。

**启用终结点**

创建Watched文件夹端点后，必须启用它。 启用终结点后，可用于调用服务。 启用该端点后，可在管理控制台中查看它。

**另请参阅**

[使用Java API添加观察文件夹端点](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加观察文件夹端点 {#add-a-watched-folder-endpoint-using-the-java-api}

使用AEM Forms Java API添加Watched文件夹端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 设置观察文件夹终结点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`WatchedFolder`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名称的字符串值而调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建Watched文件夹端点时，会调用操作的名称。

1. 指定配置值。

   对于要为Watched文件夹端点设置的每个配置值，必须调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置`url`配置值，请调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法，并传递以下字符串值：

   * 一个字符串值，它指定配置值的名称。 在设置`url`配置值时，指定`url`。
   * 指定配置值值的字符串值。 在设置`url`配置值时，指定观察文件夹位置。

   >[!NOTE]
   >
   >若要查看为EncryptDocument服务设置的所有配置值，请参阅位于[QuickStart：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)添加Watched文件夹端点的Java代码示例。

1. 定义输入参数值。

   通过调用`CreateEndpointInfo`对象的`setInputParameterMapping`方法定义输入参数值，并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称是`InDoc`。
   * 指定输入参数的数据类型的字符串值。 例如，`InDoc`输入参数的数据类型是`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，您可以指定`variable`。
   * 一个字符串值，它指定映射类型值。 例如，您可以指定&amp;amp；ast；.pdf作为文件模式。

   >[!NOTE]
   >
   >为要定义的每个输入参数值调用`setInputParameterMapping`方法。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用`CreateEndpointInfo`对象的`setOutputParameterMapping`方法定义输出参数值，并传递以下值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为`SecuredDoc`。
   * 指定输出参数的数据类型的字符串值。 例如，`SecuredDoc`输出参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，您可以指定`%F.pdf`。

1. 创建观察文件夹端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示观察文件夹终结点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递`Endpoint`方法返回的`createEndpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加观察文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 观察文件夹配置值常量文件 {#watched-folder-configuration-values-constant-file}

[QuickStart：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)添加Watched Folder端点时，使用必须作为Java项目一部分的常量文件来编译快速启动。 此常量文件表示添加Watched文件夹端点时必须设置的配置值。 以下Java代码表示常量文件。

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## 添加电子邮件端点 {#adding-email-endpoints}

您可以使用AEM Forms Java API以编程方式将电子邮件端点添加到服务。 通过添加电子邮件端点，可让用户将包含一个或多个文件附件的电子邮件发送到指定的电子邮件帐户。 然后调用配置服务操作并操作文件。 服务执行指定的操作后，会向发件人发送一封电子邮件，其中包含作为文件附件的修改文件。

为了以编程方式将电子邮件端点添加到服务，请考虑以下名为&#x200B;*MyApplication\EncryptDocument*&#x200B;的短暂进程。 有关短期进程的信息，请参阅[了解AEM Forms进程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此进程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的`EncryptPDFUsingPassword`操作。 此过程使用密码对PDF文档进行加密，并将经过密码加密的PDF文档作为输出值返回。 输入值(不安全的PDF文档)的名称为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

>[!NOTE]
>
>无法使用Web服务添加电子邮件端点。

### 步骤摘要 {#summary_of_steps-3}

要将电子邮件端点添加到服务，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置电子邮件端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建电子邮件端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加电子邮件端点。

**设置电子邮件终结点属性**

要创建服务的电子邮件端点，请指定以下值：

* **连接器标识符值**：指定创建的终结点的类型。 要创建电子邮件终结点，请指定`Email`。
* **描述**：指定终结点的描述。
* **名称**：指定终结点的名称。
* **服务标识符值**：指定终结点所属的服务。 例如，要将电子邮件端点添加到此部分中介绍的进程（使用Workbench激活进程时，该进程将成为服务），请指定`EncryptDocument`。
* **操作名称**：指定使用终结点调用的操作的名称。 通常，在为源自在Workbench中创建的进程的服务创建电子邮件端点时，操作的名称为`invoke`。

**指定配置值**

以编程方式将电子邮件端点添加到服务时，指定电子邮件端点的配置值。 如果使用管理控制台添加电子邮件端点，则这些配置值由管理员指定。

>[!NOTE]
>
>受监视的电子邮件帐户是仅用于电子邮件端点的特殊帐户。 此帐户不是常规用户的电子邮件帐户。 不能将常规用户的电子邮件帐户配置为电子邮件提供商使用的帐户，因为电子邮件提供商在完成邮件的处理之后会从收件箱中删除电子邮件。

以编程方式将电子邮件端点添加到服务时，会设置以下配置值：

* **cronExpression**：如果电子邮件必须使用cron表达式来计划，则返回cron表达式。
* **repeatCount**：电子邮件终结点扫描文件夹或目录的次数。 值–1表示无限扫描。 默认值为 -1。
* **repeatInterval**：接收方用于检查传入邮件的扫描速率（秒）。 默认值为 10。
* **startDelay**：计划程序启动后等待扫描的时间。 默认时间为0。
* **batchSize**：每次扫描接收者为获得最佳性能而处理的电子邮件数量。 值为–1表示所有电子邮件。 默认值为 2。
* **userName**：从电子邮件调用目标服务时使用的用户名。 默认值为 `SuperAdmin`。
* **domainName**：必需的配置值。 默认值为 `DefaultDom`。
* **domainPattern**：指定提供程序接受的传入电子邮件的域模式。 例如，如果使用`adobe.com`，则仅处理来自adobe.com的电子邮件，而忽略来自其他域的电子邮件。
* **filePattern**：指定提供程序接受的传入文件附件模式。 这包括具有特定文件扩展名(&amp;amp；ast；.dat、&amp;amp；ast；.xml)的文件、具有特定名称（数据）的文件以及名称和扩展名中包含复合表达式的文件(&amp;amp；ast；)。``[dD][aA]``&#39;端口&#39;)。 默认值为 `*`。
* **recipientSuccessfulJob**：发送消息以指示作业成功的电子邮件地址。 默认情况下，成功的工作消息将始终发送给发件人。 如果键入`sender`，则将电子邮件结果发送给发件人。 最多支持100个收件人。 指定具有电子邮件地址的其他收件人，每个收件人之间用逗号分隔。 要关闭此选项，请将此值留空。 在某些情况下，您可能希望触发一个进程，而不希望收到关于结果的电子邮件通知。 默认值为 `sender`。
* **recipientFailedJob**：发送消息以指示失败的作业的电子邮件地址。 默认情况下，始终将失败的作业消息发送给发件人。 如果键入`sender`，则将电子邮件结果发送给发件人。 最多支持100个收件人。 指定具有电子邮件地址的其他收件人，每个收件人之间用逗号分隔。 要关闭此选项，请将此值留空。 默认值为 `sender`。
* **inboxHost**：要扫描的电子邮件提供程序的收件箱主机名或IP地址。
* **inboxPort**：电子邮件服务器使用的端口。 POP3的默认值为110，IMAP的默认值为143。 如果启用了SSL，则POP3的默认值为995，而IMAP的默认值为993。
* **inboxProtocol**：电子邮件端点扫描收件箱所使用的电子邮件协议。 选项为`IMAP`或`POP3`。 收件箱主机邮件服务器必须支持这些协议。
* **inboxTimeOut**：电子邮件提供商等待收件箱响应的超时时间（以秒为单位）。 默认值为 60。
* **inboxUser**：登录电子邮件帐户所需的用户名。 根据电子邮件服务器和配置，这可能是电子邮件的用户名部分，也可能是完整的电子邮件地址。
* **inboxPassword**：收件箱用户的密码。
* **inboxSSLEnabled**：设置此值以强制电子邮件提供商在发送结果或错误的通知消息时使用SSL。 确保IMAP或POP3主机支持SSL。
* **smtpHost**：电子邮件提供商向其发送结果和错误消息的邮件服务器的主机名。
* **smtpPort**： SMTP端口的默认值为25。
* **smtpUser**：电子邮件提供商在发送结果和错误的电子邮件通知时使用的用户帐户。
* **smtpPassword**： SMTP帐户的密码。 某些邮件服务器不需要SMTP密码。
* **charSet**：电子邮件提供商使用的字符集。 默认值为 `UTF-8`。
* **smtpSSLEnabled**：设置此值以强制电子邮件提供商在发送结果或错误的通知邮件时使用SSL。 确保SMTP主机支持SSL。
* **failedJobFolder**：指定当SMTP邮件服务器不工作时，用于存储结果的目录。
* **asynchronous**：当设置为synchronous时，将处理所有输入文档并返回单个响应。 当设置为异步时，将为处理的每个输入文档发送响应。 例如，会为本主题中引入的流程创建一个电子邮件端点，并会向端点的收件箱发送一封电子邮件，其中包含了多个不安全的PDF文档。 使用密码对所有PDF文档进行加密后，如果端点配置为同步，则会发送一封响应电子邮件，其中附加所有安全的PDF文档。 如果端点配置为异步，则会为每个受保护的PDF文档发送单独的响应电子邮件消息。 每封电子邮件都包含一个PDF文档作为附件。 默认值为asynchronous。

**定义输入参数值**

创建电子邮件端点时，必须定义输入参数值。 即，必须描述传递给电子邮件端点调用的操作的输入值。 例如，请考虑本主题中引入的过程。 它有一个名为`InDoc`的输入值，其数据类型是`com.adobe.idp.Document`。 为此流程创建电子邮件端点时（激活流程后，该流程将成为服务），必须定义输入参数值。

要定义电子邮件端点所需的输入参数值，请指定以下值：

**输入参数名称**：输入参数的名称。 在Workbench中为进程指定输入值的名称。 如果输入值属于服务操作(不是在Workbench中创建的进程的Forms服务)，则在component.xml文件中指定输入名称。 例如，此部分引入的进程的输入参数的名称是`InDoc`。

**映射类型**：用于配置调用服务操作所需的输入值。 两种类型的映射如下所示：

* `Literal`：电子邮件端点使用在显示的字段中输入的值。 支持所有基本Java类型。 例如，如果API使用字符串、long、int和Boolean等输入，则字符串将转换为正确类型并调用服务。
* `Variable`：输入的值是电子邮件端点用于选取输入的文件模式。 例如，如果您为映射类型选择“变量”，并且输入文档必须是PDF文件，则可以指定`*.pdf`作为映射值。

**映射值**：指定映射类型的值。 例如，如果您选择变量映射类型，则可以指定`*.pdf`作为文件模式。

**数据类型**：指定输入值的数据类型。 例如，本节介绍的进程输入值的数据类型是com.adobe.idp.Document。

**定义输出参数值**

创建电子邮件端点时，必须定义输出参数值。 即，必须描述由电子邮件端点调用的服务返回的输出值。 例如，请考虑本主题中引入的过程。 它具有名为`SecuredDoc`的输出值，其数据类型是`com.adobe.idp.Document`。 为此流程创建电子邮件端点时（流程激活后，即成为服务），必须定义输出参数值。

要定义电子邮件端点所需的输出参数值，请指定以下值：

**输出参数名称**：输出参数的名称。 进程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则在component.xml文件中指定输出名称。 例如，此部分引入的进程的输出参数的名称是`SecuredDoc`。

**映射类型**：用于配置服务和操作的输出。 以下选项可供选择：

* 如果服务返回单个对象（单个文档），则模式为`%F.pdf`，源目标为sourcefilename.pdf。 例如，本节介绍的流程返回单个文档。 因此，映射类型可以定义为`%F.pdf` （`%F`表示使用给定的文件名）。 模式`%E`指定输入文档的扩展名。
* 如果服务返回列表，则模式为`Result\%F\`，源目标为Result\sourcefilename\source1 （输出1）和Result\sourcefilename\source2 （输出2）。
* 如果服务返回映射，则模式为`Result\%F\`，源目标为Result\sourcefilename\file1和Result\sourcefilename\file2。 如果映射有多个对象，则模式为`Result\%F.pdf`，源目标为Result\sourcefilename1.pdf （输出1）、Result\sourcefilenam2.pdf （输出2）等。

**数据类型**：指定返回值的数据类型。 例如，此部分引入的进程的返回值的数据类型为`com.adobe.idp.Document`。

**创建电子邮件终结点**

在设置电子邮件端点属性和配置值并定义输入和输出参数值后，必须创建电子邮件端点。

**启用终结点**

创建电子邮件端点后，必须启用它。 启用终结点后，可用于调用服务。 启用该端点后，可在管理控制台中查看它。

**另请参阅**

[使用Java API添加电子邮件端点](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加电子邮件端点 {#add-an-email-endpoint-using-the-java-api}

使用Java API添加电子邮件端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 设置电子邮件端点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`Email`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名称的字符串值而调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建电子邮件端点时，会调用操作的名称。

1. 指定配置值。

   对于要为电子邮件端点设置的每个配置值，必须调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置`smtpHost`配置值，请调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法并传递以下值：

   * 一个字符串值，它指定配置值的名称。 在设置`smtpHost`配置值时，指定`smtpHost`。
   * 指定配置值值的字符串值。 在设置`smtpHost`配置值时，请指定指定SMTP服务器名称的字符串值。

   >[!NOTE]
   >
   >要查看在此部分中为EncryptDocument服务设置的所有配置值，请参阅位于[QuickStart：使用Java API添加电子邮件终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)的Java代码示例。

1. 定义输入参数值。

   通过调用`CreateEndpointInfo`对象的`setInputParameterMapping`方法定义输入参数值，并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称是`InDoc`。
   * 指定输入参数的数据类型的字符串值。 例如，`InDoc`输入参数的数据类型是`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，您可以指定`variable`。
   * 一个字符串值，它指定映射类型值。 例如，您可以指定&amp;amp；ast；.pdf作为文件模式。

   >[!NOTE]
   >
   >为要定义的每个输入参数值调用`setInputParameterMapping`方法。 由于EncryptDocument进程只有一个输入参数，因此您需要调用此方法一次。

1. 定义输出参数值。

   通过调用`CreateEndpointInfo`对象的`setOutputParameterMapping`方法并传递以下值来定义输出参数值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为`SecuredDoc`。
   * 指定输出参数的数据类型的字符串值。 例如，`SecuredDoc`输出参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，您可以指定`%F.pdf`。

1. 创建电子邮件端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示电子邮件终结点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递`Endpoint`方法返回的`createEndpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加观察文件夹端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 电子邮件配置值常量文件 {#email-configuration-values-constant-file}

[QuickStart：使用Java API添加电子邮件端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)使用常量文件来编译快速入门，常量文件必须是Java项目的一部分。 此常量文件表示添加电子邮件端点时必须设置的配置值。 以下Java代码表示常量文件。

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## 添加远程端点 {#adding-remoting-endpoints}

>[!NOTE]
>
>JEE上的AEM表单弃用LiveCycle Remoting API。

您可以使用AEM Forms Java API以编程方式将远程端点添加到服务。 通过添加远程端点，您可以使Flex应用程序通过使用远程来调用服务。 (请参阅[使用AEM Forms调用(AEM Forms已弃用) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

为了以编程方式将远程端点添加到服务，请考虑以下名为&#x200B;*EncryptDocument*&#x200B;的短暂进程。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此进程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递到加密服务的`EncryptPDFUsingPassword`操作。 PDF文档使用密码进行加密，并且经过密码加密的PDF文档是此过程的输出值。 输入值(不安全的PDF文档)的名称为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

为了演示如何向服务添加远程端点，本节将远程端点添加到名为EncryptDocument的服务。

>[!NOTE]
>
>无法使用Web服务添加远程端点。

### 步骤摘要 {#summary_of_steps-4}

要从服务中删除端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置远程终结点属性。
1. 创建远程端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

若要以编程方式添加远程端点，您必须创建一个`EndpointRegistryClient`对象。

**设置远程终结点属性**

要为服务创建远程端点，请指定以下值：

* **连接器标识符值**：指定创建的终结点的类型。 要创建远程终结点，请指定`Remoting`。
* **描述**：指定终结点的描述。
* **名称**：指定终结点的名称。
* **服务标识符值**：指定终结点所属的服务。 例如，要将Remoting端点添加到此部分引入的进程（在Workbench中激活进程时，该进程将成为服务），请指定`EncryptDocument`。
* **操作名称**：指定使用终结点调用的操作的名称。 创建远程端点时，请指定通配符(&amp;amp；ast；)。

**创建远程终结点**

设置远程端点属性后，可以为服务创建远程端点。

**启用终结点**

创建端点后，必须启用它。 启用远程端点后，Flex客户端将能够调用该服务。

**另请参阅**

[使用Java API添加远程端点](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加远程端点 {#add-a-remoting-endpoint-using-the-java-api}

使用Java API添加远程端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 设置远程终结点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`Remoting`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 指定由`CreateEndpointInfo`对象的`setOperationName`方法调用并传递指定操作名称的字符串值的操作。 对于远程端点，请指定通配符(&amp;amp；ast；)。

1. 创建远程端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示新远程处理终结点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递`Endpoint`方法返回的`createEndpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加远程端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager端点 {#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API以编程方式将TaskManager端点添加到服务。 通过将TaskManager端点添加到服务，可以使Workspace用户能够调用该服务。 也就是说，使用Workspace的用户可以调用具有相应TaskManager端点的进程。

>[!NOTE]
>
>无法使用Web服务添加TaskManager端点。

### 步骤摘要 {#summary_of_steps-5}

要向服务添加TaskManager端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 为端点创建类别。
1. 设置TaskManager端点属性。
1. 创建TaskManager端点。
1. 启用端点。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加TaskManager端点。

**为终结点创建类别**

类别用于整理Workspace中的服务。 也就是说，Workspace用户可以通过在Workspace中选择类别来调用具有TaskManager端点的服务。 创建TaskManager端点时，您可以引用现有类别或以编程方式创建类别。

>[!NOTE]
>
>本部分将创建一个新类别作为将TaskManager端点添加到服务的一部分。

**设置TaskManager终结点属性**

要为服务创建TaskManager端点，请指定以下值：

* **连接器标识符**：指定已创建的终结点的类型。 要创建TaskManager终结点，请指定`TaskManagerConnector`。
* **描述**：指定终结点的描述。
* **名称**：指定终结点的名称。
* **服务标识符**：指定终结点所属的服务。
* **类别**：指定与TaskManager终结点关联的类别标识符值。
* **操作名称**：通常，在为源自在Workbench中创建的进程的服务创建TaskManager终结点时，操作的名称为`invoke`。

**创建TaskManager终结点**

设置TaskManager端点属性后，可以为服务创建TaskManager端点。

**启用终结点**

创建端点后，必须启用它。 启用端点后，便可用于从Workspace中调用服务。 启用该端点后，可在管理控制台中查看它。

**另请参阅**

[使用Java API添加TaskManager端点](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API添加TaskManager端点 {#add-a-taskmanager-endpoint-using-the-java-api}

使用Java API添加TaskManager端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 为端点创建类别。

   * 使用构造函数创建`CreateEndpointCategoryInfo`对象并传递以下值：

      * 一个字符串值，它指定类别的标识符值
      * 指定类别说明的字符串值

   * 通过调用`EndpointRegistryClient`对象的`createEndpointCategory`方法并传递`CreateEndpointCategoryInfo`对象来创建类别。 此方法返回表示新类别的`EndpointCategory`对象。

1. 设置TaskManager端点属性。

   * 使用构造函数创建`CreateEndpointInfo`对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`TaskManagerConnector`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定该名称的字符串值来指定终结点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名称的字符串值，指定终结点所属的服务。
   * 通过调用`CreateEndpointInfo`对象的`setCategoryId`方法并传递指定类别标识符值的字符串值，指定终结点所属的类别。 您可以调用`EndpointCategory`对象的`getId`方法以获取此类别的标识符值。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名称的字符串值而调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建`TaskManager`端点时，操作的名称为`invoke`。

1. 创建TaskManager端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建终结点。 此方法返回表示新TaskManager终结点的`Endpoint`对象。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递`Endpoint`方法返回的`createEndpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API添加TaskManager端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改端点 {#modifying-endpoints}

您可以使用AEM Forms Java API以编程方式修改现有端点。 通过修改端点，可以更改端点的行为。 例如，考虑指定用作观察文件夹的观察文件夹端点。 您可以通过编程方式修改属于Watched文件夹端点的配置值，从而产生另一个文件夹作为观察文件夹。 有关属于Watched文件夹端点的配置值的信息，请参阅[添加Watched文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

为了演示如何修改端点，本节通过更改作为Watched文件夹的文件夹来修改Watched文件夹端点。

>[!NOTE]
>
>无法使用Web服务修改端点。

### 步骤摘要 {#summary_of_steps-6}

要修改端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 检索端点。
1. 指定新的配置值。

**包含项目文件**

在开发项目中包含必要的文件。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

若要以编程方式修改端点，您必须创建一个`EndpointRegistryClient`对象。

**检索要修改的终结点**

必须先检索端点，然后才能修改端点。 要检索端点，您必须以能够访问端点的用户的身份连接。 建议您以管理员身份连接。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)）。

您可以通过检索端点列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，您可以通过确定与端点和端点类型对应的服务来定位端点。 在查找端点时，可以对其进行修改。

**指定新配置值**

修改端点时，请指定新的配置值。 例如，要修改Watched Folder端点，请重置所有Watched Folder端点配置值，而不仅仅是要修改的值。 有关属于Watched文件夹端点的配置值的信息，请参阅[添加Watched文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

>[!NOTE]
>
>有关属于电子邮件端点的配置值的信息，请参阅[添加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints)。

>[!NOTE]
>
>您无法修改终结点调用的服务。 如果尝试修改服务，则会引发异常。 要修改与给定端点关联的服务，请移除该端点并创建一个服务。 （请参阅[删除端点](programmatically-endpoints.md#removing-endpoints)。）

**另请参阅**

[使用Java API修改端点](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API修改端点 {#modifying-an-endpoint-using-the-java-api}

使用Java API修改端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 检索要修改的端点。

   * 通过调用`EndpointRegistryClient`对象的`getEndpoints`方法并传递充当过滤器的`PagingFilter`对象，检索当前用户（在连接属性中指定）可以访问的所有端点的列表。 您可以传递`(PagingFilter)null`值以返回所有端点。 此方法返回一个`java.util.List`对象，其中每个元素都是一个`Endpoint`对象。 有关`PagingFilter`对象的信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 对`java.util.List`对象进行迭代以确定它是否具有端点。 如果存在端点，则每个元素都是一个`EndPoint`实例。
   * 通过调用`EndPoint`对象的`getServiceId`方法确定与端点对应的服务。 此方法返回指定服务名称的字符串值。
   * 通过调用`EndPoint`对象的`getConnectorId`方法确定终结点的类型。 此方法返回一个指定终结点类型的字符串值。 例如，如果端点是Watched文件夹端点，则此方法返回`WatchedFolder`。

1. 指定新的配置值。

   * 通过调用其构造函数创建`ModifyEndpointInfo`对象。
   * 对于要设置的每个配置值，调用`ModifyEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置URL配置值，请调用`ModifyEndpointInfo`对象的`setConfigParameterAsText`方法并传递以下值：

      * 一个字符串值，它指定配置值的名称。 例如，要设置`url`配置值，请指定`url`。
      * 指定配置值值的字符串值。 要为`url`配置值定义值，请指定观察文件夹位置。

   * 调用`EndpointRegistryClient`对象的`modifyEndpoint`方法并传递`ModifyEndpointInfo`对象。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API修改端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 删除端点 {#removing-endpoints}

您可以使用AEM Forms Java API以编程方式从服务中删除端点。 删除终结点后，无法使用终结点启用的调用方法调用该服务。 例如，如果从服务中删除SOAP端点，则无法使用SOAP模式调用该服务。

为了演示如何从服务中删除终结点，此部分从名为&#x200B;*EncryptDocument*&#x200B;的服务中删除EJB终结点。

>[!NOTE]
>
>无法使用Web服务删除端点。

### 步骤摘要 {#summary_of_steps-7}

要从服务中删除端点，请执行以下任务：

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 检索端点。
1. 删除端点。

**包含项目文件**

将必要的文件包含在开发项目中。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

若要以编程方式删除端点，您必须创建一个`EndpointRegistryClient`对象。

**检索要删除的终结点**

在删除端点之前，必须检索它。 要检索端点，您必须以能够访问端点的用户的身份连接。 建议您以管理员身份连接。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)）。

您可以通过检索端点列表来检索端点。 然后，您可以遍历列表，搜索要删除的特定端点。 例如，您可以通过确定与端点和端点类型对应的服务来定位端点。 找到端点后，可以将其删除。

**删除终结点**

创建端点后，必须启用它。 启用终结点后，可用于调用服务。 启用该端点后，可在管理控制台中查看它。

**另请参阅**

[使用Java API删除端点](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API删除端点 {#removing-an-endpoint-using-the-java-api}

使用Java API删除端点：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用构造函数创建`EndpointRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 检索要删除的端点。

   * 通过调用`EndpointRegistryClient`对象的`getEndpoints`方法并传递充当过滤器的`PagingFilter`对象，检索当前用户（在连接属性中指定）有权访问的所有端点的列表。 您可以传递`(PagingFilter)null`以返回所有端点。 此方法返回一个`java.util.List`对象，其中每个元素都是一个`Endpoint`对象。
   * 对`java.util.List`对象进行迭代以确定它是否具有端点。 如果存在端点，则每个元素都是一个`EndPoint`实例。
   * 通过调用`EndPoint`对象的`getServiceId`方法确定与端点对应的服务。 此方法返回指定服务名称的字符串值。
   * 通过调用`EndPoint`对象的`getConnectorId`方法确定终结点的类型。 此方法返回一个指定终结点类型的字符串值。 例如，如果终结点是EJB终结点，则此方法返回`EJB`。

1. 删除端点。

   通过调用`EndpointRegistryClient`对象的`remove`方法并传递表示要移除的终结点的`EndPoint`对象来移除终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API删除端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 正在检索端点连接器信息 {#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以编程方式检索有关端点连接器的信息。 连接器允许端点使用各种调用方法调用服务。 例如，Watched文件夹连接器允许端点使用watched文件夹调用服务。 通过以编程方式检索有关端点连接器的信息，可以检索与连接器关联的配置值，例如哪些配置值是必需的以及哪些是可选的。

为了演示如何检索有关端点连接器的信息，本节检索有关Watched Folder连接器的信息。 （请参阅[添加观察文件夹端点](programmatically-endpoints.md#adding-watched-folder-endpoints)。）

>[!NOTE]
>
>无法使用Web服务检索有关端点的信息。

>[!NOTE]
>
>本主题使用`ConnectorRegistryClient` API检索有关终结点连接器的信息。 (请参阅[AEM Forms API引用](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

### 步骤摘要 {#summary_of_steps-8}

要检索终结点连接器信息，请执行以下任务：

1. 包括项目文件。
1. 创建`ConnectorRegistryClient`对象。
1. 指定连接器类型。
1. 检索配置值。

**包含项目文件**

将必要的文件包含在开发项目中。 如果使用Java创建客户端应用程序，请包含必要的JAR文件。 如果使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果在JBoss Application Server上部署了AEM Forms，则此为必填字段)
* jbossall-client.jar(如果将AEM Forms部署在JBoss Application Server上，则此为必需字段)

如果AEM Forms部署在受支持的J2EE应用程序服务器（不是JBoss）上，请将adobe-utilities.jar和jbossall-client.jar替换为特定于部署AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建ConnectorRegistry客户端对象**

若要以编程方式检索终结点连接器信息，请创建`ConnectorRegistryClient`对象。

**指定连接器类型**

指定要从中检索信息的连接器的类型。 存在以下类型的连接器：

* **EJB**：使客户端应用程序能够使用EJB模式调用服务。
* **SOAP**：允许客户端应用程序使用SOAP模式调用服务。
* **Watched文件夹**：启用Watched文件夹调用服务。
* **电子邮件**：启用电子邮件以调用服务。
* **远程处理**：允许Flex客户端应用程序调用服务。
* **TaskManagerConnector**：允许Workspace用户从Workspace中调用服务。

**检索配置值**

指定连接器类型后，可以检索有关连接器的信息，如支持的配置值。 例如，对于任何连接器，您可以确定哪些配置值是必需的，哪些是可选的。

**另请参阅**

[使用Java API检索端点连接器信息](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API检索端点连接器信息 {#retrieve-endpoint-connector-information-using-the-java-api}

使用Java API检索端点连接器信息：

1. 包括项目文件。

   将客户端JAR文件（如adobe-livecycle-client.jar）包含在Java项目的类路径中。

1. 创建ConnectorRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用对象的构造函数创建`ConnectorRegistryClient`对象并传递`ServiceClientFactory`对象。

1. 指定连接器类型。

   通过调用`ConnectorRegistryClient`对象的`getEndpointDefinition`方法并传递指定连接器类型的字符串值来指定连接器类型。 例如，要指定观察文件夹连接器类型，请传递字符串值`WatchedFolder`。 此方法返回与连接器类型相对应的`Endpoint`对象。

1. 检索配置值。

   * 通过调用`Endpoint`对象的`getConfigParameters`方法，检索在此终结点内关联的配置值。 此方法返回`ConfigParameter`对象的数组。
   * 通过检索数组中的每个元素来检索有关每个配置值的信息。 每个元素都是一个`ConfigParameter`对象。 例如，您可以通过调用`ConfigParameter`对象的`isRequired`方法来确定配置值是必需值还是可选值。 如果需要配置值，则此方法返回`true`。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速启动：使用Java API检索端点连接器信息](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
