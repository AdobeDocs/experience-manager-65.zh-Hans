---
title: ' [!DNL Adobe Experience Manager] 6.5的发行说明'
description: 查找 [!DNL Adobe Experience Manager] 6.5的版本信息、新增功能、安装操作说明和详细更改列表。
mini-toc-levels: 4
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: 27283286bd514c6f8902297cd9229b5e92a3c60d
workflow-type: tm+mt
source-wordcount: '6089'
ht-degree: 2%

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
| 版本 | 6.5.22.0 <!-- UPDATE FOR EACH NEW RELEASE --> |
| 类型 | Service Pack版本 |
| 日期 | 2024年11月21日星期四<!-- UPDATE FOR EACH NEW RELEASE --> |
| 下载 URL | [软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip) <!-- UPDATE FOR EACH NEW RELEASE --> |

## [!DNL Experience Manager] 6.5.22.0中包含的内容 {#what-is-included-in-aem-6522}

[!DNL Experience Manager] 6.5.22.0包括新增功能、客户请求的关键增强功能和错误修复。 其中还包括自2019年4月6.5首次发布以来在性能、稳定性和安全性方面做出的改进。 在[!DNL Experience Manager] 6.5上[安装此Service Pack](#install)。

<!-- UPDATE FOR EACH NEW RELEASE -->

## 主要功能和增强功能

### Forms {#forms-sp22}

此版本中的主要功能和增强功能包括：

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)和[Cloudfare Turnstile验证码服务](/help/forms/using/integrate-adaptive-forms-turnstile.md)： AEM Forms支持以下Captcha服务：
   * 验证码使用复选框小组件向用户发起挑战，保护表单免受机器人、垃圾邮件和自动滥用的侵害。 它确保只有人工用户才能进行，增强了在线交易的安全性。
   * Cloudflare Turnstile提供了一种安全措施，旨在保护表单免受自动机器人、恶意攻击、垃圾邮件和不需要的自动流量的影响。 在允许提交表单之前，它会在表单提交时显示一个复选框，以验证他们是人类。

* 自适应表单版本控制：
   * [创建自适应表单的多个版本](/help/forms/using/add-versioning-reviews-comments.md)：现在，用户可以轻松管理现有表单的变体。 这简化了版本控制，有助于表单优化比较，所有这些都在一个简化的工作流中进行。
   * [比较自适应Forms](/help/forms/using/compare-forms-core-components.md)：现在，用户可以轻松比较两个表单以找出差异。 它使团队成员能够比较修订内容，并有效地讨论相关变化，从而促进顺利协作。

* 添加了支持以在[Interactive Communications批处理API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel)中启用字体嵌入：现在，Interactive Communications支持在通过Batch API生成的PDF中嵌入Adobe Ming和Adobe Myungjo字体。 此增强功能确保生成的文档中的文本呈现准确无误，即使使用字体子集也是如此，从而改进了对PDF输出中的多语言内容的支持。

* [用于PDF辅助功能的内容表API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api)： OSGi上的AEM Forms现在支持新的TOC标记API，以增强对辅助功能标准的PDF。 它借助辅助技术使PDF更易于访问。

* [片段XDP解析](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository)： OSGi上的AEM Forms现在解析主XDP中引用并存储在AEM CRX存储库中的片段XDP。

* [PDF/A合规性增强](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents)：现在，用户可将PDF转换为PDF/A格式(1a、2a、3a)以进行存档，同时确保可访问性并验证是否符合这些标准。

* **支持静态PDF文档自动调整字体大小**： AEM Forms Designer、OutputService和FormsService现在支持静态PDF的自动调整字体大小。如果用户为文本字段、数字字段、密码字段或日期时间字段等字段在模板中提及字体大小0，则字体大小会在这些字段内自动调整，而不会更改字段本身的大小。 要使用该功能，用户在自定义xci中传递一个标记：`<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`。

<!-- * _6.5.21.0 REVIEWERS: WHAT ARE THE KEY FEATURES AND ENHANCEMENTS THAT YOU WANT TO HIGHLIGHT IN THIS RELEASE?_ -->

### Sites {#sites}

[通用编辑器](/help/sites-developing/universal-editor/introduction.md)现在可在AEM 6.5上用于应用功能包的Headless用例。

### [!DNL Assets]

IPTC选项卡现在支持[!UICONTROL 替换文本]和[!UICONTROL 扩展描述]文本字段。 (ASSETS-34918)

<!-- UPDATE BELOW FOR EACH NEW RELEASE -->

## 修复了Service Pack 22中的问题 {#fixed-issues}


### [!DNL Sites]{#sites-6522}


#### 辅助功能 {#sites-accessibility-6522}

* 注释样本选择器按钮缺少可访问的名称。 也就是说，使用屏幕阅读器，在输入新的十六进制值后，按钮没有可理解的名称可供选择。 (SITES-11992)
* 左边栏菜单中的以下元素看起来像一个列表，但在屏幕阅读器中没有如此标记：

   * 站点
   * Live Copy
   * 启动
   * 语言复制
   * 文件夹
   * CSV报表(SITES-2874)

* AEM核心Web内容管理需要在富文本编辑器中为超链接设置辅助功能标签。 在文本组件中使用超链接时，锚点标记应包含`aria-label`属性，以确保屏幕阅读器出于辅助功能目的能够准确阅读和传达链接文本。 (SITES-11511)
* 在AEM中，列表视图的表标题中的交互式元素没有所需的“按钮”角色。 因此，NVDA屏幕阅读器不会为下表标题公告预期的按钮角色：标题、名称、已修改、已发布、预览、模板、操作、工作流。 应为表标题中的每个交互式元素分配“按钮”角色，以确保与NVDA等辅助技术的兼容性。 (SITES-10962)


#### 管理员用户界面{#sites-adminui-6522}

* 在AEM的某些实例中，版本预览和比较功能在几个页面中无法按预期工作。 具体来说：

   * **预览问题：**&#x200B;当尝试预览页面版本时，最初会显示错误。 重试后，预览会生成空白页。
   * **版本比较问题：**“与当前比较”功能只显示当前版本，不突出显示版本之间的任何差异。 (SITES-23988)

* 在复制粘贴操作期间使用设置为`plaintext`的`defaultPasteMode`时，富文本编辑器(RTE)字段中出现意外的`<br>`标记。 此问题会导致同一内容出现不同的标记，从而导致同一文本内容在客户的翻译记忆库中翻译两次。 (SITES-23606)
* 在AEM 6.5.20.0中，**管理发布**&#x200B;功能出现功能问题。 当选择某个节点并计划它以供将来发布时，在尝试包含子节点时可能会显示错误消息“无法检索选定项目的子资源”。 此问题阻止使用&#x200B;**包括子项**&#x200B;选项，导致目标内容层次结构无法完全发布。 (SITES-23000)
* 在创作环境中，模板的“已发布”时间戳未更新，即使模板已成功复制到发布实例。 预期的行为是创作实例上的时间戳反映最新的发布，但此更新未按预期进行。 (SITES-21585)
* AEM创作环境中的传入链接计数存在差异。 与经典UI相比，左侧边栏显示的链接较少。 此外，某些合法的传入链接不起作用。 (SITES-24837)
* 在AEM的“时间线”视图中查看页面版本时，报告的加载时间非常长。 显示版本最多需要19分钟。 从AEM 6.4.8升级到6.5.18后，此问题持续出现，会显着中断工作流的效率。 (SITES-22468和SITES-22467)

<!-- #### Classic UI{#sites-classicui-6522} 

* A -->


#### [!DNL Content Fragments]{#sites-contentfragments-6522}

* 在升级的AEM 6.5.17中，保存内容片段导致以下错误： *错误：无法保存内容片段。* (SITES-22993)
* 在AEM中的发布者的`ContentFragmentModelOmniSearchHandler`中发现了与未关闭的资源解析程序有关的问题。 (SITES-24903)


#### [!DNL Content Fragments] — 管理员{#sites-admin-6522}

单击电子邮件通知中的链接会将用户定向到默认资产查看器或编辑器。 这样做可代替内容片段编辑器，即使确定工作流中的资产是内容片段也是如此。 (SITES-24338)


#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-6522}

将内容片段与多行文本字段项一起使用时，使用GraphQL进行查询时生成的标记未保留HTML中指定的格式。 例如，列表后缺少换行符。 其影响是最后一段成为清单的一部分。 (SITES-23233)


<!-- #### [!DNL Content Fragments] - GraphQL Query Editor{#sites-graphql-query-editor-6522}

* A


#### [!DNL Content Fragments] - REST API{#sites-restapi-6522}

* A -->

#### 核心后端{#sites-core-backend-6522}

* 在AEM创作实例上报告了循环`SegmentNotFoundException`错误。 重新启动作者暂时解决了问题，但需要长期修复以防止再次发生。 (SITES-22573)
* 在AEM Sites中提出了有关时间线功能的问题，特别是有关处理注释中缺少的`cq:lastModified`属性的问题。 应用AEM 6.5.20后，无法确定现有内容是否需要修复缺少的属性，或者时间线是否进行了更新以便在没有时间线的情况下正常工作。 (SITES-21861)


#### 核心组件{#sites-core-components-6522}

* 从AEM 6.5.18升级到6.5.21后，检查组件实时使用的功能出现问题。 当尝试在“实时使用情况”页面上滚动其他项目时，表无法加载更多结果，即使在UI中看到“正在加载更多项目”。 (SITES-23919)
* 在包含两个选项卡的AEM组件对话框中，已报告验证必填字段时出现问题。 选项卡1包含富文本编辑器(RTE)和文本字段，而选项卡2包含路径字段和文本字段。 尽管所有字段都标记为必填字段(`required=true`)，但错误通知在选项卡1中仍错误地保留，即使填写了所有必填字段后也是如此。 相反，选项卡2中的错误按预期清除。 (SITES-23243)
* 迁移到AEM 6.5.21后，HTML模板语言`data-sly-include`语句不再按预期运行，特别是无法支持`appendPath`和`prependPath`表达式。 因此，所包含资源的输出无法正确呈现，即使它在迁移之前工作正常。 此问题导致依赖这些表达式进行路径处理的资源呈现失败。 (GRANITE-52970)


<!-- #### Campaign integration{#sites-campaign-integration-6522}

* A -->


#### 体验片段{#sites-experiencefragments-6522}

* 在列表视图中单击&#x200B;**Title**&#x200B;列标题时，体验片段无法按预期按标题排序。 观察到屏幕快速闪烁，但未进行排序。 (SITES-23706)

* 在AEM 6.5.17中，在使用现成功能将页面组件转换为体验片段时遇到问题。 转换后，体验片段在编辑期间显示为空，尽管在使用该体验片段的页面上正确显示。 问题源于不正确的节点创建：组件节点放在根/容器节点之外，违反了模板的结构。 您需要手动将组件节点移动到正确的根/容器节点中，以恢复片段的可编辑性。 (SITES-22974)

* 从AEM 6.5.11迁移到6.5.20后，体验片段上的云配置无法正确保存。 尽管配置似乎保存在`crx/de`中，但在重新打开配置控制台时不会显示它们，这表明存在持久性问题。 (SITES-22287)


<!-- #### Foundation Components (Legacy){#sites-foundation-components-legacy-6522}

* A -->


#### 启动项{#sites-launches-6522}

在AEM生产中使用标记过滤器添加体验片段资源时，用户可以选择它，但在选择&#x200B;**创建语言副本**&#x200B;后遇到错误。 预期行为是从标记过滤器中选择的体验片段资产应该添加到翻译项目。 (SITES-24152)

#### 链接检查器{#sites-link-checker-6522}

LinkCheckerTask无法进行身份验证，因为HTTP客户端在基本身份验证之前尝试NTLM，导致代理在多次尝试失败后阻止用户。 系统应改用基本身份验证对代理进行身份验证，以允许LinkCheckerTask服务正常工作。 (SITES-25034)


#### MSM — 活动副本{#sites-msm-live-copies-6522}

* 将SEO Robots标记应用于主副本并转出到Live Copy页面时，值在`crx/de`中正确显示。 但是，这些值未反映在Live Copy页面的页面属性下的用户界面中。 (SITES-23475)
* 尝试通过用户界面提升启动项时，出现与启动项相关的错误。 “提升启动”向导保持为空，这将阻止提升过程完成。 (SITES-19718)
* 尝试创建活动副本和执行转出后，AEM中的体验片段出现问题。 当用户尝试从转出屏幕导航回体验片段管理屏幕时遇到`NotFound`错误时，出现问题。 (SITES-21933)


#### 页面编辑器{#sites-pageeditor-6522}

* “撤消”按钮除了将文本更改为上一个版本外，还更改了组件的位置。 (SITES-17465)
* 粘贴复制的容器组件后，该组件会以可视方式显示两次，从而会在页面上产生三个实例。 但是，在刷新页面后，重复内容消失，表明问题可能是暂时性视觉问题。 (SITES-21890)
* 使用键盘的Tab键或Shift+Tab键导航组件左窗格时，无法以可视方式和选项卡模式清楚地看到多个文本元素。 此问题会影响辅助功能，使其在键盘导航期间难以识别这些组件或与之交互。 (SITES-2266)

#### 复制{#sites-replication-6522}

在AEM 6.5.18和6.5.19中，在停用父页面时，会为每个子页面生成多个停用请求。 此问题还中断了GraphQL端点的批量取消发布。 (NPR-42075和NPR42010)


### [!DNL Assets]{#assets-6522}

* 使用“连接的Assets”功能时，在AEM Assets中所做的更新不会反映在AEM Sites环境中。 (ASSETS-42344)
* 在Experience Manager中将资源从一个位置移动到另一个位置时，资源发布状态存在问题。 (ASSETS-41158)
* 使用API上传资产会导致`unclosed resource resolver`错误消息。 (ASSETS-41049)
* 升级到Adobe Experience Manager Service Pack 21后，`AssetReferenceResolverImpl`引用查询出现问题。 (ASSETS-40384)
* 在AEM版本6.5.19中，在从搜索面板结果中删除一个选项时，它也会取消选中所有其他可用复选框。 (ASSETS-37335)
* 执行批量元数据导出操作时，会在Excel输出中显示垃圾值。 (ASSETS-37260)
* 在AEM版本6.5.19中，当您以UTF-8格式上传SVG文件时，输出会变得模糊。 (ASSETS-36616)
* “连接的Assets”配置中缺少`Fetch original rendition for Dynamic Media Connected Assets`选项。 (ASSETS-41726)
* 即使您未定义必填字段的值，也会保存资源属性。 (ASSETS-37914)
* 如果资产的处理状态为“失败”或“元数据失败”，则字幕和音频轨道UI将无法正常工作。 (ASSETS-37281)
* 在保存资源元数据并尝试编辑它时，语言名称不显示。 (ASSETS-37281)

#### [!DNL Dynamic Media]{#assets-dm-6522}

当视频上传到Dynamic Media失败时，生产问题中断了迁移过程，并在用户界面中显示进程失败错误。 (ASSETS-36038)

<!--

### [!DNL Forms]{#forms-6522}

Fixes in [!DNL Experience Manager] Forms are delivered through a separate add-on package one week after the scheduled [!DNL Experience Manager] Service Pack release date. In this case, the AEM 6.5.22.0 Forms add-on package release is scheduled for Thursday, November 28, 2024. A list of Forms fixes and enhancements is added to this section post the release.

-->

### Forms {#forms-bug-fixes-sp22}

* 在AEM Forms中已保存的草稿中，为文件附件生成的URL不反映配置的Apache Sling资源解析器工厂映射。 (FORMS-16949)
* 当AEM Forms Service Pack 19 (6.5.19.0)用户预览信件时，内容未正确对齐，因为空格显示缺失，并且字符“x”出现在某些位置。 (FORMS-16670)
* 当用户在AEM Forms Service Pack 18 (6.5.18.0)上尝试使用CIF协议打印文件时，它会失败并出现以下错误：(FORMS-16629)
  `ALC-OUT-001-401: Unknown error while printing using CIFS on the Printer: \\\\\\\\NSMVPLUETEST01\\\\TH_Test`。
* 当用户从AEM Forms Service Pack 17 (6.5.17.0)升级到AEM Forms Service Pack 20 (6.5.20.0)时，规则编辑器图标未出现在表单容器级别。 (FORMS-16430)
* 当用户从AEM Forms Service Pack 17 (6.5.17.0)升级到AEM Forms Service Pack 21 (6.5.21.0)时，修改的自适应表单提交URL路径无法正常工作。 (FORMS15894)
* 在AEM Forms Service Pack 19 (6.5.19.0)上，AEM Forms 6.5PDF/A验证因错误`creation date and modification date mismatch with timezone`而对某些文件失败，而它在Acrobat ProPDF/A验证上顺利运行以进行合规性检查。 (FORMS-15840)
* 当用户在OSGi上的AEM Forms Service Pack 15 (6.5.15.0)的站点页面上使用“草稿和提交”组件删除表单草稿时，删除失败。 (FORMS-15755)
* 当用户的SharePoint列表包含超过999个条目并且表单包含附件时，表单提交失败。 (FORMS-15057)
* 当用户使用两个标记为开始日期和结束日期的日期选择器组件时，在添加验证规则以确保结束日期不早于开始日期并设置自定义脚本验证消息后，如果结束日期早于开始日期，则不会触发验证。 (FORMS-14757)
* 当用户在自适应表单的表上应用显示和隐藏功能时，字段大小缩小。 添加和删除行时，字段大小会自行更正。 (FORMS-14756)
* 当用户在AEM Forms Service Pack 19 (6.5.19.0)上打印表单时，某些表单在服务器上无法正确呈现，导致打印过程中出现错误。 (FORMS14734)
* 当用户从AEM Forms Service Pack 15 (6.5.15.0)更新到AEM Forms Service Pack 19 (6.5.19.0)，并使用将特定变量设置为number并将自定义显示模式设置为num{$zzz，zz9.99}的表单时，该模式无法在预览和代理UI中正确呈现。 (FORMS-14694)
* 当用户使用保存的数据xml在交互式通信中预览信件时，信件在AEM UI上卡在“正在加载”状态。 使用同一XML再次预览信件可以正常进行。 (FORMS-14521)
* 当AEM Forms Service Pack 20 (6.5.20.0)上的用户使用自适应表单中的“发送电子邮件”提交操作按钮发送带有附件的电子邮件时，附件名称显示在下一行而不是内联。 (FORMS-14426)
* 当用户在AEM Forms中生成项目符号列表设置为默认“磁盘”样式的PDF时，PDF无法通过Adobe Acrobat辅助功能工具中的辅助功能检查。 具有“项目符号”和“正方形”样式的列表通过了辅助功能检查。 (FORMS-13802和LC-3922179)
* 当用户在Standalone RHEL8 JBoss设置上从AEMForms-6.5.0-0065升级到AEMForms-6.5.0-0087时，无法连接到LiveCycle服务容器。 (FORMS-15907) ·
* 在JEE上的AEM FormsAEM Workspace中，当用户选择以前提交的表单并开始新表单流程时，具有预填充数据流程的表单会清除所有以前提交的数据并将其替换为预填充的数据，而不会保留任何手动填写在上一个表单中的字段。 (FORMS-15376)
* 在AEM Forms Service Pack 20 (6.5.20.0)上，当用户使用PDFG服务将Tiff文件转换为PDF时，它会失败，并出现错误：(FORMS-14879) ALC-PDG-011-028 — 将输入图像文件转换为PDF时出错。 com/sun/image/codec/jpeg/JPEGCodec
* 在AEM Forms on JEE jar文件中升级：现在包含`commons-collections:commons-collections:jar`库，以改进各种AEM Forms JEE作业中的依赖项解析和功能，例如：
   * 汇编程序作业增强，可改进作业处理和错误处理。
   * PDF Generator(PDFG)作业增强，可确保为文档生成和转换执行更顺畅的操作。
   * LC-Upgrade Job增强功能，可在确保版本之间稳定过渡的同时改进升级过程。
   * Rights Management作业增强以确保Document Handling的安全，并改进权限管理功能。
   * 流程管理作业增强，可实现更可靠的作业处理和系统管理。


#### XMLFM {#forms-xmlfm-sp22}

* 在AEM Forms Service Pack 21 (6.5.21.0)中，当用户使用XMLFM向PDF添加非标准标签时，文档无法符合PDF规范要求。 (LC-3922484)
* 当用户使用AEM Forms Service Pack 20 (6.5.20.0)上的输出服务生成PDF时，它将因CORBA.COMM_FAILURE而失败并显示错误： `15:04:35,973 ERROR [com.adobe.formServer.PA.XMLFormAgentWrapper] (default task-14) ALCOUT-002-013: XMLFormFactory, PAexecute failure: "org.omg.CORBA.COMM_FAILURE"`。 从XDP模板的子表单中排除辅助功能角色“引用”时，服务成功通过。 但是，508项合规需要这一角色。 (LC-3922402)
* 当用户将XFA表单转换为AcroFormPDF时，它会失败。 (LC-3922363)
* 在AEM Forms Service Pack 19 (6.5.19.0)中，当用户使用未命名子表单创建XDP时，FS_DATA_SOM对于未命名子表单显示为空。 (LC-3922034)

#### Forms Designer {#forms-designer-sp22}

* 当用户通过在AEM Forms Designer版本6.5.21.0中选择片段文件夹来打开片段库时，它会崩溃。 (LC-3922439)
* 当用户卸载32位AEM Forms Designer版本6.5.20.0并安装AEM Forms Designer版本6.5.21.0时，Forms Designer无法启动。 错误日志显示Java运行时环境(JRE)的内存分配不足。 (LC-3922404)
* 用户安装AEM Forms Designer版本6.5.20.0后，菜单中不会显示“宏”选项，而是仅显示默认的“辅助功能检查器”宏，且无法运行。 (LC-3922321)
* 当用户添加用于在AEM Forms Designer版本6.5.20.0中创建XDP的新模板位置时，Forms Designer崩溃。 (LC-3922316)
* 当用户在AEM Forms 6.5 Service Pack 15 (6.5.15.0) OSGI中使用ExportData方法生成输出时，它会生成不完整和不正确的数据。 (LC-3922340)


<!-- #### [!DNL Adaptive Forms] {#forms-6522}

* A


#### [!DNL Forms Designer] {#forms-designer-6522}

* A -->


### Foundation {#foundation-6522}

在AEM Assets控制台中，尝试重新排序DITA文档时出现问题。 路径浏览器对话框顶部的痕迹导航错误地显示节点名称而非根父级的节点标题。 只有在痕迹导航中选择项目后，才会显示正确的节点标题，这表示临时显示错误。 (NPR-42106)


<!-- #### Apache Felix {#foundation-apachefelix-6522}


* A

#### Campaign{#foundation-campaign-6522}

* A


#### Cloud Services{#foundation-cloudservices-6522}

* A -->


#### 社区 {#foundation-communities-6522}

从AEM 6.5.19升级到6.5.20后，出现了一个问题，在调用`UgcSearch`后，`Connection evic`线程无法正确关闭。 在生产环境中发现的此问题会导致这些线程随时间持续存在和累积，从而可能影响性能。 (NPR-42019)


<!-- #### Content distribution{#foundation-content-distribution-6522}

* A -->


#### CRX {#foundation-crx-6522}

* 在CRX包管理器的左侧菜单中，按&#x200B;**组**&#x200B;的排序不起作用。 (GRANITE-53277)
* 默认情况下，AEM中的包管理器限制安装较低版本的包，但允许强制安装较旧的版本。 但是，使用强制安装选项可能会干扰通过标准管道进行的未来安装。 例如，如果安装了版本1.21并添加了版本1.24，则安装成功，并列出了两个版本。 但是，尝试安装1.22和1.24以上版本时，管道会失败，但如果强制安装，则会正常进行，并列出所有版本。 同样，如果版本1.24已存在，则会阻止安装版本1.23，因为管道不允许降级。 (GRANITE-53263)


#### Granite{#foundation-granite-6522}

* 使用CURL命令在AEM中安装了快照包。 在安装期间，JCR安装程序通过OSGI安装程序扫描包，以确保不需要其他OSGI包或配置。 如果包版本包含“SNAPSHOT”，则OSGI安装程序会触发VLT创建相应的快照包。 但是，由于每个AEM创作实例都运行自己的OSGI安装程序，因此两个实例都可能尝试同时生成快照，从而导致存储库中的会话冲突。 (NPR-42003)
* 使用AEM 6.5.21的`ScriptDependencyResolver`中存在锁定争用。 (GRANITE-53181)
* 将AEM升级到6.5.21后，在Sightly (HTL)语法（如`data-sly-use`）中使用相对路径时出现问题。 (GRANITE-53080)


#### 集成{#foundation-integrations-6522}

* 为Cloud Service用户界面添加了法律归因语句。 (FORMS-16373)
* 为&#x200B;**fd-cloudservice**&#x200B;用户添加了访问hCaptcha和Turnstile配置的读取权限，使其能够检索验证码渲染和验证所需的客户端ID和客户端密钥。 此外，还实施了访问控制列表模型来管理对这些配置的访问。 (FORMS-16360)


#### 本地化{#foundation-localization-6522}

在![锤子图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg)工具> **安全性** > ![用户图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_User_18_N.svg) **用户**&#x200B;中，在“用户管理”页面上，表格的&#x200B;**状态**&#x200B;列中的数据垂直显示。 (GRANITE-48304)


<!-- #### Oak {#foundation-oak-6522}

* A -->


#### Platform{#foundation-platform-6522}

* AEM 6.5.18中引入的企业信息管理跟踪在计算产品采用率分数时会导致异常。 Adobe指标库会覆盖由Omega跟踪库提供的用户数据，从而导致出现此问题。 因此，从2024年2月开始，许多AEM Sites和AEM Assets客户的采用分数降至零。 (CQ-4358438)
* 已发现在生产环境中，垃圾回收器未正确处理标记的关键问题。 具体而言，在移动或重命名标记时，垃圾回收器未能更新`cq:MovedTo`属性，从而导致标记从页面中消失。 (CQ-4358293)
* 将上下文路径添加到AEM实例时，AEM 6.5.19中的ContextHub问题导致区段解析不正确。 该问题具体影响了页面组件生成的JavaScript对象中的URL字段，该字段缺少所需的上下文路径前缀。 这种遗漏使区段无法按预期运行。 (SITES-21852)
* 更新了AEM快速入门以使用库`commons-collections-3.2.2-adobe-2`。 此更新可确保应用程序能够继续顺利运行。 (NPR-42150)
* AEM 6.5中的SMTP OAuth2设置与AEM as a Cloud Service中使用的设置有显着差异。 为了简化配置并确保一致性，AEM 6.5中的设置需要与AEM as a Cloud Service中使用的标准保持一致。 (GRANITE-53273)
* 单击![指南图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Compass_18_N.svg) > ![项目图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Project_18_N.svg)项目，然后将鼠标指针悬停在![左边栏图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![V形下图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg)上时，发现了一个问题，在工具提示文本“仅内容”之前会显示严重重音。 (CQ-4356633)

#### 安全性{#foundation-security-6522}

* 在AEM中使用过期的JSAFE加密库（版本6.0.0）时遇到问题。 AEM 6.5.22中包含一个带有JSAFE版本6.2.5的补丁包。 (NPR-42006)
* 在XSS检查期间验证允许的协议时，处理程序会与“http”和“https”进行比较。 但是，URL对象的`protocol`属性返回这些带有尾随冒号的值，如`http:`和`https:`。 此不匹配导致验证问题。 为确保解析的准确性，协议检查需要考虑冒号或相应地调整比较逻辑。  (NPR-42119)
* 在IBM®WebSphere®Liberty Profile和Semeru Java 8.0上安装AEM 6.5.21(先前版本为AEM 6.5.19)后，无法打开任何页面。 错误日志指示与需要不同捆绑包的servlet版本相关的问题。 要解决此问题，必须恢复对`org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`的依赖关系，因为它与问题相关。 (NPR-42116)
* 有几个浏览器正在逐步停止支持&#x200B;**SameSite=None** Cookie，后者用于允许跨站点访问Cookie。 作为替代方法，正在引入&#x200B;**分区Cookie**。 这些Cookie根据使用它们的上下文来隔离存储，通过阻止跨站点跟踪来增强隐私和安全性，同时仍允许Cookie在特定分区内发挥作用，例如嵌入的第三方内容。 (GRANITE-51953)


<!-- #### Sling{#foundation-sling-6522}

* A -->


#### 翻译{#foundation-translation-6522}

* 添加了对核心组件中最近更改为默认翻译规则的支持。 (NPR-42029)
* 在AEM Forms中导出XLIFF文件时发现问题。 使用&#x200B;**将选定内容导出为XLIFF （仅限字符串）**&#x200B;选项时，无法始终保持组件的顺序。 但是，在为特定语言导出XLIFF时，序列将保持正确。 提供了两个文件来演示问题：**DE-CH_Export.xliff**（顺序正确）和&#x200B;**String_Export.xliff**（顺序不正确）。 (NPR-42118)


#### 用户界面{#foundation-ui-6522}

* `coralui-component-dialog`正在更改`cq-dialog-actions`的位置，这可能会影响AEM对话框中操作按钮的布局或行为。 (NPR-42294)
* AEM中的拾色器功能出现故障。 访问时，它显示一个空白模式，阻止颜色选择。 在暂存环境中安装AEM 6.5.20后，此问题开始出现。 拾色器在&#x200B;*之前*&#x200B;对更新工作正常。 (NPR-42163)
* 在![锤子图标](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) **工具** > **工作流** > **模型** >选择任意模型> **启动工作流**&#x200B;中，**运行工作流**&#x200B;对话框的有效负荷字段中缺少“浏览”图标。 (NPR-42162)


<!-- #### WCM{#foundation-wcm-6522}

* A


#### Workflow{#foundation-workflow-6522}

* A -->


## 安装[!DNL Experience Manager] 6.5.22.0{#install}

<!-- Remaining content from here to bottom stays the same except for version updating as needed as per update team feedback. -->

* [!DNL Experience Manager] 6.5.22.0需要[!DNL Experience Manager] 6.5。有关详细说明，请参阅[升级文档](/help/sites-deploying/upgrade.md)。<!-- UPDATE FOR EACH NEW RELEASE -->
* 可在Adobe[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)上下载Service Pack。
* 在具有MongoDB和多个实例的部署中，使用包管理器在其中一个创作实例上安装[!DNL Experience Manager] 6.5.22.0。<!-- UPDATE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> Adobe不建议您删除或卸载[!DNL Experience Manager] 6.5.22.0包。 因此，在安装该包之前，您应该创建`crx-repository`的备份，以防必须回滚。<!-- UPDATE FOR EACH NEW RELEASE -->
<!-- For instructions to install Service Pack for Experience Manager Forms, see [Experience Manager Forms Service Pack installation instructions](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md). -->


### 在[!DNL Experience Manager] 6.5上安装服务包{#install-service-pack}

1. 如果实例处于更新模式（从早期版本更新实例时），请在安装之前重新启动该实例。 如果实例的当前正常运行时间较长，则Adobe建议重新启动。

1. 安装之前，请为[!DNL Experience Manager]实例拍摄快照或进行全新备份。

1. 从[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.22.0.zip)下载Service Sack。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 打开包管理器，然后选择&#x200B;**[!UICONTROL 上传包]**&#x200B;以上传包。 若要了解更多信息，请参阅[包管理器](/help/sites-administering/package-manager.md)。

1. 选择包，然后选择&#x200B;**[!UICONTROL 安装]**。

1. 要更新S3连接器，请在安装Service Pack后停止实例，使用安装文件夹中提供的新的二进制文件替换现有连接器，然后重新启动实例。 请参阅[Amazon S3数据存储](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>在安装Service Pack期间，包管理器UI上的对话框有时会退出。 Adobe建议您在访问部署之前等待错误日志稳定下来。 等待与卸载更新程序捆绑包相关的特定日志，然后确定安装成功。 通常，此问题发生在[!DNL Safari]浏览器中，但可能会间歇性地发生在任何浏览器中。

**自动安装**

可以使用两种不同的方法来安装[!DNL Experience Manager] 6.5.22.0.<!-- UPDATE FOR EACH NEW RELEASE -->

* 当服务器联机时，将包放入`../crx-quickstart/install`文件夹中。 软件包会自动安装。
* 使用包管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`安装嵌套包。

>[!NOTE]
>
>Experience Manager6.5.22.0不支持Bootstrap安装。<!-- UPDATE FOR EACH NEW RELEASE -->

**验证安装**

要了解经认证可与此版本配合使用的平台，请参阅[技术要求](/help/sites-deploying/technical-requirements.md)。

1. 产品信息页面(`/system/console/productinfo`)在[!UICONTROL 已安装的产品]下显示更新的版本字符串`Adobe Experience Manager (6.5.22.0)`。<!-- UPDATE FOR EACH NEW RELEASE -->

1. 在OSGi控制台中，所有OSGi包均为&#x200B;**[!UICONTROL 活动]**&#x200B;或&#x200B;**[!UICONTROL 片段]**（使用Web控制台： `/system/console/bundles`）。

1. OSGi捆绑包`org.apache.jackrabbit.oak-core`的版本为1.22.20或更高版本（使用Web控制台： `/system/console/bundles`）。<!-- OAK Oak oak VERSION -MAY- NEED TO BE UPDATED FOR EACH NEW RELEASE. CHECK WITH SAMEER DHAWAN -->

### 安装[!DNL Experience Manager] Forms的Service Pack{#install-aem-forms-add-on-package}

有关在Experience Manager Forms上安装Service Pack的说明，请参阅[Experience Manager Forms Service Pack安装说明](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)。

>[!NOTE]
>
>在 [AEM 6.5 快速入门](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/deploying/deploy)中谈及的自适应表单功能旨在仅作探索和评估用途。由于自适应表单功能需要适当的许可，因此必须获得 AEM Forms 的有效许可证才能作生产用途。

### 安装用于Experience Manager内容片段的GraphQL索引包{#install-aem-graphql-index-add-on-package}

使用GraphQL的客户必须安装[Experience Manager内容片段和GraphQL索引包1.1.1](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/cfm-graphql-index-def-1.1.1.zip)。

这样，您就可以根据实际使用的功能添加所需的索引定义。

无法安装此包可能会导致GraphQL查询缓慢或失败。

>[!NOTE]
>
>每个实例仅安装此包一次；无需随每个Service Pack一起重新安装。

### UberJar{#uber-jar}

[!DNL Experience Manager] 6.5.22.0的UberJar在[Maven中央存储库](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.22/)中可用。<!-- CHECK FOR UPDATE EACH NEW RELEASE -->

要在Maven项目中使用UberJar，请参阅[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，并在项目POM中包含以下依赖项： <!-- CHECK FOR UPDATE EACH NEW RELEASE -->

```shell
  <dependency>
  <groupId>com.adobe.aem</groupId>
  <artifactId>uber-jar</artifactId>
  <version>6.5.22</version>
  <scope>provided</scope>          
  </dependency>
```

>[!NOTE]
>
>UberJar和其他相关工件可在Maven中央存储库上使用，而不是Adobe公共Maven存储库(`repo.adobe.com`)。 主UberJar文件已重命名为`uber-jar-<version>.jar`。 因此，`dependency`标记中没有`classifier`，值为`apis`。


## 已弃用和已删除的功能{#removed-deprecated-features}

请参阅[已弃用和已删除的功能](/help/release-notes/deprecated-removed-features.md/)。

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

   1. 从`crx-quickstart/repository/`中删除以下两个文件夹

      * `cache`
      * `diff-cache`

   1. 安装Service Pack，或重新启动Experience Manageras a Cloud Service。
`cache`和`diff-cache`的新文件夹是自动创建的，您在`error.log`中不再遇到与`mvstore`相关的异常。

* 更新可能已为内容模型使用自定义API名称的GraphQL查询，以改用内容模型的默认名称。

* GraphQL查询可以使用`damAssetLucene`索引而不是`fragments`索引。 此操作可能会导致GraphQL查询失败或需要很长时间才能运行。

  若要更正此问题，必须将`damAssetLucene`配置为在`/indexRules/dam:Asset/properties`下包含以下两个属性：

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
为确保操作正确，必须将以下属性添加到索引定义节点`/oak:index/damAssetLucene`（不需要重新索引）：

  ```xml
  "tags": [
      "visualSimilaritySearch"
    ]
  "refresh": true
  ```

* 如果您将[!DNL Experience Manager]实例从6.5.0 - 6.5.4升级到Java™ 11上的最新Service Pack，则会在`error.log`文件中看到`RRD4JReporter`异常。 若要停止异常，请重新启动[!DNL Experience Manager]的实例。<!-- THIS BULLET POINT WAS UPDATED AS PER CQDOC-20021, JANUARY 23, 2023 -->

* 用户可以在[!DNL Assets]中重命名层次结构中的文件夹，并将嵌套文件夹发布到[!DNL Brand Portal]。 但是，在重新发布根文件夹之前，[!DNL Brand Portal]中的文件夹标题不会更新。

* 安装[!DNL Experience Manager] 6.5.x.x期间可能会显示以下错误和警告消息：
   * “当使用Adobe Target API（IMS身份验证）在[!DNL Experience Manager]中配置Target Standard集成时，将体验片段导出到Target会导致创建错误的选件类型。 Target将创建多个类型为“Experience Fragment”/源“Adobe Experience Manager”的选件，而不是类型为“HTML”/源“Adobe Target Classic”。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`：在`granite/operations/maintenance`处未找到维护时段。
   * 当使用集合函数(如SUM、MAX和MIN)时，自适应表单服务器端验证失败(CQ-4274424)。
   * `com.adobe.granite.maintenance.impl.TaskScheduler` ：在`granite/operations/maintenance`处未找到维护时段。
   * 通过可购物横幅查看器预览资源时，Dynamic Media交互式图像中的热点不可见。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` ：等待注册更改完成取消注册时超时。

* 从AEM 6.5.15开始，```org.apache.servicemix.bundles.rhino```捆绑包提供的Rhino JavaScript Engine具有新的提升行为。 使用严格模式(```use strict;```)的脚本必须声明其正确的变量。 否则，它们将不会运行，并最终引发运行时错误。

* 通过官方更新包安装与标记相关的现成内容会将`/content/cq:tags`节点的languages属性重置为默认值。 此操作适用于Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修补程序等。 因此，在安装之前，必须从属性中添加它。

### AEM Sites的已知问题 {#known-issues-aem-sites-6522}

* 内容片段 — 预览由于大型片段树的DoS保护而失败。 请参阅关于默认GraphQL查询执行器配置选项](https://experienceleague.adobe.com/zh-hans/docs/experience-cloud-kcs/kbarticles/ka-23945)的[KB文章(SITES-17934)


### AEM Forms的已知问题 {#known-issues-aem-forms-6522}

* 安装AEM Forms JEE Service Pack 21 (6.5.21.0)后，如果在`<AEM_Forms_Installation>/lib/caching/lib`文件夹下找到Geode Jar `(geode-*-1.15.1.jar and geode-*-1.15.1.2.jar)`的重复条目(FORMS-14926)，请执行以下步骤，以解决该问题：

   1. 如果定位器正在运行，请停止它们。
   1. 停止AEM服务器。
   1. 转到`<AEM_Forms_Installation>/lib/caching/lib`。
   1. 删除除`geode-*-1.15.1.2.jar`之外的所有Geode修补程序文件。 确认仅存在具有`version 1.15.1.2`的Geode jar。
   1. 在管理员模式下打开命令提示符。
   1. 使用`geode-*-1.15.1.2.jar`文件安装Geode修补程序。

* 如果用户尝试预览包含保存的XML数据的草稿信件，则对于某些特定信件，它会陷入`Loading`状态。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-14521)

* 升级到AEM Forms Service Pack 6.5.21.0后，`PaperCapture`服务无法对PDF执行OCR（光学字符识别）操作。 该服务不会以PDF或日志文件的形式生成输出。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (CQDOC-21680)

* 用户从AEM 6.5 Forms Service Pack 18或19升级到Service Pack 20或21时，遇到JSP编译错误。 此错误会阻止他们打开或创建自适应表单。 它还导致其他AEM界面出现问题。 这些界面包括页面编辑器、AEM Forms UI、工作流编辑器和系统概述UI。 (FORMS-15256)

  如果您遇到此类问题，请执行以下步骤来解决此问题：
   1. 导航到CRXDE中的目录`/libs/fd/aemforms/install/`。
   1. 删除名为`com.adobe.granite.ui.commons-5.10.26.jar`的包。
   1. 重新启动AEM Server。

* 使用AEM Forms加载项更新到Forms Service Pack 20 (6.5.20.0)后，依赖旧版Adobe Analytics Cloud Service （使用基于凭据的身份验证）的配置停止工作。 此问题会导致Analytics规则无法正确执行。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (FORMS-15428)

* 当用户在JEE服务器上更新到AEM Forms Service Pack 20 (6.5.20.0)并使用输出服务生成PDF时，PDF呈现时的辅助功能问题。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922112)
* 当用户使用JEE上的输出服务生成已标记PDF时，会显示“结构不当警告”。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922038)
* 在AEM Forms JEE上提交表单时，将从数据中删除重复XML元素的实例。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3922017)
* 当Linux®环境中的用户在HTML中渲染自适应表单（在JEE上）时，它无法正确渲染。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921957)
* 当用户使用AEM Forms JEE上的输出服务将XTG文件转换为PostScript格式时，它会失败，并出现错误： `AEM_OUT_001_003: Unexpected Exception: PAExecute Failure: XFA_RENDER_FAILURE`。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921720)
* 在JEE服务器上升级到AEM Forms Service Pack 18 (6.5.18.0)后，当用户提交表单时，将无法呈现HTML5或PDF forms，并且XMLFM崩溃。 要下载并安装修补程序，请参阅[Adobe Experience Manager Forms修补程序](/help/release-notes/aem-forms-hotfix.md#hotfix-for-adaptive-forms)文章。 (LC-3921718)
* 在交互式通信代理UI的打印预览中，所有字段值的货币符号（如美元符号$）显示方式不一致。 对于最多999的值，它出现，但对于1000及更高版本的值则缺失。 (FORMS-16557)
* 交互式通信中对嵌套布局片段XDP所做的任何修改都不会反映在IC编辑器中。 (FORMS-16575)
* 在交互式通信代理UI的打印预览中，某些计算值无法正确显示。 (FORMS-16603)
* 在打印预览中查看信件时，内容会更改。 也就是说，某些空格消失，某些字母被替换为“x”。 (FORMS-15681)
* 当用户配置WebLogic 14c实例时，由于涉及SLF4J库的类加载器冲突，因此AEM Forms Service Pack 21 (6.5.21.0)中的PDFG服务（在JBoss上运行的JEE上）失败。 错误显示如下(CQDOC-22178)：

  ```java
  Caused by: java.lang.LinkageError: loader constraint violation: when resolving method "org.slf4j.impl.StaticLoggerBinder.getLoggerFactory()Lorg/slf4j/ILoggerFactory;"
  the class loader org.ungoverned.moduleloader.ModuleClassLoader @404a2f79 (instance of org.ungoverned.moduleloader.ModuleClassLoader, child of 'deployment.adobe-livecycle-jboss.ear'
  @7e313f80 org.jboss.modules.ModuleClassLoader) of the current class, org/slf4j/LoggerFactory, and the class loader 'org.slf4j.impl@1.1.0.Final-redhat-00001' @506ab52
  (instance of org.jboss.modules.ModuleClassLoader, child of 'app' jdk.internal.loader.ClassLoaders$AppClassLoader) for the method's defining class, org/slf4j/impl/StaticLoggerBinder,
  have different Class objects for the type org/slf4j/ILoggerFactory used in the signature
  ```

## 包含的OSGi包和内容包{#osgi-bundles-and-content-packages-included}

以下文本文档列出了此[!DNL Experience Manager] 6.5 Service Pack版本中包含的OSGi包和内容包：

* [Experience Manager6.5.22.0](/help/release-notes/assets/65220-bundles.txt)中包含的OSGi包列表<!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager6.5.22.0](/help/release-notes/assets/65220-packages.txt)中包含的内容包列表<!-- UPDATE FOR EACH NEW RELEASE -->

## 受限制的网站{#restricted-sites}

这些网站仅供客户使用。 如果您是客户并且需要访问权限，请联系您的Adobe客户经理。

* [产品下载位于licensing.adobe.com](https://licensing.adobe.com/)
* [联系Adobe客户支持](https://experienceleague.adobe.com/en/docs/customer-one/using/home)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 产品页](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5文档](https://experienceleague.adobe.com/en/docs/experience-manager-65)
>* [订阅Adobe优先产品更新](https://www.adobe.com/cn/subscription/priority-product-update.html)
