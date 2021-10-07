---
title: 参与AEM
seo-title: Contributing to AEM
description: AEM的开发遵循大型开源项目中常用的行之有效的方法
seo-description: AEM is developed following proven methodologies commonly practiced in large open source projects
uuid: ffef60ae-8a9a-4c4b-8cbd-3cd72792a42e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f52402df-f6dc-4c62-82bc-cbce489b2b74
exl-id: 43fb4fa3-269a-4635-b055-4b7d787da21f
source-git-commit: 2bae11eafb875f01602c39c0dba00a888e11391a
workflow-type: tm+mt
source-wordcount: '2709'
ht-degree: 1%

---

# 参与AEM{#contributing-to-aem}

## 开发方法 {#development-methodology}

AEM是按照在大型开源项目中常用的行之有效的方法开发的。 事实上，AEM技术堆栈中的许多核心元素都作为活动的开源项目进行维护，例如Sling和Jackrabbit，这些项目对Apache Software Foundation做出了贡献。 AEM中展现的这一精神的一个重要方面是鼓励您利用可用的邮寄列表和在线论坛与开发团队进行直接交互。

如果您要为AEM的组件提供内容，则应该像向开源项目提供内容一样熟悉AEM，并像您打算向此类项目提供内容一样与现有核心团队进行沟通。

## 所需体验 {#required-experience}

超文本传输协议(HTTP)是我们所做所有工作的核心。 因此，在参与AEM之前，您应该对HTTP有深入的了解，理想的是，您应该能够使用线程池编写自己的多线程HTTP服务器Java实施。 您还应该了解HTTP/1.1保持活动状态的行为，并且应该对与JavaScript的服务器/客户端交互(尤其是AJAX表示的异步交互样式)有深入的了解。

由于页面动态性和交互式内容是WM体验的关键，因此您必须对文档对象模型及其在响应事件时进行编程操作的潜力有相当深入的了解。 您应该了解一些相关知识，例如，对多个浏览器文档（例如，使用iFrame）进行实时DOM操作和拖放行为。

那么，在最高级别上，您应该对以下内容有充分的了解：

* [HTTP/1.1协议](https://www.ietf.org/rfc/rfc2616.txt)
* HTML(最好[HTML5](https://dev.w3.org/html5/spec/Overview.html))
* 层叠样式表
* 可扩展标记语言(XML)
* 异步JavaScript和XML(AJAX)设计模式
* JavaScript对象表示法(JSON)
* 文档对象模型
* 状态交互与无状态交互
* [统一资源标识符](https://www.ietf.org/rfc/rfc2396.txt)
* 浏览器Cookie
* 和其他现代Web开发概念

Adobe Experience Manager的技术堆栈基于具有[Apache Sling](https://sling.apache.org/site/index.html) Web框架的[Apache Felix](https://felix.apache.org/) OSGI容器，并嵌入基于[Apache Jackrabbit](https://jackrabbit.apache.org/jcr-api.html)的Java内容存储库([JCR](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/index.html))。 您应该熟悉这些单独的项目，以及您打算贡献内容的区域中使用的任何其他开源组件（例如Apache Lucene）。

## 部落知识 {#tribal-knowledge}

某些概念和指导原则深深地植根于前日文化中。 本节列出了您应注意的一些“深层嵌入DNA”的问题。

### 一切都是内容 {#everything-is-content}

内容不仅包括Web应用程序保留的所有数据。 程序代码、库、脚本、模板、HTML、CSS、图像和各种对象、任何内容和所有内容将保留在内容存储库中，并通过包管理器和包共享以包的形式导入/导出。

### 大卫模型 {#david-s-model}

在Java内容存储库中建模内容的方式，需要一种与软件行业中在关系世界中进行数据建模的常见做法完全不同的思维方式。 对于任何内容管理新人而言，JCR方式都是[David的模型：内容建模指南](https://wiki.apache.org/jackrabbit/DavidsModel)。

### RESTurency {#restfulness}

REST方法深深地植根于我们的工作中。 这意味着，除其他外，避免有状态的交互，并记住URI是内容和服务的明确地址。

REST(REpresentational State Transfer)是指万维网所基于的软件体系结构样式。 它描述了使Web工作的关键要素，因此为如何设计基于Web的软件提供了一套原则。 因此，在设计要在Web上使用的API时，遵循这些“最佳实践”是明智的。

由于REST为我们所做的许多工作提供了指导性理念，因此您应该认为，熟悉RESTful设计的原则至关重要。 一个很好的入手点是[Roy Fielding的论文](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)。

### Sling请求解决方案 {#sling-request-resolution}

要了解AEM的一个关键方面是：传入请求如何与内容和应用程序行为相关联，内容存储库中内容的结构如何，以及AEM在何处查找应用程序逻辑以处理请求。 了解Apache [Sling URL分解](https://sling.apache.org/site/url-decomposition.html)以及其强制实施REST体系结构样式及其无状态、可缓存和分层系统约束的方式。

要了解Apache Sling请求解决方案的关键方面包括：请求如何主要映射到内容存储库中的特定资源、请求的其他属性以及这些内容对象的属性如何确定将调用哪个应用程序代码来渲染内容，以及/apps中的代码如何覆盖/libs中的代码。

### 快速入门 {#quickstart}

没有步骤三：要安装和运行，只需下载并双击快速入门JAR文件即可。 没有步骤三。 任何其他可选功能只需从包共享中安装相应的包即可。

较小的快速启动大小：请至少保持快速入门JAR文件的大小。 智能、优化地使用库，将可选功能移动到包共享中。

更快的启动时间：当您做出可能影响启动时间的更改时，请确保缩短，而不是延长。

### 精益与均等 {#lean-and-mean}

我们支持轻量、小、快、雅的代码和项目。 “够好”还不够。

代码重用：我们基于OSGi的产品体系结构和“一切都是内容”的理念意味着我们有异常好的机会重复使用代码和工件。 我们尽量利用这一事实来保持特点简洁和中庸。

松耦合：我们更青睐松散耦合的互动，而非紧紧的依赖和“不受欢迎的亲密”。 松耦合还可以实现更多代码重用。

### 不要破坏演示 {#don-t-break-the-demo}

熟悉演示脚本和产品功能，这些脚本和产品功能最常在演示中显示。 请至少了解，您不应该破坏“演示脚本”功能。 核心产品应始终为演示做好准备，即使在开发过程中也是如此。

### 可靠性设计 {#design-for-reliability}

我们努力以失败软方式设计和编码功能，以便（例如）单个DOM元素的问题不会导致整个页面无法呈现。 换句话说：制造应该致命的东西。 让其他一切都能活下来。 让产品“原谅”。

### 异常是新常态 {#abnormal-is-the-new-normal}

不要依赖关闭挂钩，确保启动时进行清理。 异常终止是正常终止。

`shutdown == kill -9 == power outage`

### 准备好进行弹性聚类 {#be-ready-for-elastic-clustering}

始终准备进行弹性聚类，始终假定存在聚类。 通常，遵守内容存储库中的所有内容意味着内置群集支持。

### 面向后向兼容性的设计 {#design-for-backward-compatibility}

您不应该破坏客户的旧代码。 请仅考虑`/libs`以包含可在升级期间更新的产品代码。 存储库的`/apps`部分是项目代码，而`/etc`部分包含需要保留的自定义配置。 通常，不要覆盖`/apps`、`/content`和`/home`中的任何内容。 升级后，旧项目代码、配置和内容应继续正常运行，这些操作与升级前的操作一样。

为向后兼容性进行设计还可确保升级体验与初始安装的简单性相匹配。 只需停止AEM、替换快速入门JAR文件并再次启动AEM即可。 随着安装基础的快速增长，升级效率将日益成为一项重要优势。

虽然现有API在较新版本时可以也应该标记为已弃用，但功能更好的API取代了它们，但在之前5.x版本中公开的所有API都需要保持正常运行，因为它们可能正在自定义应用程序代码中使用。 不应删除此类API。

在内容结构和用户体验的总体一致性方面，还应牢记向后兼容性。

## 核心概念 {#core-concepts}

**创作实例**  — 通常，出于安全性、管理和其他原因，生产站点会将AEM的实例分为创作实例和发布实例。有关部署架构（包括创作/发布实例）的更多信息，请参阅有关AEM实例的文档。

**缓存、煎炸和烘焙**  — 传统上，烘焙与煎炸的概念是不同Web内容管理系统之间的重要区别。在CMS术语中，“烘焙”是指在发布时将数据提交到静态文件的概念，而“煎炸”是指在请求时（即，准时）处理数据以进行最终演示的概念。

**群集和负载平衡**  — 为了提高生产环境的可用性并改进其性能，通常将多个创作和/或发布实例（发布到群集中）合并，方法是使这些实例可供不同的用户组使用，或在Dispatcher配置后对它们进行负载平衡。

还可以合并内容存储库的多个实例来创建&#x200B;*高可用性* JCR解决方案，然后，该解决方案可与您的AEM解决方案集成，以最大限度地防止硬件和软件故障。 有关更多信息，请参阅[推荐的部署](/help/sites-deploying/recommended-deploys.md#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter) 。

**组件**  — 在AEM中，组件是一种对象类型，通常可以通过从Sidekick中拖放组件来创建其实例。例如，随AEM一起提供的现成组件包括文本、标题、标签云、轮播、图像和列表组件，这些组件在运行时均可从Sidekick获取。

**内容查找器**  — 在创作模式下，内容查找器是页面左侧的一个特殊面板（框架），根据您在顶部选择的选项卡，该面板会显示图像、文档、Flash资产、页面、段落或存储库资源列表，您可以将这些资源从内容查找器拖放到您正在处理的页面（在右侧）中。

**数字资产**  — 在AEM中，数字资产（通常为）图像和富媒体文件。有关更多信息，请参阅在DAM中使用数字资产。

**Dispatcher**  - Dispatcher既是缓存和负载平衡工具，也提供了某些安全保护。

**ExtJS小组件**  - AEM中的大多数用户界面元素都使用ExtJS，ExtJS是使用JavaScript编写的第三方小组件库。ExtJS具有高性能、可自定义的UI小组件以及设计良好且可扩展的组件模型。

**JCR、Java内容存储库**  - Java内容存储库规范(JSR-283)提供了抽象数据模型和应用程序编程接口，用于实现一个可大规模扩展的NoSQL数据存储库，该数据存储库将文件系统和对象数据库的功能结合在一起。虽然您不需要详细了解JSR-283，但您应该花些时间熟悉JCR的基本功能以及JCR的基础数据模型，因为JCR是实现AEM“一切即内容”理念的最佳途径。

JCR本质上是一个节点和属性的系统，节点可以继承其他节点，所有内容都作为属性&#x200B;*values*&#x200B;存储。 请注意，除了普通继承之外，JCR还允许使用“mixin”节点的概念，该概念支持对多个继承进行建模。

JCR具有许多预定义的节点类型和属性类型，但一般而言，键入系统相当灵活，而且（事实上）JCR的一个强项是，它允许以同等轻松的方式存储/管理结构化和非结构化内容。 即，JCR可以容纳高度结构化的数据，但也可以容纳没有模式约束的任意动态数据结构。

用于JCR的Java API的JavaDoc是[此处](http://jackrabbit.apache.org/jcr/jcr-api.html)。

在尝试阅读JavaDoc或JCR规范本身之前，您可能需要查看由Adobe Experience Services实施的JCR的[这个高级说明](/help/sites-developing/the-basics.md#java-content-repository)。

**多站点管理器(MSM)**  - AEM的MSM功能可帮助客户处理多语言和跨国内容，从而在集中品牌策略与本地化内容之间实现平衡。

**OSGi**  - OSGi是基于服务的运行时技术，为AEM中的Java模块化开发提供了基础。它是一个框架，不仅为代码资源（称为包）提供了高度动态（且安全）的分类加载和执行环境，还完全控制由包公开的各种服务的可见性和生命周期。 服务注册表为包含生命周期动态（和版本要求）的包提供了合作模型。 OSGi解决了应用程序服务器想要解决的许多问题，但以轻量级、高度动态的方式解决了这些问题，例如，使热部署服务（使新代码立即可用，而无需重新启动服务器）成为可能。

**Parsys， Paragraph System**  — 段落系统(parsys)是一个复合组件，它允许作者向页面中添加不同类型的组件，并包含其他段落组件。每个段落类型表示为一个组件。段落系统本身也是一个组件，其中包含其他段落组件。

**微内核**  — 存储库中的每个工作区都可以单独配置为通过特定的微内核（用于管理数据的读写）存储其数据。同样，存储库范围的版本存储也可以单独配置为使用特定的微内核。 有许多不同的微内核可用，能够以各种文件格式或关系数据库存储数据。 (例如，MongoDB、DB2或Oracle有持久性管理器)AEM的默认微内核是TarMK（请参阅下面的进一步信息）。

**发布实例**  — 出于安全、管理和其他原因，生产站点通常会将AEM实例分为创作实例和发布实例。有关部署架构（包括创作/发布实例）的更多信息，请参阅有关AEM实例的文档。

**快速启动**  — 与许多其他程序不同，您可以使用单个“快速启动”自解压JAR文件来安装AEM。首次双击JAR文件时，您需要的所有内容都会自动安装。 快速入门JAR包括CRX存储库（包括管理设施）、虚拟存储库服务、索引和搜索服务、工作流服务、安全性和Web服务器，以及CQ Servlet引擎(CQSE)和所有AEM服务所需的所有文件。 没有其他文件可供安装：快速入门是自包含的。

首次启动快速入门时，它会在后台创建整个符合JCR的存储库，这可能需要几分钟时间。 在初始启动后，后续启动会比存储库基础结构已经布局更快。

许多启动选项(例如，活动端口号以及相关的AEM实例是发布实例还是创作实例；等等)可通过适当重命名快速入门文件来控制。 要查看这方面的选项列表，请在命令行中使用“ — help”运行JAR:

```shell
java -jar <quickstartfilename>.jar -help
```

**复制代理**  — 复制代理在AEM中是核心，它是用于将内容从创作环境发布（激活）到发布环境的机制；刷新Dispatcher缓存中的内容；将用户生成的内容（例如，表单输入）从发布环境返回到创作环境。

**基架**  — 使用基架，您可以创建一个表单（基架），其中的字段反映您需要的页面结构，然后使用此表单轻松地基于此结构创建页面。

**分段**  — 网站访客在访问网站时有不同的兴趣和目标。了解访客的目标并满足其期望是在线营销的重要成功先决条件。 分段可通过分析访客的详细信息并描述其特征，帮助实现这一点。

**Sidekick**  - Sidekick是一个类似面板的浮动窗口，显示在可编辑的页面上，可从中拖动新组件并执行应用于页面的操作。

**Site Catalyst**  -SiteCatalyst为营销人员提供了一个位置，用于测量、分析和优化跨多个营销渠道的所有在线计划的集成数据。您可以使用Adobe SiteCatalyst分析AEM网站中的数据。

**Tar存储(TarMK)**  - TarMK是AEM中的默认持久系统。虽然AEM可以配置为使用不同的持久性系统（如MongoDB），但TarMK具有一些优势，即它针对典型的JCR用例进行了性能优化（因此速度非常快），使用行业标准数据格式，并且可以快速轻松地进行备份。

**模板**  — 在AEM中，模板可指定特定类型的页面。它定义页面的结构（同时通常还指定缩略图图像和各种属性）。 例如，对于产品页面、Sitemap 和联系人信息，您可能有不同的模板。

**工作流**  - AEM工作流系统允许创建涉及页面或资产的自动化流程。
