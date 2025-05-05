---
title: ' [!DNL Adobe Experience Manager] 6.5的一般发行说明'
description: '[!DNL Adobe Experience Manager] 6.5说明概述了发行信息、新增功能、安装方法和详细的更改列表。'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '4493'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5的一般发行说明{#general-release-notes-for-adobe-experience-manager}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 类型 | 主要版本 |
| 正式发布日期 | 2019 年 4 月 8 日 |
| 建议的更新 | 查看[AEM最近更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans)。 |

### Trivia {#trivia}

此版本的[!DNL Adobe Experience Manager]的发布周期从2018年4月4日开始，经历了23次质量保证和错误修复迭代，并于2019年3月28日结束。 此版本中修复的增强功能和新增功能等客户相关问题的总数量为1345。

[!DNL Adobe Experience Manager] 6.5自2019年4月8日起正式推出。

![AEM 6.5登录屏幕](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5是[!DNL Adobe Experience Manager] 6.4代码库的升级版本。 它提供新功能和增强功能、关键客户修复、高优先级客户增强功能以及面向产品稳定性的常规错误修复。它还包含最多SP4的[!DNL Adobe Experience Manager] 6.4 Service Pack版本。

下面的列表提供了概述，而后续页面列出了完整的详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5平台在基于OSGi的框架的更新版本（Apache Sling和Apache Felix）以及Java™内容存储库(Apache Jackrabbit Oak 1.10.2)的基础上构建。

快速入门使用Eclipse Jetty 9.4.15作为Servlet引擎。

#### Java™支持  {#java-support}

* 新增对Java™ 11和已支持的Java™ 8的支持。
* 为获得最佳性能，请用其他值覆盖默认的GC值。 有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* Java™ 11和Java™ 8维护更新按Adobe分发，以供客户在AEM相关项目中使用(如果未从Oracle公开提供)。

#### Java™开发 {#java-development}

* Uberjar[&#128279;](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)现在有两个版本，一个是带有未标记为弃用的公共接口的推荐版本，另一个是包含标记为弃用的接口的版本。

#### 用户界面 {#user-interface}

对UI进行了各种增强，使其更高效、更易于使用。

* 新的用户和组权限管理UI。
* 列视图现在也仅加载屏幕上可见的条目，并且仅在用户开始滚动时才加载更多条目。 列表和卡片视图自6.0之后便已执行该操作（在6.4中进行了改进）。
* 列视图现在包含页面/资产的工作流状态（如果适用）。
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作是一种快速执行操作的方法，适用于同一文件夹中的所有页面/资产。
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作会尝试对所有页面/资产执行该操作，而不只是加载的内容。 如果操作未升级为处理批量操作，则会显示警告对话框。

>[!CAUTION]
>
>Adobe不打算进一步增强经典UI。 AEM 6.5包含经典UI，从早期版本升级的客户可以继续按原样使用它。 经典UI在弃用后仍得到完全支持。 [了解详情](/help/sites-deploying/ui-recommendations.md)。

#### 搜索和编制索引 {#indexing-and-search}

* Oak中的搜索现在支持动态Facet。 例如，资源搜索中的过滤器边栏会显示估计的结果数。
* 扩展了QueryBuilder以提供带有动态Facet的结果。

#### 升级 {#upgrade}

* 运行AEM 6.2、6.3和6.4的客户支持直接就地升级到AEM 6.5。使用5.x或6.0/6.1且希望就地升级的客户，需要先升级到6.4。 然后，升级到6.5，或通过直接将实例之间的内容传输到AEM 6.5的方式进行升级。
* 升级程序在6.5中基本上保持不变。
* 我们将继续支持6.4中引入的向后兼容性、升级复杂性评估和可持续升级功能。在需要时，对这些区域进行了特定于版本的更新。
* 模式检测器封装现已得到简化。 有一个软件包针对可用的源版本评估升级到6.5的情况。
* 有关升级过程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

#### 项目和工作流 {#projects-and-workflows}

* 6.4中引入的新工作流模型编辑器已得到改进，现在包括更多操作，如复制和Publish、工作流步骤中的变量支持以及增强的`OR`和`AND`拆分。

#### 存储库 {#repository}

* Adobe Experience Manager 6.5的基础基于基于OSGi的框架的更新版本（Apache Sling和Apache Felix）和Java™ Content Repository： Apache Jackrabbit Oak 1.10.2.
* 有关已修复问题的概述，请参阅[Apache Jackrabbit Oak Jira版本1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira版本1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt)和[Apache Jackrabbit Oak Jira版本1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自AEM 6.3以来一直存在的Oak区段Tar的新版本要求迁移存储库。 如果您从旧版TarMK升级，或者希望从其他类型的持久性中切换新的Segment Tar，则必须执行此步骤。 有关新区段Tar的好处的详细信息，请参阅[迁移到Oak区段Tar常见问题解答](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

#### OSGI {#osgi}

* 添加了OSGi Promises和Converter实用程序库。

#### 安全性 {#security}

* 添加了管理员用户的密码过期时间。

#### Web 服务器 {#web-server}

* 快速入门分发使用Eclipse Jetty 9.4.15作为Servlet引擎(AEM 6.4随9.3.22提供)。

### [!DNL Experience Manager]站点 {#experience-manager-sites}

#### 受管的单页应用程序 {#managed-single-page-apps}

页面编辑器添加了在客户端渲染体验(也称为[即SPA编辑器](/help/sites-developing/spa-architecture.md))中的上下文编辑内容和撰写/布局的功能。 可以使用AEM SJ SDK扩展使用JavaScript Framework React或Angular构建的现有单页应用程序，以便让从业人员可编辑。

首次作为AEM 6.4 SP2的一部分提供，对于AEM 6.5，SPA支持将获得以下功能：

* 使用模板编辑器编辑和配置SPA的AEM可编辑部分
* 使用多站点管理创建国家/地区、特许经营或带有白色标签的SPA体验

#### Headless内容管理 {#headless-content-management}

AEM可以以各种格式和从栈栈的各个级别提供内容。 一些服务自2008年以来一直使用[SlingGET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html)和[POSTServlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。 内容服务（[Sling模型导出器](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=zh-hans)）是在AEM 6.3中引入的，它是AEM SJ SDK用于水合单页应用程序的方法。 适用于Assets[&#128279;](/help/assets/mac-api-assets.md)的HTTP API是针对AEM 6.5扩展的CRUD API。

新的HTTP API功能：

* 向Assets[&#128279;](/help/assets/assets-api-content-fragments.md)的HTTP API添加了内容片段支持，用于创建、更新、读取和删除片段。
* 通过[内容片段列表核心组件](https://www.aemcomponents.dev)的内容服务公开内容片段的列表。
* [核心组件库](https://www.aemcomponents.dev)，显示每个组件的默认Content Services JSON输出

#### Screens加载项 {#screens-add-on}

高效地设计、交付和优化所有数字显示器（从交互式信息亭到数字标牌）上的体验。

* 通过改进的内容重复使用跨数字和实体店整合体验和内容
* 支持启动项的简化创作和批准/发布工作流程
* 使用SPA编辑器编辑并提供丰富的交互式体验
* 使用启动项规划标牌内容的未来内容更改
* 序列渠道中的按流量计费的播放
* 使用源文件（如Excel工作表）自动创建项目结构
* 通过强大的在线和离线操作(Smart Sync)扩展了媒体播放器支持，甚至能够扩展到最大的标牌网络。
* 使用动态占位符，按位置或配置数据触发的内容进行个性化。
* 由Adobe Analytics集成到AEM Screens Player驱动的统一见解

有关AEM Screens更改的更多详细信息 — 请参阅[AEM Screens用户指南](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=zh-Hans)中的发行说明。

#### 组件和模板开发 {#component-amp-template-development}

* Maven项目原型18+对于新项目，请参阅[GitHub获取发行说明](https://github.com/adobe/aem-project-archetype/releases)。
* 单页应用程序Maven项目原型1.0.6+对于新项目，请参阅[GitHub获取发行说明](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL版本1.4，请参阅[GitHub获取发行说明](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字符串、数组和对象的“in”运算符：

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * 具有data-sly-set的变量声明：

     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出并重复控制参数：开始、步骤、结束：

     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的标识符：

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * 支持负数

* 核心组件2.3.2+，请参阅[GitHub获取发行说明](https://github.com/adobe/aem-core-wcm-components/releases)。
* 布局容器的网格系统，请参阅[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib Manager：将Google Closure Compiler默认为缩小JavaScript clientlibs（旧默认为Yahoo YUI），并将Google Closure Compiler更新为版本v20190121
* 模板编辑器和策略

   * 为使用JS SDK(也称为SPA编辑器)的单页应用程序创建和编辑模板

* 引用网站We.Retail 4.0，请参阅[GitHub获取发行说明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 升级现有站点以使用最新编辑器功能的工具包，请参阅[GitHub存储库](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含1.12.4版本的jQuery库，可提供与现有自定义代码的最大兼容性。 Adobe已做出修改以解决已知安全问题。

#### 站点管理 {#site-administration}

* [引用](/help/sites-authoring/author-environment-tools.md#references)边栏有一个新部分，用于列出指向所选页面的内部链接。 在计划使页面脱机或删除时，这非常有用 — 可查看在使页面脱机之前需要调整哪些页面。
* [列表视图](/help/sites-authoring/basic-handling.md#list-view)有一个新的工作流列，当页面处于工作流中时，该列会显示状态。
* 在[页面属性](/help/sites-authoring/editing-page-properties.md)中，现在可以在为页面分配缩略图时浏览现有资源（缩略图选项卡）。

#### 页面编辑器 {#page-editor}

* 允许对使用JS SDK(也称为SPA编辑器)的React和Angular客户端组件构建的单页应用程序体验进行上下文编辑和合成
* 仅当页面配置了基架页面时，才会显示基架模式。

#### 内容片段和编辑器 {#content-fragments-amp-editor}

* 内容片段编辑器中新增了[注释](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)边栏，用于发表常规注释并查看在文本中发表的注释（也会显示在时间轴边栏中）
* 能够将[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)中多行文本元素的默认内容类型设置为简单文本、富文本或Markdown
* 通过在RTE（全屏视图）中选择文本来添加[注释/批注](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [通过参考边栏并排比较内容片段的版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 资产下载报表现在会显示相应的内容片段
* 通过/api.json向Assets HTTP API[&#128279;](/help/assets/assets-api-content-fragments.md)添加内容片段支持。 有用于创建、更新、读取和删除内容片段的API。

#### 体验片段 {#experience-fragments}

* 改进了[体验片段](/help/sites-authoring/experience-fragments.md)的索引，以便在搜索正在使用它们的页面中找到其内容。
* 现在，[导出到Target](/help/sites-administering/experience-fragments-target.md)选项允许您以JSON(默认值为HTML)或同时以两者形式发送体验片段。

#### 翻译 {#translation}

* 使用项目母版简化翻译项目的创建过程。
* 通过将翻译作业设置为默认批准状态，简化翻译项目的执行。
* 允许更新第三方翻译记忆库中具有更改的已翻译页面。
* 允许以JSON格式导出翻译作业。
* 更新Microsoft®翻译集成以使用V3 API。

#### 多站点管理(MSM) {#multi-site-management-msm}

* 对于使用PushOnModify的转出配置，更好地处理页面移动操作以避免状态不一致。
* 默认情况下，在LiveCopy结构中创建页面会创建一个独立页面。
* 在使用JS SDK(也称为SPA编辑器)的单页应用程序中使用MSM功能

#### 启动项 {#launches}

* 适用于启动项的新审核和批准工作流，以及仅提升已批准启动页面的功能
* 在UI中添加了[选项，以选择在提升步骤](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)之后立即删除启动项

#### 内容定位和模拟 {#content-targeting-simulation}

* ContextHub数据层和客户端规则引擎JavaScript已更新，默认使用jQuery 3。

#### AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>当前：
>
>* 如果您在AEM的“活动”控制台中使用Adobe Target作为定位引擎，则仅支持`at.js 1.x`。
>
>* 如果您使用导出到Target的体验片段并在Target控制台中运行活动，则同时支持`at.js. 1.x`和`at.js 2.x`。

* Adobe Target集成现在使用Target Standard API。 AEM的早期版本使用Target Classic HTTP API，该API现已弃用。
* 包括Adobe Target `mbox.js`版本63。 Adobe强烈建议您将实现切换到`at.js` v1.x。
* 现已包含`at.js`版本1.5.0。 Adobe建议您使用[Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)将`at.js` v1.x配置到站点中。

#### AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* 包括`s_code.js` H.27.5。 Adobe建议您将实现切换到`AppMeasurement.js`
* 已包括`AppMeasurement.js` v1.8.0。 Adobe建议您使用[Adobe Experience Platform Launch](https://business.adobe.com/products/experience-platform/launch.html)将AppMeasurement.js配置到站点中。

#### AEM和Commerce {#aem-commerce}

自AEM 6.4以来，Commerce integration framework的改进速度更快。使用Commerce integration framework[&#128279;](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html?lang=zh-Hans)从AEM和Adobe Commerce集成了解详情。

#### Communities加载项 {#communities-add-on}

要获取最新版本，请参阅文档的[部署社区](/help/communities/deploy-communities.md)部分。

##### 社区参与改进 {#enhancements-to-community-engagement}

**@Mentions支持**
AEM Communities现在允许注册用户在用户生成的内容中标记（提及）其他注册成员以吸引他们的注意。 随后，系统会通知已标记（提及）的成员，并提供指向相应用户生成内容的深层链接。 但是，用户可以选择禁用/启用Web和电子邮件通知。

![At提及支持](/help/release-notes/assets/at-mentions.png)

社区用户无需搜索其名字、姓氏或用户名即可查看是否有人联系过他们或需要他们关注。 此外，它允许UGC作者从能够最好地解决问题并添加输入的特定注册用户处寻求响应。

社区管理员需要在社区组件上&#x200B;**启用提及功能**，以允许注册用户使用这些组件上的功能。

**组消息**

注册的社区成员现在可以通过单个电子邮件组合向群组批量发送直邮，而不是单独向群组成员发送相同的邮件。 要允许[组消息传递](/help/communities/configure-messaging.md)，请启用[消息传递操作服务](/help/communities/messaging.md#group-messaging)的两个实例。

![组消息](/help/release-notes/assets/group-messaging.png)

##### 批量审核的增强功能 {#enhancements-to-bulk-moderation}

批量审核中的自定义筛选器

现在可以开发[自定义筛选器](/help/communities/moderation.md#custom-filters)并将其添加到批量审核UI。

在[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)中提供了一个演示通过标记进行筛选的[示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)。 此项目可用作开发类似自定义筛选器的基础。

![自定义筛选条件](/help/release-notes/assets/custom-tag-filter.png)

**正在批量审核的列表视图**

已批量适度提供具有改进UI的新列表视图，以显示用户生成的内容条目。

![在列表视图中批量审阅](/help/release-notes/assets/list-view-moderation.png)

##### 站点和组管理的增强功能 {#enhancements-to-site-and-group-management}

**作者端站点和组管理员**

从AEM 6.5开始，Communities允许分散管理（和管理）不同的社区站点和组/嵌套组。 现在，托管多个社区站点和嵌套组的组织可以在创建站点（和组）时为作者端的管理员角色选择成员。

![站点管理员](/help/release-notes/assets/site-admin.png)

站点管理员可以在任何层次结构级别创建组，并成为默认管理员。 这些管理员以后可由其他组管理员删除。 组管理员可以管理其组G1并创建嵌套在G1下的子组。

##### 增强功能 {#enhancements-to-enablement}

**SCORM 2017.1支持**

AEM 6.5 Communities的启用功能支持可共享的内容对象引用模型[ (SCORM) 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/)引擎。

* 启用组件上的键盘导航支持
* AEM Communities中的启用组件（例如，目录和课程播放、任务、文件库）支持键盘导航以提高辅助功能。

##### 其他增强功能 {#other-enhancements}

* Solr 7支持
* 在设置MSRP和DSRP时，AEM 6.5社区支持Apache Solr 7.0版本的搜索平台。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5引入了以下功能和增强功能，以提高AEM用户、DAM角色以及关联的创意和营销角色的工作效率。

#### 与[!DNL Adobe Creative Cloud]和创意工作流程集成 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager]提供了多种方法来与[!DNL Adobe Creative Cloud]集成并共享资产，以便在创意和营销团队或业务团队密切协作的工作流中使用。 [!DNL Experience Manager] 6.5继续改进集成并进一步简化集成以发掘更多机会并简化现有方法。

请阅读并了解[!DNL Experience Manager] 6.5的特定功能和集成，您可以使用这些功能和集成来最好地支持您的Content Velocity用例。

##### Adobe资源链接 {#aal}

[!DNL Adobe Asset Link]在内容创建过程中加强了创意专业人士与营销人员之间的协作。 创意人员无需离开他们最熟悉的应用，即可访问[!DNL Experience Manager Assets]中存储的内容。 创意人员可以使用[!DNL Adobe Photoshop]、[!DNL Adobe Illustrator]和[!DNL Adobe InDesign]应用中的应用内面板无缝浏览、搜索、签出和签入资源。

[!DNL Adobe Asset Link]是企业[&#128279;](https://www.adobe.com/cn/creativecloud/business/enterprise.html)产品Creative Cloud的一部分。 有关它的详细信息，包括[!DNL Experience Manager]部署的必要配置，请参阅[AdobeAsset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。

![在Adobe Photoshop中搜索资源](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock]集成 {#stock}

您的组织可以在[!DNL Experience Manager Assets]内使用其[!DNL Adobe Stock]企业计划，以确保许可的资产广泛可用于您的创意和营销项目。 您可以使用[!DNL Experience Manager]的强大DAM功能快速查找、预览和许可Experience Manager中保存的[!DNL Adobe Stock]资源。

[!DNL Adobe Stock]服务允许设计人员和企业访问其所有创意项目中的数百万张高质量、精选的、免版税的照片、矢量、插图、视频、模板和3D资产。

有关详细信息，请参阅[在Experience Manager Assets中使用Adobe Stock资源](/help/assets/aem-assets-adobe-stock.md)。

![在Experience Manager Assets中预览Adobe Stock图像和许可证](/help/release-notes/assets/stock_image_preview_license_options.png)

*图：从[!DNL Experience Manager Assets].*&#x200B;内预览[!DNL Adobe Stock]图像和许可证

![在Experience Manager中搜索和筛选许可的Adobe Stock图像](/help/release-notes/assets/aem-search-filters2.jpg)

*图：在[!DNL Experience Manager].*&#x200B;中搜索和筛选许可的[!DNL Adobe Stock]图像

##### [!DNL Adobe InDesign]中的动态引用 {#dynamic-references-in-indesign}

[!DNL Adobe InDesign]文件中使用的[!DNL Experience Manager Assets]是动态的。 如果引用的资产在存储库中移动，引用将自动更新。 有关详细信息，请参阅[如何管理复合资产](/help/assets/managing-linked-subassets.md)。

#### Brand Portal功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal]帮助您轻松获取、有效控制并安全地跨设备将批准的资产分发给外部供应商/代理和内部业务用户。 它有助于提高资产共享效率，加快资产上市速度，并消除不合规使用和未经授权访问的风险。

有关详细信息，请参阅[Brand Portal的新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans)。

#### 连接的资源 {#connectedassets}

在大型企业中，可以分发创建网站所需的基础架构。 有时，网站创建功能和所需的数字资产存放在不同的思洛存储器中。

[!DNL Experience Manager Sites]提供创建网页的功能，[!DNL Experience Manager Assets]是向网站提供所需资产的数字资产管理(DAM)系统。 通过集成[!DNL Sites]和[!DNL Assets]，[!DNL Experience Manager]现在支持上述用例。 请参阅[如何配置和使用“连接的Assets”功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![从其他[!DNL Experience Manager]部署的[!DNL Sites]页面上的[!DNL Experience Manager]部署中拖动资产](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*图：从其他[!DNL Experience Manager]部署上的[!DNL Sites]页面上的[!DNL Experience Manager]部署拖动资产。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media]在[!DNL Experience Manager Assets]中提供增强的富媒体创作和交付，以推动沉浸式个性化前沿体验。 通过上传单个高质量主资源并使用Adobe的高级云渲染和查看器，您可以动态提供演绎版的任意组合以支持贵组织的媒体策略。

有关新[!DNL Dynamic Media]功能的更多详细信息，请参阅[Dynamic Media发行说明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html?lang=zh-Hans)。

##### 360视频支持 {#video-support}

使用先进的查看器直接在[!DNL Experience Manager]中管理360视频文件，为台式机、移动设备和VR头戴式耳机提供VR体验。 有关详细信息，请参阅[使用360视频](/help/assets/360-video.md)。

##### 自定义视频缩略图 {#custom-video-thumbnails}

您现在可以使用视频本身的帧或存储在DAM中的其他内容来自定义视频资源的缩略图。 有关其他说明，请参阅[关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

##### 辅助功能增强功能 {#accessibility-enhancements}

[!DNL Dynamic Media]查看器现在支持Aria支持、屏幕阅读器和Alt-text等增强的辅助功能。 有关其他详细信息，请参阅[查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=zh-Hans)。

#### 搜索体验增强功能 {#experience-enhancement-for-searching}

从[!DNL Experience Manager] 6.5开始，营销人员可以从搜索结果页面更快地发现所需的资产。 即使在应用搜索过滤器之前，搜索Facet也会更新为资源数。 查看筛选器的预期计数有助于用户有效地在搜索结果中导航。 有关详细信息，请参阅[在Experience Manager](/help/assets/search-assets.md)中搜索资源。

![在搜索Facet中查看未筛选搜索结果的资产数量](/help/assets/assets/asset_search_results_in_facets_filters.png)

*图：在搜索Facet中查看未筛选搜索结果的资产数量。*

#### 可用性增强 {#usability-enhancement}

您现在可以选择文件夹中所有已加载的资源，也可以一次性从搜索结果中选择资源。 它可帮助您快速管理多个资源。 复选框会选择符合场景的所有资源，例如搜索结果，而不仅仅是[!DNL Experience Manager]界面中显示的资源。

![使用“全选”选项单击即可选择所有加载的资源。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*图：使用“全选”选项单击即可选择所有加载的资源。*

#### 元数据增强功能 {#metadata-enhancements}

[!DNL Assets]允许您为资源文件夹创建元数据架构，这些文件夹定义文件夹属性页面中显示的布局和元数据。 您现在可以将文件夹元数据架构分配给现有文件夹或在创建文件夹时。 有关详细信息，请参阅[文件夹元数据架构](/help/assets/metadata-config.md#folder-metadata-schema)。

指定层叠元数据时，可在运行时从JSON文件加载选项，例如在表单中无需手动键入。 有关详细信息，请参阅[级联元数据](/help/assets/metadata-schemas.md#cascading-metadata)。

#### 报表增强功能 {#reporting-enhancements}

内容片段和链接共享现在包含在下载的报表中。 有关详细信息，请参阅[Assets报表](/help/assets/asset-reports.md)。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms引入了几项新增功能和增强功能。 这些亮点包括：

* 用于跟踪已提交的表单、已处理的文档和已渲染文档的数量的交易报表
* 改进了交互式通信的可用性
* 自适应表单中基于云的数字签名
* 将自适应表单和交互式通信嵌入到AEM Sites单页应用程序(SPA)中。
* 在AEM Workflow中支持变量
* 交互式通信中的数据显示模式支持
* 排序自适应表单和交互式通信表
* 自动验证表单数据模型中的输入数据

有关新增功能和改进功能以及文档资源的信息，请参阅[AEM 6.5 Forms中新增功能和增强功能摘要](/help/forms/using/whats-new.md)。

### 使用以客户为中心的开发 {#use-customer-focused-development}

Adobe使用以客户为中心的开发模型，允许客户在规范、开发和测试过程中参与开发流程的所有阶段。 在此过程中，我们感谢所有参与的客户和合作伙伴。

Adobe已制定程序和流程，以便能够收集、优先处理和跟踪以客户为中心的错误解决和增强请求开发。 [Experience Manager支持门户](https://experienceleague.adobe.com/zh-hans?support-solution=Experience+Manager#support)已与Adobe增强和缺陷跟踪系统集成。 客户支持团队会尽可能识别和解决客户问题。 在升级至R&amp;D时，将捕获所有客户信息，并用于优先级和报告目的。 在开发中优先考虑付费支持、被保证人问题和客户付费的增强功能。

此优先级划分过程产生了750多项以客户为中心的更改，这些更改在AEM 6.5中得到了修复。

## 属于发行版的文件列表 {#list-of-files-that-are-part-of-the-release}

**基础**

* 独立快速入门： `cq-quickstart-6.5.0.jar`。
* 应用程序服务器快速启动： `cq-quickstart-6.5.0.war`。
* 适用于各种Web服务器和平台的Dispatcher 4.3.2或更高版本。 查看[下载链接](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=zh-Hans)
* 适用于Eclipse IDE的插件（[阅读更多内容并下载](/help/sites-developing/aem-eclipse.md)）

* Brackets代码编辑器的扩展（[阅读更多内容并下载](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle依赖项（[下载链接](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**站点**

* 核心组件（[GitHub项目](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail引用实施（[了解更多](/help/sites-developing/we-retail.md)）
* Maven项目原型：

   * 对于全栈站点： [GitHub项目](https://github.com/adobe/aem-project-archetype)
   * 对于具有React/Angular的单页应用程序： [GitHub项目](https://github.com/adobe/aem-spa-project-archetype)

* 适用于各种目标平台的AEM Screens Player （[下载](https://download.macromedia.com/screens/)）

* 智能内容语言模型。 已预安装英语 — 可以下载更多语言

   * [德语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [意大利语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM现代化工具套件，例如，对话框转换工具。 （[GitHub项目](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 用于添加增强型PDF光栅器的包（[阅读更多](/help/assets/aem-pdf-rasterizer.md)）
* 用于添加扩展RAW映像支持的包（[阅读更多](/help/assets/camera-raw.md)）

**Forms**

* 用于AEM Forms功能的[包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)
* [AEM Forms OSGi客户端SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

## 语言 {#languages}

用户界面提供以下语言版本：

* 英语
* 德语
* 法语
* 西班牙语
* 意大利语
* 巴西葡萄牙语
* 日语
* 简体中文
* 繁体中文（有限支持）
* 朝鲜语

[!DNL Experience Manager] 6.5已获得GB18030-2005 CITS使用中文编码标准的认证。

## 安装和更新 {#install-update}

有关安装要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 支持的平台 {#supported-platforms}

查找支持的平台的完整列表，包括有关[AEM 6.5技术要求](/help/sites-deploying/technical-requirements.md)的支持级别。

>[!NOTE]
>
>oracle已转为使用OracleJava™ SE产品的长期支持(LTS)模型。 Java™ 9和10是按Oracle划分的非LTS版本。 请参阅[OracleJava™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html)。 Adobe支持LTS版本的Java™，以便仅在生产中运行AEM。 推荐将Java™ 11与AEM 6.5一起使用。

## 已弃用和已删除的功能 {#deprecated-and-removed-features}

Adobe会持续评估产品功能，不断使用更强大的版本替换旧功能，也可能决定重新推出部分组件，更好地满足未来的期望或扩展要求。

对于[!DNL Adobe Experience Manager] 6.5，[请阅读已弃用和已删除的功能的列表](/help/release-notes/deprecated-removed-features.md)。 本页还包含未来变更的预先公告以及适用于从先前版本进行更新的客户的重要通知。

## 已知问题 {#known-issues}

### Platform {#platform}

* 报告删除CRX-Quickstart及其内容的问题。

  对于以下每个操作，请确保属性`htmllibmanager.fileSystemOutputCacheLocation`不是空字符串：

   1. 正在调用`/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升级到AEM 6.5。
   3. 在AEM 6.5上执行“延迟内容迁移”。

  提供了[知识库](https://helpx.adobe.com/experience-manager/kb/avoid-crx-quickstart-deletion-in-aem-6-5.html)文章，其中包含有关此问题的更多详细信息和解决方法。

* 如果将JDK 11与AEM 6.5实例一起使用，则在部署某些包后，某些页面可能会显示为空白。 日志文件中显示以下错误消息：

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

要解决此错误，请执行以下操作：

1. 停止AEM实例。 转到`<aem_server_path_on_server>crx-quickstart\conf`并打开`sling.properties`文件。 Adobe建议对此文件进行备份。

1. 搜索`org.osgi.framework.bootdelegation=`。 添加`jdk.internal.reflect,jdk.internal.reflect.*`属性以作为显示结果。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存文件并重新启动AEM实例。

### Sites {#sites}

* **使用页面版本**： [如果页面已被移动，您将无法再对移动前创建的任何版本执行预览](/help/sites-authoring/working-with-page-versions.md#previewing-a-version)。

### 资源 {#assets}

* **搜索：**&#x200B;如果搜索字符串包含前导空格([OAK-4786](https://issues.apache.org/jira/browse/OAK-4786))，则不会返回任何结果
* **文件夹元数据架构**：添加选择按钮后，ID和值字段未按预期呈现，并且删除功能不起作用。 (CQ-4261144)
* 重命名资源时，无法在资源名称中使用空格。 (CQ-4266403)

### Forms {#forms}

* 在Linux®操作系统上安装AEM Forms时，Digital Signature with Hardware Security Module不起作用。 (CQ-4266721)
* (仅限WebSphere上的AEM Forms®)如果您搜索将&#x200B;**用户名**&#x200B;作为搜索条件的&#x200B;**Forms Workflow**，则&#x200B;**任务搜索** > **任务搜索**&#x200B;选项不会返回任何结果。 (CQ-4266457)

* AEM Forms无法将具有JPEG压缩功能的TIF和TIFF文件转换为PDF文档。 (CQ-4265972)
* **AEM Forms Assets扫描程序**&#x200B;和&#x200B;**Letter to Interactive Communication迁移**&#x200B;选项在&#x200B;**AEM Forms迁移**&#x200B;页面上不起作用。 (CQ-4266572)

* (仅限JBoss® 7)当您从以前的版本升级到AEM 6.5 Forms时，如果以前的版本具有创建并使用默认提交或默认渲染进程副本的进程(.lca)，则使用此类进程(.lca)的HTML5 Forms无法执行所需的操作。 (CQ-4243928)
* 在自适应源中，当从规则编辑器调用表单数据模型服务以动态更新图像选择组件的值时，图像选择组件的值未更新。 (CQ-4254754)
* AEM Forms Designer安装程序需要32位版本的[Visual C++可再分发运行时包2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170)和[Visual C++可再分发运行时包2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1)。 在开始安装之前，请确保已安装前面提到的可再分发运行时包。 (CQ-4265668)

* PDF Generator不支持基于智能卡的身份验证。 当管理员在Windows服务器上启用组策略`Interactive Logon: Require Smart card`时，所有现有的PDF Generator用户都将失效。

* 当自适应表单配置为动态更新组件的值，并且通过Dispatcher访问承载该表单的发布实例时，动态更新字段值的功能停止工作。 要解决此问题，请在发布实例上打开CRXDE，导航到`/libs/fd/af/runtime/clientlibs/guideChartReducer`，然后创建下面列出的属性。

   * 名称： allowProxy
   * 类型：布尔值
   * 值： true
   * 受保护：假
   * 必填： False
   * 多个：False
   * 自动创建： False

  属性允许运行时文件夹下的客户端库访问代理。 (CQ-4268679)

* 启动AEM Forms时，出现`SAX Security Manager could not be setup`警告。
* 在运行20.10.00版Adobe Acrobat Reader的Apple iOS或iPadOS上打开受AEM Forms Document Security保护的PDF时
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。Apple iOS 15.1 修复了此问题。

## 产品下载和支持（受限制的站点） {#product-download-and-support-restricted-sites}

以下网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载位于licensing.adobe.com](https://licensing.adobe.com/)。

* [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上其他功能的产品更新、修补程序和软件包。

* 通过Admin Console[客户支持](https://adminconsole.adobe.com/)。 有关详细信息，请参阅[新Adobe客户支持体验](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=zh-Hans)。
