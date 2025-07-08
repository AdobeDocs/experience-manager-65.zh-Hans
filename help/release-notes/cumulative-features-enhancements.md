---
title: Adobe Experience Manager 6.5版本中的关键功能和增强功能的汇总。
description: Adobe Experience Manager 6.5中比前八个Service Pack版本所具有的主要功能和增强功能的汇总列表。
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: 03c070f7bba1d66ce2a5309d2ab79567dbef3264
workflow-type: tm+mt
source-wordcount: '3539'
ht-degree: 13%

---

# 主要功能和增强功能汇总

对于以前的Service Pack版本，Adobe Experience Manager 6.5中的主要功能和增强功能的累积列表。

另请参阅[Adobe Experience Manager 6.5最新Service Pack发行说明](/help/release-notes/release-notes.md)。


## AEM 6.5，Service Pack 23—2025年5月22日

### Forms {#forms-sp23}

* [静态PDF中具有混合文本样式的辅助超链接](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：静态PDF中包含混合文本样式的超链接现在被标记为单个辅助元素。 此增强功能简化了标记树结构，改进了屏幕阅读器导航，并支持更好的辅助功能合规性。

* [已更新支持的平台矩阵](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本引入了受支持平台矩阵的更新，确保与新技术兼容。

   * IBM® Content Manager客户端8.7

   * MongoDB Enterprise 7.0

   * MySQL 8.4

   * Microsoft® SQL Server 2022

   * Microsoft® SQL Server JDBC驱动程序12.8

   * Red Hat® Enterprise Linux® 9（内核4.x，64位）

* [强化的文件附件组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作为安全措施，该组件现在阻止提交具有修改扩展名的文件，这些文件尝试绕过允许的文件类型检查。 在提交期间将阻止此类文件，以确保仅接受有效的文件类型。

## AEM 6.5，Service Pack 22—2024年11月21日

### Sites {#sites}

[通用编辑器](/help/sites-developing/universal-editor/introduction.md)现已在AEM 6.5上可用，可用于应用功能包的Headless用例。

### [!DNL Assets]

IPTC选项卡现在支持[!UICONTROL 替换文本]和[!UICONTROL 扩展描述]文本字段。 (Assets-34918)

### Forms {#forms-sp22}

#### AEM Forms中的新GA功能 {#ga-aem-forms-sp22}

* 添加了支持以在[Interactive Communications批处理API](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel)中启用字体嵌入 — Interactive Communications现在支持在通过批处理API生成的PDF中嵌入Adobe Ming和Adobe Myungjo字体。 此增强功能可确保生成的文档中的准确文本渲染，即使使用字体子集也是如此，从而改进了对PDF输出中的多语言内容的支持。

* [用于PDF辅助功能的内容表API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api) - OSGi上的AEM Forms现在支持新的目录标记API，以增强PDF的辅助功能标准。 它借助辅助技术使用户更容易访问PDF。

* [片段XDP解析](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository) - OSGi上的AEM Forms现在解析主XDP中引用并存储在AEM CRX存储库中的片段XDP。

* [PDF/A合规性增强功能](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents) — 现在，用户可将PDF转换为PDF/A格式(1a、2a、3a)以进行存档，同时确保可访问性并验证是否符合这些标准。

* **支持对静态PDF文档自动调整字体大小** - AEM Forms Designer、OutputService和FormsService现在支持对静态PDF自动调整字体大小。 如果用户将文本、数字、密码或日期时间字段的字体大小设置为0，则字体大小将在这些字段中自动调整，而不会更改字段的整体大小。 要使用该功能，用户在自定义XCI中传递一个标记：`<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`。

#### AEM Forms中的Beta新增功能 {#beta-aem-forms-sp22}

Beta版功能为您提供独一无二的机会，让您能够访问尖端创新并帮助塑造其发展。 有兴趣为您的环境启用Beta测试版功能吗？ 请将您的官方地址中的电子邮件发送至aem-forms-ea@adobe.com ，其中包含您感兴趣的功能列表。

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)和[Cloudflare Turnstile验证码服务](/help/forms/using/integrate-adaptive-forms-turnstile.md)： AEM Forms支持以下Captcha服务：
   * 验证码使用复选框小组件向用户发起挑战，保护表单免受机器人、垃圾邮件和自动滥用的侵害。 它确保只有人工用户才能进行，增强了在线交易的安全性。
   * Cloudflare Turnstile提供了一种安全措施，旨在保护表单免受自动机器人、恶意攻击、垃圾邮件和不需要的自动流量的影响。 在允许提交表单之前，它会在表单提交时显示一个复选框，以验证他们是人类。

* 自适应表单版本控制：
   * [创建自适应表单的多个版本](/help/forms/using/add-versioning-reviews-comments.md) — 现在，用户可以轻松管理现有表单的变体。 此过程简化了版本控制，并有助于在单个简化的工作流中比较表单优化。
   * [比较自适应Forms](/help/forms/using/compare-forms-core-components.md)：现在，用户可以轻松比较两个表单以找出差异。 它使团队成员能够比较修订内容，并有效地讨论相关变化，从而促进顺利协作。

## AEM 6.5，Service Pack 21—2024年6月6日

### [!DNL Assets]

#### 增强功能

IPTC选项卡现在支持[!UICONTROL 替换文本]和[!UICONTROL 扩展描述]文本字段。 (Assets-34918)

#### 辅助功能

* 如果资产的处理状态为“失败”或“元数据失败”，则字幕和音频轨道UI现在可以正常工作。 (Assets-37281)
* 现在，在保存资源元数据并尝试编辑该元数据时，会显示语言名称。 (Assets-37281)

### [!DNL Forms]

此版本中的某些主要功能和增强功能包括：

* **对Oauth凭据的支持**：用于服务器到服务器身份验证的更易于使用的新凭据，正在替换现有的服务帐户(JWT)凭据。 (NPR-41994)
* AEM Forms中的[规则编辑器增强功能](/help/forms/using/rule-editor-core-components.md)：
   * 支持使用`When-then-else`功能实现嵌套条件。
   * 验证或重置面板和表单，包括字段。
   * 支持现代JavaScript功能，如自定义函数中的let和arrow函数（支持ES10）。
* [适用于PDF辅助功能的AutoTag API](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services)： OSGi上的AEM Forms现在支持新的AutoTag API，可通过添加标记（段落和列表）来增强PDF的辅助功能标准。 它借助辅助技术使用户更容易访问PDF。
* **16位PNG支持**： PDF Generator的ImageToPdf服务现在支持转换具有16位颜色深度的PNG。
* **将工件应用于XDP中的单个文本块**： Forms Designer现在允许用户在XDP文件中配置单个文本块的设置。 此功能允许您控制在生成的PDF中被视为工件的元素。 辅助技术可访问这些元素，例如页眉和页脚。 主要功能包括将文本块标记为工件，并将这些设置嵌入到XDP元数据中。 Forms输出服务在生成PDF期间应用这些设置，从而确保正确的PDF/UA标记。
* **AEM Forms Designer通过`GB18030:2022`标准认证**：通过`GB18030:2022`认证，Forms Designer现在支持中文Unicode字符集，该字符集允许您在所有可编辑的字段和对话框中输入汉字符。
* [在JEE服务器上支持WebToPDF路由](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings)使用PDF Generator服务时，现在支持将HTML文件转换为JEE上的PDF文档的WebToPDF路由。 此支持是在现有Webkit和WebCapture（仅限Windows）路由之外提供的。 而WebToPDF路由已在OSGi上可用，并且已扩展到JEE。 现在，在JEE和OSGi平台上，PDF Generator服务支持跨不同操作系统的以下路由：
   * **Windows**： Webkit、WebCapture、WebToPDF
   * **Linux®**： Webkit， WebToPDF


## AEM 6.5，Service Pack 20—2024年2月22日

### [!DNL Assets]

* Dynamic Media现在支持Apple iOS/iPadOS的无损HEIC图像格式。 请参阅Dynamic Media图像服务和渲染API中的[fmt](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt)。
* 多站点管理器(MSM)现在支持体验片段结构（包括文件夹和子文件夹），以便有效地将体验片段批量转出到活动副本。

### [!DNL Forms]

* **JEE上的AEM Forms中的Transaction Reporting**：已为JEE上的AEM Forms引入了事务报告功能。 它允许全面记录文档事务，如转化、演绎版和提交。 此增强功能可提高效率并有助于更好地保存记录。 默认情况下，该功能处于禁用状态。 您可以从管理员UI中启用它。
* **支持ECDSA的增强安全性**：AEM Forms现在支持跨JEE和OSGi栈栈的椭圆曲线数字签名算法(ECDSA)。 用户现在可以对具有增强安全性的PDF文档进行签名、认证和验证。 支持的EC曲线算法包括：
   * 采用SHA256摘要算法的ECDSA椭圆曲线P256
   * 采用SHA384摘要算法的ECDSA椭圆曲线P384
   * 采用SHA512摘要算法的ECDSA椭圆曲线P512
* **与Forms Designer的Windows 11无缝兼容**： AEM Forms Designer现在支持Windows 11，确保顺利安装和操作。 用户可以放心地升级到Windows 11，而不必重新安装Forms Designer或担心兼容性问题，从而确保工作流不中断。
* **AEM Forms Designer中的自定义“Caption”角色增强了辅助功能**： AEM Forms Designer现在包含一个名为“Caption”的自定义辅助功能角色，使用户能够使用个性化的字幕元素创建XDP。 此功能通过允许用户将自定义字幕集成到其文档设计中来增强辅助功能，以便他们提高包容性和用户体验。

## AEM 6.5，Service Pack 19—2023年12月7日

* 启用了站点页面编辑器/图像组件用户从远程Assets Cloud Service引用资源的功能。 (SITES-13448和SITES-13433)
* AEM现在支持服务器端排序，从而加快列表视图中的项目导航速度。 项目节点在显示在界面中之前根据用户选择的列排序。

### [!DNL Forms]

* **新的自适应表单核心组件**：添加了垂直选项卡、条款和条件以及复选框以增强表单的可扩展性。
   * **[复选框组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**：基于核心组件的自适应表单现在包含复选框组件。通过它，用户可二选一，即选择或取消选择特定选项。它一般显示为一个小框，单击或点按它即可在选中和取消选中两种状态之间切换。复选框是一个常见的表单元素，用于提供是/否或 true/false 选择。

   * **[条款和条件组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**：基于核心组件的自适应Forms现在包含条款和条件组件。 表单作者添加此部分以向用户显示服务、产品或平台的条款、条件或法律协议。 此组件旨在通知用户其提交表单即表示同意的规则、法规和义务。

     ![垂直选项卡、条款和条件以及复选框组件](/help/forms/using/assets/forms-components.png)

   * **[垂直选项卡组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**：基于核心组件的自适应表单现在可将表单内容整理到选项卡垂直列表中，从而提供结构化的、可导航的布局。表单中的垂直选项卡通过简化导航和组织内容来增强用户体验。 当表单包含多个部分或复杂信息时，这些功能特别有用。

* **[64位版本的AEM Forms Designer](/help/forms/using/installing-configuring-designer.md)**： 64位版本的AEM Forms Designer提供增强的性能、可扩展性和内存管理，以增强您的表单创建体验。 利用 64 位架构，您可以轻松处理更大、更复杂的项目，确保无缝的设计工作流程和优化的效率。利用此最新版本，提升您的表单设计能力并迎接 AEM Forms Designer 的未来。

* **[将自适应Forms连接到Microsoft® SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**：AEM Forms提供现成的集成，可直接将表单数据提交到SharePoint List，让您使用SharePoint的“列表”功能。 您可以将Microsoft® SharePoint列表配置为表单数据模型的数据源，并使用使用表单数据模型提交操作将自适应表单与SharePoint列表连接起来。

* **[支持为自适应表单片段配置记录文档属性](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：您现在可以在自适应表单编辑器中轻松自定义自适应表单片段及其字段。

* **64位XMLFM**： XMLFM的64位迭代引入了更高的性能、可扩展性和更精细的内存管理。 它是第一个部署在服务器端的64位本机服务。 XMLFM 64位利用其固有的功能访问比32位对等项更大的内存资源，从而能够无缝处理更大的渲染工作负载。 这一里程碑不仅实现了性能的飞跃，而且还对AEM Forms服务器中的本机服务框架引入了关键增强功能。 此更新使AEM Forms Server能够无缝支持任何64位本机服务。

## AEM 6.5，Service Pack 18—2023年8月24日

* Assets、Dynamic Media - [Dynamic Media支持视频的多字幕和音轨](/help/assets/video.md#about-msma) — 您现在可以轻松地将多个字幕和多个音轨添加到主视频中。 此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。
* Assets — 现在，您可以在搜索结果中导航到包含资源的文件夹位置，以便执行各种资源管理任务。
* 内容片段中的Sites Polaris选取器改进了性能。
* 启用了站点页面编辑器/图像组件用户从远程Assets Cloud Service引用资源的功能。
* 为了快速在列表视图中查找系统中可能有许多项目的项目，Adobe现在支持服务器端排序。 项目节点在用户界面中呈现之前，会根据用户选择的列在后端进行排序。
* AEM 6.5.18.0支持MongoDB 5.0到6.0。

### [!DNL Forms]

* **[规则编辑器中使用自定义错误处理程序的增强错误处理](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)** — 您现在可以调用自定义函数（使用客户端库）来响应外部服务返回的错误。 而且，您可以为最终用户提供量身定制的响应。 或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后端中调用自定义工作流以获取特定错误代码，或通知客户服务已中断

* **[增强的Adobe Sign工作流步骤](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)** - AEM工作流中的Adobe Sign工作流步骤包含以下增强功能。

   * **通过基于Government ID的身份验证增强Adobe Sign的安全性** - Adobe Acrobat Sign基于Government ID的身份验证提供额外的验证层。 它允许用户使用政府颁发的ID（驾照、身份证、护照）进行身份认证。 通过利用可信身份证明文件，此增强将签名过程的可信度提高一级，使其成为需要更高的安全性、合规性和用户验证的场景的理想之选。

   * **使用Adobe Sign文档的审核记录增强透明度** — 使用审核记录功能详细了解Adobe Sign文档的生命周期。 通过审核记录，您现在可以维护与文档相关的所有操作和交互的全面记录。 这些操作和交互包括查看、编辑或签署文档的人员，以及每个事件的时间戳。 此增强对于保持合规性、解决争议和确保数字协议的完整性至关重要。


   * **扩展了协议收件人的角色，而不只是签名者** — 通过Adobe Acrobat Sign，您可以将协议收件人的角色扩展到仅包括签名者，以更好地匹配他们的工作流要求。 启用后，协议中的每个收件人可以单独配置其角色，签名者是默认角色。


* **[JEE上的AEM Forms完整安装程序](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)** — 此Service Pack为JEE上的AEM Forms提供完整安装程序，该安装程序支持多种新的软件组合，包括：
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Windows Server 2022上的Oracle WebLogic 14C
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC连接器8

如果您在JEE环境中安装或计划使用适用于AEM 6.5 Forms的最新软件，Adobe建议在JEE上使用AEM 6.5.18.0 Forms完整安装程序。 要探索新添加和已弃用的软件的完整列表，请参阅JEE上的AEM Forms或OSGi上的AEM Forms的文档。

## AEM 6.5，Service Pack 17—2023年5月25日

* **搜索体验增强** - 您现在可以对搜索结果中显示的资源快速执行以下操作：
   * 创建工作流
   * 创建一个版本
   * 关联或取消关联资源

  您无需导航到资源的位置并查看其属性即可执行这些操作。

* **Dynamic Media _快照_**允许您使用测试图像或Dynamic Media URL预览图像修饰符和智能成像优化，例如WebP或AVIF输出、带宽感知压缩和设备像素比缩放。 然后，您可以立即比较每个设置对质量和文件大小的影响。
请参阅 [Dynamic Media 快照。](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)
* 使用Dynamic Media的&#x200B;**DASH流** — 为Dynamic Media视频交付中的自适应流启动新协议（DASH — 通过HTTP的动态自适应流）（启用了CMAF）。 现在可供所有地区使用。
* **Experience Manager Sites和内容片段与Assets新一代Dynamic Media的集成** — 用户现在可以在Experience Manager Sites 6.5中使用其云托管的资源。他们可以在内部部署或Managed Services实例上创作和交付这些资源。

### [!DNL Forms]

* **[AEM页面编辑器中的自适应Forms](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)** — 您现在可以使用AEM页面编辑器快速创建多个表单并将其添加到站点页面。 通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：
   * 创建自适应表单，方法是将表单组件拖放到AEM Sites编辑器或体验片段中的自适应Forms容器组件。
   * 可在AEM Sites编辑器中使用“自适应Forms向导”，以便您能够独立于任何Sites页面创建表单，从而让您自由地跨多个页面重用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。
* **[在Experience Manager Forms中支持reCAPTCHA Enterprise](/help/forms/using/captcha-adaptive-forms.md)** — 在Experience Manager Forms中添加了对reCAPTCHA Enterprise的支持。 除了现有的Google reCAPTCHA v2支持之外，此功能还增强了针对欺诈活动和垃圾邮件的保护。
* **[通过Experience Manager Forms为Adobe Acrobat Sign政府版添加支持](/help/forms/using/adobe-sign-integration-adaptive-forms.md)** - AEM Forms现在与Adobe Acrobat Sign政府版集成（符合FedRAMP）。 此集成通过为政府关联帐户（政府部门和机构）提交自适应表单，为电子签名提供了高级的合规性和安全性。 与Adobe Acrobat Sign for Government的集成使Adobe的合作伙伴和政府客户能够在Adaptive Forms中使用电子签名处理一些任务最关键和最敏感的业务线。 这层额外的安全保障机制确保所有电子签名完全符合 FedRAMP Moderate 合规性，使 Adobe 的政府客户能够安心使用。
* **启用Salesforce与Experience Manager Forms的集成，以便进行数据交换** — 使用OAuth 2.0客户端凭据流配置Experience Manager Forms与Salesforce应用程序之间的集成。 此功能支持对应用程序进行安全而直接的身份验证和授权，并允许无缝通信，而无需用户参与。
* **工作流引擎的优化和增强功能**：通过最大限度地减少工作流实例的数量来提高工作流引擎的性能。 除了`COMPLETED`和`RUNNING`状态值之外，工作流还支持三个新状态值： `ABORTED`、`SUSPENDED`和`FAILED`。

## AEM 6.5，Service Pack 16—2023年2月23日

为Dynamic Media视频交付中的自适应比特率流启动的新协议DASH(Dynamic Adaptive Streaming over HTTP)（启用了CMAF [通用媒体应用程序格式]）。

* 自适应流(DASH/HLS)确保获得更好的视频最终用户观看体验。
* DASH是自适应视频流的国际标准协议，在业界得到广泛应用。
* 目前已在亚太和北美推出；即将推出欧洲 — 中东 — 非洲版本。

### [!DNL Forms]

* [Headless自适应Forms](https://experienceleague.adobe.com/en/docs/experience-manager-headless-adaptive-forms/using/overview)使您的开发人员能够创建、发布和管理可通过API（而不是通过传统的图形用户界面）访问和交互的交互式表单。

* [自适应Forms核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction#features)是基于Adobe Experience Manager WCM核心组件构建的一组24个开源、符合BEM的组件。 这些组件是开源的，使开发人员能够轻松地自定义和扩展这些组件，以满足其组织的特定需求。 具备自定义[WCM核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/get-started/authoring)的现有技能的任何人都可以轻松自定义这些组件并设置其样式。

* OSGi上的Reader扩展服务现在提供单独的选项，以启用PDF上的导入和导出使用权限，从而在Adobe Acrobat Reader中导入或导出数据。

## AEM 6.5，Service Pack 15—2022年11月24日

### [!DNL Forms]

* AEM Forms Designer现在提供[西班牙区域设置](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)版本。
* 您现在可以使用[OAuth2通过Microsoft® Office 365邮件服务器协议（SMTP和IMAP）](/help/forms/using/oauth2-support-for-mail-service.md)进行身份验证。
* 您可以将服务器[属性上的](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#enabling-server-side-validation-br)Revalidate设置为true以标识要从服务器端记录文档中排除的隐藏字段。
* AEM Forms Designer需要32位版本的Visual C++ 2019可再分发(x86)。

## AEM 6.5，Service Pack 14—2022年8月25日

仅错误修复。

## AEM 6.5，Service Pack 13—2022年5月26日

* 以自适应表单使用不可见CAPTCHA：现在，只有在可疑活动的情况下，您才可以使用不可见CAPTCHA显示CAPTCHA挑战。 如果未发现可疑活动，则不显示CAPTCHA质询。 它有助于评估人工表单的完成情况，而无需使用复选框要求，减少自定义工作，并改善最终用户体验。

* 添加了对在表单数据模型后处理中获取REST端点的响应标头的支持。

* 现在，在生成自适应表单翻译文件时，生成的XLIFF文件中的相同文本序列与相应自适应表单中的组件序列相同。

* 本地化自适应表单并对基础语言的文本进行微小更改时，所有其他语言的完整翻译都将丢失。 已在[!DNL Experience Manager] 6.5.13.0中修复该问题。

* Forms的辅助功能改进：

   * 添加了对屏幕阅读器的支持，用于将表的标题和正文识别为连续和连接的实体。 它有助于屏幕阅读器正确导航表格。 (NPR-37139)
   * 增加了对屏幕阅读器的支持，以便在对话框打开之前停止在HTML工作区中导航。

## AEM 6.5，Service Pack 12—2022年2月24日

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行更新、删除、重命名和移动操作。更新会在 Sites 部署中自动提供，但会有一些延迟。
* 现在，默认情况下可以将Live Copy源推送转出到多个Live Copy，而无需使用Blueprint配置。
* 正在进行的异步操作的状态现在显示在用户界面中，以帮助防止用户意外触发同一路径上的多个异步操作。
* 为Analytics 2.0 API提供对基于IMS的身份验证的支持。
* api支持JSON选件类型体验片段。
* 现在为IMS中的删除选件（体验片段API）提供了选件请求。
* 内置存储库(Apache Jackrabbit Oak)仍为1.22.9。
