---
title: ' [!DNL Adobe Experience Manager] 6.5 常规发行说明'
description: '[!DNL Adobe Experience Manager] 6.5 说明信息概述了发行信息、新增功能、安装方法以及详细的变更列表。'
exl-id: b3d4a527-44ca-4eb6-b393-f3e8117cf1a6
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '4477'
ht-degree: 100%

---

# [!DNL Adobe Experience Manager] 6.5 常规发行说明{#general-release-notes-for-adobe-experience-manager}

## 版本信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] |
|---|---|
| 版本 | 6.5 |
| 类型 | 主要版本 |
| 正式发行日期 | 2019 年 4 月 8 日 |
| 推荐更新 | 请参阅 [AEM 最新更新](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans)。 |

### 普通 {#trivia}

此版本 [!DNL Adobe Experience Manager] 的发布周期始于 2018 年 4 月 4 日，历经 23 轮质量保证与错误修复，于 2019 年 3 月 28 日结束。本次发布共修复了 1345 个与客户相关的问题，其中包括功能增强和新增特性。

[!DNL Adobe Experience Manager] 6.5 自 2019 年 4 月 8 日起正式发布。

![AEM 6.5 登录界面](/help/assets/assets/aem65-login-v4.png)

## 新增功能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 是基于 [!DNL Adobe Experience Manager] 6.4 代码库的升级版本。它提供了新功能和增强功能、关键客户修复、高优先级客户增强功能，以及旨在提高产品稳定性的常规错误修复。它还包括 [!DNL Adobe Experience Manager] 6.4 服务包版本，最高至 SP4。

以下列表提供了概览，而后续页面则列出了全部详细信息。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 平台构建于更新版本后的基于 OSGi 框架（Apache Sling 和 Apache Felix）以及 Java™ 内容存储库 Apache Jackrabbit Oak 1.10.2 之上。

Quickstart 使用 Eclipse Jetty 9.4.15 作为 Servlet 引擎。

#### Java™ 支持  {#java-support}

* 新增对 Java™ 11 的支持，同时继续支持 Java™ 8。
* 为获得最佳性能，请使用其他值覆盖默认 GC 值。有关详细信息，请参阅[安装和更新](/help/sites-deploying/custom-standalone-install.md)部分。
* 当 Oracle 未公开提供时，Adobe 会为客户在 AEM 相关项目中分发 Java™ 11 和 Java™ 8 的维护更新。

#### Java™ 开发 {#java-development}

* 现在提供[两个版本的 Uberjar](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)，一个是推荐版本，其中包含未标记为弃用的公共接口，另一个是完整版本，其中包含已标记为弃用的接口。

#### 用户界面 {#user-interface}

同时，UI 也进行了多项增强，以提升生产效率并简化使用体验。

* 全新用户和组权限管理用户界面。
* 列视图现在仅加载屏幕上可见的条目，并会在用户开始滚动时才加载更多内容。列表视图和卡片视图自 6.0 起已具备该功能（并在 6.4 中得到改进）。
* 在适用情况下，列视图现在还会显示页面/资产的工作流状态。
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作是一种快速方式，可对同一文件夹中的所有页面/资产执行操作。
* [全选](/help/sites-authoring/basic-handling.md#select-all)操作会尝试对所有页面/资产执行操作，而不仅限于当前已加载的内容。如果该操作尚未升级以支持批量操作，则会显示警告对话框。

>[!CAUTION]
>
>Adobe 不计划对经典 UI 进行进一步增强。AEM 6.5 仍包含经典 UI，升级自早期版本的客户可以继续按原样使用。经典 UI 在弃用的同时，仍然获得完整支持。[了解详情](/help/sites-deploying/ui-recommendations.md)。

#### 搜索和索引 {#indexing-and-search}

* Oak 中的搜索现已支持动态分面。例如，资产搜索中的筛选边栏会显示预估的结果数量。
* QueryBuilder 已经过扩展，以支持返回包含动态分面的结果。

#### 升级 {#upgrade}

* 对于运行 AEM 6.2、6.3 和 6.4 的客户，支持直接就地升级至 AEM 6.5。使用 5.x 或 6.0/6.1 的客户，如需进行就地升级，必须先升级至 6.4。然后再升级至 6.5，或者也可以通过在实例之间直接传输内容的方式升级至 AEM 6.5。
* 在 6.5 中，升级流程基本保持不变。
* 我们继续支持在 6.4 中引入的向后兼容性、升级复杂性评估以及可持续升级功能，并在必要时针对这些功能进行了特定于相关版本的更新。
* 模式检测器的打包方式现已简化。提供了一个统一的包，用于评估从可用源版本升级至 6.5 的可行性。
* 有关升级流程的详细信息，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

#### 项目和工作流 {#projects-and-workflows}

* 在 6.4 中引入的新工作流模型编辑器已得到改进，其中新增了更多操作，例如复制和发布，支持在工作流步骤中使用变量，并增强了 `OR` 和 `AND` 分支功能。

#### 存储库 {#repository}

* Adobe Experience Manager 6.5 的基础构建于更新版本后的基于 OSGi 的框架（Apache Sling 和 Apache Felix）以及 Java™ 内容存储库 Apache Jackrabbit Oak 1.10.2 之上。
* 有关已修复问题的概述，请参阅 [Apache Jackrabbit Oak Jira v. 1.10.0](https://archive.apache.org/dist/jackrabbit/oak/1.10.0/RELEASE-NOTES.txt)、[Apache Jackrabbit Oak Jira v. 1.10.1](https://archive.apache.org/dist/jackrabbit/oak/1.10.1/RELEASE-NOTES.txt) 和 [Apache Jackrabbit Oak Jira v. 1.10.2](https://archive.apache.org/dist/jackrabbit/oak/1.10.2/RELEASE-NOTES.txt)。

>[!CAUTION]
>
>自 AEM 6.3 起提供的新版本 Oak Segment Tar 需要进行存储库迁移。如果您是从较早版本的 TarMK 升级，或希望从其他持久化类型切换到新的 Segment Tar，则此步骤是必需的。有关新 Segment Tar 优势的更多信息，请参阅[迁移至 Oak Segment Tar 常见问题](/help/sites-deploying/revision-cleanup.md#migrating-to-oak-segment-tar)。

#### OSGI {#osgi}

* 新增 OSGi Promises 和 Converter 实用程序库。

#### 安全性 {#security}

* 为管理员用户新增密码过期功能。

#### Web 服务器 {#web-server}

* Quickstart 发行版现使用 Eclipse Jetty 9.4.15 作为 Servlet 引擎（AEM 6.4 使用的是 9.3.22）。

### [!DNL Experience Manager] Sites {#experience-manager-sites}

#### 托管单页应用程序 {#managed-single-page-apps}

页面编辑器提供了在客户端渲染体验中进行内容上下文编辑以及编排/布局的功能（也称[为 SPA 编辑器](/help/sites-developing/spa-architecture.md)）。使用 React 或 Angular 等 JavaScript 框架构建的现有单页应用程序，可以通过 AEM SJ SDK 进行扩展，从而为从业人员提供可编辑功能。

最初随 AEM 6.4 SP2 一同发布，在 AEM 6.5 中，SPA 支持新增以下功能：

* 使用模板编辑器编辑和配置 SPA 中可由 AEM 编辑的部分
* 使用多站点管理创建国家站点、加盟站点或白标 SPA 体验

#### Headless 内容管理 {#headless-content-management}

AEM 可通过多种格式和不同层级的技术栈提供内容。其中部分功能自 2008 年就已存在，如 [Sling GET](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) 和 [POST Servlet](https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html)。内容服务（[Sling 模型导出器](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=zh-Hans)）是在 AEM 6.3 中引入的，并由 AEM SJ SDK 用于为单页应用程序提供内容。[HTTP API for Assets](/help/assets/mac-api-assets.md) 是一个 CRUD API，它已针对 AEM 6.5 进行了扩展。

新增 HTTP API 功能：

* 为 [HTTP API for Assets 增加内容片段支持](/help/assets/assets-api-content-fragments.md)，以创建、更新、读取和删除片段。
* 通过内容服务和[内容片段列表核心组件](https://www.aemcomponents.dev)提供内容片段列表。
* 展示各组件在内容服务中的默认 JSON 输出的[核心组件库](https://www.aemcomponents.dev)

#### Screens 附加组件 {#screens-add-on}

可高效设计、交付和优化从交互式自助终端到数字标牌在内的所有数字显示体验。

* 借助对内容复用功能的改进，实现线上与门店的体验和内容统一
* 借助发布项简化创作、审批与发布工作流
* 使用 SPA 编辑器编辑和交付丰富的交互式体验
* 使用发布项来规划未来的标牌内容更新
* 在序列频道中实现按需播放
* 使用 Excel 表等源文件自动创建项目结构
* 扩展对媒体播放器的支持，结合强大的在线与离线操作（Smart Sync），可扩展至超大型标牌网络。
* 借助动态占位符，根据数据触发内容的位置或配置进行个性化。
* 通过 Adobe Analytics 与 AEM Screens Player 的集成，提供统一的洞察

有关对 AEM Screens 所做更改的更多详细信息，请参阅 [AEM Screens 用户指南](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/aem-screens-introduction.html?lang=zh-Hans)中的发行说明。

#### 组件与模板开发 {#component-amp-template-development}

* 新项目可使用 Maven Project Archetype 18 及以上版本，详见 [GitHub 发行说明](https://github.com/adobe/aem-project-archetype/releases)。
* 单页应用程序可使用 Maven Project Archetype 1.0.6 及以上版本，详见 [GitHub 发行说明](https://github.com/adobe/aem-spa-project-archetype/releases)。
* 支持 HTL 1.4，详见 [GitHub 发行说明](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 支持字符串、数组和对象的 &quot;in&quot; 运算符：

     ```html
     ${'a' in 'abc'}
     ${100 in myArray}
     ${'a' in myObject}
     ```

   * 支持使用 data-sly-set 变量声明：
     `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列表与循环控制参数：begin、step、end：
     `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap 的标识符：

     ```html
     <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
     text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
     </div>
     ```

   * 支持负数

* 核心组件 2.3.2 及以上版本，详见 [GitHub 发行说明](https://github.com/adobe/aem-core-wcm-components/releases)。
* 布局容器网格系统，详见 [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib 管理器：将 JavaScript clientlibs 的默认压缩工具改为 Google Closure Compiler（此前默认为 Yahoo YUI），并将 Google Closure Compiler 更新至 v20190121 版本。
* 模板编辑器与策略

   * 为使用 JS SDK（即 SPA 编辑器）的单页应用程序创建和编辑模板

* 参考站点 We.Retail 4.0，详见 [GitHub 发行说明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 用于将现有网站升级至最新编辑器功能的工具包，详见 [GitHub 代码库](https://github.com/adobe/aem-modernize-tools)。

>[!CAUTION]
>
>AEM 内置 jQuery 1.12.4 版本，以确保与现有自定义代码的最大兼容性。已对 Adobe 进行修改，以修复已知安全问题。

#### 网站管理 {#site-administration}

* [引用](/help/sites-authoring/author-environment-tools.md#references)边栏新增一栏，用于列出指向所选页面的内部链接。这在规划下线或删除页面时非常有用，可提前识别需要调整的页面。
* [列表视图](/help/sites-authoring/basic-handling.md#list-view)新增工作流列，当页面处于工作流中时会显示其状态。
* 在[页面属性](/help/sites-authoring/editing-page-properties.md)中，分配页面缩略图时现在可以直接浏览现有资产。

#### 页面编辑器 {#page-editor}

* 允许对使用 JS SDK（即 SPA 编辑器）构建的 React 和 Angular 客户端组件的单页应用程序体验进行上下文内编辑与编排。
* 仅当页面已配置基架页面时，才会显示基架模式。

#### 内容片段和编辑器 {#content-fragments-amp-editor}

* 在内容片段编辑器中新增[注释](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)边栏，可用于撰写一般性评论并查看文本中的评论（也会显示在时间线边栏中）
* 能够在[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)中将多行文本元素的默认内容类型设置为纯文本、富文本或 Markdown
* 在 RTE 的全屏视图中，选择文本即可添加[评论/注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* 可通过引用边栏并排[比较内容片段的不同版本](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 资产下载报告现已相应显示内容片段
* 通过 /api.json 在 [Assets HTTP API 中新增内容片段支持](/help/assets/assets-api-content-fragments.md)。可通过 API 创建、更新、读取和删除内容片段。

#### 体验片段 {#experience-fragments}

* 改进了[体验片段](/help/sites-authoring/experience-fragments.md)的索引，确保其内容能在所用页面的搜索结果中被检索到。
* [导出至 Target](/help/sites-administering/experience-fragments-target.md) 选项现在允许以 JSON 格式（默认是 HTML 格式）或同时以这两种格式发送体验片段。

#### 翻译 {#translation}

* 通过使用项目母板，简化翻译项目的创建。
* 执行翻译项目时，翻译任务会默认设置为“已批准”状态，从而简化流程。
* 支持将第三方翻译记忆库中的变更内容应用到已经翻译的页面中。
* 支持以 JSON 格式导出翻译任务。
* 更新 Microsoft® 翻译集成，以使用 V3 API。

#### 多网站管理（MSM） {#multi-site-management-msm}

* 对于使用 PushOnModify 的发布配置，改进了对页面移动操作的处理，以避免出现不一致的状态。
* 在 livecopy 结构中创建页面时，默认会生成独立页面。
* 在使用 JS SDK（也称为 SPA 编辑器）的单页应用程序中可以使用 MSM 功能

#### 发布项 {#launches}

* 新增发布项的审阅和审批工作流，并支持仅推广已批准的发布页面
* 新增 [UI 选项，可在推广步骤后选择删除发布项](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

#### 内容定向与模拟 {#content-targeting-simulation}

* ContextHub 数据层和客户端规则引擎 JavaScript 已默认更新为 jQuery 3。

#### AEM 与 Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>当前：
>
>* 如果在 AEM 的活动控制台中使用 Adobe Target 作为定位引擎，则仅支持 `at.js 1.x`。
>
>* 如果通过体验片段导出至 Target 并在 Target 控制台运行活动，则同时支持 `at.js. 1.x` 和 `at.js 2.x`。

* Adobe Target 集成现已使用 Target Standard API。AEM 的早期版本使用的 Target Classic HTTP API 现已弃用。
* 包含 Adobe Target `mbox.js` 版本 63。Adobe 强烈建议将实施切换至 `at.js` v1.x。
* 包含 `at.js` 版本 1.5.0。Adobe 建议使用 [Adobe Experience Platform Launch](https://business.adobe.com/cn/products/experience-platform/launch.html) 来配置 `at.js` v1.x，并将其部署到网站。

#### AEM 与 Adobe Analytics {#aem-amp-adobe-analytics}

* 包含 `s_code.js` H.27.5。Adobe 建议将实施切换至 `AppMeasurement.js`。
* 包含 `AppMeasurement.js` v1.8.0。Adobe 建议使用 [Adobe Experience Platform Launch](https://business.adobe.com/cn/products/experience-platform/launch.html) 将 AppMeasurement.js 部署到网站。

#### AEM 和 Commerce {#aem-commerce}

自 AEM 6.4 起，对 Commerce 集成框架的改进已进入更快的发布周期。详见 [AEM 与 Adobe Commerce 集成（使用 Commerce 集成框架）](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/content-and-commerce/integrations/magento.html?lang=zh-Hans)。

#### Communities 附加组件 {#communities-add-on}

要获取最新版本，请参阅文档中的[部署 Communities](/help/communities/deploy-communities.md) 部分。

##### 社区参与增强功能 {#enhancements-to-community-engagement}

**@提及支持**
AEM Communities 现支持注册用户在用户生成内容中标记（提及）其他注册成员以引起其注意。被标记（提及）的成员会收到通知，并带有指向相应用户生成内容的深度链接。但是，用户可选择启用或禁用 Web 和电子邮件通知。

![@提及支持](/help/release-notes/assets/at-mentions.png)

社区用户无需搜索自己的名字、姓氏或用户名，即可查看是否有人联系过他们或需要他们的关注。此外，它还允许用户生成内容的作者向特定的注册用户发起回应请求，由这些用户来更好地解决问题并补充意见。

社区管理员需要在社区组件上&#x200B;**启用提及**&#x200B;功能，以便注册用户在这些组件中使用该功能。

**群组消息**

注册的社区成员现在可以通过一次邮件撰写向群组批量发送私信，而无需再逐一向群组成员单独发送相同的消息。要启用[群组消息](/help/communities/configure-messaging.md)，需启用[消息操作服务](/help/communities/messaging.md#group-messaging)的两个实例。

![群组消息](/help/release-notes/assets/group-messaging.png)

##### 批量审核功能增强 {#enhancements-to-bulk-moderation}

批量审核中的自定义筛选条件

现在可以在批量审核 UI 中开发并添加[自定义筛选条件](/help/communities/moderation.md#custom-filters)。

[GitHub](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) 上提供了一个[示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter)，展示了如何通过标记进行筛选。该项目可作为开发类似自定义筛选条件的基础。

![自定义筛选条件](/help/release-notes/assets/custom-tag-filter.png)

**批量审核中的列表视图**

在批量审核中提供了全新的列表视图，配备改进的 UI，用于显示用户生成内容条目。

![批量审核的列表视图](/help/release-notes/assets/list-view-moderation.png)

##### 站点和群组管理增强 {#enhancements-to-site-and-group-management}

**作者端的站点和群组管理员**

从 AEM 6.5 开始，Communities 支持对不同的社区站点和群组/嵌套群组进行分布式管理。托管多个社区站点和嵌套群组的组织，现在可以在创建站点（和群组）时，在作者端选择成员担任管理员角色。

![站点管理员](/help/release-notes/assets/site-admin.png)

站点管理员可以在层级结构的任意级别创建群组，并自动成为默认管理员。之后，这些管理员可以由其他群组管理员移除。群组管理员可以管理其所属的群组 G1，并在 G1 下创建一个子群组。

##### 学习功能增强 {#enhancements-to-enablement}

**支持 SCORM 2017.1**

AEM 6.5 Communities 的学习功能现已支持可共享内容对象参考模型 [（SCORM）2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) 引擎。

* 学习组件的键盘导航支持
* AEM Communities 中的学习组件（例如目录、课程播放、作业、文件库）现已支持键盘导航，以提升无障碍访问体验。

##### 其他增强功能 {#other-enhancements}

* Solr 7 支持
* 在设置 MSRP 和 DSRP 时，AEM 6.5 Communities 支持搜索平台 Apache Solr 7.0 版本。

### [!DNL Experience Manager Assets] {#experience-manager-assets}

AEM 6.5 引入了以下功能和增强，旨在提升 AEM 用户、DAM 角色以及相关创意和营销角色的工作效率。

#### 与 [!DNL Adobe Creative Cloud] 及创意工作流的集成 {#integration-with-adobe-creative-cloud-and-creative-workflows}

[!DNL Adobe Experience Manager] 提供多种与 [!DNL Adobe Creative Cloud] 集成的方式，并会共享资产，以在创意团队与营销或业务团队紧密协作的工作流中使用。在 [!DNL Experience Manager] 6.5 中，集成功能得到了进一步优化和简化，既能提供更多机会，也能让现有方法更加高效。

请继续阅读，了解 [!DNL Experience Manager] 6.5 提供的具体功能与集成方式，从而更好地支持您的内容提速用例。

##### Adobe Asset Link {#aal}

[!DNL Adobe Asset Link] 在内容创作过程中强化了创意人员与营销人员之间的协作。创意人员无需离开他们最熟悉的应用程序，就可以访问存储在 [!DNL Experience Manager Assets] 中的内容。通过 [!DNL Adobe Photoshop]、[!DNL Adobe Illustrator] 和 [!DNL Adobe InDesign] 应用程序中的面板，创意人员可以无缝浏览、搜索、签出和签入资产。

[!DNL Adobe Asset Link] 是 [Creative Cloud 企业版](https://www.adobe.com/creativecloud/business/enterprise.html)产品的一部分。如需了解更多信息，包括部署 [!DNL Experience Manager] 所需的配置，请参阅 [Adobe Asset Link](https://helpx.adobe.com/cn/enterprise/using/adobe-asset-link.html)。

![在 Adobe Photoshop 中搜索资产](/help/release-notes/assets/asset_search_photoshop.png)

##### [!DNL Adobe Stock] 集成 {#stock}

您的组织可以在 [!DNL Experience Manager Assets] 中使用其 [!DNL Adobe Stock] 企业版计划，确保已授权的资产能够广泛应用于创意和营销项目。借助 [!DNL Experience Manager] 强大的 DAM 功能，您可以快速查找、预览并授权保存到 Experience Manager 的 [!DNL Adobe Stock] 资产。

[!DNL Adobe Stock] 服务为设计师和企业提供数百万高质量、精选的免版税照片、矢量图、插图、视频、模板和 3D 资产，可满足各种创意项目需求。

更多信息，请参阅[在 Experience Manager Assets 中使用 Adobe Stock 资产](/help/assets/aem-assets-adobe-stock.md)。

![在 Experience Manager Assets 中预览并授权 Adobe Stock 图像](/help/release-notes/assets/stock_image_preview_license_options.png)

*图：在 [!DNL Experience Manager Assets] 中预览并授权 [!DNL Adobe Stock] 图像。*

![在 Experience Manager 中搜索并筛选已授权的 Adobe Stock 图像](/help/release-notes/assets/aem-search-filters2.jpg)

*图：[!DNL Experience Manager] 中搜索并筛选已授权的 [!DNL Adobe Stock] 图像。*

##### [!DNL Adobe InDesign] 中的动态引用 {#dynamic-references-in-indesign}

在 [!DNL Adobe InDesign] 文件中使用的 [!DNL Experience Manager Assets] 具备动态特性。当引用的资产在存储库中移动时，引用会自动更新。有关更多信息，请参阅[如何管理复合资产](/help/assets/managing-linked-subassets.md)。

#### Brand Portal 功能 {#brand-portal-capabilities}

[!DNL Experience Manager Assets Brand Portal] 可帮助您轻松获取、有效管控并安全地向外部供应商/代理机构和内部业务用户分发已批准的资产，且支持跨设备访问。它能够提升资产共享效率，加快资产上市时间，并降低不合规使用和未经授权的访问的风险。

有关更多信息，请参阅[ Brand Portal 新增功能](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/whats-new.html?lang=zh-Hans)。

#### 连接的资产 {#connectedassets}

在大型企业中，创建网站所需的基础架构可能是分布式的。有时，网站创建功能和所需的数字资产会分散在不同的系统中。

[!DNL Experience Manager Sites] 提供网页创建功能，而 [!DNL Experience Manager Assets] 作为数字资产管理（DAM）系统，为网站提供所需的资产。[!DNL Experience Manager] 现已通过集成 [!DNL Sites] 和 [!DNL Assets] 来支持上述用例。请参阅[如何配置和使用“连接的资产”功能](/help/assets/use-assets-across-connected-assets-instances.md)。

![从一个 [!DNL Experience Manager] 部署中将资产拖动到另一个 [!DNL Experience Manager] 部署的 [!DNL Sites] 页面](/help/release-notes/assets/connected-assets-drag-and-drop-only.gif)

*图：从一个 [!DNL Experience Manager] 部署中将资产拖动到另一个 [!DNL Experience Manager] 部署的 [!DNL Sites] 页面。*

#### Dynamic Media {#dynamic-media}

[!DNL Dynamic Media] 在 [!DNL Experience Manager Assets] 中提供了增强的富媒体创作与投放能力，助力打造沉浸式和个性化的前沿体验。通过上传单个高质量的主资产，并利用 Adobe 的先进云渲染与查看器，您可以即时交付任意组合的渲染版本，以支持组织的媒体战略。

有关新 [!DNL Dynamic Media] 功能的详细信息，请参阅 [Dynamic Media 发行说明](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/release-notes/s7rn2017.html?lang=zh-Hans)。

##### 360 视频支持 {#video-support}

您可以在 [!DNL Experience Manager] 中直接管理 360 视频文件，并利用先进的查看器将 VR 体验交付至桌面、移动设备和 VR 头显。若要了解更多信息，请参阅[使用 360 视频](/help/assets/360-video.md)。

##### 自定义视频缩略图 {#custom-video-thumbnails}

现在，您可以使用视频中的帧或存储在 DAM 中的其他内容，自定义视频资产的缩略图。有关更多操作说明，请参阅[关于视频缩略图](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-scene-mode)。

##### 辅助功能增强 {#accessibility-enhancements}

[!DNL Dynamic Media] 查看器现已支持增强的辅助功能，例如 Aria 支持、屏幕阅读器和替代文本。有关更多详细信息，请参阅[查看器参考指南](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/homeviewers.html?lang=zh-Hans)。

#### 搜索体验增强 {#experience-enhancement-for-searching}

从 [!DNL Experience Manager] 6.5 开始，营销人员可以在搜索结果页面更快地找到所需资产。搜索分面会在应用搜索筛选条件之前就更新显示资产数量。通过在筛选条件旁查看预期数量，用户能够更高效地浏览搜索结果。如需了解更多信息，请参阅[在 Experience Manager 中搜索资产](/help/assets/search-assets.md)。

![在搜索分面中查看资产数量，而无需先筛选搜索结果](/help/assets/assets/asset_search_results_in_facets_filters.png)

*图：在搜索分面中查看资产数量，而无需先筛选搜索结果。*

#### 可用性增强 {#usability-enhancement}

现在，您可以一次性选择文件夹中的所有已加载资产或搜索结果中的所有资产。这有助于您快速管理多个资产。复选框会选择符合当前场景的所有资产（例如搜索结果），而不仅仅是 [!DNL Experience Manager] 界面上可见的资产。

![使用“全选”选项一键选择所有已加载的资产。](/help/release-notes/assets/select-all-in-aem-assets.gif)

*图：使用“全选”选项一键选择所有已加载的资产。*

#### 元数据增强 {#metadata-enhancements}

[!DNL Assets] 允许您为资产文件夹创建元数据架构，用于定义文件夹属性页面中显示的布局和元数据。现在，您可以在创建文件夹时或针对现有文件夹分配文件夹元数据架构。有关更多信息，请参阅[文件夹元数据架构](/help/assets/metadata-config.md#folder-metadata-schema)。

在指定级联元数据时，可以在运行时从 JSON 文件中加载选项，而无需在表单中手动输入。有关详细信息，请参阅[级联元数据](/help/assets/metadata-schemas.md#cascading-metadata)。

#### 报告增强 {#reporting-enhancements}

下载的报告中现已包含内容片段和链接共享。有关更多信息，请参阅[资产报告](/help/assets/asset-reports.md)。

### [!DNL Adobe Experience Manager Forms] {#experience-manager-forms}

AEM 6.5 Forms 新增功能与增强。亮点包括：

* 事务报告：用于跟踪已提交表单、已处理文档和已渲染文档的数量
* 交互式通信的可用性改进
* 自适应表单中的云端数字签名
* 在 AEM Sites 单页应用程序（SPA）中嵌入自适应表单和交互式通信。
* 在 AEM 工作流中支持变量
* 在交互式通信中支持数据展示模式
* 支持对自适应表单和交互式通信表格进行排序
* 在表单数据模型中自动验证输入数据

请参阅 [AEM 6.5 Forms 新增功能与增强概述](/help/forms/using/whats-new.md)，了解新增和改进功能及相关文档资源。

### 采用以客户为中心的开发 {#use-customer-focused-development}

Adobe 采用以客户为中心的开发模式，允许客户在规范制定、开发和测试等各个阶段参与开发过程。感谢在此过程中作出贡献的所有客户和合作伙伴。

Adobe 已建立相应的流程和机制，用于收集、优先排序并跟踪以客户为导向的错误修复和功能增强请求的开发。[Experience Manager 支持门户](https://experienceleague.adobe.com/zh-hans?support-solution=Experience+Manager#support) 已与 Adobe 增强与缺陷跟踪系统集成。客户问题会在可能的情况下由客户支持团队识别并解决。当问题升级至研发团队时，所有客户信息均会被记录，并用于优先级排序和报告。在开发中，优先处理付费支持、保修问题以及客户付费的功能增强。

这一优先级流程在 AEM 6.5 中已促成了 750 多项以客户为中心的修复与改进。

## 发布版本中所包含的文件列表 {#list-of-files-that-are-part-of-the-release}

**基础**

* 独立版快速入门：`cq-quickstart-6.5.0.jar`。
* 应用程序服务器快速入门：`cq-quickstart-6.5.0.war`。
* 适用于各类 Web 服务器和平台的 Dispatcher 4.3.2 或更高版本。请参阅[下载链接](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=zh-Hans)
* Eclipse IDE 插件（[了解更多并下载](/help/sites-developing/aem-eclipse.md)）

* Brackets 代码编辑器扩展（[了解更多并下载](/help/sites-developing/aem-brackets.md)）
* Maven/Gradle 依赖项（[下载链接](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.0/)）

**Sites**

* 核心组件（[GitHub 项目](https://github.com/adobe/aem-core-wcm-components)）
* We.Retail 参考实施（[了解更多](/help/sites-developing/we-retail.md)）
* Maven 项目原型：

   * 用于全栈站点：[GitHub 项目](https://github.com/adobe/aem-project-archetype)
   * 用于 React/Angular 单页应用程序：[GitHub 项目](https://github.com/adobe/aem-spa-project-archetype)

* 适用于各类目标平台的 AEM Screens 播放器（[下载](https://download.macromedia.com/screens/)）

* 智能内容语言模型。预装英语——可下载更多语言

   * [德语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
   * [西班牙语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
   * [意大利语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
   * [法语](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)

* AEM 现代化工具套件，例如对话框转化工具。（[GitHub 项目](https://github.com/adobe/aem-modernize-tools)）

**Assets**

* 用于添加增强型 PDF 光栅化器的包（[了解更多](/help/assets/aem-pdf-rasterizer.md)）
* 用于添加扩展型 RAW 图像支持的包（[了解更多](/help/assets/camera-raw.md)）

**Forms**

* [AEM Forms 功能包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=zh-Hans)
* [AEM Forms OSGi 客户端 SDK](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/)

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
* 繁体中文（支持有限）
* 韩语

[!DNL Experience Manager] 6.5 已通过 GB18030-2005 CITS 认证，以支持使用中国国家编码标准。

## 安装和更新 {#install-update}

有关设置要求，请参阅[安装说明](/help/sites-deploying/custom-standalone-install.md)。

有关详细步骤，请参阅[升级文档](/help/sites-deploying/upgrade.md)。

## 支持的平台 {#supported-platforms}

有关所支持的平台的完整矩阵（包括支持级别），请参阅 [AEM 6.5 技术要求](/help/sites-deploying/technical-requirements.md)。

>[!NOTE]
>
>Oracle 已将 Oracle Java™ SE 产品转为长期支持（LTS）模式。Java™ 9 和 10 属于 Oracle 的非 LTS 版本。请参阅 [Oracle Java™ SE 支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html)。Adobe 仅支持在生产环境中使用 Java™ 的 LTS 版本来运行 AEM。推荐在 AEM 6.5 中使用 Java™ 11。

## 已弃用和已移除的功能 {#deprecated-and-removed-features}

Adobe 会持续评估产品功能，并在未来逐步以更强大的版本替代现有功能，或重新实施部分组件，以更好地满足未来的需求和扩展。

有关 [!DNL Adobe Experience Manager] 6.5 的相关信息，[请参阅已弃用和已移除功能列表](/help/release-notes/deprecated-removed-features.md)。该页面还包含未来变更的预先公告，以及针对从早期版本升级客户的重要提示。

## 已知问题 {#known-issues}

### 平台 {#platform}

* 已报告一个问题：CRX-Quickstart 及其内容遭到删除。

  在执行以下操作时，请确保属性 `htmllibmanager.fileSystemOutputCacheLocation` 不是空字符串：

   1. 调用 `/libs/granite/ui/content/dumplibs.rebuild.html?invalidate=true`。
   2. 升级至 AEM 6.5。
   3. 在 AEM 6.5 上执行“延迟内容迁移”。

* 如果在 AEM 6.5 实例中使用 JDK 11，部署某些包后部分页面可能会显示为空白。日志文件中会出现如下错误消息：

  ```java
  *ERROR* [OsgiInstallerImpl] org.apache.sling.scripting.sightly bundle org.apache.sling.scripting.sightly:1.1.2.1_4_0 (558)[org.apache.sling.scripting.sightly.impl.engine.extension.use.JavaUseProvider(3345)] : Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl)
  java.lang.NoClassDefFoundError: jdk/internal/reflect/ConstructorAccessorImpl
  ```

解决方法：

1. 停止 AEM 实例。转到 `<aem_server_path_on_server>crx-quickstart\conf` 并打开 `sling.properties` 文件。Adobe 建议先备份此文件。

1. 搜索 `org.osgi.framework.bootdelegation=`。添加 `jdk.internal.reflect,jdk.internal.reflect.*` 属性，使结果如下所示。

```java
org.osgi.framework.bootdelegation=sun.*,com.sun.*,jdk.internal.reflect,jdk.internal.reflect.*
```

1. 保存文件并重新启动 AEM 实例。

### Sites {#sites}

* **页面版本管理**：[如果页面已被移动，则无法再预览移动前创建的任何版本](/help/sites-authoring/working-with-page-versions.md#previewing-a-version)。

### Assets {#assets}

* **搜索：**&#x200B;当搜索字符串包含前导空格时，搜索不会返回任何结果（[OAK-4786](https://issues.apache.org/jira/browse/OAK-4786)）
* **文件夹元数据架构**：添加选择按钮后，ID 和 Value 字段未按预期呈现，并且删除功能不可用。（CQ-4261144）
* 重命名资产时，资产名称中无法使用空格字符。（CQ-4266403）

### Forms {#forms}

* 在 Linux® 操作系统上安装 AEM Forms 时，使用硬件安全模块的数字签名功能无法正常工作。（CQ-4266721）
* （仅适用于 WebSphere® 上的 AEM Forms）在 **Forms Workflow** > **任务搜索**&#x200B;中，如果以&#x200B;**用户名**&#x200B;作为搜索条件来搜索&#x200B;**管理员**，则不会返回任何结果。（CQ-4266457）

* AEM Forms 无法将使用 JPEG 压缩的 TIF 和 TIFF 文件转化为 PDF 文档。（CQ-4265972）
* 在 **AEM Forms 迁移**&#x200B;页面上，**AEM Forms Assets Scanner** 以及 **Letter to Interactive Communication Migration** 选项无法使用。（CQ-4266572）

* （仅适用于 JBoss® 7）当您从早期版本升级至 AEM 6.5 Forms，并且早期版本中存在创建并使用默认提交或默认渲染流程副本的流程（.lca）时，基于此类流程（.lca）的 HTML5 Forms 无法执行所需操作。（CQ-4243928）
* 在自适应表单中，当通过规则编辑器调用表单数据模型服务以动态更新图像选择组件的值时，图像选择组件的值不会更新。（CQ-4254754）
* AEM Forms Designer 安装程序需要 32 位版本的 [Visual C++ 可再发行运行时包 2012](https://docs.microsoft.com/en-US/cpp/windows/latest-supported-vc-redist?view=msvc-170) 以及 [Visual C++ 可再发行运行时包 2013](https://support.microsoft.com/en-us/topic/update-for-visual-c-2013-and-visual-c-redistributable-package-5b2ac5ab-4139-8acc-08e2-9578ec9b2cf1)。在开始安装前，请确保已安装上述可再发行运行时包。（CQ-4265668）

* PDF Generator 不支持基于智能卡的身份验证。当管理员在 Windows 服务器上启用组策略 `Interactive Logon: Require Smart card` 时，所有现有的 PDF Generator 用户都会失效。

* 当自适应表单被配置为动态更新某组件的值，并且承载该表单的发布实例是通过 Dispatcher 访问时，字段的动态更新功能将会停止工作。要解决此问题，请在发布实例上打开 CRXDE，导航至 `/libs/fd/af/runtime/clientlibs/guideChartReducer`，并创建如下所示的属性。

   * 名称：allowProxy
   * 类型：布尔值
   * 值：真
   * 受保护：假
   * 必填：假
   * 多值：假
   * 自动创建：假

  该属性允许运行时文件夹下的客户端库访问代理。（CQ-4268679）

* 当启动 AEM Forms 时，会出现 `SAX Security Manager could not be setup` 警告。
* 在 Apple iOS 或 iPadOS 上运行 Adobe Acrobat Reader 20.10.00 版本时，打开使用 AEM Forms Document Security 保护的 PDF 文件会出现问题。
* 在从 Apple iOS 设备提交包含标准 HTML 上传字段的表单时，有时不会发送文件内容，而在另一端会收到一个 0 字节的文件。Apple iOS 15.1 修复了此问题。

## 产品下载与支持（受限网站） {#product-download-and-support-restricted-sites}

以下网站仅向客户开放。如果您已是客户并需要访问权限，请联系您的 Adobe 客户经理。

* [在 licensing.adobe.com 下载产品](https://licensing.adobe.com/)。

* 在[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)中获取产品更新、补丁及附加功能包。

* [通过 Admin Console 获取客户支持](https://adminconsole.adobe.com/)。若要了解更多信息，请参阅[全新 Adobe 客户支持体验](https://experienceleague.adobe.com/docs/customer-one/using/home.html?lang=zh-Hans)。
