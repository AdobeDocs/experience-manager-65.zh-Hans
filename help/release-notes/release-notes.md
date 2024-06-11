---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作说明以及的详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: a52311b9-ed7a-432e-8f35-d045c0d8ea4c
source-git-commit: 004cf5b30fa3bd108a45a8b6322f2ee3d3085ee5
workflow-type: tm+mt
source-wordcount: '3050'
ht-degree: 3%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in this release information, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.21.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2024年6月6日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包括的内容 [!DNL Experience Manager] 6.5.21.0 {#what-is-included-in-aem-6521}

[!DNL Experience Manager] 6.5.21.0包括新增功能、客户请求的关键增强功能和错误修复。 其中还包括自2019年4月6.5首次发布以来在性能、稳定性和安全性方面做出的改进。 [安装此Service Pack](#install) 日期 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增强功能

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的某些主要功能和增强功能包括：

* 用于服务器到服务器身份验证的更易于使用的新凭据，替换了现有的服务帐户(JWT)凭据。 (NPR-41994)

### [!DNL Assets]

#### 增强

以下是此版本中包含的增强功能列表：

* IPTC选项卡现在支持 [!UICONTROL 替换文本] 和 [!UICONTROL 扩展描述] 文本字段。 (ASSETS-34918)

#### 辅助功能修复

以下是此版本中包含的辅助功能修复列表：

* 如果资产的处理状态为“失败”或“元数据失败”，则字幕和音频轨道UI将无法正常工作。 (ASSETS-37281)
* 在保存资源元数据并尝试编辑它时，语言名称不显示。 (ASSETS-37281)

<!-- ### [!DNL Forms]
* A -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 21中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-6521}

#### 辅助功能 {#sites-accessibility-6521}

* 此 **[!UICONTROL 保存的搜索]** 标签不是永久性的。 占位符用作文本字段的唯一可视标签。 (SITES-3050)

#### 管理员用户界面{#sites-adminui-6521}

* 当您单击 **[!UICONTROL 站点]** > **[!UICONTROL 核心组件]** > **[!UICONTROL 属性]** > **[!UICONTROL 权限]** 选项卡> **[!UICONTROL 有效权限]**， **有效权限** 对话框在中未打开。 (SITES-17378)

<!-- #### Classic UI{#sites-classicui-6521} 

* A -->

#### [!DNL Content Fragments]{#sites-contentfragments-6521}

* 修复了重复包含表单元素的问题。 (SITES-21109)
* 创建内容片段时，“关闭”按钮有时变得无响应，导致整个页面冻结，并需要页面刷新以关闭内容片段。 至于版本创建问题，系统正在创建新版本的内容片段。 即使用户未进行任何更改，仅通过与RTE或文本字段交互也会发生此问题。 (SITES-21187)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6521}

* 将Adobe Experience Manager从6.5.19.0升级到6.5.20.0时，路径 `/libs/cq/graphql/sites/graphiql` 正在被删除。 (SITES-20098)

<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6521}

* W -->

<!-- #### [!DNL Content Fragments] - REST API{#sites-restapi-6521}

* W -->

<!-- #### Core Backend{#sites-core-backend-6521}

* W -->

<!-- #### Core Components{#sites-core-components-6521}

* I -->

<!-- #### Campaign integration{#sites-campaign-integration-6521}

* A -->

#### 体验片段{#sites-experiencefragments-6521}

* 从中转出体验片段 `masters/language` 到 `country/language` 不会更新交叉引用。 (SITES-21172)
* 模板不仅在 `cq:allowedTemplates`，但模板具有 `allowedPaths` 在模板级别配置，在创建新体验片段时显示为选项。 (SITES-20855)

<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6521}

* T -->

<!-- #### Launches{#sites-launches-6521} -->

<!-- DELETED MAY 22, 2024 FROM TOTAL RELEASE CANDIDATE ISSUES * The `sourceRootResource` configured in the Launch configuration within CRXDE Lite points to content that no longer exists, leading to a malfunction when attempts are made to delete launches. Delete launches even if the page is deleted or if the path is not the same. (SITES-20750) -->

#### MSM — 活动副本{#sites-msm-live-copies-6521}

* 叠加页面组件以在页面属性中添加选项卡。 其中之一是页面配置，并具有用于添加体验片段URL的属性。 在体验片段的页面属性中配置的链接，不会更改为该页面创建的任何语言副本。 配置的链接应随语言副本URL而更改。 (SITES-19580)

#### 页面编辑器{#sites-pageeditor-6521}

* 编辑模式应用灰色背景的方式不一致，因此无法符合WCAG（Web内容辅助功能准则）颜色对比度标准。 (SITES-20060)

### [!DNL Assets]{#assets-6521}

* 如果将资产发布到Brand Portal，则发布状态将保持不一致。 (ASSETS-36807)
* 使用API调用从实例中删除资产时，不会删除资产。 (ASSETS-35131)
* 当您尝试导入元数据时， `question mark (?)` 替换以英语以外的任何语言插入的字符。  (ASSETS-35091)
* 时间 `dc:title` 属性与数据类型字符串一起使用，安装Service Pack 6.5.19后，资产内容树无法正常工作。 (ASSETS-34684)
* 如果资产名称中包含任何特殊字符，则会显示错误。 (ASSETS-33248)

#### [!DNL Dynamic Media]{#assets-dm-6521}

* 在AEM 6.5.18中，当您编辑热点时，不会显示添加到资源的所有热点。 但是，所有热点都可以在已发布的资产中使用，但如果您需要编辑，则以后无法再编辑它们。 (ASSETS-33609)
* 上传的最新EPS文件在重新处理后不会生成缩略图。 (ASSETS-32617)
* 在“工具”>“Assets”>“Dynamic Media发布设置”>“请求属性”选项卡中，输入以下内容 `Width(px)` 和 `Height(px)` 西班牙语、意大利语和葡萄牙语看起来都不一样。 对于这些位置，它们彼此不对齐。 (ASSETS-31896)
* 自2024年5月1日起，AdobeDynamic Media停止支持以下内容：
   * SSL（安全套接字层）2.0
   * SSL 3.0
   * TLS（传输层安全性）1.0 和 1.1
   * TLS 1.2 中的以下弱密码：
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`

### [!DNL Forms]{#forms-6521}

中的修复 [!DNL Experience Manager] Forms在计划的一周后通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack发行日期。 在本例中，AEM 6.5.21.0 Forms附加组件包版本计划于2024年6月13日星期四发布。 发布后，此部分中添加了Forms修复和增强功能的列表。

<!-- #### [!DNL Adaptive Forms]

* THIS BUG WAS ALREADY REPORTED IN THE 6.5.20.0 RELEASE NOTES. IS IT NEEDED AGAIN IN THE 6.5.21.0 RELEASE NOTES? (AEM Forms on JEE Only) The PDF Generator service fails to enumerate the fonts available on the server. Consequently, the font selection panel on the Adobe PDF Settings page in the PDFG Admin UI remains empty, effectively preventing (un)embedding of chosen fonts. (FORMS-12095) -->


<!-- #### [!DNL Forms Designer] {#forms-designer-6521}

* W -->

### Foundation {#foundation-6521}

#### Apache Felix {#foundation-apachefelix-6521}

* 在AEM 6.5 Service Pack 19 (SP19)中升级的问题，该问题导致在安装SP19之后对Apache Felix的未授权请求缺少应用程序服务器上下文根路径。 更新至Apache Felix Web Management Console 4.9.8。 (NPR-41933)

#### 营销活动{#foundation-campaign-6521}

* AEM 6.5 Service Pack 15正在生成包含重要条目的连续错误日志。 报告了以下问题：

   * 路径中缺少资源时出现404 INFO错误 `/libs/granite/ui/content/shell/start.html`
   * 未捕获的SlingException的错误日志条目，原因是 `NullPointerException` 在 `CampaignsDataSourceServlet.java:147`

  错误日志中不应填充频繁且大量的错误条目，AEM实例应该可以正常运行，而不会出现与缺少资源或异常相关的问题。 (CQ-4357064)

#### Cloud Service{#foundation-cloudservices-6521}

* 从AEMCloud Service中删除Google Guava。 (CQ-4356436)

<!-- #### Communities {#foundation-communities-6521}

* U -->

<!-- #### Content distribution{#foundation-content-distribution-6521}

* T -->

#### Granite{#foundation-granite-6521}

* 您无法选择 **删除** 或 **修改** 不含 **浏览** 权限。 (GRANITE-51002)

#### 集成{#foundation-integrations-6521}

* 相关 `cq-target-integration`，需要删除Google Guava的非测试用法。 (CQ-4357101)
* 使用OAuth2服务器到服务器凭据（也称为服务主体）替换服务帐户（JSON Web令牌或JWT）凭据。 (NPR-41994)
* 创建Audience请求失败，无法进行IMS (Identity Management System)配置。 (NPR-41888)
* 当客户尝试查看有效负载页面时，由于URL格式不正确，内容无法正确显示；显示404错误。 URL中查询参数前缺少问号符号会导致错误。 此问题要求客户插入问号符号以正确查看有效负载页面。 (NPR-41957)
* 从AEM 6.5中删除了AdobeSearch&amp;Promote的代码和依赖项，这些代码和依赖项已在生命周期结束 [2022年9月（按通知）](https://experienceleague.adobe.com/en/docs/discontinued/using/search-promote). (NPR-41855)

#### 本地化{#foundation-localization-6521}

* 在模板编辑器中，文本字符串 *`No video available.`* 未本地化。 (SITES-13190)
* 激活或停用用户后的字符串在中未本地化 **工具** > **安全性** > **用户** > *任意用户名* > **激活** > **确定**，并选择 *任意用户名* > **取消激活** > **确定**. (NPR-41737)

#### Oak {#foundation-oak-6521}

* 性能回归修复 — 避免对类似条件进行范围查询。 (OAK-9481)
* 新的Oak版本是1.22.20。

#### Platform{#foundation-platform-6521}

* 此 `Unclosed resource resolver` 以下对象正在遇到错误 `com.day.cq.mailer.impl.DefaultMailService`. 此 `MessageGatewayService` 类是现成的，在没有资源解析程序的情况下使用。 任何带有表单提交按钮的页面出现问题，该按钮使用此类发送电子邮件。 (NPR-41853)
* 在 **关于Adobe Experience Manager** 对话框，版权年份仍为2023。 (CQ-4356349)


<!-- #### Sling{#foundation-sling-6521}

* T -->

#### 翻译{#foundation-translation-6521}

* AEM 6.5.19现成翻译状态无法按启动项预期更新的问题。 在将翻译文件导入与AEM启动关联的翻译作业后，状态应更改为 `Approved`. 相反，状态更改为 `Ready for Review`，这不是预期行为。 (NPR-41756)
* 在创建多个配置并转到翻译Cloud Service配置时，并非所有元素都会显示在UI中。 仅显示前40个元素/文件夹；触发延迟加载，但不添加更多内容。 (NPR-41829)
* 如果触控用户界面的“权限”页面上包含日语，则会出现乱码字符。 (NPR-41794)
* AEM 6.5.14和6.5.9不发送用于翻译的emoji。 (CQ-4357000)

#### 用户界面{#foundation-ui-6521}

* 在工具>安全>用户>中 &lt;user_name> >用户档案，在 **编辑用户设置** 对话框，单击“取消”不会退出对话框。 (NPR-41793)
* Granite `pathfield` 组件位于 `/libs/granite/ui/components/coral/foundation/form/pathfield` 无法启用 **[!UICONTROL 选择]** 按钮。 在弹出路径字段并且用户选中资产复选框后， **[!UICONTROL 选择]** 按钮未启用；它不会从灰色更改为蓝色。 (NPR-41970)
* AEM中的内容片段模型(CFM)引用字段存在问题。 尽管CFM参考字段设置为必填字段，但系统允许用户单击“保存”，以在某些情况下使用非CFM值保存内容。 保存按钮应灰显（不可用）。 (NPR-41894)
* 标准Coral用户界面对话框，使用 `successresponse` 操作必须在操作之后触发成功响应。 但在AEM 6.5 Service Pack 19中，不会调用重新加载操作，并且不会显示任何消息。 (NPR-41797)
* AEM通知链接在AEM 6.5 Service Pack 18中不起作用。 升级到Service Pack 18时，通过“通知”按钮选择消息时，“AEM通知”链接不起作用。 (NPR-41792)

<!-- #### WCM{#foundation-wcm-6521}

* T -->

#### 工作流{#foundation-workflow-6521}

* 在AEM 6.5.18中，在清除期间从用户元数据缓存中删除时反复出现错误。 (NPR-41762)

## 安装 [!DNL Experience Manager] 6.5.21.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.21.0需要 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以获取详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 使用包管理器对某个Author实例执行6.5.21.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.21.0程序包。 因此，在安装该包之前，您应该创建 `crx-repository` 万一你一定要把它退回。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装服务包 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。

1. 下载Service Sack，从 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.21.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack期间，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能间歇性地在任何浏览器中出现。

**自动安装**

可以使用两种不同的方法来安装 [!DNL Experience Manager] 6.5.21.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.21.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.21.0)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.20或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装服务包的说明，请参阅 [Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装 [GraphQL索引包1.1.1的Experience Manager内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

UberJar用于 [!DNL Experience Manager] 6.5.21.0可从以下网站获取： [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.21/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.21</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件可在Maven中央存储库而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件将重命名为 `uber-jar-<version>.jar`. 所以，没有 `classifier`，替换为 `apis` 作为值，用于 `dependency` 标记之前。


## 已弃用和已删除的功能{#removed-deprecated-features}

请参阅 [已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md/).

## 已知问题{#known-issues}

<!-- THESE KNOWN ISSUES CARRY OVER EACH RELEASE. THE "PRODUCT UPDATES TEAM" IS SUPPOSED TO VERIFY EACH ISSUE AND LET YOU KNOW IF ANYTHING NEEDS TO BE ADDED, DELETED, OR CHANGED IN THIS LIST.-->

<!-- * **Page publishing not working in Page Editor after upgrading to Service Pack 18 (6.5.18.0)** -->

<!-- https://jira.corp.adobe.com/browse/SITES-15856 REMOVE FOR 6.5.19.0 -->
<!-- After you upgrade an instance of AEM 6.5.0.0&mdash;6.5.17.0 to AEM 6.5.19.0, when you click **Publish Page** inside the Page Editor, you are redirected to a URL that does not exist.

  To work around this issue, do one of the following:

  * Remove the following "path" property.

       `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/publish/granite:data`

  * Paste the correct URL directly into the browser.

       `http://localhost:4504/editor.html/libs/wcm/core/content/sites/publishpagewizard.html?item=/content/we-retail/language-masters/en/about-us.html` -->


* **与Oak相关**
在Service Pack 13及更高版本中，已开始出现以下错误日志，这会影响持久性缓存：

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.0.202/5]
  at org.h2.mvstore.DataUtils.newMVStoreException(DataUtils.java:1004)
      at org.h2.mvstore.MVStore.getUnsupportedWriteFormatException(MVStore.java:1059)
      at org.h2.mvstore.MVStore.readStoreHeader(MVStore.java:878)
      at org.h2.mvstore.MVStore.<init>(MVStore.java:455)
      at org.h2.mvstore.MVStore$Builder.open(MVStore.java:4052)
      at org.h2.mvstore.db.Store.<init>(Store.java:129)
  ```

  或者

  ```shell
  org.h2.mvstore.MVStoreException: The write format 1 is smaller than the supported format 2 [2.1.214/5].
  ```

  要解决此异常，请执行以下操作：

   1. 从删除以下两个文件夹 `crx-quickstart/repository/`

      * `cache`
      * `diff-cache`

   1. 安装Service Pack，或重新启动Experience Manageras a Cloud Service。
的新文件夹 `cache` 和 `diff-cache` 自动创建，并且您不再遇到与相关的异常 `mvstore` 在 `error.log`.

* 更新可能已为内容模型使用自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询可能使用 `damAssetLucene` 索引而非 `fragments` 索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  要更正此问题， `damAssetLucene` 必须配置为在以下位置包含以下两个属性： `/indexRules/dam:Asset/properties`：

   * `contentFragment`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/contentFragment"`
      * `propertyIndex="{Boolean}true"`
      * `type="Boolean"`
   * `model`
      * `jcr:primaryType="nt:unstructured"`
      * `name="jcr:content/data/cq:model"`
      * `ordered="{Boolean}true"`
      * `propertyIndex="{Boolean}true"`
      * `type="String"`

  更改索引定义后，需要重新索引(`reindex` = `true`)。

  执行这些步骤后，GraphQL查询的执行速度应该会更快。

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题。 后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您升级您的 [!DNL Experience Manager] 从6.5.0到6.5.4的实例一直到Java™ 11上的最新Service Pack，请参见 `RRD4JReporter` 中的例外 `error.log` 文件。 要停止例外，请重新启动您的实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在以下位置重命名层级中的文件夹： [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题不会在中更新 [!DNL Brand Portal] 直到重新发布根文件夹。

* 安装期间可能会显示以下错误和警告消息 [!DNL Experience Manager] 6.5.x.x：
   * “当在中配置Adobe Target集成时 [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型为“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance中未找到维护窗口。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在granite/operations/maintenance中未找到维护窗口。
   * 通过可购物横幅查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，Rhino JavaScript引擎由 ```org.apache.servicemix.bundles.rhino``` 捆绑有新的提升行为。 使用严格模式(```use strict;```)必须声明其正确的变量。 否则，它们将不会运行，并最终引发运行时错误。

* 通过官方更新包安装与标记相关的现成内容会重置的languages属性。 `/content/cq:tags` 节点默认为。 此操作适用于Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修补程序等。 因此，在安装之前，必须从属性中添加它。

### AEM Sites的已知问题 {#known-issues-aem-sites-6521}

* SITES-17934 - 内容片段 - 由于大型片段树的 DoS 保护，预览失败。请参阅 [关于默认GraphQL查询执行器配置选项的知识库文章](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)

### AEM Forms的已知问题 {#known-issues-aem-forms-6521}

* 在基于XDP的自适应表单中，如果复选框上嵌入了脚本，则此类复选框之后的元素将不会执行脚本。 (FORMS-14244)
* 用户无法创建通信管理信件。 当用户创建信件时，出现描述“ ”的错误`Object Object`“”出现，且书信未创建。 在信件创建屏幕上加载布局缩略图也失败。 您可以安装 [最新的AEM 6.5表单Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解决问题。 (FORMS-13496)
* Interactive Communications服务会创建PDF文档，但用户数据不会自动填充到表单字段中。 预填充服务未按预期运行。 您可以安装 [最新的AEM 6.5表单Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解决问题。 (FORMS-13413和FORMS-13493)
* 无法加载automated forms conversion服务的审核和更正(RnC)编辑器。 您可以安装 [最新的AEM 6.5表单Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解决问题。 (FORMS-13491)
* 从AEM 6.5 Forms Service Pack 18 (6.5.18.0)或AEM 6.5 Forms Service Pack 19 (6.5.19.0)更新到AEM 6.5 Forms Service Pack 20 (6.5.20.0)后，用户遇到JSP编译错误。 他们无法打开或创建自适应表单，并且在页面编辑器、AEM Forms UI和AEM Workflow编辑器等其他AEM界面中遇到错误。 您可以安装 [最新的AEM 6.5表单Service Pack 20 (6.5.20.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) 以解决问题。 (FORMS-13492)
* 在弹出小部件中遍历具有编辑/显示模式的字段的月份时，日期选取器小部件中的行会被截断。 (FORMS-13620)
* 尝试在后端使用DOR（记录文档）服务时，表单提交失败。 遇到的错误消息是：“提交操作无法完成，因为未正确分配表单资源。” (FORMS-13798)
* 将自适应表单从Adobe Experience Manager发布实例提交到Adobe Experience Manager Workflow时，工作流无法保存附件。 (FORMS-14209)
* 安装AEM 6.5 Forms Service Pack 20包(适用于SP20的AEM Forms附加组件包)时，AEM Sites用户界面(UI)性能会显着降低。 (FORMS-13791)
* 预填充服务失败，交互式通信中出现空指针异常。 (CQDOC-21355)
* 自适应Forms允许您在ECMAScript版本5或更早版本中使用自定义函数。 当自定义函数使用ECMAScript版本6或更高版本时，例如 `let`， `const`或箭头函数时，规则编辑器可能无法正确打开。

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此包中包含的OSGi包和内容包 [!DNL Experience Manager] 6.5 Service Pack版本：

* [Experience Manager6.5.21.0中包含的OSGi包列表](/help/release-notes/assets/65210-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.21.0中包含的内容包列表](/help/release-notes/assets/65210-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/en/docs/customer-one/using/home).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [订阅Adobe优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)
