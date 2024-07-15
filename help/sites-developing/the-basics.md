---
title: AEM核心概念
description: 概述了Adobe Experience Manager (AEM)的结构以及如何在此基础上进行开发的核心概念，包括了解JCR、Sling、OSGi、Dispatcher、工作流和MSM。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 0%

---

# AEM核心概念 {#aem-core-concepts}

>[!NOTE]
>
>在介绍Adobe Experience Manager (AEM)的核心概念之前，Adobe建议完成[AEM Sites开发入门](/help/sites-developing/getting-started.md)文档中的WKND教程。 它包括AEM开发过程的概述以及核心概念的简介。

## 在AEM上进行开发的先决条件 {#prerequisites-for-developing-on-aem}

您需要具备以下技能才能在AEM的基础上进行开发：

* Web应用程序技术的基本知识，包括：

   * request -response (XMLHttpRequest / XMLHttpResponse)循环
   * HTML
   * CSS
   * JavaScript

* 具有Experience Server (CRX)的工作知识，包括Content Explorer
* 对于在经典UI中进行开发，还需要JSP的基础知识(JavaServer Pages)，包括理解和修改简单JSP示例的能力。

还建议您阅读并遵循[准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java™内容存储库 {#java-content-repository}

Java™ Content Repository (JCR)标准[JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)指定了一种独立于供应商且独立于实施的方法，用于在内容存储库内的粒度级别双向访问内容。

规范主管由Adobe研究（瑞士） AG担任。

[JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html)包，javax.jcr。&amp;amp；ast；用于直接访问和处理存储库内容。

## Experience Server (CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供了AEM所基于的、可用于构建自定义应用程序的Experience Services ，并嵌入了基于Jackrabbit的内容存储库。

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html)是一个完全符合JCR API 2.0的开放源代码。

## Sling请求处理 {#sling-request-processing}

### Sling简介 {#introduction-to-sling}

AEM是使用[Sling](https://sling.apache.org/index.html)构建的，这是一个基于REST原则的Web应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（例如Apache Jackrabbit）或者CRX内容存储库(如果存在AEM)作为其数据存储。 Sling已加入到Apache Software Foundation — 有关详细信息，请访问Apache。

使用Sling时，要呈现的内容类型不是第一个处理注意事项。 相反，主要考虑的问题是URL是否解析为内容对象，然后可以找到该内容对象的脚本来执行渲染。 这为Web内容作者提供了极佳的支持，使他们能够根据自己的需求轻松自定义页面。

在包含各种不同内容元素的应用程序中，或者在您需要可以轻松自定义的页面时，这种灵活性的优势非常明显。 特别是在AEM解决方案中实施Web内容管理系统（如WCM）时。

有关使用Sling进行开发的第一步，请参阅[在15分钟内发现Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)。

下图说明了Sling脚本解析。 它显示了如何从HTTP请求获取到内容节点、从内容节点获取到资源类型、从资源类型获取到脚本，以及提供了哪些脚本变量。

![了解Apache Sling脚本解析](assets/sling-cheatsheet-01.png)

下图说明了可在处理SlingPostServlet时使用的所有隐藏的强大请求参数。 它包括所有POST请求的默认处理程序，可为您提供用于在存储库中创建、修改、删除、复制和移动节点的无限选项。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心 {#sling-is-content-centric}

Sling以&#x200B;*内容为中心*。 这意味着处理侧重于内容，因为每个(HTTP)请求都映射到JCR资源（存储库节点）形式的内容：

* 第一个目标是保存内容的资源（JCR节点）
* 第二，表示法或脚本从与请求的某些部分（例如，选择器和/或扩展）组合的资源属性中定位

### RESTful Sling {#restful-sling}

由于以内容为中心的理念，Sling实施了面向REST的服务器，从而在Web应用程序框架中引入了新概念。 其优点是：

* RESTful，而不仅仅是在曲面上；资源和表示在服务器内正确建模
* 删除一个或多个数据模型

   * 以前需要用到的URL结构、业务对象、数据库架构；
   * 现在简化为： URL =资源= JCR结构

### URL分解 {#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这会定义相应脚本要显示的内容。 为此，将从URL中提取信息。

如果您分析以下URL：

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

您可以将它分解为其复合部分：

| 协议 | 主机 | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/间谍 | .printable.a4. | html | / | a/b | ? | x=12 |

**协议** HTTP

**主机**&#x200B;网站的名称。

**内容路径**&#x200B;指定要渲染的内容的路径。 与扩展一起使用。 在此示例中，它们将转换为`tools/spy.html`。

**选择器**&#x200B;用于呈现内容的替代方法；在此示例中，使用A4格式的打印机友好版本。

**扩展**&#x200B;内容格式；还指定要用于渲染的脚本。

**后缀**&#x200B;可用于指定其他信息。

**参数**&#x200B;动态内容所需的任何参数。

#### 从URL到内容和脚本 {#from-url-to-content-and-scripts}

使用以下原则：

* 映射使用从请求提取的内容路径来定位资源
* 找到相应的资源后，将提取sling资源类型，并用于定位要用于呈现内容的脚本

下图说明了所使用的机制，下节将对此进行更详细的讨论。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪个脚本呈现特定实体（通过在JCR节点中设置`sling:resourceType`属性）。 此机制提供的自由度比脚本访问数据实体的自由度要多（PHP脚本中的SQL语句就是这样），因为资源可以具有多个格式副本。

#### 将请求映射到资源 {#mapping-requests-to-resources}

对请求进行细分，提取出必要的信息。 在存储库中搜索请求的资源（内容节点）：

* 第一个Sling检查请求中指定的位置是否存在节点；例如，`../content/corporate/jobs/developer.html`
* 如果未找到节点，则将丢弃该扩展并重复搜索；例如，`../content/corporate/jobs/developer`
* 如果未找到节点，则Sling返回http代码404（未找到）。

Sling还允许将JCR节点以外的内容作为资源，但这是一项高级功能。

### 查找脚本 {#locating-the-script}

找到相应的资源（内容节点）后，将提取&#x200B;**sling资源类型**。 这是一个路径，用于查找要用于呈现内容的脚本。

`sling:resourceType`指定的路径可以是：

* 绝对
* 相对于配置参数

  随着相对路径的可移植性提高，Adobe会推荐这些路径。

所有Sling脚本都存储在`/apps`或`/libs`的子文件夹中，并按此顺序搜索（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

其他几点需要注意的是：

* 当需要方法(GET、POST)时，将根据HTTP规范(例如jobs.POST.esp)以大写形式指定（见下文）
* 支持各种脚本引擎：

   * HTL(HTML模板语言 — Adobe Experience Manager首选和推荐的用于HTML的服务器端模板系统)： `.html`
   * ECMAScript (JavaScript)页面（服务器端执行）： `.esp, .ecma`
   * Java™服务器页面（服务器端执行）： `.jsp`
   * Java™ Servlet编译器（服务器端执行）： `.java`
   * JavaScript模板（客户端执行）： `.jst`

Felix管理控制台(`http://<host>:<port>/system/console/slingscripting`)上列出了给定的AEM实例支持的脚本引擎列表。

此外，Apache Sling支持与其他常用脚本引擎（例如，Groovy、JRuby、Freemarker）集成，并提供了一种集成新脚本引擎的方法。

在上例中，如果`sling:resourceType`为`hr/jobs`，则：

* 以.html结尾的GET/HEAD请求和URL（默认请求类型，默认格式）

  脚本为/apps/hr/jobs/jobs.esp；sling：resourceType的最后一个部分构成了文件名。

* POST请求(除GET/HEAD之外的所有请求类型，方法名称必须大写)

  POST在脚本名称中使用。

  脚本为`/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以.html结尾

  例如，`../content/corporate/jobs/developer.pdf`

  脚本为`/apps/hr/jobs/jobs.pdf.esp`；后缀已添加到脚本名称中。

* 带有选择器的URL

  选择器可用于以替代格式显示相同的内容。 例如，打印机友好版本、RSS馈送或摘要。

  如果您查看打印机友好版本，该版本中的选择器可以是&#x200B;*print*，如`../content/corporate/jobs/developer.print.html`

  脚本为`/apps/hr/jobs/jobs.print.esp`；选择器已添加到脚本名称中。

* 如果未定义sling：resourceType ，则：

   * 内容路径用于搜索适当的脚本（如果基于路径的ResourceTypeProvider处于活动状态）。

     例如，`../content/corporate/jobs/developer.html`的脚本将在`/apps/content/corporate/jobs/`中生成搜索。

   * 使用主节点类型。

* 如果未找到脚本，则使用默认脚本。

  默认演绎版支持纯文本(.txt)、HTML(.html)和JSON (.json)，所有这些都列出了节点的属性（格式适当）。 扩展名.res或不带请求扩展名的请求的默认演绎版是假脱机资源（如果可能）。
* 对于http错误处理（代码403或404），Sling会在以下位置查找脚本：

   * [自定义脚本](/help/sites-developing/customizing-errorhandler-pages.md)的/apps/sling/servlet/errorhandler位置
   * 或标准脚本/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果给定请求应用了多个脚本，则会选择具有最佳匹配的脚本。 匹配项越具体，其效果就越好；换句话说，无论请求扩展名或方法名称是否匹配，选择器越匹配越好。

例如，考虑访问资源的请求
`/content/corporate/jobs/developer.print.a4.html`
类型
`sling:resourceType="hr/jobs"`

假设您在正确的位置拥有以下脚本列表：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

则优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了资源类型（主要由`sling:resourceType`属性定义）之外，还有资源超级类型。 这由`sling:resourceSuperType`属性指示。 在尝试查找脚本时，也会考虑这些超类型。 资源超级类型的优点在于，它们可以形成资源的层次结构，其中默认资源类型`sling/servlet/default`（由默认servlet使用）有效地作为根。

可以通过两种方式定义资源的资源超级类型：

* 按资源的`sling:resourceSuperType`属性。
* `sling:resourceType`指向的节点的`sling:resourceSuperType`属性。

例如：

* /

   * a
   * b

      * sling：resourceSuperType = a

   * c

      * sling：resourceSuperType = b

   * x

      * sling：resourceType = c

   * y

      * sling：resourceType = c
      * sling：resourceSuperType = a

类型层次结构：

* `/x`
   * 为`[ c, b, a, <default>]`
* 当`/y`时
   * 层次结构为`[ c, a, <default>]`

这是因为`/y`具有`sling:resourceSuperType`属性，而`/x`没有，因此其超类型取自其资源类型。

#### 无法直接调用Sling脚本 {#sling-scripts-cannot-be-called-directly}

在Sling中，无法直接调用脚本，因为这会破坏REST服务器的严格概念；您将混合使用资源和表示法。

如果直接调用表示形式（脚本），则会在脚本中隐藏资源，因此框架(Sling)不再知道该表示形式。 因此，您将失去某些特征：

* 自动处理GET以外的http方法，包括：

   * 使用sling默认实现处理的POST、PUT、DELETE
   * sling：resourceType位置中的`POST.jsp`脚本

* 您的代码架构不再像以前那样干净或结构清晰；这对于大规模开发至关重要

### Sling API {#sling-api}

这会使用Sling API包org.apache.sling。&amp;amp；ast；和标记库。

### 使用sling：include引用现有元素 {#referencing-existing-elements-using-sling-include}

最后需要考虑的是需要引用脚本中的现有元素。

更复杂的脚本（聚合脚本）必须访问多个资源（例如，导航、侧栏、页脚、列表元素），并通过包含&#x200B;*资源*&#x200B;来实现此目的。

为此，请使用sling：include(&quot;/&lt;path>/&lt;resource>&quot;)命令。 这实际上包括引用的资源的定义，如下面的语句所示，该语句引用用于渲染图像的现有定义：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定义了一种用于开发和部署模块化应用程序和库的架构(也称为“适用于Java™的动态模块系统”)。 通过OSGi容器，您可以将应用程序划分为单独的模块（这些模块是包含其他元信息的jar文件，在OSGi术语中称为捆绑包），并通过以下方式管理它们之间的交叉依赖关系：

* 在容器中实现的服务
* 容器与您的应用程序之间的合同

这些服务和合同提供了一个体系结构，使各个元素能够动态地发现彼此进行协作。

然后，OSGi框架为您提供这些捆绑包的动态加载/卸载、配置和控制 — 无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问[OSGi网站](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此架构允许您通过应用程序特定的模块扩展Sling。 Sling和CQ5使用OSGI （开放服务网关计划）的[Apache Felix](https://felix.apache.org/documentation/index.html)实现并基于OSGi Service Platform 4.2版规范。 它们都是在OSGi框架内运行的OSGi捆绑包的集合。

这使您能够对安装中的任何软件包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看状态
* 访问有关特定捆绑包的更多详细信息（例如，符号名称、版本和位置）

有关详细信息，请参阅[Web控制台](/help/sites-deploying/web-console.md)、[OSGI配置](/help/sites-deploying/configuring-osgi.md)和[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

## AEM环境中的开发对象 {#development-objects-in-the-aem-environment}

以下内容对开发很有帮助：

**项**&#x200B;项是节点或属性。

有关处理Item对象的详细信息，请参阅接口javax.jcr.Item的[Java™文档](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html)

**节点（及其属性）**&#x200B;节点及其属性在JCR API 2.0规范(JSR 283)中定义。 它们存储内容、对象定义、渲染脚本和其他数据。

节点定义内容结构，其属性存储实际内容和元数据。

内容节点驱动渲染。 Sling从传入请求获取内容节点。 此节点的属性sling：resourceType指向要使用的Sling渲染组件。

在Sling环境中，节点（一个JCR名称）也称为资源。

例如，要获取当前节点的属性，您可以在脚本中使用以下代码：

`PropertyIterator properties = currentNode.getProperties();`

当前节点对象为currentNode。

有关处理Node对象的详细信息，请参阅[Java™文档](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**小组件**&#x200B;在AEM中，所有用户输入都由小组件管理。 这些通常用于控制内容的编辑。

对话框通过组合构件来构建。

AEM是使用ExtJS构件库开发的。

**对话框**&#x200B;对话框是一种特殊类型的构件。

要编辑内容，AEM会使用应用程序开发人员定义的对话框。 这些组件组合了一系列构件，向用户展示编辑相关内容所需的所有字段和操作。

对话框也用于编辑元数据和各种管理工具。

**组件**&#x200B;软件组件是一个系统元素，它提供预定义的服务或事件，并能与其他组件通信。

在AEM中，组件通常用于呈现资源的内容。 当资源是页面时，呈现它的组件称为顶级组件或页面组件。 但是，组件不必呈现内容，也不必链接到特定资源。 例如，导航组件显示有关多个资源的信息。

组件的定义包括以下内容：

* 用于呈现内容的代码
* 用于用户输入和配置结果内容的对话框。

**模板**&#x200B;模板是特定类型页面的基础。 在网站选项卡中创建页面时，用户必须选择模板。 然后，通过复制此模板创建新页面。

模板是一种节点层次结构，与要创建页面的结构相同，但没有任何实际内容。

它定义用于呈现页面的页面组件和默认内容（主要顶级内容）。 内容定义其呈现方式，因为AEM以内容为中心。

**页面组件（顶级组件）**&#x200B;要用于呈现页面的组件。

**页面**&#x200B;页面是模板的“实例”。

页面具有类型为cq：Page的层次结构节点和类型为cq：PageContent的内容节点。 内容节点的属性sling：resourceType指向用于呈现页面的页面组件。

例如，要获取当前页面的名称，您可以在脚本中使用以下代码：

S`tring pageName = currentPage.getName();`

TcurrentPage是当前页面对象。 有关处理页面对象的详细信息，请参阅[Java™文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)。

**页面管理器**&#x200B;页面管理器是一个提供页面级操作方法的界面。

例如，要获取资源的包含页面，您可以在脚本中使用以下代码：

页面myPage = pageManager.getContainingPage(myResource)；

pageManager是页面管理器对象，myResource是资源对象。 有关页面管理器所提供方法的详细信息，请参阅[Java™文档](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 存储库中的结构 {#structure-within-the-repository}

以下列表概述了您在存储库中看到的结构。

>[!CAUTION]
>
>对此结构或其中的文件进行更改时应当谨慎。
>
>在开发时需要更改，但是您应该注意要完全了解所做任何更改的影响。

>[!CAUTION]
>
>请勿更改`/libs`路径中的任何内容。 对于配置和其他更改，请将项目从`/libs`复制到`/apps`，并在`/apps`内进行任何更改。

* `/apps`

  与应用程序相关；包括特定于您网站的组件定义。 您开发的组件可以基于`/libs/foundation/components`提供的现成组件。

* `/content`

  为您的网站创建的内容。

* `/etc`

* `/home`

  用户和组信息。

* `/libs`

  属于AEM核心的库和定义。 `/libs`中的子文件夹表示现成的AEM功能，如搜索或复制。 不应修改`/libs`中的内容，因为它影响AEM的工作方式。 应在`/apps`下开发特定于您网站的功能（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

* `/tmp`

  临时工作区。

* `/var`

  系统更改和更新的文件；例如审核日志、统计数据、事件处理。

## 环境 {#environments}

使用AEM时，生产环境通常包含两种不同类型的实例： [创作实例和Publish实例](/help/sites-deploying/deploy.md#author-and-publish-installs)。

## Dispatcher {#the-dispatcher}

Dispatcher是Adobe用于缓存和/或负载平衡的工具。 可在[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)下找到更多信息。

## FileVault（源修订版系统） {#filevault-source-revision-system}

FileVault为JCR存储库提供文件系统映射和版本控制。 它可用于管理AEM开发项目，完全支持在标准版本控制系统（例如，Subversion）中存储和版本控制项目代码、内容、配置等。

有关详细信息，请参阅[FileVault工具](/help/sites-developing/ht-vlttool.md)文档。

## 工作流 {#workflows}

您的内容通常受组织流程约束，包括各个参与者的批准和签署等步骤。 这些进程可以表示为在AEM](/help/sites-developing/workflows-models.md)中定义和开发的[工作流，然后根据需要应用于[适当的内容页面](/help/sites-administering/workflows.md)或[数字资产](/help/assets/assets-workflow.md)。

工作流引擎用于管理工作流的实施，以及工作流对内容的后续应用程序。

## 多站点管理 {#multi-site-management}

多站点管理器(MSM)使您能够轻松管理共享公共内容的多个网站。 MSM允许您定义站点之间的关系，以便将一个站点中的内容更改自动复制到其他站点。

例如，通常以多种语言为国际受众提供网站。 当使用相同语言的网站数量较少（三到五）时，可以手动执行跨网站同步内容的过程。 但是，当站点的数量增加或涉及多种语言时，自动化该过程会变得更加高效。

* 高效地管理网站的不同语言版本。
* 根据源站点自动更新一个或多个站点：

   * 实施通用的基础结构并在多个站点间使用通用内容。
   * 最大限度地利用可用资源。
   * 保持统一的外观和风格。
   * 将工作重点放在管理不同站点之间的内容上。

有关详细信息，请参阅[多站点管理器](/help/sites-administering/msm.md)。
