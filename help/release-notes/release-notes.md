---
title: 的发行说明 [!DNL Adobe Experience Manager] 6.5
description: 查找版本信息、新增功能、安装操作说明以及的详细更改列表 [!DNL Adobe Experience Manager] 6.5.
mini-toc-levels: 4
source-git-commit: 53bfd33a8bbb10d0ed82968a115ed316f63efecb
workflow-type: tm+mt
source-wordcount: '3466'
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

### [!DNL Forms]

* **JEE上的AEM Forms中的Transaction Reporting**：在JEE上为AEM Forms引入了事务报表功能，以便全面记录文档事务，如转化、演绎版和提交。 此增强功能可提高效率并有助于更好地保存记录。 默认情况下，该功能处于禁用状态。 您可以从管理员UI中启用它。
* **通过ECDSA支持增强的安全性**：AEM Forms现在跨JEE和OSGi栈栈提供对椭圆曲线数字签名算法(ECDSA)的强大支持。 用户现在可以对PDF文档进行签名、认证和验证，而安全性更高。 支持的EC曲线算法包括：
   * 采用SHA256摘要算法的ECDSA椭圆曲线P256
   * 采用SHA384摘要算法的ECDSA椭圆曲线P384
   * 采用SHA512摘要算法的ECDSA椭圆曲线P512
* **与Windows 11无缝兼容，适用于Forms Designer**：AEM Forms Designer现在支持Windows 11，从而确保顺利安装和操作。 用户可以放心地升级到Windows 11，而不必重新安装Forms Designer或担心兼容性问题，从而确保工作流不会中断。
* **AEM Forms Designer中的自定义“Caption”角色增强了辅助功能**：AEM Forms Designer现在包含一个名为“Caption”的自定义辅助功能角色，使用户能够使用个性化字幕元素创建XDP。 此功能通过允许用户将自定义字幕集成到其文档设计中来增强辅助功能，以便他们提高包容性和用户体验。

<!-- ### [!DNL Forms]

* text -->

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 20中的问题 {#fixed-issues}

### [!DNL Sites]{#sites-6520}

<!--#### Accessibility{#sites-accessibility-6520}

* text -->

#### 管理员用户界面{#sites-adminui-6520}

* 此 `Workflow Title` 字段标记为 `*` 根据要求，但没有验证。 (SITES-16491)

<!--#### Classic UI{#sites-classicui-6520}

* text -->

#### [!DNL Content Fragments]{#sites-contentfragments-6520}

* 升级到AEM 6.5.18或AEM 6.5.19后，嵌套配置文件夹不再受支持，内容片段模型文件夹不再可见。 (SITES-18110)
* 某些子文件夹无法从继承的内容片段模型中选取。 它必须支持文件夹而不具有 `jcr:content` 属性，即使通过用户界面创建的DAM文件夹具有此类节点。 (SITES-17943)

#### [!DNL Content Fragments] - GRAPHQL API {#sites-graphql-api-6520}

<!-- REMOVED AS PER EMAIL FROM SAMEER DHAWAN FEBRUARY 19, 2024 * When upgrading AEM from 6.5.19.0 to 6.5.20.0, the path `/libs/cq/graphql/sites/graphiql` was getting deleted. (SITES-19530) CRITICAL -->
* 在对执行GraphQL查询时 [筛选结果](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#filtering) 使用可选变量(如果特定值为 **非** 为可选变量提供的，则在过滤器评估中忽略该变量。 (SITES-17051)

<!--#### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6520}

* text -->

#### [!DNL Content Fragments] - REST API{#sites-restapi-6520}

* 随着 `org.json` 库中，小数点的反序列化方式发生了变化。 之前，它们被“默认地”转换为双面，现在则转换为大小数。 相反，通过REST API存储的元数据属性值应该从BigDecimal转换为Double。 (SITES-16857)

#### 核心后端{#sites-core-backend-6520}

* 使用内容片段的快速发布时，它会继续加载并且不会发布。 也就是说，从AEM 6.5.7升级到AEM 6.5.17的Service Pack后，快速发布不适用于内容片段。当用户尝试托管发布时，该操作有效。 但是，当他们尝试快速发布时，它未发布。 具体来说， `com.day.cq.wcm.core.impl.reference.ActivationReferenceSearchBuilder` 导致系统崩溃。 (SITES-17311)
* 无法使用Jackson导出程序序列化内容片段：当页面中引用的内容片段（使用Jackson导出程序代码）和任何标记被添加到内容片段时，页面加载会中断。 (SITES-18096)

#### 核心组件{#sites-core-components-6520}

* 在CIF上安装AEM核心组件包导致 `:type` 要更改的现有组件的值。 此更改意味着它们不再呈现在已添加到的页面上。 (SITES-17601)

#### Campaign集成{#sites-campaign-integration-6520}

* AEM使用的允许列表也称为 `whitelist` — 由于漏洞报告。 该允许列表使客户无法使用所需的功能。 (SITES-16822)

#### 体验片段{#sites-experiencefragments-6520}

* MSM for Experience Fragments现在支持批量转出到体验片段内容结构，包括文件夹和子文件夹。 (SITES-16004)

<!--#### Foundation Components (Legacy){#sites-foundation-components-legacy-6520}

* text

#### Launches{#sites-launches-6520}

* text -->

#### MSM — 活动副本{#sites-msm-live-copies-6520}

* 一个“`Is not modifiable`转出组件时引发“ ”异常。 具体而言， `org.apache.sling.servlets.post.impl.operations.ModifyOperation` 处理响应期间出现异常。 (SITES-18809)
* 无法转出对体验片段的特定活动副本的更改。 (SITES-17930)
* 当用户将注释添加到Blueprint页面上的组件，然后将其转出时，Live Copy上的注释计数显示不正确。 (SITES-17099)
* 在触控图形用户界面中，从父页面到子页面的MSM转出按钮被损坏；选中时，显示以下错误： `Uncaught TypeError: _g.shared is undefined`. (SITES-16991)

#### 页面编辑器{#sites-pageeditor-6520}

* Forms主题编辑器预览已损坏。 选择“预览”时，仅显示加载图标。 (SITES-17164)

### [!DNL Assets]{#assets-6520}

* 无法在元数据编辑器帮助程序中验证基于规则的字段，并显示错误消息“缺少必填字段”。 (ASSETS-31396)
* 将PDF移动到另一个位置后， **[!UICONTROL 查看页面]** 选项将消失。 (ASSETS-30538)
* 无法选择具有读取权限的图像。 (ASSETS-32199)
* 无法在视图设置中更改卡片大小。 (ASSETS-31667)
* 上传.oft文件类型时上传失败。 (ASSETS-30109)
* 当您尝试将自定义元数据字段作为附加列添加到报表时，未选中复选框。 (ASSETS-31671)
* 资源移动操作在Experience ManagerService Pack 16中无法正常工作。 (ASSETS-30598)

#### [!DNL Dynamic Media]{#assets-dm-6520}

* 将资源上传到AEM后， `Update_asset` 工作流已触发。 但是，该工作流永远不会完成。 该工作流仅在产品上传步骤之前完成。 下一步是Scene7批量上传，但不会将该流程提取到AEM中。 (ASSETS-30443)
* 需要一种更好的方式才能在Dynamic Media组件中正常处理非Dynamic Media视频。 此问题提供了实例化异常 `dynamicmedia_sly.js`. (ASSETS-31301)
* 预览适用于所有资产、自适应视频集和视频。 但是，它引发了403错误 `.m3u8` 文件（顺便说一下，这些文件仍通过公共链接使用）。 (ASSETS-31882)
* 此 `scene7SmartCropProcessingStatus` 已更正状态。 智能裁剪视频元数据曾用于显示失败，即使成功也是如此。 (ASSETS-31255)

### [!DNL Forms]{#forms-6520}

<!--Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of Forms fixes and enhancements is added to this section post the release.-->

#### [!DNL Adaptive Forms]

* 当用户尝试将AEM Forms集成到具有AEM已发布URL的邮件平台时，AEM Forms未添加 `method=post` 渲染页面时。 即使出现此问题 `POST` 在包含URL的提交操作中设置。 它会导致邮件平台不识别此表单。 (FORMS-12614)
* 当用户在AEM Form Service Pack 6.5.18.0中选择具有显示模式的日期字段时，用户无法使用键盘选择当前日期。 (FORMS-12736)
* 在AEM Forms Service Pack 6.5.17.0和Service Pack 6.5.18.0上，当用户在日历小组件中的月份之间切换时，日期选取器组件会显示一行。 (FORMS-11869)
* 当用户在iOS设备上的附件组件中使用“拍摄照片”单击图像时，所有图像都会添加到该文件夹中的相同名称。 (FORMS-12224)
* 当用户更新单选按钮组中的现有选项时，会发布不正确的翻译值。 (FORMS-12575)
* 当用户向Android™设备上的自适应表单添加字符时，在Android™设备上，用户在focus out上的文本字段中键入的字符数可以超过定义的最大字符数。 但是，当用户选择HTML5输入类型时，它才起作用。 (FORMS-12748)
* 由于标签匹配Arial® labelledby和Arial® label，屏幕阅读器无法区分这两者。 要解决此问题 — 对于表单字段，标签“aria-labelledby”会被替换为“aria-describedby”。 (FORMS-12436)
* 当作者使用“自适应Forms — 嵌入(v2)”组件在其站点页面中嵌入自适应表单，并且嵌入的表单上包含CAPTCHA组件（CAPTCHA服务 — > reCAPTCHA，设置 — > reCAPTCHA-v2）时，当用户尝试在创作实例上使用“以发布的形式查看”查看站点页面时，站点页面不会呈现。 以下错误显示为(FORMS-11859)：
  `Failed to construct 'URL': Invalid base URL at Object.renderRecaptcha`

* 当用户尝试使用日期选取器组件选择日期时，值未更新并显示NULL。 (FORMS-12742和FORMS-12736)

* 当用户升级到AEM Form Service Pack 6.5.19.0时，在将新语言更新到现有词典后，它不会与“guideContainer”行合并以向表单添加区域设置。 (FORMS-12947)

* 在AEM Forms Service Pack 6.5.19.0上，在Java™ 11上调用的Web服务操作失败，并返回错误(FORMS-12329)：
  `java.lang.NoClassDefFoundError message:sun/misc/BASE64Decoder`

* 当用户在AEM Forms Service Pack 6.5.18.0上调用“EmailService”的“接收”操作时，出现异常(FORMS-12050)：
  `java.util.ServiceConfigurationError: javax.mail.Provider: Provider com.sun.mail.imap.IMAPProvider not a subtype`

* 在AEM Forms Service Pack 6.5.18.0上启用FIPS模式后，在默认DOM下创建用户失败，并出现错误(FORMS-11857)：
  `com.adobe.idp.cx.a: error seeding random number generator`

* 当用户在ADMINUI中选择路径下的字体时 `Home>Services>PDF Generator>Adobe PDF Settings`，则不会选中它。 此外，在标准或个性化配置文件中，可用的字体列表框为空。 因此，无法个性化以下项的子列表： **始终嵌入** 或 **从不嵌入**. 用户无法使用PDF Generator配置其PDF的字体。 日志不会显示任何相关的错误消息。 (FORMS-12095)

* 在AEM Forms Service Pack 6.5.18.0上，用户无法创建安全设置，它不显示错误或服务器日志，但屏幕上会显示弹出错误消息。 (FORMS-12212)

* 当AEM Forms Service Pack 6.5.18.0上的用户在JEE工作流中提交自适应表单时，自适应表单中的附件未发送到JEE流程，从而导致应用程序失败。 (FORMS-12232和FORMS-12228)

* 当用户将PDF转换为PDF/A-2b或PDF/A-3B时，转换失败，错误显示为：(FORMS-12790)

  ```
  OCCD contains Order key that does not reference all layers.
  -> Optional content configuration dictionary has no Name entry.
  -> Font not embedded (and text rendering mode not 3).
  obj(65, 0)
  Page: 1
  -> Font not embedded (and text rendering mode not 3).
  obj(67, 0)
  Page: 1
  -> PDF/A entry missing. 
  -> PDF/A entry missing.
  ```

* 在AEM Forms 6.5.18.0上，发布自适应表单时，其所有依赖项（包括策略）都会重新发布，即使尚未对它们进行任何修改也是如此。 (FORMS-10454)

* 当用户在具有JBoss® Turnkey设置的AEM Forms 6.5.19.1上运行配置管理器时选择“Microsoft SharePoint”时，LiveCycleJBoss® EAR安装失败，并显示以下错误：(FORMS-12463)

  ` Caused by: org.jboss.as.server.deployment.DeploymentUnitProcessingException: WFLYEE0031: Unable to process modules in application.xml for EAR ["/C:/AEM/jboss/bin/content/ adobe-livecycle-jboss.ear "], module file adobe-connectorformssharepoint-config-ejb.jar not found.`

#### [!DNL Forms Designer] {#forms-designer-6520}


* 当用户升级到AEM Forms Service Pack 6.5.18.0时，由于缺少异常处理，通过启用了标记PDF选项的输出服务传递的XDP失败。 (LC-3921757)

* 当用户使用AEM Forms Designer生成PDF时，标题级别与图形元素（例如，矩形框）一起在辅助功能树中进行标记。 (LC-3921687)

* 在通过Workbench安装的AEM Forms Designer上，版本信息未明确显示在 `Control Panel/Programs/Programs and Features`. (LC-3921976)

<!--* When a user creates an XDP on AEM Forms Designer, the user is not able to add the custom Caption Tag. (LC-3921246)-->

* 当用户在AEM Forms Designer上创建XDP时，在PDF输出上，按钮表单标记未嵌套在父段落标记(p-tag)中。 (LC-3921719)

* 当用户在AEM Forms Designer上创建XDP时，当用户浏览表单标签时，在PDF输出上，后台对象也被标记。 (LC-3921687)

### Foundation {#foundation-6520}

#### 社区 {#communities-6520}

* 成功配置用户同步后，用户同步诊断失败。 (NPR-41693)

<!-- #### Content distribution{#foundation-content-distribution-6520}

* text -->

#### 集成{#integrations-6520}

* 从AEM 6.5中删除AdobeSearch&amp;Promote的所有代码和依赖项。 (NPR-40856)

#### 本地化{#localization-6520}

* Aria标签“关闭”在中未本地化 **[!UICONTROL 资产]** > **[!UICONTROL 文件]**，选择一个文件夹，然后在工具栏上，选择 **[!UICONTROL 属性]** > **[!UICONTROL 权限]** 选项卡>成员名称。 (NPR-41705)
* 的工具提示被截断 **[!UICONTROL 密钥存储密码]** 区域设置ENG、FRA、KOR、DEU和PTB的“SSL设置”页面上的字段。 (NPR-41367)

#### Platform{#foundation-platform-6520}

* 将Campaign与AEM集成时存在的问题，原因是/api servlet未在href json中返回正确的方案。 原因是AEM未接收X-Forward-Proto标头，该标头强制请求使用HTTP方案而不是HTTPS方案进行响应。 因此，应添加基于OSGI配置切换方案选择的功能。 (GRANITE-48454)

#### Sling{#foundation-sling-6520}

* 此 `org.apache.sling.resourceMerger` 捆绑包1.4.2从AEM 6.5、Service Pack 17及更高版本中引发异常。 Service Pack 20中应包含Sling资源合并器1.4.4。 (NPR-41630)

#### 翻译{#foundation-translation-6520}

* 部署AEM 6.5 Service Pack 18后，翻译规则编辑器中的过滤器选项卡出现问题。 选择上下文后，单击“编辑”>“保存”，下次打开同一上下文时，将出现一个双引号作为HTML字符。 本质上，翻译规则无法正确保存。 (NPR-41624)
* 与内容片段翻译相关的问题，其中已翻译字符串从翻译提供商发送回AEM，但被卡在 `/content/projects` 级别而不更新内容片段。 (NPR-41516)
* 创建语言副本时显示错误消息。 它发生在具有在页面属性中引用的内容片段的页面上，使用内容片段模型。 (NPR-41441)
* 在语言复制过程中，体验片段中的链接未调整为正确的语言。 相反，体验片段指向主区域设置。 (NPR-41343)

#### 用户界面{#foundation-ui-6520}

* 升级到AEM 6.5 Service Pack 18后，出现控制台错误。 错误位于 `coralUI3.js` 文件，当您在AEM中选择任意下拉列表时，会出现此情况。 具体来说，它发生在 `onOverlayToggle` 事件。 错误 `Uncaught TypeError: Cannot read properties of null (reading 'innerText')` 将显示。 (NPR-41467)
* 在AEM中， **[!UICONTROL 工具]** > **[!UICONTROL 常规]** > **[!UICONTROL 标记]** > **[!UICONTROL 创建]** > **[!UICONTROL 创建标记]**，在中输入非拉丁字符 **标题** 字段导致 **名称** 要仅用连字符填充的字段( `-` )。 (NPR-41623)
* 中的版权年度不正确 `About Adobe Experience Manager` 对话框。 (NPR-41526)
* 有未翻译的 **[!UICONTROL 配置文件属性]** 编辑用户设置时的字符串。 在所有区域设置中发生。 (NPR-41365)

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


### AEM Forms的已知问题 {#known-issues-aem-forms-6520}

* 从AEM 6.5 Forms Service Pack 18 (6.5.18.0)或AEM 6.5 Forms Service Pack 19 (6.5.19.0)更新到AEM 6.5 Forms Service Pack 20 (6.5.20.0)后，用户遇到JSP编译错误。 他们无法打开或创建自适应表单，并且在页面编辑器、AEM Forms UI和AEM Workflow编辑器等其他AEM界面中遇到错误。 出现与以下内容类似的错误消息：

  `Unable to compile class for JSP: An error occurred at line: 162 in the jsp file: /libs/granite/ui/components/coral/foundation/anchorbutton/anchorbutton.jsp The method transformLinkInUriIfExternal(String) is undefined for the type ComponentHelper`

  您可以联系Adobe支持部门以获取解决此问题的帮助。


* 预填充服务失败，交互式通信中出现空指针异常。 (CQDOC-21355)

<!--Known issues in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.20.0 Forms add-on package release is scheduled for Thursday, February 29, 2024. A list of known issues for forms is added to this section post the release.-->

<!--
#### Install the servlet fragment (AEM Service Pack 6.5.14.0 or earlier)

* If you are upgrading to AEM Service Pack 6.5.15.0 or higher, and your AEM instance is operating on Tomcat 8.5.88, it is mandatory that you install the servlet fragment *before* you proceed with the installation of Service Pack 6.5.15.0 or higher.
* It is mandatory that you install the servlet fragment for all application servers except those running on JBoss&reg; EAP 7.4.0.

**To install the servlet fragment:**

1. Download the servlet fragment from [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).
1. Start the application server. 
1. Wait for the logs to stabilize and check the bundle state.
1. Open Web Console Bundles. The default URL is `http://[Server]:[Port]/system/console/bundles`.
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Select the downloaded fragment 
`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar` 
1. Select **[!UICONTROL Install]** or **[!UICONTROL Update]**. 
1. Wait for the application server to stabilize.
1. Stop the application server.

-->

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
