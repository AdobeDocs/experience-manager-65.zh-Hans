---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作说明以及的详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 19fe527ce44d8ec5be50ebd32b46f13df96c52cc
workflow-type: tm+mt
source-wordcount: '2928'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5最新Service Pack发行说明 {#aem-service-pack-release-notes}

<!-- For an itemized list of all issues found in these release notes, see the following spreadsheet: https://adobe-my.sharepoint.com/:x:/r/personal/anujkapo_adobe_com/_layouts/15/Doc.aspx?sourcedoc=%7B3ea81ae4-e605-4153-b132-f2698c86f84e%7D&action=edit&wdinitialsession=d8c7b903-87fc-4f2d-9ef2-542a82169570&wdrldsc=3&wdrldc=1&wdrldr=SessionMemoryQuotaExceededDuringSession -->

<!-- DO NOT DELETE THIS HIDDEN NOTE      DO NOT DELETE THIS HIDDEN NOTE
>[!NOTE]
>
>Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the add-on packages release Thursday, November 30, 2023. In addition, a list of Forms fixes and enhancements is added to this section. -->

## 发行版信息 {#release-information}

| 产品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.20.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2024年2月22日星期四 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## 中包括的内容 [!DNL Experience Manager] 6.5.20.0 {#what-is-included-in-aem-6520}

[!DNL Experience Manager] 6.5.20.0包括自2019年4月首次推出6.5以来发布的新功能、关键客户请求的增强功能、错误修复以及性能、稳定性和安全性改进。 [安装此Service Pack](#install) 日期 [!DNL Experience Manager] 6.5.

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增强功能

<!-- * _6.5.20.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

此版本中的某些主要功能和增强功能包括：

* Dynamic Media现在支持Apple iOS/iPadOS的无损HEIC图像格式。 请参阅 [格式](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt.html?lang=en) 在Dynamic Media图像服务和渲染API中。

* 多站点管理器(MSM)现在支持体验片段结构（包括文件夹和子文件夹），以便有效地将体验片段批量转出到活动副本。

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 20中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### 管理员用户界面{#sites-adminui-6520}

* 此 `Workflow Title` 字段标记为 `*` 根据要求，但没有验证。 (SITES-16491)普通

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* 升级到AEM 6.5.18或AEM 6.5.19后，嵌套配置文件夹不再受支持，内容片段模型文件夹不再可见。 (SITES-18110)主要
* 某些子文件夹无法从继承的内容片段模型中选取。 它必须支持文件夹而不具有 `jcr:content` 属性，即使通过用户界面创建的DAM文件夹具有此类节点。 (SITES-17943)普通

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* 在对执行GraphQL查询时 [筛选结果](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) 使用可选变量(如果特定值为 **非** 为可选变量提供的，则在过滤器评估中忽略该变量。 (SITES-17051)普通

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* 随着 `org.json` 库中，小数点的反序列化方式发生了变化。 之前，它们被“默认地”转换为双面，现在则转换为大小数。 相反，通过REST API存储的元数据属性值应该从BigDecimal转换为Double。 (SITES-16857)普通

#### 核心后端{#sites-core-backend-6520}

* 使用内容片段的快速发布时，它会继续加载并且不会发布。 也就是说，从AEM 6.5.7升级到AEM 6.5.17的Service Pack后，快速发布不适用于内容片段。当用户尝试托管发布时，该操作有效。 但是，当他们尝试快速发布时，它未发布。 具体来说， `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` 导致系统崩溃。 (SITES-17311)主要
* 无法使用Jackson导出程序序列化内容片段：当页面中引用的内容片段（使用Jackson导出程序代码）和任何标记被添加到内容片段时，页面加载会中断。 (SITES-18096)普通

#### 核心组件{#sites-core-components-6520}

* 在CIF上安装AEM核心组件包导致 `:type` 要更改的现有组件的值。 此更改意味着它们不再呈现在已添加到的页面上。 (SITES-17601)主要

#### Campaign集成{#sites-campaign-integration-6520}

* AEM使用的允许列表也称为 `whitelist` — 由于漏洞报告。 该允许列表使客户无法使用所需的功能。 (SITES-16822)关键

#### 体验片段{#sites-experiencefragments-6520}

* MSM for Experience Fragments现在支持批量转出到体验片段内容结构，包括文件夹和子文件夹。 (SITES-16004)主要

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM — 活动副本{#sites-msm-live-copies-6520}

* 一个“`Is not modifiable`转出组件时引发“ ”异常。 具体而言， `org.apache.sling.servlets.post.impl.operations.ModifyOperation` 处理响应期间出现异常。 (SITES-18809)主要
* 无法转出对体验片段的特定活动副本的更改。 (SITES-17930)主要
* 当用户将注释添加到Blueprint页面上的组件，然后将其转出时，Live Copy上的注释计数显示不正确。 (SITES-17099)主要
* 在触控图形用户界面中，从父页面到子页面的MSM转出按钮被损坏；选中时，显示以下错误： `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)主要

#### 页面编辑器{#sites-pageeditor-6520}

* Forms主题编辑器预览已损坏。 选择“预览”时，仅显示加载图标。 (SITES-17164)阻止程序

### [!DNL Assets]{#assets-6520}

* 无法在元数据编辑器帮助程序中验证基于规则的字段，并显示错误消息“缺少必填字段”。 (ASSETS-31396)主要
* 将PDF移动到另一个位置后， **[!UICONTROL 查看页面]** 选项将消失。 (ASSETS-30538)主要
* 无法选择具有读取权限的图像。 (ASSETS-32199)普通
* 无法在视图设置中更改卡片大小。 (ASSETS-31667)普通
* 上传.oft文件类型时上传失败。 (ASSETS-30109)普通
* 当您尝试将自定义元数据字段作为附加列添加到报表时，未选中复选框。 (ASSETS-31671)轻微
* 资源移动操作在Experience ManagerService Pack 16中无法正常工作。 (ASSETS-30598)轻微

#### [!DNL Dynamic Media]{#assets-dm-6520}

* 将资源上传到AEM后， `Update_asset` 工作流已触发。 但是，该工作流永远不会完成。 该工作流仅在产品上传步骤之前完成。 下一步是Scene7批量上传，但不会将该流程提取到AEM中。 (ASSETS-30443)关键
* 需要一种更好的方式才能在Dynamic Media组件中正常处理非Dynamic Media视频。 此问题提供了实例化异常 `dynamicmedia_sly.js`. (ASSETS-31301)主要
* 预览适用于所有资产、自适应视频集和视频。 但是，它引发了403错误 `.m3u8` 文件（顺便说一下，这些文件仍通过公共链接使用）。 (ASSETS-31882)主要
* 此 `scene7SmartCropProcessingStatus` 已更正状态。 智能裁剪视频元数据曾用于显示失败，即使成功也是如此。 (ASSETS-31255)轻微

### [!DNL Forms]{#forms-6520}

中的修复 [!DNL Experience Manager] Forms在计划的一周后通过单独的附加组件包提供 [!DNL Experience Manager] Service Pack发行日期。 在本例中，AEM 6.5.20.0 Forms附加组件包版本计划于2024年2月29日星期四发布。 发布后，此部分中添加了Forms修复和增强功能的列表。

<!-- #### [!DNL Adaptive Forms] -->

<!--LEFT BULLET LIST HERE IN CASE OF REUSE BY FORMS IN THE FUTURE 
* **Document Services**
  * text
* **Adaptive Forms** 
  * text
* **Accessibility**
  * text
* **Interactive Communications**
  * text -->

<!--### Commerce{#commerce-6520}

* text -->

#### [!DNL Forms Designer]{#forms-designer-6520}

* text

<!-- ### Foundation{#foundation-6520}

* text -->

#### 社区 {#communities-6520}

* 成功配置用户同步后，用户同步诊断失败。 (NPR-41693)普通

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### 集成{#integrations-6520}

* 从AEM 6.5中删除AdobeSearch&amp;Promote的所有代码和依赖项。 (NPR-40856)普通

#### 本地化{#localization-6520}

* Aria标签“关闭”在中未本地化 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**，选择一个文件夹，然后在工具栏上，选择 **[!UICONTROL 属性]** > **[!UICONTROL 权限]** 选项卡>成员名称。 (NPR-41705)主要
* 的工具提示被截断 **[!UICONTROL 密钥存储密码]** 区域设置ENG、FRA、KOR、DEU和PTB的“SSL设置”页面上的字段。 (NPR-41367)普通

<!-- #### Oak{#oak-6520}

* text -->

#### Platform{#foundation-platform-6520}

* 将Campaign与AEM集成时存在的问题，原因是/api servlet未在href json中返回正确的方案。 原因是AEM未接收X-Forward-Proto标头，该标头强制请求使用HTTP方案而不是HTTPS方案进行响应。 因此，应添加基于OSGI配置切换方案选择的功能。 (GRANITE-48454)主要

<!-- #### Replication{#foundation-replication-6520}

* text -->

#### Sling{#foundation-sling-6520}

* 此 `org.apache.sling.resourceMerger` 捆绑包1.4.2从AEM 6.5、Service Pack 17及更高版本中引发异常。 Service Pack 20中应包含Sling资源合并器1.4.4。 (NPR-41630)普通

#### 翻译{#foundation-translation-6520}

* 部署AEM 6.5 Service Pack 18后，翻译规则编辑器中的过滤器选项卡出现问题。 选择上下文后，单击“编辑”>“保存”，下次打开同一上下文时，将出现一个双引号作为HTML字符。 本质上，翻译规则无法正确保存。 (NPR-41624)主要
* 与内容片段翻译相关的问题，其中已翻译字符串从翻译提供商发送回AEM，但被卡在 `/content/projects` 级别而不更新内容片段。 (NPR-41516)主要
* 创建语言副本时显示错误消息。 它发生在具有在页面属性中引用的内容片段的页面上，使用内容片段模型。 (NPR-41441)主要
* 在语言复制过程中，体验片段中的链接未调整为正确的语言。 相反，体验片段指向主区域设置。 (NPR-41343)普通

#### 用户界面{#foundation-ui-6520}

* 升级到AEM 6.5 Service Pack 18后，出现控制台错误。 错误位于 `coralUI3.js` 文件，当您在AEM中选择任意下拉列表时，会出现此情况。 具体来说，它发生在 `onOverlayToggle` 事件。 错误 `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` 将显示。 (NPR-41467)主要
* 在AEM中， **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 标记]** > **[!UICONTROL 创建]** > **[!UICONTROL 创建标记]**，在中输入非拉丁字符 **标题** 字段导致 **名称** 要仅用连字符填充的字段( `-` )。 (NPR-41623)普通
* 中的版权年度不正确 `About Adobe Experience Manager` 对话框。 (NPR-41526)普通
* 有未翻译的 **[!UICONTROL 配置文件属性]** 编辑用户设置时的字符串。 在所有区域设置中发生。 (NPR-41365)普通

<!-- #### WCM{#wcm-6520}

* text

#### Workflow{#foundation-workflow-6520}

* text -->

## 安装 [!DNL Experience Manager] 6.5.20.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.20.0需要 [!DNL Experience Manager] 6.5.见 [升级文档](/help/sites-deploying/upgrade.md) 以获取详细说明。 <!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe上获取Service Pack下载 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip).
* 在具有MongoDB和多个实例的部署中，安装 [!DNL Experience Manager] 使用包管理器对某个Author实例执行6.5.20.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载 [!DNL Experience Manager] 6.5.20.0包。 因此，在安装该包之前，您应该创建 `crx-repository` 万一你一定要把它退回。 <!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在上安装服务包 [!DNL Experience Manager] 6.5{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请拍摄快照或进行全新备份 [!DNL Experience Manager] 实例。

1. 从以下位置下载Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.20.0.zip). <!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择 **[!UICONTROL 上传包]** 以上传包。 要了解更多信息，请参阅 [包管理器](/help/sites-administering/package-manager.md).

1. 选择包，然后选择 **[!UICONTROL 安装]**.

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅 [Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>在安装Service Pack期间，有时会退出包管理器UI上的对话框。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题出现在 [!DNL Safari] 浏览器，但可能间歇性地在任何浏览器上出现。

**自动安装**

可以使用两种不同的方法来自动安装 [!DNL Experience Manager] 6.5.20.0。<!-- UPDATE FOR EACH NEW RELEASE -->

* 将包放入 `../crx-quickstart/install` 文件夹（当服务器联机时）。 软件包会自动安装。
* 使用 [包管理器中的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.20.0不支持Bootstrap安装。 <!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与本版本配合使用的平台，请参阅 [技术要求](/help/sites-deploying/technical-requirements.md).

1. 产品信息页面(`/system/console/productinfo`)显示更新的版本字符串 `Adobe Experience Manager (6.5.20.0)` 下 [!UICONTROL 已安装的产品]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. 所有OSGi捆绑包包 **[!UICONTROL 活动]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi包 `org.apache.jackrabbit.oak-core` 是版本1.22.18或更高版本(使用Web控制台： `/system/console/bundles`)。 <!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE -->

### 安装Service Pack for [!DNL Experience Manager] Forms{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装服务包的说明，请参阅 [Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md).

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/deploying/deploy.html)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装 [GraphQL索引包1.1.1的Experience Manager内容片段](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip).

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

UberJar用于 [!DNL Experience Manager] 6.5.20.0可从以下网站获取： [Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.20/). <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.20</version>
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

* 尝试移动、删除或发布内容片段、站点或页面时，在获取内容片段引用时出现问题，因为后台查询失败。 也就是说，功能无法正常工作。
为确保操作正确，必须将以下属性添加到索引定义节点 `/oak:index/damAssetLucene` （无需重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您升级您的 [!DNL Experience Manager] 从6.5.0 - 6.5.4到Java™ 11上最新Service Pack的实例，请参见 `RRD4JReporter` 中的例外 `error.log` 文件。 要停止例外，请重新启动您的实例 [!DNL Experience Manager]. <!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在以下位置重命名层级中的文件夹： [!DNL Assets] 并将嵌套文件夹发布到 [!DNL Brand Portal]. 但是，文件夹的标题不会在中更新 [!DNL Brand Portal] 直到重新发布根文件夹。

* 安装期间可能会显示以下错误和警告消息 [!DNL Experience Manager] 6.5.x.x：
   * “当在中配置Adobe Target集成时 [!DNL Experience Manager] 使用Target Standard API（IMS身份验证），然后将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型为“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在granite/operations/maintenance中未找到维护窗口。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance中未找到维护窗口。
   * 通过可购物横幅查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，Rhino JavaScript引擎由 ```org.apache.servicemix.bundles.rhino``` 捆绑有新的提升行为。 使用严格模式(```use strict;```)必须正确声明其变量，否则它们不会运行，而是会引发运行时错误。

### AEM Forms的已知问题

#### 支持的平台

* JDK 11.0.20不支持在JEE安装程序上安装AEM Forms。 在JEE安装程序上安装AEM Forms仅支持JDK 11.0.19或更早版本。 (FORMS-10659)

#### 安装

* 在JBoss® 7.1.4平台上，当用户安装Experience Manager6.5.16.0或更高版本的Service Pack时， `adobe-livecycle-jboss.ear` 部署失败。 (CQ-4351522和CQDOC-20159)

<!-- 
* After upgrading to AEM Forms 6.5.18.0 JBoss&reg; Turnkey full installer environment on Windows Server 2022, when compiling Output client application code using Java&trade; 11, the following compilation error may occur:
  
  ```
  error: error reading [AEM_Forms_Installation_dir]\sdk\client-libs\common\adobe-output-client.jar; java.net.URISyntaxException: 
  Illegal character in path at index 70: file:/[AEM_Forms_Installation_dir]/sdk/client-libs/common/${clover.jar.name} 1 error
  
  ```
  
  To resolve the issue, perform the following steps:
    1. Navigate to `[AEM_Forms_Installation_dir]\sdk\client-libs\common\` and unzip `adobe-output-client.jar` to extract the `Manifest.mf` file.
    1. Update the `Manifest.mf` file by removing the entry `${clover.jar.name}` from the class-path attribute. 

        >[!NOTE]
        >
        > You can also use an in-place editing tool, for example, 7-zip, to update the `Manifest.mf` file.  

    1. Save the updated the `Manifest.mf` in the `adobe-output-client.jar` archive. 
    1. Save the modified `adobe-output-client.jar` file and rerun the setup. (CQDOC-20878) -->

* 安装AEM Service Pack 6.5.20.0完整安装程序后，EAR部署在使用JBoss® Turnkey的JEE上失败。 <!-- UPDATE FOR EACH NEW RELEASE -->

要解决此问题，请找到 `<AEM_Forms_Installation_dir>\jboss\bin\standalone.bat` 文件和更新 `Adobe_Adobe_JAVA_HOME` 到 `Adobe_JAVA_HOME` 所有出现的次数。 (CQDOC-20803)

#### 安装servlet片段(AEM Service Pack 6.5.14.0或更低版本)

* 如果您要升级到AEM Service Pack 6.5.15.0或更高版本，并且AEM实例在Tomcat 8.5.88上运行，则必须安装servlet片段。 执行此安装 *早于* 请继续安装Service Pack 6.5.15.0或更高版本。
* 必须为所有应用程序服务器(在JBoss® EAP 7.4.0上运行的除外)安装servlet片段。

**安装servlet片段：**

1. 下载servlet片段，从 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. 启动应用程序服务器。
1. 等待日志稳定并检查捆绑包状态。
1. 打开Web控制台包。 默认URL为 `http://[Server]:[Port]/system/console/bundles`.
1. 选择 **[!UICONTROL 安装]** 或 **[!UICONTROL 更新]**.
1. 选择下载的片段
   `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`
1. 选择 **[!UICONTROL 安装]** 或 **[!UICONTROL 更新]**.
1. 等待应用程序服务器稳定下来。
1. 停止应用程序服务器。

#### 自适应表单

* 发布自适应表单时，其所有依赖项（包括策略）都会重新发布，即使尚未对它们进行任何修改也是如此。 (FORMS-10454)
* 当用户选择在自适应表单中首次配置字段时，属性浏览器中不显示保存配置的选项。 选择在同一编辑器中配置自适应表单的某些其他字段可解决此问题。
* 当用户执行提交操作时，提交失败并出现错误：
  `javax.servlet.ServletException: java.lang.NoSuchMethodError`
要解决此问题， [重新编译Sling脚本，例如JSP、Java™和Sightly](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html#resolution). (FORMS-8542)
* 安装AEM Service Pack 6.5.14.0及更高版本后，导航到时，用户无法从JEE管理员UI中选择用于PDF文档的字体 `Home` > `Services` > `PDF Generator` > `Adobe PDF Settings`，因为字体列表显示为空。 (FORMS-12095)
<!-- When a form is signed using the OOTB Scribble Signature component, it appears in the image dialogue but does not preview and appears blank when you click on it. (FORMS-12073). A hotfix is available for this issue. To download and install the hotfix, see [Adobe Experience Manager Forms Hotfixes](/help/release-notes/aem-forms-hotfix.md) -->
* 在JEE上的AEM Forms上，使用上下文路径的HTML5 Forms无法呈现。 (FORMS-12485和FORMS-12691)。 有针对此问题的修补程序。 要下载并安装修补程序，请参阅 [Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md).
* 自适应Forms允许您在ECMAScript版本5或更早版本中使用自定义函数。 当自定义函数使用ECMAScript版本6或更高版本（如“let”、“const”或箭头函数）时，规则编辑器可能无法正确打开。

#### JEE上的AEM Forms

* Struts 2 RCE是一种用于开发Java™ EE Web应用程序的流行开放源码Web应用程序框架，已经报告了它存在严重的安全漏洞。 Adobe已发布 [AEM 6.5 Service Pack 19.1 (6.5.19.1)](/help/forms/using/mitigating-struts-2-rce-vulnerabilities-for-experience-manager-manager-form.md) 解决JEE上AEM Forms中的漏洞。

<!--The font enumeration fails due to the missing Ps2Pdf service file.-->

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此包中包含的OSGi包和内容包 [!DNL Experience Manager] 6.5 Service Pack版本：

* [Experience Manager6.5.20.0中包含的OSGi包列表](/help/release-notes/assets/65200-bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.20.0中包含的内容包列表](/help/release-notes/assets/65200-packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载地址：licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hans)
>* [订阅Adobe产品更新早知道](https://www.adobe.com/cn/subscription/priority-product-update.html)
