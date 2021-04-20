---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: AEM 6.5 Developing 用户指南
breadcrumb-title: Developing 指南
user-guide-description: 本指南介绍如何构建 AEM 实例。
feature-set: Experience Manager Sites
feature: Developing
role: Developer
translation-type: tm+mt
source-git-commit: d7b0803385aaa451a1ec7ec280ff51c3e96e36e7
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 16%

---


# AEM 6.5 Developing 用户指南 {#developing}

+ [开发用户指南概述](home.md)
+ 开发人员简介{#introduction}
   + [AEM Sites 开发入门- WKND 教程](getting-started.md)
   + [AEM Core Concepts](the-basics.md)
   + [AEM触屏优化UI的结构](touch-ui-structure.md)
   + [AEM触屏优化UI的概念](touch-ui-concepts.md)
   + [AEM开发 — 准则和最佳实践](dev-guidelines-bestpractices.md)
   + [使用客户端库](clientlibs.md)
   + [开发和页面差异](pagediff.md)
   + [编辑器限制](editor-limitations.md)
   + [CSRF保护框架](csrf-protection.md)
   + [数据建模 — David Nuescheler的模型](model-data.md)
   + [对AEM贡献](contributing-to-cq.md)
   + [安全](security.md)
   + [参考材料](reference-materials.md)
   + [创建功能齐备的网站（经典UI）](website.md)
   + [设计与设计人员（经典UI）](designer.md)
   + [迁移到触屏UI](/help/sites-developing/touch-ui-migration.md)
+ 平台{#platform}
   + [Sling 备忘单](sling-cheatsheet.md)
   + [使用 Sling 适配器](sling-adapters.md)
   + [标签库](taglib.md)
   + 模板{#templates}
      + [模板](templates.md)
      + [页面模板 — 可编辑  ](page-templates-editable.md)
      + [页面模板 — 静态](page-templates-static.md)
      + [内容片段模板](content-fragment-templates.md)
      + [自适应模板渲染](templates-adaptive-rendering.md)
   + [AEM中Sling资源合并的应用](sling-resource-merger.md)
   + [叠加](overlays.md)
   + [命名约定](naming-conventions.md)
   + [创建新的Granite UI字段组件](granite-ui-component.md)
   + 查询生成器{#query-builder}
      + [为查询 Builder实施自定义谓词计算器](implementing-custom-predicate-evaluator.md)
      + [查询 Builder谓词引用](querybuilder-predicate-reference.md)
      + [查询生成器 API](querybuilder-api.md)
   + 标记{#tagging}
      + [标记](tags.md)
      + [AEM Tagging Framework](framework.md)
      + [将标记构建到AEM应用程序](building.md)
   + [自定义由错误处理程序显示的页面](customizing-errorhandler-pages.md)
   + [自定义节点类型](custom-nodetypes.md)
   + [为图形渲染添加字体](adding-fonts.md)
   + [连接到SQL数据库](jdbc.md)
   + [外部化URL](externalizer.md)
   + [为卸载创建和使用作业](dev-offloading.md)
   + [配置Cookie使用](cookie-optout.md)
   + [如何以编程方式访问AEM JCR](access-jcr.md)
   + [将服务与JMX控制台集成](jmx-integration.md)
   + [开发批量编辑器](dev-bulk-editor.md)
   + [开发报告](dev-reports.md)
   + 电子商务{#ecommerce}
      + [电子商务](ecommerce.md)
      + [开发（通用）](generic.md)
      + [使用SAPCommerce Cloud进行开发](sap-commerce-cloud.md)
+ 组件{#components}
   + [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html)
   + [样式系统](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html)
   + [组件概述](components.md)
   + [AEM组件 — 基础](components-basics.md)
   + [开发AEM组件](developing-components.md)
   + [开发AEM组件 — 代码示例](developing-components-samples.md)
   + [内容服务的JSON导出器](json-exporter.md)
   + [为组件启用JSON导出](json-exporter-components.md)
   + [图像编辑器](image-editor.md)
   + [修饰标记](decoration-tag.md)
   + [使用隐藏条件](hide-conditions.md)
   + [配置多个就地编辑器](multiple-inplace-editors.md)
   + [开发人员模式](developer-mode.md)
   + [测试您的UI](hobbes.md)
   + [内容片段的组件](components-content-fragments.md)
   + [以JSON格式获取页面信息](pageinfo.md)
   + 国际化{#internationalization}
      + [组件国际化](i18n.md)
      + [国际化UI字符串](i18n-dev.md)
      + [使用翻译器管理词典](i18n-translator.md)
      + [提取字符串以进行翻译](i18n-extract.md)
   + 经典UI组件{#classic-ui-components}
      + [开发AEM组件（经典UI）](developing-components-classic.md)
      + [使用和扩展构件（经典UI）](widgets.md)
      + [使用xtypes（经典UI）](xtypes.md)
      + [开发Forms（经典UI）](developing-forms.md)
+ 无外设体验管理{#headless}
   + [无外设与包含AEM的混合](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
   + [为组件启用JSON导出](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/json-exporter-components.html)
   + 单页应用程序{#spas}
      + [SPA简介和演练](spa-walkthrough.md)
      + [SPA WKND教程](spa-wknd.md)
      + [AEM中的SPA入门 — 反应](spa-getting-started-react.md)
      + [AEM中的SPA入门 — Angular](spa-getting-started-angular.md)
      + [为 SPA 实施 React 组件](spa-implementing-react-component.md)
      + [SPA深潜](spa-deep-dives.md)
      + [SPA Editor概述](spa-overview.md)
      + [为AEM开发SPA](spa-architecture.md)
      + [SPA Blueprint](spa-blueprint.md)
      + [SPA页面组件](spa-page-component.md)
      + [SPA的动态模型到组件映射](spa-dynamic-model-to-component-mapping.md)
      + [SPA模型路由](spa-routing.md)
      + [SPA和Adobe Experience Platform Launch集成](spa-launch.md)
      + [SPA和服务器端渲染](spa-ssr.md)
      + [RemotePage组件](spa-remote-page.md)
      + [在AEM中编辑外部SPA](spa-edit-external.md)
      + [在SPA中组合组件](spa-composite-component.md)
      + [SPA参考材料](spa-reference-materials.md)
   + [HTTP API](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html)
   + [内容片段](https://experienceleague.adobe.com/docs/experience-manager-65/assets/fragments/content-fragments.html)
   + [体验片段](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/authoring/experience-fragments.html)
   + [了解AEM中的内容片段和内容服务](https://helpx.adobe.com/experience-manager/kt/sites/using/content-fragments-content-services-feature-video-understand.html)
+ 开发工具{#devtools}
   + [开发工具](dev-tools.md)
   + [AEM 现代化工具](modernization-tools.md)
   + [对话框编辑器](dialog-editor.md)
   + [对话框转换工具](dialog-conversion.md)
   + [使用CRXDE Lite开发](developing-with-crxde-lite.md)
   + [使用Maven管理包](vlt-mavenplugin.md)
   + [如何使用Eclipse开发AEM项目](howto-projects-eclipse.md)
   + [如何使用Apache Maven构建AEM项目](ht-projects-maven.md)
   + [如何使用IntelliJ IDEA开发AEM项目](ht-intellij.md)
   + [如何使用VLT工具](ht-vlttool.md)
   + [如何使用Proxy Server Tool](ht-proxy-server.md)
   + [AEM Brackets扩展](aem-brackets.md)
   + [AEM Developer Tools for Eclipse](aem-eclipse.md)
   + [AEM Repo 工具](aem-repo-tool.md)
+ 个性化{#personlization}
   + [ContextHub](contexthub.md)
   + [配置Context Hub](ch-configuring.md)
   + [将ContextHub添加到页面和访问存储](ch-adding.md)
   + [扩展ContextHub](ch-extend.md)
   + [示例ContextHub存储候选项](ch-samplestores.md)
   + [示例ContextHub UI模块类型](ch-samplemodules.md)
   + [ContextHub诊断](ch-diagnostics.md)
   + [针对目标内容进行开发](target.md)
   + [ContextHub Javascript API参考](contexthub-api.md)
   + ClientContext{#client-context}
      + [Client Context详解](client-context.md)
      + [Client Context Javascript API](ccjsapi.md)
+ 扩展AEM{#extending-aem}
   + [自定义页面创作](customizing-page-authoring-touch.md)
   + [自定义控制台](customizing-consoles-touch.md)
   + [自定义页面属性的视图](page-properties-views.md)
   + [配置页面以批量编辑页面属性](bulk-editing.md)
   + [自定义和扩展内容片段](customizing-content-fragments.md)
   + [内容片段配置用于渲染的组件](content-fragments-config-components-rendering.md)
   + [体验片段](experience-fragments.md)
   + 扩展工作流{#extending-workflows}
      + [开发和扩展工作流](workflows.md)
      + [创建工作流模型](workflows-models.md)
      + [扩展工作流功能](workflows-customizing-extending.md)
      + [以编程方式与工作流交互](workflows-program-interaction.md)
      + [工作流步骤参考](workflows-step-ref.md)
      + [工作流程最佳实践](workflows-best-practices.md)
      + [工作流过程参考](workflows-process-ref.md)
      + [AEM工作流中的变量](/help/sites-developing/using-variables-in-aem-workflows.md)
   + [扩展多站点管理器](extending-msm.md)
   + 跟踪和分析{#extending-analytics}
      + [扩展事件跟踪](extending-analytics.md)
      + [将Adobe Analytics跟踪添加到组件](extending-analytics-components.md)
      + [自定义Adobe Analytics Framework](extending-analytics-framework.md)
      + [为Analytics实施服务器端页面命名](extending-analytics-pa-naming.md)
   + 云服务{#extending-cloud-services}
      + [云服务配置](extending-cloud-config.md)
      + [创建自定义Cloud Service](extending-cloud-config-custom-cloud.md)
   + [创建自定义扩展](extending-campaign-extensions.md)
   + 表单{#extending-forms}
      + [创建自定义表单映射](extending-campaign-form-mapping.md)
      + [使用AEM表单组件创建自定义Adobe Campaign页面模板](extending-campaign-custom-template.md)
      + [请求分析脚本](analyze-request.md)
   + [将服务与JMX控制台集成](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/jmx-integration.html)
   + [开发批量编辑器](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-bulk-editor.html)
   + 扩展经典UI{#extending-classic-ui}
      + [自定义网站控制台（经典UI）](customizing-siteadmin.md)
      + [自定义欢迎控制台（经典UI）](customizing-the-welcome-console.md)
      + [开发报告](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-reports.html)
+ 测试{#testing}
   + [规划](planning.md)
   + [需要哪些测试环境?](test-environments.md)
   + [定义测试用例](test-cases.md)
   + [测试 — 何时和与谁一起？](when-who.md)
   + [编译测试计划](test-plan.md)
   + [跟踪结果并提供反馈](results-and-feedback.md)
   + [测试和跟踪工具](tools.md)
   + [接受和签署](acceptance-signoff.md)
   + [下一个版本……](the-next-release.md)
   + [核对清单](checklists.md)
   + [《苦日》](tough-day.md)
   + [测试您的UI](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/hobbes.html)
+ 最佳实践{#bestpractices}
   + [最佳实践概述](best-practices.md)
   + [AEM开发指南和最佳实践](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/dev-guidelines-bestpractices.html)
   + [开发最佳实践](development-practices.md)
   + [内容架构](content-architecture.md)
   + [软件架构](software-architecture.md)
   + We.Retail Reference Implementation{#we-retail}
      + [We.Retail Reference Implementation](we-retail.md)
      + [在We.Retail中试用内容片段](we-retail-content-fragments.md)
      + [在We.Retail中试用核心组件](we-retail-core-components.md)
      + [在We.Retail中试用可编辑的模板](we-retail-editable-templates.md)
      + [在We.Retail中试用响应式布局](we-retail-responsive-layout.md)
      + [We.Retail中的全球化网站结构](we-retail-globalized-site-structure.md)
      + [在We.Retail中试用体验片段](we-retail-experience-fragments.md)
   + [编码提示](coding-tips.md)
   + [代码缺陷](code-pitfalls.md)
   + [OSGI捆绑](osgi-bundles.md)
   + [JCR集成](jcr-integration.md)
   + [代码样本](code-samples.md)
   + [慢速查询疑难解答](troubleshooting-slow-queries.md)
+ 移动 Web{#mobileweb}
   + [移动 Web](mobile-web.md)
   + [创建设备组过滤器](groupfilters.md)
   + [网页响应式设计](responsive.md)
   + [为移动设备创建站点](mobile.md)
   + [模拟器](emulators.md)
