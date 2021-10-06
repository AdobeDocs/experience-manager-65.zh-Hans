---
title: ' [!DNL Adobe Experience Manager] 6.5的常规发行说明'
description: '[!DNL Adobe Experience Manager] 6.5 说明概述了发行信息、新增功能、安装方式以及详细的更改列表。'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: f8fcfa9e09167cd4dbaafe938bcbe3ee6ece270f
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 67%

---

# [!DNL Adobe Experience Manager] 6.5的常规发行说明{#general-release-notes-for-adobe-experience-manager}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 类型 | 主要版本 |
| 公开发行日期 | 2019 年 4 月 8 日 |
| 推荐的更新 | 请参阅[AEM近期更新](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。 |

### 相关事项 {#trivia}

此版本[!DNL Adobe Experience Manager]的发布周期从2018年4月4日开始，经过23次质量保证和错误修复迭代，于2019年3月28日结束。 此版本中修复的客户相关问题（包括增强功能和新增功能）总数为 1345。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起正式发布。

![AEM 6.5 登录屏幕](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是6.4代码库 [!DNL Adobe Experience Manager] 的升级版本。它提供了一些新功能和增强功能、重要的客户修复、高优先级的客户增强功能，以及针对产品稳定性的一般错误修复。它还包括[!DNL Adobe Experience Manager] 6.4 Service Pack版本，最高配置为SP4。

下面的列表提供了概述 — 而后续页面则列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[AEM Foundation](/help/release-notes/wcm-platform.md) 中提供了完整的更改列表。

[!DNL Adobe Experience Manager] 6.5的平台基于基于OSGi的框架（Apache Sling和Apache Felix）和Java内容存储库的更新版本而构建：阿帕奇·杰克拉布特橡1.10.2。

快速入门使用 Eclipse Jetty 9.4.15 作为 servlet 引擎。

#### Java 支持  {#java-support}

* 新增对 Java 11 及已支持的 Java 8 的支持。
* 为获取最佳性能，请使用其他值覆盖默认的 GC 值。有关更多信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Java 11和Java 8维护更新由Adobe分发，以便客户在与AEM相关的项目中使用(如果未从Oracle公开提供)。

#### Java 开发 {#java-development}

* 现在有[两个版本的Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，一个推荐的版本，其中包含未标记为弃用的公共接口，另一个版本包含标记为弃用的接口。

#### 用户界面 {#user-interface}

对 UI 进行了各种增强，使其更高效，更易于使用。

* 用户和组的新权限管理 UI.
* 列视图现在也只加载屏幕上可见的条目，并且仅在用户开始滚动时加载更多条目。列表视图和卡片视图已在 6.0 之后的版本中实现了此功能（在 6.4 中进行了改进）。
* 列视图现在包括页面/资产的工作流状态（如果适用）.
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作是一种快速方法，可以对同一文件夹中的所有页面/资产执行操作.
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作会尝试对所有页面/资源执行操作，而不仅仅是加载的页面/资源。如果未升级操作以处理批量操作，则会显示警告对话框。

>[!CAUTION]
>
>Adobe 不打算进一步增强经典 UI。AEM 6.5 包含经典 UI，从早期发行版升级的客户可以继续按原样使用它。请注意，经典 UI 在弃用期间仍完全受支持。[了解更多](/help/sites-deploying/ui-recommendations.md)。

#### 搜索和索引 {#indexing-and-search}

* 在 Oak 中搜索现在支持动态 Facet。例如，资产搜索中的过滤器边栏会显示预计的结果量。
* 扩展了 QueryBuilder 以提供包含动态 Facet 的结果.

#### 升级 {#upgrade}

* 运行 AEM 6.2、6.3 和 6.4 的客户可以直接就地升级到 AEM 6.5。使用 5.x 或 6.0/6.1 的客户如果想要使用就地升级，则需要先升级到 6.4，然后再升级到 6.5，或者通过在实例之间直接传输内容升级到 AEM 6.5。

#### 项目和工作流 {#projects-and-workflows}

* 改进了 6.4 中引入的新工作流模型编辑器以包含更多操作，如复制和发布、工作流步骤中的变量支持以及增强的 OR 和 AND 拆分。

### [!DNL Experience Manager] 站点 {#experience-manager-sites}

[AEM Sites和加载项](/help/release-notes/sites.md)中的更改的完整列表。

#### 托管单页应用程序 {#managed-single-page-apps}

“页面编辑器”添加了在上下文中编辑内容以及在客户端呈现的体验中撰写/布局的功能（也称为 [SPA 编辑器](/help/sites-developing/spa-architecture.md)）。使用 JavaScript 框架 React 或 Angular 构建的现有单页应用程序可以使用 AEM SJ SDK 进行扩展，以便从业人员可对其进行编辑。

SPA 支持首先作为 AEM 6.4 SP2 的一部分发布，在 AEM 6.5 中，其增加了以下功能：

* 使用“模板编辑器”来编辑和配置 SPA 的 AEM 可编辑部分
* 使用“多站点管理”来创建国家/地区、获特许权的机构或白标 SPA 体验

#### 无头内容管理 {#headless-content-management}

AEM 能够以不同的格式并且从堆栈的不同级别提供内容。自 2008 年以来，有些就已经使用 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。Content Services（[Sling Model 导出程序](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html)）在 AEM 6.3 中引入，是一种 AEM SJ SDK 用于保护单页应用程序的方法。[资产的 HTTP API](/help/assets/mac-api-assets.md) 是一个 CRUD API，已针对 AEM 6.5 进行了扩展。

新的HTTP API功能：

* 添加了[对资产的 HTTP API 的内容片段支持](/help/assets/assets-api-content-fragments.md)，以创建、更新、读取和删除片段。
* 使用[内容片段列表核心组件](https://opensource.adobe.com/aem-core-wcm-components/library/content-fragment-list.html)，通过 Content Services 显示内容片段列表。
* [核心组件库](https://opensource.adobe.com/aem-core-wcm-components/library.html)，可显示每个组件的默认 Content Services JSON 输出

#### Screens 加载项 {#screens-add-on}

从交互式信息亭到数字标牌，高效设计、交付和优化所有数字显示屏的体验。

**Design**

* 通过改进内容重用，将数字和存储中的体验和内容统一起来
* 通过支持启动项简化了创作和批准/发布工作流
* 使用 SPA 编辑器编辑和提供丰富的交互式体验

**交付**

* 扩展的媒体播放器支持执行强大的联机和脱机操作（智能同步），甚至可以扩展到最大的标牌网络。

**优化**

* 通过使用动态占位符，按照数据触发内容的位置或配置进行个性化。
* 通过将 Adobe Analytics 集成到 AEM Screens 播放器驱动的统一分析

有关对AEM Screens所做更改的更多详细信息 — 请参阅[AEM Screens用户指南](https://docs.adobe.com/content/help/zh-Hans/experience-manager-screens/user-guide/aem-screens-introduction.html)中的发行说明。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

[AEM 6.5 Assets发行说明](/help/release-notes/assets.md)中的完整更改列表。

AEM 6.5 引入了以下功能和增强功能，以提高 AEM 用户、DAM 角色以及相关的创意和营销角色的生产力。

#### 与 Adobe Creative Cloud 集成 {#integration-with-adobe-creative-cloud}

引入了 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)（一种面向使用 Adobe Creative Cloud 应用程序（包括 Photoshop、Illustrator 和 InDesign）的创意用户的应用程序内体验，简化了创意人员和营销人员在内容创建过程中的协作。AEM桌面应用程序继续支持用户使用任何文件类型和任何桌面应用程序从桌面上的AEM处理资产。

此外，AEM 与 Adobe Stock 集成，可帮助直接从 AEM Web UI 中查找、预览、许可和保存 Adobe Stock 资产。

![Photoshop 中的“资产链接”面板](/help/assets/assets/aem65-assetlink-photoshop.png)

#### 连接的资产 {#connected-assets}

“连接的资产”功能针对的是具有许多AEM Sites部署的较大部署，这些部署需要从中央AEM Assets DAM部署中利用资产。 它允许围绕集中管理的资产改进管理，同时允许为各种站点部署高效地提供资产。

### Dynamic Media {#dynamic-media}

Dynamic Media 在 AEM Assets 中提供了增强的富媒体创作和交付，以提供沉浸式的个性化前沿体验。借助单一的高品质主资产，您可以利用我们的高级云呈现、智能裁剪和一流的查看器，以业界领先的性能提供最具吸引力的体验。

新增功能包括：

* 支持360视频和VR耳机
* 自定义视频缩略图
* 增强的辅助功能支持
* 热连接保护

#### 用户体验和搜索 {#user-experience-and-search}

关键增强功能可以通过提供动态搜索 Facet，帮助更快地找到正确的资产，并通过提供从任意文件夹或搜索结果中选择所有资产的功能，更有效地管理多个资产。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms 中引入了一些新增功能和增强功能。主要功能包括：

* 事务报告，用于跟踪所提交表单、已处理文档和已呈现文档的数量
* 交互式通信的可用性改进
* 自适应表单中基于云的数字签名
* 在 AEM Sites 单页应用程序 (SPA) 中嵌入了自适应表单和交互式通信。
* 支持 AEM 工作流中的变量
* 交互式通信中的数据显示模式支持
* 对自适应表单和交互式通信表格进行排序
* 自动验证表单数据模型中的输入数据

有关新增和改进功能及文档资源的信息，请参阅AEM 6.5 Forms中的[新增功能和增强功能摘要](/help/forms/using/whats-new.md)。

### [!DNL Experience Manager Communities] {#communitiesreleasenotes}

AEM 6.5 为 Communities 添加了一些新增功能和增强功能。此版本的主要功能包括：

* 在创作用户生成的内容时支持注册的成员标记 (@mention)。
* 现在支持向成员组直接批量发送消息。
* 在批量审核 UI 中开发并添加了自定义筛选器。演示按标记进行筛选的[示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)可用作开发类似自定义筛选器的基础。
* 在批量审核中提供了一个改进了 UI 的新列表视图。
* 可以为不同的社区站点和嵌套组分配多个单独的管理员，而不是单个社区管理员。
* AEM 6.5 Communities的启用功能支持[(SCORM)2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)引擎。
* 启用组件上支持键盘导航以改进辅助功能。
* 设置 MSRP 和 DSRP 时支持 Apache Solr 7.0。

有关更改的详细列表，请参阅[AEM 6.5 Communities发行说明](/help/release-notes/communities-release-notes.md)。

### [!DNL Experience Manager Livefyre] {#experience-manager-livefyre}

您可以将 Livefyre 与 AEM 6.5 实例集成。请参阅[如何将Livefyre与AEM](https://docs.adobe.com/content/help/en/experience-manager-64/administering/integration/livefyre.html)集成。

### 利用以客户为中心的开发 {#leverage-customer-focused-development}

Adobe 正在使用以客户为中心的开发模型，借助该模型，客户可以在规范、开发和测试期间对开发流程的所有阶段做出贡献。我们衷心感谢在这一流程中做出贡献的所有客户和合作伙伴。

Adobe 实施了多种规程和流程来对以客户为中心的错误解决方案和增强请求开发进行收集、优先级排序和跟踪。[Experience Manager支持门户](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support)与Adobe增强和缺陷跟踪系统集成。 客户问题由客户支持团队在可能的情况下识别并解决。 升级到 R&amp;D 时，将捕获所有客户信息，并将这些信息用于确定优先级和报告。在开发过程中，优先考虑付费支持、被担保人问题和客户付费增强功能。

这一确定优先级的流程已经产生了 750 多个以客户为中心的更改，并已在 AEM 6.5 中进行了修复。

## 作为发布一部分的文件列表 {#list-of-files-that-are-part-of-the-release}

**Foundation**

* 独立快速入门：`cq-quickstart-6.5.0.jar`。
* 应用程序服务器快速启动：`cq-quickstart-6.5.0.war`。
* 适用于各种Web服务器和平台的Dispatcher 4.3.2或更高版本。 请参阅[下载链接](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/getting-started/release-notes.html)
* 用于 Eclipse IDE 的插件（[了解更多并下载](/help/sites-developing/aem-eclipse.md)）

* 用于 Brackets 代码编辑器的扩展（[了解更多并下载](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle 依赖（[下载链接](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**站点**

* 核心组件（[GitHub 项目](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail 参考实施（[了解更多](/help/sites-developing/we-retail.md)）
* Maven 项目原型：

   * 对于全堆栈站点：[GitHub 项目](https://github.com/adobe/aem-project-archetype)
   * 对于使用 React/Angular 的单页应用程序：[GitHub 项目](https://github.com/adobe/aem-spa-project-archetype)

* 适用于各种不同平台的 AEM Screens 播放器（[下载](https://download.macromedia.com/screens/)）

* 智能内容语言模型。已预先安装英语 - 可以下载更多语言

   * [德语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [意大利语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM 现代化工具套件，例如对话框转换工具。（[GitHub 项目](https://github.com/adobe/aem-modernize-tools)）

**资产**

* 用于添加增强型 PDF 栅格化程序的软件包（[了解更多](/help/assets/aem-pdf-rasterizer.md)）
* 用于添加扩展 RAW 图像支持的软件包（[了解更多](/help/assets/camera-raw.md)）

**表单**

* [用于 AEM Forms 功能的软件包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)
* [AEM Forms OSGi客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 语言 {#languages}

用户界面提供了下列语言版本：

* 英语
* 德语
* 法语
* 西班牙语
* 意大利语
* 巴西葡萄牙语
* 日语
* 简体中文
* 繁体中文（有限支持）
* 韩语

[!DNL Experience Manager] 6.5 已通过 GB18030-2005 CITS 认证，可使用中文编码标准。

## 安装和更新 {#install-update}

有关安装要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 支持的平台 {#supported-platforms}

查找支持的平台的完整矩阵，包括[AEM 6.5技术要求](/help/sites-deploying/technical-requirements.md)上的支持级别。

>[!NOTE]
>
>Oracle已转为使用OracleJava SE产品的长期支持(LTS)模型。 Java 9和10是按Oracle列出的非LTS版本。请参阅[OracleJava SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html)。 Adobe支持LTS版本的Java，以便仅在生产中运行AEM。 Java 11是要与AEM 6.5一起使用的推荐版本。

## 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe 不断评估产品中的功能，以便随着时间的推移，计划使用更强大的版本来替换这些功能，或是决定重新实现选定部分，以便为未来的预期或扩展做更充分的准备。

对于[!DNL Adobe Experience Manager] 6.5, [请阅读已弃用和已删除功能的列表](/help/release-notes/deprecated-removed-features.md)。 该页面还包含近期更改的预先公告，以及面向从先前版本中更新的客户的重要通知。

## 已知问题 {#known-issues}

[已知问题列表](/help/release-notes/known-issues.md)

### 产品下载和支持（受限网站） {#product-download-and-support-restricted-sites}

以下网站仅供客户使用。 如果您是客户并且需要访问，请联系您的 Adobe 客户经理。

* [产品下载：licensing.adobe.com](https://licensing.adobe.com/).

* 产品更新、修补程序和软件包，以获取[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上的其他功能。

* [通过Admin Console提供客户支持](https://adminconsole.adobe.com/)。有关更多信息，请参阅[新Adobe客户支持体验](https://docs.adobe.com/content/help/en/customer-one/using/home.html)。
