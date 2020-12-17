---
title: AEM核心概念
seo-title: 基本信息
description: 概述AEM的结构化方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
seo-description: 概述AEM的结构化方式以及如何在其上进行开发的核心概念，包括了解JCR、Sling、OSGi、调度程序、工作流和MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: 28fdb57f51a5bd97ce78b626db86f4a59de6f0be
workflow-type: tm+mt
source-wordcount: '3386'
ht-degree: 0%

---


# AEM核心概念{#aem-core-concepts}

>[!NOTE]
>
>在深入探讨AEM的核心概念之前，Adobe建议完成[开发AEM Sites](/help/sites-developing/getting-started.md)文档中的WKND教程，了解AEM开发过程的概述和核心概念的简介。

## 在AEM{#prerequisites-for-developing-on-aem}上进行开发的先决条件

在AEM基础上进行开发需要以下技能：

* Web应用技术的基本知识，包括：

   * 请求——响应(XMLHttpRequest / XMLHttpResponse)循环
   * HTML
   * CSS
   * JavaScript

* Experience Server(CRX)（包括Content Explorer）的使用知识
* 在经典UI中进行开发时，还需要JSP(JavaServer Pages)的基本知识，包括理解和修改简单JSP示例的能力。

还建议您阅读并遵循[准则和最佳实践](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java内容存储库{#java-content-repository}

Java内容存储库(JCR)标准[JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)指定了一种独立于供应商和独立于实施的方式，用于在内容存储库中的粒度级别上双向访问内容。

Adobe研究公司（瑞士）AG持有规格线索。

[JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html)包，javax.jcr。&amp;ast;用于直接访问和操作存储库内容。

## Experience Server(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供AEM构建的Experience Services，可利用它构建自定义应用程序，并嵌入基于Jackrabbit的内容存储库。

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis是一个开放源，完全符合JCR API 2.0的实现。

## Sling请求处理{#sling-request-processing}

### Sling {#introduction-to-sling}简介

AEM是使用[Sling](https://sling.apache.org/site/index.html)构建的，这是一个基于REST原则的Web 应用程序框架，可轻松开发面向内容的应用程序。 Sling使用JCR存储库（如Apache Jackrabbit）或AEM（如果是）CRX内容存储库（如果是）作为其数据存储。 Sling已经为Apache Software Foundation贡献了力量——有关更多信息，请访问Apache。

使用Sling，要呈现的内容类型不是第一个处理考虑事项。 而主要考虑的是URL是否解析为内容对象，然后可以找到脚本来执行渲染。 这为Web内容作者提供了极好的支持，使他们能够轻松地根据自己的要求定制页面。

这种灵活性的优势在具有各种不同内容元素的应用程序中显而易见，或者在您需要可轻松自定义的页面时也显而易见。 特别是，在实施Web内容管理系统(如AEM解决方案中的WCM)时。

请参阅[在15分钟内发现Sling，了解使用Sling进行开发的最初步骤。](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)

下图说明了Sling脚本分辨率：它说明了如何从HTTP请求到内容节点、从内容节点到资源类型、从资源类型到脚本以及可以使用哪些脚本变量。

![了解Apache Sling脚本分辨率](assets/sling-cheatsheet-01.png)

下图说明了处理SlingPostServlet时可以使用的所有隐藏但功能强大的请求参数，SlingPostServlet是所有POST请求的默认处理函数，为您提供了在存储库中创建、修改、删除、复制和移动节点的无限选项。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以内容为中心{#sling-is-content-centric}

Sling是&#x200B;*以内容为中心的*。 这意味着，当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理将集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）
* 其次，表示或脚本与请求的某些部分（例如选择器和／或扩展）一起从资源属性中定位

### REST风格的Sling {#restful-sling}

由于以内容为中心的理念，Sling实现了面向REST的服务器，因此在Web应用程序框架中具有新的概念。 优点是：

* 非常RESTful，而不仅仅是表面；资源和表示形式在服务器内部正确建模
* 删除一个或多个数据模型

   * 以前需要：URL结构、业务对象、数据库模式;
   * 现在，它已简化为：URL =资源= JCR结构

### URL分解{#url-decomposition}

在Sling中，处理由用户请求的URL驱动。 这定义了要由相应脚本显示的内容。 为此，会从URL中提取信息。

如果我们分析以下URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我们可以把它分解成复合部分：

| 协议 | 主机 | 内容路径 | 选择器 | 扩展 |  | 后缀 |  | 参数 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具／间谍 | .printable.a4. | html | / | a/b | ? | x=12 |

**协** 议HTTP

**主** 机网站的名称。

**内容** 路径指定要呈现的内容的路径。与扩展结合使用；在此示例中，它们转换为tools/spy.html。

**选择器用** 于呈现内容的替代方法；在此示例中，打印机友好版本采用A4格式。

**** extensionContent格式；还指定要用于渲染的脚本。

**后** 缀可用于指定其他信息。

**参数是动** 态内容所需的任何参数。

#### 从URL到内容和脚本{#from-url-to-content-and-scripts}

使用以下原则：

* 映射使用从请求中提取的内容路径来查找资源
* 找到适当的资源后，将提取sling资源类型，并用于查找要用于渲染内容的脚本

下图说明了所使用的机制，将在以下各节中更详细地讨论该机制。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪个脚本渲染特定实体（通过在JCR节点中设置`sling:resourceType`属性）。 此机制比脚本访问数据实体（PHP脚本中的SQL语句可以）的优惠更自由，因为资源可以具有多个再现。

#### 将请求映射到资源{#mapping-requests-to-resources}

请求被分解并提取必要的信息。 系统会搜索存储库以查找所请求的资源（内容节点）:

* 首先，Sling检查节点是否存在于请求中指定的位置；例如，`../content/corporate/jobs/developer.html`
* 如果未找到节点，则会丢弃扩展，重复搜索；例如，`../content/corporate/jobs/developer`
* 如果找不到节点，则Sling将返回http代码404（找不到）。

Sling还允许JCR节点以外的其他资源，但这是一个高级功能。

### 查找脚本{#locating-the-script}

当找到相应的资源（内容节点）时，将提取&#x200B;**sling资源类型**。 这是一个路径，用于定位要用于呈现内容的脚本。

`sling:resourceType`指定的路径可以是：

* 绝对
* 相对，到配置参数

   相对路径是Adobe推荐的，因为它们提高了可移植性。

所有Sling脚本都存储在`/apps`或`/libs`的子文件夹中，按此顺序搜索（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

需要注意的其他几点是：

* 当需要“方法”(GET、POST)时，它将按照HTTP规范(如jobs.POST.esp)以大写形式指定（见下文）
* 支持各种脚本引擎：

   * HTL(HTML模板语言-Adobe Experience Manager首选的、推荐的HTML服务器端模板系统):`.html`
   * ECMAScript(JavaScript)页（服务器端执行）:`.esp, .ecma`
   * Java服务器页（服务器端执行）:`.jsp`
   * Java Servlet编译器（服务器端执行）:`.java`
   * JavaScript模板（客户端执行）:`.jst`

AEM的给定实例支持的脚本引擎列表列在Felix管理控制台(`http://<host>:<port>/system/console/slingscripting`)上。

此外，Apache Sling支持与其他流行脚本引擎（如Groovy、JRuby、Freemarker）的集成，并提供了集成新脚本引擎的方法。

使用上例，如果`sling:resourceType`为`hr/jobs`，则表示：

* GET/HEAD请求和以。html结尾的URL（默认请求类型，默认格式）

   脚本为/apps/hr/jobs/jobs.esp;sling:resourceType的最后一部分构成文件名。

* POST请求(除GET/HEAD外的所有请求类型，方法名称必须为大写)

   POST将用在脚本名称中。

   脚本将为`/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以。html结尾

   例如`../content/corporate/jobs/developer.pdf`

   脚本将为`/apps/hr/jobs/jobs.pdf.esp`;后缀将添加到脚本名称。

* 包含选择器的URL

   选择器可用于以替代格式显示相同的内容。 例如打印机友好版本、rss源或摘要。

   如果查看打印机友好版本，选择器可以是&#x200B;*print*;as in `../content/corporate/jobs/developer.print.html`

   脚本将为`/apps/hr/jobs/jobs.print.esp`;选择器将添加到脚本名称。

* 如果未定义sling:resourceType，则：

   * 内容路径将用于搜索相应的脚本（如果基于路径的ResourceTypeProvider处于活动状态）。

      例如，`../content/corporate/jobs/developer.html`的脚本将在`/apps/content/corporate/jobs/`中生成搜索。

   * 将使用主节点类型。

* 如果根本找不到脚本，则将使用默认脚本。

   默认再现当前支持为纯文本(.txt)、HTML(.html)和JSON(.json)，所有这些都将列表节点的属性（格式合适）。 扩展名。res（或无请求扩展名的请求）的默认演绎版用于假设资源（如果可能）。
* 对于http错误处理（代码403或404）,Sling将在以下位置中查找脚本：

   * [自定义脚本](/help/sites-developing/customizing-errorhandler-pages.md)的位置/apps/sling/servlet/errorhandler
   * 或标准脚本的位置(分别为/libs/sling/servlet/errorhandler/403.esp或404.esp)。

如果多个脚本应用于给定请求，则选择具有最佳匹配项的脚本。 比赛越具体，越好；换言之，无论请求扩展名或方法名称是否匹配，选择器越多匹配越好。

例如，考虑访问资源的请求
`/content/corporate/jobs/developer.print.a4.html`
类型
`sling:resourceType="hr/jobs"`

假设我们在正确的位置具有以下脚本列表:

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

优先顺序为(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除资源类型（主要由`sling:resourceType`属性定义）外，还有资源超类型。 这通常由`sling:resourceSuperType`属性指示。 在尝试查找脚本时，也会考虑这些超类型。 资源超级类型的优势在于，它们可以构成资源的层次结构，其中默认资源类型`sling/servlet/default`（由默认servlet使用）实际上是根。

资源的资源超类型可以通过两种方式进行定义：

* 按资源的`sling:resourceSuperType`属性。
* 由`sling:resourceType`指向的节点的`sling:resourceSuperType`属性。

例如：

* /

   * 某个 
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




类型层次结构：

* `/x`
   * 是 `[ c, b, a, <default>]`
* while for `/y`
   * 层次结构为`[ c, a, <default>]`

这是因为`/y`具有`sling:resourceSuperType`属性，而`/x`没有，因此其超类型从其资源类型中获取。

#### 无法直接调用Sling脚本{#sling-scripts-cannot-be-called-directly}

在Sling中，无法直接调用脚本，因为这会破坏REST服务器的严格概念；您可以混合资源和演示。

如果您直接调用表示法（脚本），则将资源隐藏在脚本中，因此框架(Sling)不再了解它。 因此，您会丢失某些功能：

* 自动处理GET以外的http方法，包括：

   * POST、PUT、DELETE，使用sling默认实现处理
   * sling:resourceType位置中的`POST.jsp`脚本

* 您的代码架构不再像原来那样清晰、结构清晰；对于大规模开发至关重要

### Sling API {#sling-api}

它使用Sling API包org.apache.sling。&amp;ast；和标记库。

### 使用sling:include {#referencing-existing-elements-using-sling-include}引用现有元素

最后需要参考脚本中的现有元素。

更复杂的脚本（聚合脚本）可能需要访问多个资源(例如导航、提要栏、页脚、列表元素)，并通过包括&#x200B;*资源*&#x200B;来实现。

要执行此操作，您可以使用sling:include(&quot;/&lt;path>/&lt;resource>&quot;)命令。 这将有效地包括引用资源的定义，如以下语句中的定义，该语句引用渲染图像的现有定义：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定义了用于开发和部署模块化应用程序和库的架构（也称为Dynamic Module System for Java）。 OSGi容器允许您将应用程序分为多个单个模块（它们是带有附加元信息的jar文件，在OSGi术语中称为绑定），并通过以下方式管理它们之间的交叉依赖关系：

* 在该容器内实施的服务
* 容器与您的应用程序之间的合同

这些服务和合同提供了一种使单个元素能够动态发现彼此以进行协作的架构。

然后，OSGi框架将您动态加载／卸载、配置和控制这些包，无需重新启动。

>[!NOTE]
>
>有关OSGi技术的完整信息，请访问[OSGi网站](https://www.osgi.org)。
>
>特别是，他们的“基础教育”页面包含一系列演示和教程。

此体系结构允许您使用特定于应用程序的模块扩展Sling。 Sling，因此CQ5使用OSGI（Open Services Gateway计划）的[Apache Felix](https://felix.apache.org/)实施，并基于OSGi Service Platform Release 4 Version 4.2规范。 它们都是在OSGi框架中运行的OSGi捆绑包的集合。

这样，您就可以对安装中的任何包执行以下操作：

* 安装
* 开始
* 停止
* 更新
* 卸载
* 查看当前状态
* 访问有关特定包的更多详细信息（如符号名称、版本、位置等）

有关详细信息，请参阅[Web控制台](/help/sites-deploying/web-console.md)、[OSGI配置](/help/sites-deploying/configuring-osgi.md)和[OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

## AEM环境{#development-objects-in-the-aem-environment}中的开发对象

以下是对发展感兴趣的内容：

**项** 目项是节点或属性。

有关操作Item对象的详细信息，请参阅接口javax.jcr.Item的[Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html)

**节点（及其属性）** 节点及其属性在JCR API 2.0规范(JSR 283)中定义。他们存储内容、对象定义、渲染脚本和其他数据。

节点定义内容结构，其属性存储实际内容和元数据。

内容节点驱动渲染。 Sling从传入请求中获取内容节点。 此节点的属性sling:resourceType指向要使用的Sling渲染组件。

节点是JCR名称，在Sling环境中也称为资源。

例如，要获取当前节点的属性，您可以在脚本中使用以下代码：

`PropertyIterator properties = currentNode.getProperties();`

将currentNode作为当前节点对象。

有关操作Node对象的详细信息，请参阅[Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**构** 件在AEM中，所有用户输入由构件管理。它们通常用于控制内容的编辑。

对话框通过组合构件来构建。

AEM已使用构件的ExtJS库进行开发。

**对** 话框对话框是一种特殊类型的构件。

要编辑内容，AEM使用由应用程序开发人员定义的对话框。 这些组件组合了一系列构件，向用户显示编辑相关内容所需的所有字段和操作。

对话框还用于编辑元数据和各种管理工具。

**组** 件软件组件是提供预定义服务或事件并能够与其他组件通信的系统组件。

在AEM中，组件通常用于呈现资源的内容。 当资源是页面时，呈现该资源的组件称为顶级组件或页面组件。 但是，组件不必呈现内容，也不必链接到特定资源；例如，导航组件将显示有关多个资源的信息。

组件的定义包括：

* 用于呈现内容的代码
* 用户输入和结果内容的配置对话框。

**模** 板模板是特定类型页面的基础。在“网站”选项卡中创建页面时，用户必须选择模板。 然后，通过复制此模板来创建新页面。

模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。

它定义用于呈现页面的页面组件和默认内容（主要顶级内容）。 内容定义了如何呈现AEM以内容为中心。

**页面组件（顶级组件）** 要用于呈现页面的组件。

**页** 面页面是模板的“实例”。

页面具有cq:Page类型的层次结构节点和cq:PageContent类型的内容节点。 内容节点的属性sling:resourceType指向用于呈现页面的页面组件。

例如，要获取当前页面的名称，您可以在脚本中使用以下代码：

S`tring pageName = currentPage.getName();`

将currentPage设置为当前页面对象。 有关处理页面对象的详细信息，请参阅[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)。

**页面** 管理器页面管理器是一个界面，它提供页面级别操作的方法。

例如，要获取资源的包含页面，您可以在脚本中使用以下代码：

页面myPage = pageManager.getContainingPage(myResource);

将pageManager作为页面管理器对象，将myResource作为资源对象。 有关页面管理器提供的方法的详细信息，请参阅[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 存储库{#structure-within-the-repository}中的结构

以下列表概述了在存储库中将看到的结构。

>[!CAUTION]
>
>应谨慎更改此结构或其中的文件。
>
>进行开发时需要进行更改，但您应确保完全了解所做的任何更改的含义。

>[!CAUTION]
>
>不得更改`/libs`路径中的任何内容。 对于配置和其他更改，将项目从`/libs`复制到`/apps`，并在`/apps`中进行任何更改。

* `/apps`

   与应用程序相关；包括特定于您的网站的组件定义。 您开发的组件可以基于`/libs/foundation/components`提供的现成组件。

* `/content`

   为您的网站创建的内容。

* `/etc`

* `/home`

   用户和组信息。

* `/libs`

   属于AEM核心的库和定义。 `/libs`中的子文件夹表示现成的AEM功能，例如搜索或复制。 不应修改`/libs`中的内容，因为它影响AEM的工作方式。 网站特有的功能应在`/apps`下开发（请参阅[自定义组件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

* `/tmp`

   临时工作区。

* `/var`

   系统更改和更新的文件；如审计日志、统计、事件处理。 子文件夹`/var/classes`包含源和编译表单中的java servlet，这些表单是从组件脚本生成的。

## 环境 {#environments}

对于AEM，生产环境通常由两种不同类型的实例组成：[作者实例和发布实例](/help/sites-deploying/deploy.md#author-and-publish-installs)。

## 调度程序{#the-dispatcher}

调度程序是Adobe的缓存和／或负载平衡工具。 在[调度程序](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)下可以找到更多信息。

## FileVault（源修订系统）{#filevault-source-revision-system}

FileVault为您的JCR存储库提供文件系统映射和版本控制。 它可用于管理AEM开发项目，并完全支持在标准版控制系统（例如，Subversion）中存储和版本化项目代码、内容、配置等。

有关详细信息，请参阅[FileVault工具](/help/sites-developing/ht-vlttool.md)文档。

## 工作流 {#workflows}

您的内容通常受组织流程的约束，包括由不同参加者批准和注销等步骤。 这些过程可以表示为工作流，在AEM](/help/sites-developing/workflows-models.md)中定义和开发[，然后根据需要应用于[适当的内容页面](/help/sites-administering/workflows.md)或[数字资产](/help/assets/assets-workflow.md)。

该工作流引擎用于管理工作流的实施及其后对内容的应用。

## 多站点管理{#multi-site-management}

多站点管理器(MSM)使您能够轻松管理共享公共内容的多个网站。 MSM允许您定义站点之间的关系，以便在一个站点中的内容更改自动复制到其他站点中。

例如，网站通常以多种语言为国际受众提供。 当同一语言的站点数量较少（三到五个）时，可以手动跨站点同步内容。 但是，只要站点数量增加或涉及多种语言，自动化流程就会变得更高效。

* 有效管理网站的不同语言版本。
* 根据源站点自动更新一个或多个站点：

   * 强制实施通用的基本结构并跨多个站点使用通用内容。
   * 最大限度地利用可用资源。
   * 保持相同的外观。
   * 将精力集中在管理不同站点之间不同的内容上。

有关详细信息，请参阅[多站点管理器](/help/sites-administering/msm.md)。