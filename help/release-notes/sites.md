---
title: AEM Sites 发行说明
description: 以下发行说明特定于 Adobe Experience Manager 6.5 Sites。
exl-id: 0bd0933c-f14d-4be2-9ad0-3f8207d7fa5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 68%

---

# AEM Sites 发行说明 {#aem-sites-release-notes}

有关 AEM Sites 6.5 增强功能的详细信息，请参阅以下内容：

## 组件和模板开发{#component-amp-template-development}

* 用于新项目的 Maven Project Archetype 18+，请参阅 [Github 以查看发行说明](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases)。
* 用于新项目的单页应用程序 Maven Project Archetype 1.0.6+，请参阅 [Github 以查看发行说明](https://github.com/adobe/aem-spa-project-archetype/releases)。
* HTL 版本 1.4，请参阅 [Github 以查看发行说明](https://github.com/adobe/htl-spec/releases/tag/1.4)。

   * 字符串、数组和对象的“in”运算符：

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * 具有data-sly-set的变量声明：
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * 列出和重复控制参数：开始、步骤、结束：
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * data-sly-unwrap的标识符：

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * 支持负数

* Core Components 2.3.2+，请参阅 [Github 以查看发行说明](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases)。
* 布局容器的网格系统，请参阅 [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid)。
* Clientlib管理器：将Google Closure Compiler设为JavaScript clientlibs缩小的默认值（以前的默认值为Yahoo YUI），并将Google Closure Compiler更新为版本v20190121
* 模板编辑器和策略

   * 为使用 JS SDK（也称为 SPA 编辑器）的单页应用程序创建和编辑模板

* 引用站点 We.Retail 4.0，请参阅 [Github 以查看发行说明](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases)。
* 用于升级现有站点以利用最新编辑器功能的工具包，请参阅[Github存储库](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM包含jQuery库版本1.12.4，可最大程度地与现有自定义代码兼容。 Adobe 已对其进行了修改以解决已知的安全问题。

## 站点管理  {#site-administration}

* [引用](/help/sites-authoring/author-environment-tools.md#references)边栏中新增了一个部分，用于列出指向所选页面的内部链接。如果计划使页面处于脱机状态或删除页面，此边栏非常有用 - 可在脱机之前查看需要调整的页面。
* [列表视图](/help/sites-authoring/basic-handling.md#list-view)中有一个新的工作流列，用于显示页面当前在工作流中的状态。
* 在[页面属性](/help/sites-authoring/editing-page-properties.md)中，现在可以在为页面指定缩略图（“缩略图”选项卡）时浏览现有资产。

## 页面编辑器 {#page-editor}

* 允许对利用 JS SDK（也称为 SPA 编辑器）的 React 和 Angular 客户端组件构建的单页应用程序体验执行上下文编辑和合成操作
* 仅当页面配置了基架页面时，才会显示基架模式。

## 内容片段和编辑器 {#content-fragments-amp-editor}

* 在内容片段编辑器中新增了[注释](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations)边栏，用于发表常规评论和查看文本中的评论（也显示在“时间轴”边栏中）
* 能够将[内容片段模型](/help/assets/content-fragments/content-fragments-models.md)中多行文本元素的默认内容类型设置为简单文本、富文本或标记
* 可通过选择 RTE 中的文本（全屏视图）添加[评论/注释](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* 可通过“引用”边栏并排[比较各个版本的内容片段](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions)
* 资产“下载报表”现在会相应地显示内容片段
* 可通过 /api.json 将[内容片段支持添加到资产 HTTP API](/help/assets/assets-api-content-fragments.md)。提供了用于创建、更新、读取和删除内容片段的 API。

## 体验片段 {#experience-fragments}

* 改进了[体验片段](/help/sites-authoring/experience-fragments.md)的索引，现在可通过搜索正在使用它们的页面查找它们的内容
* 通过[导出到 Target](/help/sites-administering/experience-fragments-target.md) 选项，您现在可以将体验片段作为 JSON（默认为 HTML）或两者发送

## 翻译 {#translation}

* 使用项目母版简化了翻译项目创建过程
* 通过默认将翻译作业设置为已批准状态，简化了翻译项目执行过程
* 允许使用第三方翻译记忆库中的更改更新翻译页面
* 允许以 JSON 格式导出翻译作业
* 更新了 Microsoft Translation 集成以使用 V3 API

## 多站点管理 (MSM) {#multi-site-management-msm}

* 对于使用 PushOnModify 的转出配置，优化了页面移动操作的处理以避免出现不一致的状态
* 现在，在活动副本结构中创建新页面将会默认创建一个独立页面
* 可在使用 JS SDK（也称为 SPA 编辑器）的单页应用程序中使用 MSM 功能

## 启动项 {#launches}

* 新增了启动项的审核和批准工作流，可仅提升已批准的启动页面
* 向 UI 中添加了[可选择在提升步骤后立即删除启动项的选项](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## 内容定位和模拟  {#content-targeting-simulation}

* 已将 ContextHub 数据层和客户端规则引擎 JavaScript 更新为默认使用 jQuery 3。

## AEM和Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>当前：
>
>* 如果在AEM Activities控制台中将Adobe Target用作定位引擎，则仅支持`at.js 1.x`。
   >
   >
* 如果您使用将体验片段导出到Target并在Target控制台中运行活动，则`at.js. 1.x`和`at.js 2.x`都受支持。


* Adobe Target 集成现在可以使用 Target Standard API。AEM的早期版本使用Target Classic HTTP API，该API现已弃用。
* 包含Adobe Target `mbox.js`版本63。 Adobe强烈建议将实施切换到`at.js` v1.x。
* `at.js` 现已包含版本1.5.0。Adobe建议您使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)将`at.js` v1.x配置到站点中。

## AEM和Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` 包含H.27.5。Adobe建议您将实施切换为`AppMeasurement.js`
* `AppMeasurement.js` 包含v1.8.0。Adobe建议使用[Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html)将AppMeasurement.js配置到站点中。

## AEM和Commerce {#aem-commerce}

自AEM 6.4以来，商务集成框架的改进更快了发行周期。 [单击此处了解详情](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html)。

## Communities 加载项 {#communities-add-on}

请参阅 [Communities 发行说明页面](../release-notes/communities-release-notes.md)

## Screens 加载项  {#screens-add-on}

* 使用启动项规划标牌内容的未来内容更改
* 序列渠道中按流量计费的播放
* 使用源文件（例如 Excel 表格）自动创建项目结构

有关对AEM Screens所做更改的更多详细信息 — 请参阅[AEM Screens用户指南](https://docs.adobe.com/content/help/zh-Hans/experience-manager-screens/user-guide/aem-screens-introduction.html)中的发行说明。
