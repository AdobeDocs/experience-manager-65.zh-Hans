---
title: 以编程方式管理端点
seo-title: 以编程方式管理端点
description: 使用Endpoint Registry服务可添加EJB端点、添加SOAP端点、添加监视文件夹端点、添加电子邮件端点、添加远程处理端点、添加任务 Manager端点、修改端点、删除端点和检索端点连接器信息。
seo-description: 使用Endpoint Registry服务可添加EJB端点、添加SOAP端点、添加监视文件夹端点、添加电子邮件端点、添加远程处理端点、添加任务 Manager端点、修改端点、删除端点和检索端点连接器信息。
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '10863'
ht-degree: 1%

---


# 以编程方式管理终结点{#programmatically-managing-endpoints}

**本文档中的示例和示例仅适用于JEE环境上的AEM Forms。**

**关于Endpoint Registry服务**

Endpoint Registry服务提供以编程方式管理端点的功能。 例如，您可以向服务添加以下类型的端点：

* EJB
* SOAP
* 监视文件夹
* 电子邮件
* (AEM表单已弃用)远程处理
* 任务 Manager

>[!NOTE]
>
>SOAP、EJB和(JEE上的AEM表单已弃用)为每个激活的服务自动创建远程端点。 SOAP和EJB端点为所有服务操作启用SOAP和EJB。

远程处理端点使Flex客户端能够调用将端点添加到的AEM Forms服务上的操作。 将创建与端点同名的Flex目标，Flex客户端可创建指向此目标的RemoteObjects以调用相关服务上的操作。

电子邮件、任务管理器和监视文件夹终结点仅显示服务的特定操作。 添加这些端点需要第二个配置步骤来选择要调用的方法、设置配置参数以及指定输入和输出参数映射。

可以将TaskManager终结点组织到名为&#x200B;*类别*&#x200B;的组中。 然后，这些类别会通过TaskManager向Workspace公开，最终用户将看到TaskManager端点，因为它们是分类的。 在Workspace中，最终用户可在导航窗格中看到这些类别。 每个类别内的端点在Workspace的“开始进程”(Processes)页面上显示为进程卡。

您可以使用Endpoint Registry服务完成以下任务:

* 添加EJB终结点。 （请参阅[添加EJB端点](programmatically-endpoints.md#adding-ejb-endpoints)。）
* 添加SOAP端点。 （请参阅[添加SOAP端点](programmatically-endpoints.md#adding-soap-endpoints)。）
* 添加监视文件夹终结点（请参阅[添加监视文件夹终结点](programmatically-endpoints.md#adding-watched-folder-endpoints)。）
* 添加电子邮件端点。 （请参阅[添加电子邮件终结点](programmatically-endpoints.md#adding-email-endpoints)。）
* 添加远程处理端点。 （请参阅[添加远程端点](programmatically-endpoints.md#adding-remoting-endpoints)。）
* 添加TaskManager终结点（请参阅[添加TaskManager终结点](programmatically-endpoints.md#adding-taskmanager-endpoints)。）
* 修改终结点（请参阅[修改终结点](programmatically-endpoints.md#modifying-endpoints)。）
* 删除端点（请参阅[删除端点](programmatically-endpoints.md#removing-endpoints)。）
* 检索终结点连接器信息（请参阅[检索终结点连接器信息](programmatically-endpoints.md#retrieving-endpoint-connector-information)。）

## 添加EJB端点{#adding-ejb-endpoints}

可以使用AEM Forms Java API以编程方式将EJB端点添加到服务。 通过向服务添加EJB端点，可以使客户端应用程序通过使用EJB模式调用该服务。 即，在设置调用AEM Forms所需的连接属性时，可以选择EJB模式。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。）

>[!NOTE]
>
>不能使用Web服务添加EJB端点。

>[!NOTE]
>
>通常，默认情况下会向服务添加EJB端点，但是，可以将EJB端点添加到以编程方式部署的进程，或者删除EJB端点后必须再次添加。

### 步骤{#summary-of-steps}的摘要

要向服务添加EJB端点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistry Client`对象。
1. 设置EJB端点属性。
1. 创建EJB端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加EJB端点。

**设置EJB端点属性**

要为服务创建EJB端点，请指定以下值：

* **连接器标识符**:指定要创建的端点的类型。要创建EJB端点，请指定`EJB`。
* **描述**:指定端点描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。
* **操作名称**:指定使用端点调用的操作的名称。创建EJB端点时，请指定通配符(`*`)。 但是，如果要指定特定操作而不是调用所有服务操作，则指定操作的名称而不是使用通配符(`*`)。

**创建EJB端点**

设置EJB端点属性后，可以为服务创建EJB端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，它可用于调用服务。 启用终结点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加EJB端点](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#adding-an-ejb-endpoint-using-the-java-api}添加EJB端点

使用Java API添加EJB端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。 （

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置EJB端点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`EJB`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法调用的操作，并传递一个指定操作名称的字符串值。 对于SOAP和EJB端点，指定通配符(`*`)，表示所有操作。

1. 创建EJB端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示新的EJB端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的enable方法并传递由`createEndpoint`方法返回的`Endpoint`对象来启用终结点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加EJB端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加SOAP端点{#adding-soap-endpoints}

可以使用AEM Forms Java API以编程方式向服务添加SOAP端点。 通过添加SOAP端点，您使客户端应用程序能够使用SOAP模式调用服务。 即，在设置调用AEM Forms所需的连接属性时，可以选择SOAP模式。

>[!NOTE]
>
>不能使用Web服务添加SOAP端点。

>[!NOTE]
>
>通常，SOAP端点在默认情况下添加到服务中。但是，SOAP端点可以添加到以编程方式部署的进程中，或者在删除SOAP端点后必须再次添加。

### 步骤{#summary_of_steps-1}的摘要

要向服务添加SOAP端点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置SOAP端点属性。
1. 创建SOAP端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

创建SOAP端点时需要这些JAR文件。 但是，如果使用SOAP端点调用服务，则需要添加JAR文件。 有关AEM Forms JAR文件的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式向服务添加SOAP端点，必须创建一个`EndpointRegistryClient`对象。

**设置SOAP端点属性**

要向服务添加SOAP端点，请指定以下值：

* **连接器标识符值**:指定要创建的端点的类型。要创建SOAP端点，请指定`SOAP`。
* **描述**:指定端点描述。
* **名称**:指定端点名称。
* **服务标识符值**:指定端点所属的服务。
* **操作名称**:指定使用端点调用的操作的名称。创建SOAP端点时，请指定通配符(`*`)。 但是，如果要指定特定操作而不是调用所有服务操作，则指定操作的名称而不是使用通配符(`*`)。

**创建SOAP端点**

设置SOAP端点属性后，可以创建SOAP端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，它可用于调用服务。 启用终结点后，您可以在管理控制台中视图查看它。

**另请参阅**

[使用Java API添加SOAP端点](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#add-a-soap-endpoint-using-the-java-api}添加SOAP端点

使用Java API向服务添加SOAP端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置SOAP端点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`SOAP`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名的字符串值来调用的操作。 对于SOAP和EJB端点，指定通配符(`*`)，表示所有操作。

1. 创建SOAP端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示新的SOAP端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的enable方法来启用端点，并传递由`createEndpoint`方法返回的`Endpoint`对象。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加SOAP端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加监视文件夹终结点{#adding-watched-folder-endpoints}

您可以使用AEM Forms Java API以编程方式将监视文件夹端点添加到服务。 通过添加“监视文件夹”端点，用户可以将文件（如PDF文件）放置到文件夹中。 将文件放入文件夹后，将调用所配置的服务并处理文件。 在服务执行指定操作后，它将修改的文件保存在指定的输出文件夹中。 监视的文件夹配置为以固定速率间隔或使用cron计划进行扫描，如每周一、周三和周五中午。

为了以编程方式向服务添加监视文件夹端点，请考虑以下名为&#x200B;*EncryptDocument*&#x200B;的短时进程。 (请参阅[了解AEM Forms进程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

此过程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递给加密服务的`EncryptPDFUsingPassword`操作。 PDF文档使用密码加密，而密码加密的PDF文档是此过程的输出值。 输入值的名称(不安全的PDF文档)为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

>[!NOTE]
>
>无法使用Web服务添加监视文件夹终结点。

### 步骤{#summary_of_steps-2}的摘要

要向服务添加监视文件夹终结点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置监视文件夹终结点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建监视文件夹终结点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式添加监视文件夹端点，必须创建一个`EndpointRegistryClient`对象。

**设置监视文件夹终结点属性**

要为服务创建监视文件夹终结点，请指定以下值：

* **连接器标识符**:指定所创建的端点的类型。要创建监视文件夹终结点，请指定`WatchedFolder`。
* **描述**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。例如，要向本节介绍的进程添加监视文件夹终结点（当使用Workbench激活某个进程时，该进程将变为服务），请指定`EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。通常，为源自在Workbench中创建的进程的服务创建监视文件夹终结点时，操作的名称为`invoke`。

**指定配置值**

在以编程方式将监视文件夹终结点添加到服务时，必须指定监视文件夹终结点的配置值。 如果通过使用管理控制台添加监视文件夹终结点，则管理员将指定这些配置值。

以下列表指定在以编程方式将监视文件夹终结点添加到服务时设置的配置值：

* **url**:指定监视的文件夹位置。在群集环境中，此值必须指向可从群集中的每台计算机访问的共享网络文件夹。
* **异步**:将调用类型标识为异步或同步。瞬态和同步进程只能同步调用。 默认值为true。 建议使用异步。
* **cronExpression**:由石英计划输入目录的轮询。有关配置cron表达式的详细信息，请参阅[https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html](https://quartz.sourceforge.net/javadoc/org/quartz/CronTrigger.html)。
* **purgeDuration**:这是必填属性。当结果文件夹中的文件和文件夹早于此值时，将清除这些文件和文件夹。 此值以天为单位。 此属性有助于确保结果文件夹不变为完整。 值为–1天表示从不删除结果文件夹。 默认值为–1。
* **repeatInterval**:扫描监视文件夹以进行输入的时间间隔（以秒为单位）。除非启用限制，否则此值应比处理平均作业的时间长；否则，系统可能会超载。 默认值为 5。
* **repeatCount**:监视文件夹扫描文件夹或目录的次数。值为–1表示不确定扫描。 默认值为–1。
* **throttleOn**:限制可在任何给定时间处理的监视文件夹作业数。作业的最大数量由batchSize值确定。
* **userName**:从监视文件夹调用目标服务时使用的用户名。此值为必填项。 默认值为SuperAdmin。
* **domainName**:用户的域。此值为必填项。 默认值为DefaultDom。
* **batchSize**:每次扫描要拾取的文件或文件夹数。使用此值可防止系统过载；一次扫描过多文件可能会导致崩溃。 默认值为 2。
* **waitTime**:在创建后扫描文件夹或文件之前等待的时间（以毫秒为单位）。例如，如果等待时间为36,000,000毫秒（1小时），而文件是在一分钟前创建的，则此文件将在59分钟或更长时间后被拾取。 此属性有助于确保将文件或文件夹完全复制到输入文件夹。 例如，如果要处理一个大文件，并且该文件需要10分钟才能下载，请将等待时间设置为10&amp;ast;60&amp;ast;1000毫秒。 此设置可防止监视的文件夹在等待十分钟时扫描文件。 默认值为 0。
* **excludeFilePattern**:监视文件夹用于确定扫描和拾取哪些文件和文件夹的模式。不会扫描任何具有此模式的文件或文件夹进行处理。 当输入是包含多个文件的文件夹时，此设置很有用。 文件夹的内容可以复制到一个文件夹中，该文件夹的名称将由监视的文件夹拾取。 此步骤可防止监视文件夹在文件夹被完全复制到输入文件夹之前拾取要处理的文件夹。 例如，如果excludeFilePattern值为`data*`，则不会选取与`data*`匹配的所有文件和文件夹。 这包括名为`data1`、`data2`的文件和文件夹，依此类推。 此外，可以用通配符模式来补充该模式以指定文件模式。 监视的文件夹会修改常规表达式以支持通配符模式，如`*.*`和`*.pdf`。 常规表达式不支持这些通配符模式。
* **includeFilePattern**:监视文件夹用于确定扫描和拾取哪些文件夹和文件的模式。例如，如果此值为`*`，则会选取所有与`input*`匹配的文件和文件夹。 这包括名为`input1`、`input2`的文件和文件夹，依此类推。 默认值为 `*`. 此值指示所有文件和文件夹。 此外，可以用通配符模式来补充该模式以指定文件模式。 监视的文件夹会修改常规表达式以支持通配符模式，如`*.*`和`*.pdf`。 常规表达式不支持这些通配符模式。 此值是必填项。
* **resultFolderName**:存储保存结果的文件夹。此位置可以是绝对路径或相对目录路径。 如果结果未显示在此文件夹中，请检查失败文件夹。 只读文件不会处理，并将保存在失败文件夹中。 默认值为 `result/%Y/%M/%D/`. 这是监视文件夹内的结果文件夹。
* **preserveFolderName**:成功扫描和拾取文件后存储文件的位置。此位置可以是绝对、相对或空目录路径。 默认值为 `preserve/%Y/%M/%D/`.
* **failureFolderName**:保存失败文件的文件夹。此位置始终相对于监视的文件夹。 只读文件不会处理，并将保存在失败文件夹中。 默认值为 `failure/%Y/%M/%D/`.
* **perserveOnFailure**:在无法对服务执行操作时保留输入文件。默认值为true。
* **overwriteDuplicateFilename**:设置为true时，结果文件夹和保留文件夹中的文件将被覆盖。设置为false时，名称将使用具有数字索引后缀的文件和文件夹。 默认值为false。

**定义输入参数值**

创建监视文件夹端点时，必须定义输入参数值。 也就是说，您必须描述传递给监视文件夹调用的操作的输入值。 例如，请考虑本主题中介绍的过程。 它有一个名为`InDoc`的输入值，其数据类型为`com.adobe.idp.Document`。 为此进程创建监视文件夹终结点时（激活进程后，该进程成为服务），必须定义输入参数值。

要定义监视文件夹端点所需的输入参数值，请指定以下值：

**输入参数名称**:输入参数的名称。在Workbench中为流程指定输入值的名称。 如果输入值属于服务操作（不是在Workbench中创建的进程的服务），则输入名称在component.xml文件中指定。 例如，本节中引入的进程的输入参数名称为`InDoc`。

**映射类型**:用于配置调用服务操作所需的输入值。映射类型有两种：

* `Literal`:监视文件夹端点使用显示时在字段中输入的值。支持所有基本的Java类型。 例如，如果API使用String、long、int和Boolean等输入，则字符串将转换为正确的类型并调用服务。
* `Variable`:输入的值是监视文件夹用来选取输入的文件模式。例如，如果为映射类型选择“变量”，且输入文档必须是PDF文件，则可以指定`*.pdf`作为映射值。

**映射值**:指定映射类型的值。例如，如果选择`Variable`映射类型，则可指定`*.pdf`作为文件模式。

**数据类型**:指定输入值的数据类型。例如，本节介绍的进程输入值的数据类型为`com.adobe.idp.Document`。

**定义输出参数值**

创建监视文件夹端点时，必须定义输出参数值。 也就是说，您必须描述由监视文件夹端点调用的服务返回的输出值。 例如，请考虑本主题中介绍的过程。 它的输出值名为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。 为此进程创建监视文件夹终结点时（激活进程后，它将成为服务），必须定义输出参数值。

要定义监视文件夹端点所需的输出参数值，请指定以下值：

**输出参数名称**:输出参数的名称。流程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则输出名称在component.xml文件中指定。 例如，本节中引入的进程的输出参数名称为`SecuredDoc`。

**映射类型**:用于配置服务和操作的输出。以下选项可供选择：

* 如果服务返回单个对象(单个文档)，则模式为`%F.pdf`，源目标为sourcefilename.pdf。 例如，本节中引入的进程返回单个文档。 因此，映射类型可定义为`%F.pdf`（`%F`表示使用给定的文件名）。 模式`%E`指定输入文档的扩展。
* 如果服务返回列表，则模式为`Result\%F\`，源目标为Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服务返回映射，则模式为`Result\%F\`，源目标为Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多个对象，则模式为`Result\%F.pdf`，源目标为Result\sourcefilename1.pdf(output 1)、Result\sourcefilename2.pdf(output 2)，依此类推。

**数据类型**:指定返回值的数据类型。例如，本节介绍的进程返回值的数据类型为`com.adobe.idp.Document`。

**创建监视文件夹终结点**

在设置端点的属性、配置值并定义输入和输出参数值后，必须创建“监视文件夹”端点。

**启用端点**

创建监视文件夹终结点后，必须启用它。 启用端点后，它可用于调用服务。 启用终结点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加监视文件夹终结点](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#add-a-watched-folder-endpoint-using-the-java-api}添加监视文件夹终结点

使用AEM Forms Java API添加监视文件夹端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置监视文件夹终结点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`WatchedFolder`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名的字符串值来调用的操作。 通常，为源自在Workbench中创建的进程的服务创建监视文件夹终结点时，将调用操作的名称。

1. 指定配置值。

   对于要为监视文件夹端点设置的每个配置值，必须调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置`url`配置值，请调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法并传递以下字符串值：

   * 一个字符串值，它指定配置值的名称。 设置`url`配置值时，请指定`url`。
   * 一个字符串值，它指定配置值的值。 设置`url`配置值时，请指定监视的文件夹位置。

   >[!NOTE]
   >
   >要查看为EncryptDocument服务设置的所有配置值，请参阅位于[QuickStart的Java代码示例：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)添加监视文件夹终结点。

1. 定义输入参数值。

   通过调用`CreateEndpointInfo`对象的`setInputParameterMapping`方法定义一个输入参数值并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称为`InDoc`。
   * 一个字符串值，它指定输入参数的数据类型。 例如，`InDoc`输入参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，可以指定`variable`。
   * 一个字符串值，它指定映射类型值。 例如，可以指定&amp;ast;.pdf作为文件模式。

   >[!NOTE]
   >
   >为要定义的每个输入参数值调用`setInputParameterMapping`方法。 由于EncryptDocument进程只有一个输入参数，因此需要调用此方法一次。

1. 定义输出参数值。

   通过调用`CreateEndpointInfo`对象的`setOutputParameterMapping`方法来定义输出参数值并传递以下值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为`SecuredDoc`。
   * 一个字符串值，它指定输出参数的数据类型。 例如，`SecuredDoc`输出参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，可以指定`%F.pdf`。

1. 创建监视文件夹终结点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示“监视文件夹”端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递由`createEndpoint`方法返回的`Endpoint`对象来启用端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加监视文件夹终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 监视文件夹配置值常量文件{#watched-folder-configuration-values-constant-file}

[快速入门：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)添加监视文件夹端点时，会使用一个常量文件，该常量文件必须是Java项目的一部分，才能编译快速开始。 此常量文件表示在添加监视文件夹终结点时必须设置的配置值。 以下Java代码表示常量文件。

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

## 添加电子邮件终结点{#adding-email-endpoints}

您可以使用AEM Forms Java API以编程方式向服务添加电子邮件端点。 通过添加电子邮件端点，用户可以向指定的电子邮件帐户发送包含一个或多个文件附件的电子邮件。 然后，调用配置服务操作并处理文件。 服务执行指定操作后，会向发送者发送一封电子邮件，其中已修改的文件作为文件附件。

为了以编程方式向服务添加电子邮件端点，请考虑以下名为&#x200B;*MyApplication\EncryptDocument*&#x200B;的短时进程。 有关短时间进程的信息，请参阅[了解AEM Forms进程](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)。

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

此过程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递给加密服务的`EncryptPDFUsingPassword`操作。 此过程使用密码加密PDF文档，并返回密码加密的PDF文档作为输出值。 输入值的名称(不安全的PDF文档)为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

>[!NOTE]
>
>不能使用Web服务添加电子邮件端点。

### 步骤{#summary_of_steps-3}的摘要

要向服务添加电子邮件端点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置电子邮件端点属性。
1. 指定配置值。
1. 定义输入参数值。
1. 定义输出参数值。
1. 创建电子邮件端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加Email端点。

**设置电子邮件端点属性**

要为服务创建电子邮件端点，请指定以下值：

* **连接器标识符值**:指定所创建的端点的类型。要创建电子邮件端点，请指定`Email`。
* **描述**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符值**:指定端点所属的服务。例如，要向本节介绍的进程添加一个电子邮件端点（当使用Workbench激活某个进程时，该进程将变为服务），请指定`EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。通常，为源自在Workbench中创建的进程的服务创建电子邮件端点时，操作的名称为`invoke`。

**指定配置值**

在以编程方式将电子邮件端点添加到服务时，必须指定电子邮件端点的配置值。 如果使用管理控制台添加了电子邮件终结点，则管理员将指定这些配置值。

>[!NOTE]
>
>被监视的电子邮件帐户是仅用于电子邮件端点的特殊帐户。 此帐户不是普通用户的电子邮件帐户。 不能将常规用户的电子邮件帐户配置为电子邮件提供者使用的帐户，因为电子邮件提供者在邮件处理完毕后将从收件箱中删除电子邮件。

以编程方式将电子邮件端点添加到服务时，将设置以下配置值：

* **cronExpression**:一个cron表达式，如果必须使用cron表达式来计划电子邮件。
* **repeatCount**:电子邮件端点扫描文件夹或目录的次数。值为–1表示不确定扫描。 默认值为–1。
* **repeatInterval**:接收器用于检查传入邮件的扫描速率（以秒为单位）。默认值为 10。
* **startDelay**:在调度程序开始后等待扫描的时间。默认时间为0。
* **batchSize**:接收方每次扫描处理的电子邮件数以获得最佳性能。值–1表示所有电子邮件。 默认值为 2。
* **userName**:从电子邮件调用目标服务时使用的用户名。默认值为 `SuperAdmin`.
* **domainName**:必需的配置值。默认值为 `DefaultDom`.
* **domainPattern**:指定提供者接受的传入电子邮件的域模式。例如，如果使用`adobe.com`，则只处理来自adobe.com的电子邮件，忽略来自其他域的电子邮件。
* **filePattern**:指定提供程序接受的传入文件附件模式。这包括具有特定文件扩展名(&amp;ast;.dat，&amp;ast;.xml)的文件，具有特定名称（数据）的文件，以及具有名称和扩展名(&amp;ast;)中的复合表达式的文件。[D][aA]&#39;port&#39;)。默认值为 `*`.
* **recipientSuccessfulJob**:发送邮件以指示作业成功的电子邮件地址。默认情况下，成功的作业消息始终发送给发送者。 如果键入`sender`，则电子邮件结果将发送给发件人。 最多支持100个收件人。 使用电子邮件地址指定其他收件人，每个地址以逗号分隔。 要关闭此选项，请将此值留空。 在某些情况下，您可能希望触发某个进程，而不希望收到有关结果的电子邮件通知。 默认值为 `sender`.
* **recipientFailedJob**:发送邮件以指示失败作业的电子邮件地址。默认情况下，失败的作业消息始终发送给发送者。 如果键入`sender`，则电子邮件结果将发送给发件人。 最多支持100个收件人。 使用电子邮件地址指定其他收件人，每个地址以逗号分隔。 要关闭此选项，请将此值留空。 默认值为 `sender`.
* **inboxHost**:要扫描的电子邮件提供程序的收件箱主机名或IP地址。
* **inboxPort**:电子邮件服务器使用的端口。POP3的默认值为110,IMAP的默认值为143。 如果启用了SSL，则POP3的默认值为995,IMAP的默认值为993。
* **inboxProtocol**:用于扫描收件箱的电子邮件端点的电子邮件协议。选项为`IMAP`或`POP3`。 收件箱主机邮件服务器必须支持这些协议。
* **inboxTimeOut**:电子邮件提供商等待收件箱响应的超时（以秒为单位）。默认值为 60。
* **inboxUser**:登录电子邮件帐户所需的用户名。根据电子邮件服务器和配置的不同，这可能仅是电子邮件的用户名部分，也可能是完整的电子邮件地址。
* **inboxPassword**:收件箱用户的口令。
* **inboxSSLEnabled**:设置此值后，在发送结果或错误的通知消息时，强制电子邮件提供者使用SSL。确保IMAP或POP3主机支持SSL。
* **smtpHost**:电子邮件提供者向其发送结果和错误消息的邮件服务器的主机名。
* **smtpPort**:SMTP端口的默认值为25。
* **smtpUser**:电子邮件提供商在发送结果和错误的电子邮件通知时要使用的用户帐户。
* **smtpPassword**:SMTP帐户的口令。某些邮件服务器不需要SMTP密码。
* **charSet**:电子邮件提供者使用的字符集。默认值为 `UTF-8`.
* **smtpSSLEnabled**:设置此值后，在发送结果或错误的通知消息时，强制电子邮件提供者使用SSL。确保SMTP主机支持SSL。
* **failedJobFolder**:指定在SMTP邮件服务器不工作时存储结果的目录。
* **异步**:设置为同步时，将处理所有输入文档并返回单个响应。设置为异步时，将针对处理的每个输入文档发送响应。 例如，将为本主题中引入的进程创建电子邮件终结点，并向包含多个不安全PDF文档的终结点的收件箱发送电子邮件。 当所有PDF文档都使用密码加密，并且如果终结点配置为同步，则会发送一封单一响应电子邮件，并附加所有安全的PDF文档。 如果将端点配置为异步，则会为每个受保护的PDF文档发送单独的响应电子邮件。 每封电子邮件都包含一个作为附件的PDF文档。 默认值为异步。

**定义输入参数值**

创建电子邮件端点时，必须定义输入参数值。 也就是说，您必须描述传递给由电子邮件端点调用的操作的输入值。 例如，请考虑本主题中介绍的过程。 它有一个名为`InDoc`的输入值，其数据类型为`com.adobe.idp.Document`。 为此进程创建电子邮件端点时（在激活进程后，它将变为服务），必须定义输入参数值。

要定义电子邮件端点所需的输入参数值，请指定以下值：

**输入参数名称**:输入参数的名称。在Workbench中为流程指定输入值的名称。 如果输入值属于服务操作(不是在Workbench中创建的进程的Forms服务)，则输入名称在component.xml文件中指定。 例如，本节中引入的进程的输入参数名称为`InDoc`。

**映射类型**:用于配置调用服务操作所需的输入值。映射类型有两种：

* `Literal`:“电子邮件”端点使用显示时在字段中输入的值。支持所有基本的Java类型。 例如，如果API使用String、long、int和Boolean等输入，则字符串将转换为正确的类型并调用服务。
* `Variable`:输入的值是电子邮件端点用来选取输入的文件模式。例如，如果为映射类型选择“变量”，且输入文档必须是PDF文件，则可以指定`*.pdf`作为映射值。

**映射值**:指定映射类型的值。例如，如果选择“变量”映射类型，则可以指定`*.pdf`作为文件模式。

**数据类型**:指定输入值的数据类型。例如，本节介绍的进程输入值的数据类型是com.adobe.idp.文档。

**定义输出参数值**

创建电子邮件端点时，必须定义输出参数值。 也就是说，您必须描述由电子邮件端点调用的服务返回的输出值。 例如，请考虑本主题中介绍的过程。 它的输出值名为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。 为此进程创建电子邮件端点时（在激活进程后，它将变为服务），必须定义输出参数值。

要定义电子邮件端点所需的输出参数值，请指定以下值：

**输出参数名称**:输出参数的名称。流程输出值的名称在Workbench中指定。 如果输出值属于服务操作（不是在Workbench中创建的进程的服务），则输出名称在component.xml文件中指定。 例如，本节中引入的进程的输出参数名称为`SecuredDoc`。

**映射类型**:用于配置服务和操作的输出。以下选项可供选择：

* 如果服务返回单个对象(单个文档)，则模式为`%F.pdf`，源目标为sourcefilename.pdf。 例如，本节中引入的进程返回单个文档。 因此，映射类型可定义为`%F.pdf`（`%F`表示使用给定的文件名）。 模式`%E`指定输入文档的扩展。
* 如果服务返回列表，则模式为`Result\%F\`，源目标为Result\sourcefilename\source1 (output 1)和Result\sourcefilename\source2 (output 2)。
* 如果服务返回映射，则模式为`Result\%F\`，源目标为Result\sourcefilename\file1 and Result\sourcefilename\file2。 如果映射有多个对象，则模式为`Result\%F.pdf`，源目标为Result\sourcefilename1.pdf(output 1)、Result\sourcefilename2.pdf(output 2)，依此类推。

**数据类型**:指定返回值的数据类型。例如，本节介绍的进程返回值的数据类型为`com.adobe.idp.Document`。

**创建电子邮件端点**

在设置“电子邮件”端点属性和配置值并定义输入和输出参数值后，必须创建“电子邮件”端点。

**启用端点**

在创建电子邮件端点后，必须启用该端点。 启用端点后，它可用于调用服务。 启用终结点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加电子邮件端点](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#add-an-email-endpoint-using-the-java-api}添加电子邮件端点

使用Java API添加电子邮件端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置电子邮件端点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`Email`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名的字符串值来调用的操作。 通常，为源自在Workbench中创建的进程的服务创建电子邮件端点时，将调用操作的名称。

1. 指定配置值。

   对于要为Email端点设置的每个配置值，必须调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置`smtpHost`配置值，请调用`CreateEndpointInfo`对象的`setConfigParameterAsText`方法并传递以下值：

   * 一个字符串值，它指定配置值的名称。 设置`smtpHost`配置值时，请指定`smtpHost`。
   * 一个字符串值，它指定配置值的值。 设置`smtpHost`配置值时，请指定一个字符串值，用于指定SMTP服务器的名称。

   >[!NOTE]
   >
   >要查看本节中引入的EncryptDocument服务的所有配置值设置，请参阅位于[QuickStart的Java代码示例：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)添加电子邮件终结点。

1. 定义输入参数值。

   通过调用`CreateEndpointInfo`对象的`setInputParameterMapping`方法定义一个输入参数值并传递以下值：

   * 一个字符串值，它指定输入参数的名称。 例如，EncryptDocument服务的输入参数的名称为`InDoc`。
   * 一个字符串值，它指定输入参数的数据类型。 例如，`InDoc`输入参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，可以指定`variable`。
   * 一个字符串值，它指定映射类型值。 例如，可以指定&amp;ast;.pdf作为文件模式。

   >[!NOTE]
   >
   >为要定义的每个输入参数值调用`setInputParameterMapping`方法。 由于EncryptDocument进程只有一个输入参数，因此需要调用此方法一次。

1. 定义输出参数值。

   通过调用`CreateEndpointInfo`对象的`setOutputParameterMapping`方法并传递以下值来定义输出参数值：

   * 一个字符串值，它指定输出参数的名称。 例如，EncryptDocument服务的输出参数的名称为`SecuredDoc`。
   * 一个字符串值，它指定输出参数的数据类型。 例如，`SecuredDoc`输出参数的数据类型为`com.adobe.idp.Document`。
   * 指定映射类型的字符串值。 例如，可以指定`%F.pdf`。

1. 创建电子邮件端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示Email端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递由`createEndpoint`方法返回的`Endpoint`对象来启用端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加监视文件夹终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 电子邮件配置值常量文件{#email-configuration-values-constant-file}

[快速入门：使用Java API](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api)添加电子邮件端点时，会使用一个常量文件，该常量文件必须是Java项目的一部分，才能编译快速开始。 此常量文件表示在添加电子邮件端点时必须设置的配置值。 以下Java代码表示常量文件。

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

## 添加远程处理端点{#adding-remoting-endpoints}

>[!NOTE]
>
>LiveCycle Remoting API已在JEE上为AEM表单弃用。

您可以使用AEM Forms Java API以编程方式向服务添加远程处理端点。 通过添加远程处理端点，您可以使Flex应用程序通过使用远程处理调用服务。 (请参阅[使用调用AEM Forms(对于AEM表单已弃用)AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。)

为了以编程方式向服务添加远程处理端点，请考虑以下名为&#x200B;*EncryptDocument*&#x200B;的短时进程。

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

此过程接受不安全的PDF文档作为输入值，然后将不安全的PDF文档传递给加密服务的`EncryptPDFUsingPassword`操作。 PDF文档使用密码加密，而密码加密的PDF文档是此过程的输出值。 输入值的名称(不安全的PDF文档)为`InDoc`，数据类型为`com.adobe.idp.Document`。 输出值(密码加密的PDF文档)的名称为`SecuredDoc`，数据类型为`com.adobe.idp.Document`。

为了说明如何向服务添加远程处理端点，本节将远程处理端点添加到名为EncryptDocument的服务。

>[!NOTE]
>
>不能使用Web服务添加远程处理端点。

### 步骤{#summary_of_steps-4}的摘要

要从服务中删除终结点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 设置远程处理端点属性。
1. 创建远程处理端点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式添加Remoting端点，必须创建`EndpointRegistryClient`对象。

**设置远程处理端点属性**

要为服务创建远程处理端点，请指定以下值：

* **连接器标识符值**:指定所创建的端点的类型。要创建远程处理端点，请指定`Remoting`。
* **描述**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符值**:指定端点所属的服务。例如，要向本节介绍的进程添加远程处理端点（当在Workbench中激活某个进程时，该进程将成为服务），请指定`EncryptDocument`。
* **操作名称**:指定使用端点调用的操作的名称。创建远程处理端点时，请指定通配符(&amp;ast;)。

**创建远程处理端点**

设置“远程处理”端点属性后，可以为服务创建远程处理端点。

**启用端点**

创建新端点后，必须启用它。 启用远程处理端点后，Flex客户端将调用该服务。

**另请参阅**

[使用Java API添加远程处理端点](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#add-a-remoting-endpoint-using-the-java-api}添加远程处理端点

使用Java API添加远程处理端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 设置远程处理端点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`Remoting`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 指定由`CreateEndpointInfo`对象的`setOperationName`方法调用的操作，并传递指定操作名称的字符串值。 对于远程处理端点，请指定通配符(&amp;ast;)。

1. 创建远程处理端点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示新的Remoting端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递由`createEndpoint`方法返回的`Endpoint`对象来启用端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加远程处理端点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 添加TaskManager终结点{#adding-taskmanager-endpoints}

您可以使用AEM Forms Java API以编程方式将TaskManager端点添加到服务。 通过向服务添加TaskManager端点，可使Workspace用户调用该服务。 即，在Workspace中工作的用户可以调用具有相应TaskManager端点的进程。

>[!NOTE]
>
>不能使用Web服务添加TaskManager终结点。

### 步骤{#summary_of_steps-5}的摘要

要向服务添加TaskManager终结点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 为端点创建类别。
1. 设置TaskManager终结点属性。
1. 创建TaskManager终结点。
1. 启用端点。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

必须先创建`EndpointRegistryClient`对象，然后才能以编程方式添加TaskManager终结点。

**为端点创建类别**

类别用于在Workspace中组织服务。 也就是说， Workspace用户可以通过在Workspace中选择类别来调用具有TaskManager端点的服务。 创建TaskManager端点时，可以引用现有类别或以编程方式创建新类别。

>[!NOTE]
>
>此部分将创建新类别，作为向服务添加TaskManager端点的一部分。

**设置TaskManager终结点属性**

要为服务创建TaskManager终结点，请指定以下值：

* **连接器标识符**:指定所创建的端点的类型。要创建TaskManager终结点，请指定`TaskManagerConnector`。
* **描述**:指定端点的描述。
* **名称**:指定端点的名称。
* **服务标识符**:指定端点所属的服务。
* **类别**:指定与TaskManager端点关联的类别标识符值。
* **操作名称**:通常，在为源自在Workbench中创建的进程的服务创建TaskManager终结点时，操作的名称为 `invoke`。

**创建TaskManager终结点**

在设置TaskManager端点属性后，可以为服务创建TaskManager端点。

**启用端点**

创建新端点后，必须启用它。 启用端点后，它可用于从Workspace中调用服务。 启用终结点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API添加TaskManager终结点](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#add-a-taskmanager-endpoint-using-the-java-api}添加TaskManager终结点

使用Java API添加TaskManager终结点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 为端点创建类别。

   * 使用`CreateEndpointCategoryInfo`对象的构造函数并传递以下值，创建对象：

      * 一个字符串值，它指定类别的标识符值
      * 一个字符串值，它指定类别的描述
   * 通过调用`EndpointRegistryClient`对象的`createEndpointCategory`方法并传递`CreateEndpointCategoryInfo`对象来创建类别。 此方法返回一个表示新类别的`EndpointCategory`对象。


1. 设置TaskManager终结点属性。

   * 使用`CreateEndpointInfo`对象的构造函数创建对象。
   * 通过调用`CreateEndpointInfo`对象的`setConnectorId`方法并传递字符串值`TaskManagerConnector`来指定连接器标识符值。
   * 通过调用`CreateEndpointInfo`对象的`setDescription`方法并传递描述该端点的字符串值来指定端点的描述。
   * 通过调用`CreateEndpointInfo`对象的`setName`方法并传递指定名称的字符串值来指定端点的名称。
   * 通过调用`CreateEndpointInfo`对象的`setServiceId`方法并传递指定服务名的字符串值，指定端点所属的服务。
   * 通过调用`CreateEndpointInfo`对象的`setCategoryId`方法并传递指定类别标识符值的字符串值，指定端点所属的类别。 可以调用`EndpointCategory`对象的`getId`方法来获取此类别的标识符值。
   * 指定通过调用`CreateEndpointInfo`对象的`setOperationName`方法并传递指定操作名的字符串值来调用的操作。 通常，在为源自在Workbench中创建的进程的服务创建`TaskManager`端点时，操作的名称为`invoke`。

1. 创建TaskManager终结点。

   通过调用`EndpointRegistryClient`对象的`createEndpoint`方法并传递`CreateEndpointInfo`对象来创建端点。 此方法返回一个`Endpoint`对象，它表示新的TaskManager端点。

1. 启用端点。

   通过调用`EndpointRegistryClient`对象的`enable`方法并传递由`createEndpoint`方法返回的`Endpoint`对象来启用端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API添加TaskManager终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 修改终结点{#modifying-endpoints}

您可以使用AEM Forms Java API以编程方式修改现有端点。 通过修改端点，可以更改端点的行为。 例如，考虑一个指定用作监视文件夹的文件夹的监视文件夹终结点。 您可以通过编程方式修改属于监视文件夹端点的配置值，从而使另一个文件夹能够充当监视文件夹。 有关属于监视文件夹终结点的配置值的信息，请参阅[添加监视文件夹终结点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

为了说明如何修改终结点，本节通过更改与监视文件夹一样的文件夹来修改监视文件夹终结点。

>[!NOTE]
>
>不能使用Web服务修改端点。

### 步骤{#summary_of_steps-6}的摘要

要修改端点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 检索端点。
1. 指定新的配置值。

**包括项目文件**

在开发项目中包含必要的文件。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式修改端点，必须创建一个`EndpointRegistryClient`对象。

**检索要修改的端点**

在修改端点之前，必须检索它。 要检索终结点，您必须以可访问终结点的用户身份进行连接。 建议您以管理员身份进行连接。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)）。

可以通过检索端点列表来检索端点。 然后，您可以循环访问列表，搜索要删除的特定端点。 例如，可以通过确定与端点对应的服务以及端点的类型来定位端点。 在您找到端点时，可以修改它。

**指定新配置值**

修改端点时，请指定新的配置值。 例如，要修改监视文件夹终结点，请重置所有监视文件夹终结点配置值，而不仅仅是要修改的值。 有关属于监视文件夹终结点的配置值的信息，请参阅[添加监视文件夹终结点](programmatically-endpoints.md#adding-watched-folder-endpoints)。

>[!NOTE]
>
>有关属于电子邮件端点的配置值的信息，请参阅[添加电子邮件端点](programmatically-endpoints.md#adding-email-endpoints)。

>[!NOTE]
>
>不能修改由端点调用的服务。 如果尝试修改服务，将引发异常。 要修改与给定端点关联的服务，请删除该端点并创建新端点。 （请参阅[删除终结点](programmatically-endpoints.md#removing-endpoints)。）

**另请参阅**

[使用Java API修改终结点](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#modifying-an-endpoint-using-the-java-api}修改终结点

使用Java API修改端点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 检索要修改的端点。

   * 通过调用`EndpointRegistryClient`对象的`getEndpoints`方法并传递充当过滤器的`PagingFilter`对象，检索当前用户（在连接属性中指定）可访问的所有端点的列表。 可以传递`(PagingFilter)null`值以返回所有端点。 此方法返回一个`java.util.List`对象，其中每个元素都是一个`Endpoint`对象。 有关`PagingFilter`对象的信息，请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 对`java.util.List`对象进行迭代以确定它是否具有端点。 如果存在端点，则每个元素都是`EndPoint`实例。
   * 通过调用`EndPoint`对象的`getServiceId`方法，确定与端点对应的服务。 此方法返回一个指定服务名称的字符串值。
   * 通过调用`EndPoint`对象的`getConnectorId`方法确定端点的类型。 此方法返回一个字符串值，它指定端点的类型。 例如，如果终结点是监视文件夹终结点，则此方法返回`WatchedFolder`。

1. 指定新的配置值。

   * 通过调用其构造函数创建`ModifyEndpointInfo`对象。
   * 对于要设置的每个配置值，调用`ModifyEndpointInfo`对象的`setConfigParameterAsText`方法。 例如，要设置url配置值，请调用`ModifyEndpointInfo`对象的`setConfigParameterAsText`方法并传递以下值：

      * 一个字符串值，它指定配置值的名称。 例如，要设置`url`配置值，请指定`url`。
      * 一个字符串值，它指定配置值的值。 要为`url`配置值定义值，请指定监视的文件夹位置。
   * 调用`EndpointRegistryClient`对象的`modifyEndpoint`方法并传递`ModifyEndpointInfo`对象。


**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API修改终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 删除端点{#removing-endpoints}

您可以使用AEM Forms Java API以编程方式从服务中删除端点。 删除终结点后，无法通过使用该终结点启用的调用方法调用该服务。 例如，如果从服务中删除SOAP端点，则无法使用SOAP模式调用服务。

为了说明如何从服务中删除终结点，本节将从名为&#x200B;*EncryptDocument*&#x200B;的服务中删除EJB终结点。

>[!NOTE]
>
>不能使用Web服务删除终结点。

### 步骤{#summary_of_steps-7}的摘要

要从服务中删除终结点，请执行以下任务:

1. 包括项目文件。
1. 创建`EndpointRegistryClient`对象。
1. 检索端点。
1. 删除端点。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

有关这些JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建EndpointRegistry客户端对象**

要以编程方式删除端点，必须创建一个`EndpointRegistryClient`对象。

**检索要删除的端点**

在删除端点之前，必须先检索它。 要检索终结点，您必须以可访问终结点的用户身份进行连接。 建议您以管理员身份进行连接。 （请参阅[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)）。

可以通过检索端点列表来检索端点。 然后，您可以循环访问列表，搜索要删除的特定端点。 例如，可以通过确定与端点对应的服务以及端点的类型来定位端点。 在您找到端点时，可以删除它。

**删除端点**

创建新端点后，必须启用它。 启用端点后，它可用于调用服务。 启用终结点后，可以在管理控制台中视图它。

**另请参阅**

[使用Java API删除终结点](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#removing-an-endpoint-using-the-java-api}删除终结点

使用Java API删除终结点：

1. 包括项目文件。

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建EndpointRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`EndpointRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 检索要删除的端点。

   * 通过调用`EndpointRegistryClient`对象的`getEndpoints`方法并传递充当过滤器的`PagingFilter`对象，检索当前用户（在连接属性中指定）可以访问的所有端点的列表。 可以传递`(PagingFilter)null`以返回所有端点。 此方法返回一个`java.util.List`对象，其中每个元素都是一个`Endpoint`对象。
   * 对`java.util.List`对象进行迭代以确定它是否具有端点。 如果存在端点，则每个元素都是`EndPoint`实例。
   * 通过调用`EndPoint`对象的`getServiceId`方法，确定与端点对应的服务。 此方法返回一个指定服务名称的字符串值。
   * 通过调用`EndPoint`对象的`getConnectorId`方法确定端点的类型。 此方法返回一个字符串值，它指定端点的类型。 例如，如果终结点是EJB终结点，则此方法返回`EJB`。

1. 删除端点。

   通过调用`EndpointRegistryClient`对象的`remove`方法并传递表示要删除的端点的`EndPoint`对象来删除端点。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API删除终结点](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 正在检索终结点连接器信息{#retrieving-endpoint-connector-information}

您可以使用AEM Forms API以编程方式检索有关端点连接器的信息。 连接器使端点能够使用各种调用方法调用服务。 例如，监视文件夹连接器使终结点能够使用监视文件夹调用服务。 通过以编程方式检索有关端点连接器的信息，您可以检索与连接器相关的配置值，例如需要哪些配置值以及哪些配置值是可选的。

要演示如何检索有关端点连接器的信息，本节将检索有关监视文件夹连接器的信息。 （请参阅[添加监视文件夹终结点](programmatically-endpoints.md#adding-watched-folder-endpoints)。）

>[!NOTE]
>
>无法使用Web服务检索有关端点的信息。

>[!NOTE]
>
>本主题使用`ConnectorRegistryClient` API检索有关终结点连接器的信息。 (请参阅[AEM Forms API参考](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。)

### 步骤{#summary_of_steps-8}的摘要

要检索端点连接器信息，请执行以下任务:

1. 包括项目文件。
1. 创建`ConnectorRegistryClient`对象。
1. 指定连接器类型。
1. 检索配置值。

**包括项目文件**

将必要的文件包含到开发项目中。 如果要使用Java创建客户端应用程序，请包含必要的JAR文件。 如果您使用Web服务，请确保包含代理文件。

必须将以下JAR文件添加到项目的类路径中：

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)
* jbossall-client.jar(如果AEM Forms部署在JBoss Application Server上，则为必需)

如果AEM Forms部署在非JBoss的受支持J2EE应用程序服务器上，则将adobe-utilities.jar和jbossall-client.jar替换为特定于部署了AEM Forms的J2EE应用程序服务器的JAR文件。 有关所有AEM Forms JAR文件位置的信息，请参阅[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)。

**创建ConnectorRegistry客户端对象**

要以编程方式检索端点连接器信息，请创建`ConnectorRegistryClient`对象。

**指定连接器类型**

指定要从中检索信息的连接器的类型。 存在以下类型的连接器：

* **EJB**:使客户端应用程序能够使用EJB模式调用服务。
* **SOAP**:使客户端应用程序能够使用SOAP模式调用服务。
* **监视文件夹**:允许监视文件夹调用服务。
* **电子邮件**:使电子邮件能够调用服务。
* **远程处理**:使Flex客户端应用程序能够调用服务。
* **TaskManagerConnector**:使Workspace用户能够从Workspace内调用服务。

**检索配置值**

指定连接器类型后，可以检索有关连接器的信息，如支持的配置值。 例如，对于任何连接器，您可以确定需要哪些配置值以及哪些配置值是可选的。

**另请参阅**

[使用Java API检索端点连接器信息](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 使用Java API {#retrieve-endpoint-connector-information-using-the-java-api}检索端点连接器信息

使用Java API检索端点连接器信息：

1. 包括项目文件。.

   在Java项目的类路径中包含客户端JAR文件，如adobe-livecycle-client.jar。

1. 创建ConnectorRegistry客户端对象。

   * 创建包含连接属性的`ServiceClientFactory`对象。
   * 使用`ConnectorRegistryClient`对象的构造函数并传递`ServiceClientFactory`对象，创建对象。

1. 指定连接器类型。

   通过调用`ConnectorRegistryClient`对象的`getEndpointDefinition`方法并传递指定连接器类型的字符串值来指定连接器类型。 例如，要指定“监视文件夹”连接器类型，请传递字符串值`WatchedFolder`。 此方法返回与连接器类型对应的`Endpoint`对象。

1. 检索配置值。

   * 通过调用`Endpoint`对象的`getConfigParameters`方法，检索此端点中关联的配置值。 此方法返回`ConfigParameter`对象的数组。
   * 通过检索数组中的每个元素，检索有关每个配置值的信息。 每个元素都是`ConfigParameter`对象。 例如，可以通过调用`ConfigParameter`对象的`isRequired`方法来确定配置值是必需的还是可选的。 如果需要配置值，则此方法返回`true`。

**另请参阅**

[步骤摘要](programmatically-endpoints.md#summary-of-steps)

[快速入门：使用Java API检索端点连接器信息](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[包括AEM Forms Java库文件](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[设置连接属性](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
