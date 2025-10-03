---
title: Adobe Experience Manager 6.5 版本中已弃用和已移除的功能。
description: Adobe Experience Manager 6.5 中已弃用和已移除功能的发行说明。
exl-id: d9b6140a-c37d-4b90-a60c-01f471d65621
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: bd29ae46ead836e16362ad3a9a63bb31548415ff
workflow-type: ht
source-wordcount: '1765'
ht-degree: 100%

---

# 已弃用和已移除的功能 {#deprecated-and-removed-features}

<!-- Search&Promote is end-of-life September 1, 2022 | Assets | If a user does not have sufficient (read and write) permissions on `/content/dam/collections`, the user cannot create a Collection. | Honor the access control setup of user and ensure appropriate permissions. ||
|Adobe Search & Promote|The integration with Adobe Search & Promote is deprecated. Adobe does not plan to make further enhancements to the Search & Promote integration. Adobe Search & Promote integration remains fully supported while being deprecated.||| -->

Adobe 持续评估产品功能，并在长期演进中不断重塑或替换旧功能，以更现代的替代方案提升整体客户价值，同时始终谨慎考量向后兼容性。

为传达即将移除或替换的 Adobe Experience Manager（AEM）功能，适用以下规则：

1. 首先发布弃用公告。功能在弃用阶段仍可使用，但不会再进行改进。
1. 弃用功能最早会在下一个主要版本中移除。实际移除目标日期将在稍后公布。

在实际移除之前，此流程会为客户提供至少一个发布周期，以便他们有时间将其实施调整到新版本或已弃用功能的后继版本。

## 已弃用的功能  {#deprecated-features}

本节列出了在 AEM 6.5 中已标记为弃用的功能和特性。通常，计划在未来版本中移除的功能会先标记为弃用，并同时提供替代方案。

建议客户检查其当前部署中是否正在使用该特性/功能，并计划将实施方式调整为使用所提供的替代方案。

| 区域 | 专题 | 替换 | 版本（SP） |
|---|---|---|---|
| Sites | [SPA 编辑器](/help/sites-developing/spa-editor-deprecation.md) | 针对 Headless 用例，请使用[通用编辑器](/help/sites-developing/universal-editor/introduction.md)进行可视化编辑，或使用[内容片段编辑器](/help/sites-developing/universal-editor/introduction.md)进行基于表单的编辑。 | 6.5.23 |
| Sites | **Adobe AEM 托管的轮询配置**&#x200B;服务：`com.day.cq.polling.importer.impl.ManagedPollConfigImpl` | **Adobe AEM Analytics 报告 Sling 导入器**&#x200B;服务。参见《连接到 Adobe Analytics 并创建框架》——[配置导入间隔](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval) | 6.5.19.0 |
| Screens | Adobe Experience Manager（AEM）中的 ActiveMQ。ActiveMQ 曾用于两个 AEM 发布实例之间的通信。 | Adobe 建议客户现在改为使用负载均衡器。 | 6.5.18.0 |
| **社交媒体状态**&#x200B;的体验片段属性。 |   | 6.5.11.0 |
| [!DNL Sites] | 内容片段模板，用于创建简单的内容片段。 | 现已提供[基于模型的结构化内容片段](/help/assets/content-fragments/content-fragments-models.md)。 | 6.5.11.0 |
| Creative Cloud 集成 | AEM 至 Creative Cloud 文件夹共享功能是在 AEM 6.2 中引入的。它为创意用户提供了一种从 AEM 访问资产的方式，以便在 [!DNL Creative Cloud] 应用程序中打开，并将新文件上传或将更改保存到 AEM。Creative Cloud 应用程序中推出的新功能 Adobe Asset Link，能够在 Photoshop、InDesign 和 Illustrator 中直接访问 AEM 资产，从而带来更佳的用户体验和更强大的功能。Adobe 不再计划增强 AEM 与 Creative Cloud 文件夹共享的集成功能。尽管该功能仍包含在 AEM 中，但建议客户使用替代方案。 | 建议客户改用新的 Creative Cloud 集成功能，包括 Adobe Asset Link 或 AEM 桌面应用程序。 |  |
| Assets | 在发布实例中，`AssetDownloadServlet` 默认被禁用。详情请参阅 [AEM 安全清单](/help/sites-administering/security-checklist.md)。 | 配置说明见 [AEM 安全清单](/help/sites-administering/security-checklist.md)。 |  |
| 集成 | 界面 **[!UICONTROL Experience Manager 云服务选择加入]**&#x200B;功能已弃用，因为 [!DNL Experience Manager] 与 [!DNL Adobe Target] 的集成已在 [!DNL Experience Manager] 6.5 中更新。该集成支持 Adobe Target Standard API。该 API 使用 Adobe IMS 和 [!DNL Adobe I/O Runtime] 进行身份验证。它支持利用 Adobe Launch 对 [!DNL Experience Manager] 页面进行分析与个性化的增强功能，因此原有的选择加入向导已不再具有实际意义。 | 请通过相应的 [!DNL Experience Manager] 云服务配置系统连接、Adobe IMS 身份验证及 [!DNL Adobe I/O Runtime] 集成。 | 6.5.7.0 |
| 连接器 | 适用于 [!DNL Experience Manager] 6.5 的 Adobe JCR 连接器（用于 Microsoft® SharePoint 2010 和 Microsoft® SharePoint 2013）已弃用。 | 不适用 |  |
| 动态标记管理器（DTM） | 与 DTM 的集成已弃用。 | 请改用 Adobe Experience Platform Launch 作为标记管理器。 |   |
| Adobe Target | 在 AEM 6.5 中，新增了使用基于 [!DNL Adobe I/O] 的 Adobe Target Standard API（REST API）连接 Adobe Target 服务的功能，因此 Target Classic API（XML）方式已弃用。 | 请重新配置集成以[使用新的 API](/help/sites-administering/target.md)。 |  |
| Adobe Target | 在 AEM 中使用基于 `mbox.js` 的 Adobe Target 集成已弃用。 | 请改用 `at.js` 1.x。 |  |
| Commerce | 2018 年，[CIF REST](https://github.com/adobe/commerce-cif-api) 作为一组微服务提供，用于支持 AEM 与电商引擎的集成。Adobe 在于 2018 年中期收购 Adobe Commerce（原 Magento）后，基于以下两点原因决定调整策略。Commerce 已有自己的一套 Commerce API（REST 和 GraphQL），维持两套 API 并不是好的做法。市场趋势表明，客户正逐步转向 GraphQL，因为这是一种更高效的数据查询方式。2019 年，Adobe 发布了新的 Commerce 集成框架，其中使用 Commerce 的 GraphQL API 作为可信的数据源。Adobe 不再计划对 CIF REST 进行进一步投入。建议客户使用替代方案。 | 对于 AEM-Commerce 集成，请切换至 [AEM CIF Archetype](https://github.com/adobe/aem-cif-project-archetype) 和 [AEM CIF 核心组件](https://github.com/adobe/aem-core-cif-components)。请参阅[使用 Commerce 集成框架](/help/commerce/cif/integrating/magento.md)实现 AEM 与 Adobe Commerce 的集成。支持采用该新方法的第三方（非 Commerce）集成已纳入 Adobe 的产品路线图。 |  |
| 组件（AEM Sites） | Adobe 不再计划对存储在 `/libs/foundation/components` 下的大多数基础组件进行进一步增强。可在组件文件夹中查找 `cq:deprecated` 和 `cq:deprecatedReason` 属性。AEM 6.5 仍包含基础组件，客户从早期版本升级后可继续按原方式使用。此外，尽管这些基础组件已弃用，但仍为其提供支持。 | Adobe 建议在未来的项目中使用核心组件。现有站点可保持不变，或使用 [AEM Modernize Tools Suite](https://github.com/adobe/aem-modernize-tools) 将站点重构为使用核心组件。 |  |
| 组件（AEM Sites） | 自 6.5 起，Design Importer 组件 `/libs/wcm/designimporter/components` 已标记为弃用。Adobe 不再计划增强该设计导入器的实施。 | Adobe 计划在未来版本中为该用例提供替代实施。 |  |
| 基础 | Granite 卸载框架。Adobe 不再计划增强在 CQ 5.6.1 中引入的用于实现资产处理外部化的卸载框架。 | Adobe 正在开发下一代云原生卸载框架。 |  |
| 开发人员 | `Hobbes.js`。Adobe 不再计划增强 `hobbes.js` 用户界面测试框架。 | Adobe 建议客户改用 Selenium 自动化工具。 |  |
| 开发人员 | jQuery UI 客户端库。Adobe 不再计划维护和更新随发行版（快速入门）提供的 jQuery UI 客户端库。 | Adobe 建议仍需要 jQuery UI 的客户将其直接添加到项目代码库中。 |  |
| 开发人员 | jQuery 动画客户端库（`granite.jquery.animation`）。Adobe 不再计划维护和更新随发行版（快速入门）提供的 jQuery 动画客户端库。 | Adobe 建议仍需要 jQuery 动画的客户将其直接添加到项目代码库中。 |  |
| 开发人员 | Handlebars 客户端库。Adobe 不再计划维护和更新随发行版（快速入门）提供的 Handlebars 客户端库。 | Adobe 建议仍需要 `Handlebars` 的客户将其直接添加到项目代码库中。 |  |
| 开发人员 | Lawnchair 客户端库。Adobe 不再计划维护和更新随发行版（快速入门）提供的 Lawnchair 客户端库。 | Adobe 建议仍需要 Lawnchair 的客户将其直接添加到项目代码库中。 |  |
| 开发人员 | `Granite.Sling.js` 客户端库。Adobe 不再计划增强随发行版（快速入门）提供的 Granite.Sling.js 客户端库。 | Adobe 建议依赖此库功能的客户重构代码，以停止使用该库。 |  |
| 开发人员 | 使用 YUI 对 JavaScript 客户端库进行压缩/缩小。Adobe 不再计划更新 YUI 库。在 AEM 6.4 之前，YUI 默认用于压缩 JavaScript，并提供切换至 Google Closure Compiler（GCC）的选项。从 AEM 6.5 开始，GCC 成为默认选项。 | Adobe 建议升级至 AEM 6.5 的客户在实施中改用 GCC。 |  |
| 开发人员 | CRXDE Lite 中的经典 UI 对话框编辑器。Adobe 不再计划增强随发行版（快速入门）提供的经典 UI 对话框编辑器。 | 暂无替代方案。 |  |
| Forms | AEM Forms 与 AEM Mobile 的集成已弃用。 | 暂无替代方案。 |
| 开发人员 | CRXDE Lite 中的经典 UI 对话框编辑器。Adobe 不再计划增强随发行版（快速入门）提供的经典 UI 对话框编辑器。 | 暂无替代方案。 |  |
| 开发人员 | Lodash/underscore 客户端库。Adobe 不再计划维护和更新随发行版（快速入门）提供的 Lodash/underscore 客户端库。 | Adobe 建议仍需要 Lodash/underscore 的客户将其直接添加到项目代码库中。 |  |

## 已移除的功能  {#removed-features}

本节列出了已从 AEM 6.5 中移除的功能和特性。在之前的版本中，这些功能已被标记为弃用。

| 区域 | 专题 | 替换 | 版本（SP） |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic 已移除。 | 您应迁移至 [AEM CIF](/help/commerce/cif/migration.md)。如仍需使用 CIF Classic，Adobe 创建了一份兼容包，请[联系 Adobe 客户支持](https://experienceleague.adobe.com/zh-hans?support-solution=General#support)。 | 6.5.22.0 |
| 与 [!DNL Experience Cloud] 集成 | 您可以通过 [!DNL Adobe I/O] 进行配置，将资产与 [!DNL Experience Cloud] 同步。[!DNL Adobe Experience Cloud] 之前称为 [!DNL Adobe Experience Cloud]。 | 如有任何问题，请[联系 Adobe 客户支持](https://experienceleague.adobe.com/zh-hans?support-solution=General#support)。 |  |
| Analytics Activity Map | AEM 中包含的 Activity Map 版本。 | 由于 Adobe Analytics API 的安全性更改，AEM 内置的 Activity Map 版本已无法继续使用。请使用 [Adobe Analytics 提供的 ActivityMap 插件](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=zh-Hans)。 |  |
| 集成 | ExactTarget 集成已从默认发行版（快速入门）中移除，且不再提供。 | 暂无替代方案。 |  |
| 集成 | Salesforce Force API 集成已从默认发行版（快速入门）中移除，现在作为额外安装包提供，可从[软件分发平台](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)获取。 | 该功能仍然可用。 |
| Forms | 对 Adobe Central Migration Bridge 服务的支持已移除，因为 Adobe Central 产品已不再受到支持。 | 暂无替代方案。 |  |
| Forms | `com.adobe.fd.df.fdinternal.model.ConfigurationInstance` | 暂无替代方案。 |  |
| Forms | `com.adobe.fd.ccm.channels.print.fdinternal.api.service.PrintDataTransformer` | 暂无替代方案 |  |
| Forms | 从 LiveCycle ES4 SP1 直接升级到 JEE 上的 AEM 6.5 Forms 的单步升级不可用 | 请参阅 AEM Forms 升级文档中的[可用升级路径](../forms/using/upgrade.md)。 |  |
| Forms | 已移除 JEE 上的 AEM Forms 中基于 UDP 的集群支持 | JEE 上的 AEM Forms 仅支持基于 TCP 的集群。如果您将早期版本中的 UDP 多播服务器升级至 JEE 上的 AEM 5.5 Forms，请执行手动配置，以切换至基于 TCP 的 gemfire 集群。详细说明请参阅[升级至 JEE 上的 AEM 6.5 Forms](../forms/using/upgrade-forms-jee.md)。 |  |
| 开发人员 | Firebug Lite 已从默认发行版（快速入门）中移除。 | 请使用浏览器内置开发者控制台。 |
| 开发人员 | HTML 客户端库管理器中对 `customJavaScriptPath` 的支持已移除。 | 暂无替代方案 |  |
| [!DNL Assets] | 在 [!DNL Adobe Experience Manager] 6.5 中已移除资产卸载功能。 | 暂无替代方案。 |  |
| 缓存 | `system/console/slingjsp` 已移除，并且在 AEM 6.5 中不再可用。 | 类和 Slightly 缓存存储在 Apache Sling Commons FileSystem ClassLoader 捆绑包下。您可以在 AEM网页控制台中查看捆绑包编号，并直接从文件系统（`crx-quickstart/launchpad/felix/bundle<ID>`）中移除缓存文件夹。 |  |
| Screens | 已移除 activemq 捆绑包支持及相关配置。 |  |  |

<!-- ## Pre-announcement for next release {#pre-announcement-for-next-release}

This section is used to pre-announce the upcoming changes in the future releases. The announced changes are not yet effective but will impact customers. For example, the features are not yet deprecated but impacts the users after deprecation. These updates are provided for planning purpose.

|Area|Feature|Announcement|
|--- |--- |--- |
|Foundation|UI Framework|Adobe is planning to deprecate the Coral UI 2 components in 2019. Coral UI 3 was introduced with AEM 6.2, and AEM 6.5 is fully based on Coral 3. Adobe recommends customers and partners that have build custom UIs with Coral 2 to refactored them to Coral 3. Adobe is providing a tool to convert Coral 2 dialogs to Coral 3 - [Read more](/help/sites-developing/modernization-tools.md).|
-->
