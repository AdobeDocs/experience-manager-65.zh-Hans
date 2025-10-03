---
title: Adobe Experience Manager 6.5 版本中的主要功能与增强功能汇总
description: 该汇总内容列出了 Adobe Experience Manager 6.5 在前八个服务包中新增的主要功能与增强功能。
content-type: reference
docset: aem65
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 01fe5b53-2244-445f-a4d0-bd58ea38b611
solution: Experience Manager
source-git-commit: eef3ad559612c338de0c4232aadc4133c910aaf8
workflow-type: ht
source-wordcount: '3109'
ht-degree: 100%

---

# 主要功能与增强功能汇总

该汇总内容列出了 Adobe Experience Manager 6.5 在前八个服务包中新增的主要功能与增强功能。

另请参阅 [Adobe Experience Manager 6.5 最新服务包发行说明](/help/release-notes/release-notes.md)。


## AEM 6.5 服务包 23 - 2025 年 5 月 22 日

### Forms {#forms-sp23}

* [静态 PDF 中支持混合文本样式的可访问超链接](https://helpx.adobe.com/cn/content/dam/help/en/experience-manager/6-5/forms/pdf/using-designer.pdf)：包含混合文本样式的静态 PDF 超链接现已标记为单一可访问元素。此增强简化了标记树结构，改善了屏幕阅读器导航，并提升了无障碍合规性。

* [更新了支持平台矩阵](/help/forms/using/aem-forms-jee-supported-platforms.md)

  最新版本更新了支持的平台矩阵，确保与新技术的兼容性。

   * IBM® Content Manager 客户端 8.7

   * MongoDB 企业版 7.0

   * MySQL 8.4

   * Microsoft® SQL 服务器 2022

   * Microsoft® SQL 服务器 JDBC 驱动程序 12.8

   * Red Hat® Enterprise Linux® 9（内核 4.x，64 位）

* [强化了文件附件组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment)：作为一项安全措施，该组件现已阻止提交扩展名经过修改、试图绕过允许文件类型检查的文件。此类文件在提交过程中会被拦截，以确保仅接受有效文件类型。

## AEM 6.5 服务包 22 - 2024 年 11 月 21 日

### Sites {#sites}

[通用编辑器](/help/sites-developing/universal-editor/introduction.md) 现已通过功能包在 AEM 6.5 上提供，支持 Headless 用例。

### [!DNL Assets]

IPTC 选项卡现已支持[!UICONTROL 替代文本]和[!UICONTROL 扩展描述]文本字段。（Assets-34918）

### Forms {#forms-sp22}

#### AEM Forms 中的新 GA 功能 {#ga-aem-forms-sp22}

* 在[交互式通信批处理 API](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/interactive-communications/create-interactive-communication#output-format-print-channel) 中新增了对字体嵌入的支持——交互式通信现已支持在通过批处理 API 生成的 PDF 中嵌入 Adobe 明体和 Adobe Myungjo 字体。这一增强确保了生成文档中的文本渲染更加准确，即使在使用字体子集时也能保持效果，从而为 PDF 输出中的多语言内容提供了更完善的支持。

* [PDF 辅助功能目录 API](/help/forms/using/aem-document-services-programmatically.md#auto-tag-pdf-documents-auto-tag-api)：现已在 OSGi 上的 AEM Forms 中支持全新的 TOC 标记 API，以提升 PDF 对无障碍标准的符合性。此功能可让使用辅助技术的用户更方便地访问 PDF。

* [片段 XDP 解析](/help/forms/using/assembler-service.md#resolve-references-on-crx-repository-resolve-references-on-crx-repository)：现已在 OSGi 上的 AEM Forms 中支持解析在主 XDP 中引用的并存储于 AEM CRX 存储库中的片段 XDP。

* [PDF/A 合规性增强](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdfa-documents-converting-documents-to-pdf-a-documents)：用户现在可以将 PDF 转化为 PDF/A 格式（1a、2a、3a）以满足存档需求，同时还可确保无障碍访问并验证其对这些标准的符合性。

* **支持静态 PDF 文档自动调整字体大小**：AEM Forms Designer、OutputService 和 FormsService 现已支持静态 PDF 自动调整字体大小。当用户将文本、数字、密码或日期时间字段的字体大小设置为 0 时，字体大小会在这些字段中自动调整，而不会改变字段的整体尺寸。要使用此功能，用户需在自定义 XCI 中传递以下标记：`<behaviorOverride>patch-LC-3921991:1</behaviorOverride>`。

#### AEM Forms 中的新 Beta 功能 {#beta-aem-forms-sp22}

Beta 功能为您提供获取前沿创新的独家体验，并参与塑造其未来发展的宝贵机会。有兴趣在您的环境中启用 Beta 功能吗？请使用您的官方邮箱发送电子邮件至 aem-forms-ea@adobe.com，并在邮件中列出您感兴趣的功能列表。

* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md) 和 [Cloudflare Turnstile CAPTCHA 服务](/help/forms/using/integrate-adaptive-forms-turnstile.md)：AEM Forms 支持以下验证码服务：
   * hCaptcha 通过复选框小组件对用户进行验证，从而保护表单免受机器人、垃圾信息和自动滥用的侵扰。它确保只有真实用户才能继续操作，从而提升在线交易的安全性。
   * Cloudflare Turnstile 提供了一种安全机制，旨在保护表单免受自动化机器人、恶意攻击、垃圾信息和不必要的自动化流量的侵扰。在提交表单之前，它会呈现一个复选框以验证用户身份，确认其为真人后才允许提交表单。

* 自适应表单版本控制：
   * [创建自适应表单的多个版本](/help/forms/using/add-versioning-reviews-comments.md)：现在用户可以轻松管理现有表单的不同变体。该流程简化了版本控制，并便于对表单进行比较和优化，且整个操作均在一个统一而高效的工作流中完成。
   * [比较自适应表单](/help/forms/using/compare-forms-core-components.md)：现在用户可以轻松对比两个表单，以识别其中的差异。它使团队成员能够比较修订内容，并有效地讨论相关变化，从而促进顺利协作。

## AEM 6.5 服务包 21 - 2024 年 6 月 6 日

### [!DNL Assets]

#### 增强功能

IPTC 选项卡现已支持[!UICONTROL 替代文本]和[!UICONTROL 扩展描述]文本字段。（Assets-34918）

#### 辅助功能

* 如果资产的处理状态为“失败”或“元数据失败”，则字幕和音轨界面现在可以正常工作。（Assets-37281）
* 当您保存资产元数据并尝试编辑时，会显示语言名称。（Assets-37281）

### [!DNL Forms]

* **支持 Oauth 凭据**：提供一种全新且更易用的凭据，用于服务器间身份验证，以取代现有的服务帐户（JWT）凭据。（NPR-41994）
* [AEM Forms 中的规则编辑器增强功能](/help/forms/using/rule-editor-core-components.md)：
   * 支持使用 `When-then-else` 功能实施嵌套条件。
   * 验证或重置面板和表单（包括字段）。
   * 在自定义函数中支持现代 JavaScript 特性，如 let 和箭头函数（支持 ES10）。
* [适用于 PDF 辅助功能的 AutoTag API](/help/forms/using/aem-document-services-programmatically.md#doc-utility-services-doc-utility-services)：OSGi 上的 AEM Forms 现已支持新的 AutoTag API，可通过添加段落和列表等标记来增强 PDF 的无障碍标准。此功能可让使用辅助技术的用户更方便地访问 PDF。
* **16 位 PNG 支持**：PDF Generator 的 ImageToPdf 服务现已支持将具有 16 位色深的 PNG 转化为 PDF。
* **将工件应用于 XDP 中的单个文本块**：Forms Designer 现在允许用户在 XDP 文件中的单个文本块上配置设置。通过此功能，您可以控制在生成的 PDF 中哪些元素会被视为工件。这些元素（如页眉和页脚）可供辅助技术访问，从而提升无障碍性。主要功能包括：可将文本块标记为工件，并将这些设置嵌入到 XDP 元数据中。Forms Output 服务会在生成 PDF 时应用这些设置，以确保正确的 PDF/UA 标记。
* **AEM Forms Designer 已通过 `GB18030:2022` 标准认证**：凭借 `GB18030:2022` 认证，Forms Designer 现已支持中文 Unicode 字符集，允许您在所有可编辑字段和对话框中输入中文字符。
* [在 JEE 服务器中支持 WebToPDF 路径](/help/forms/using/admin-help/configure-service-settings.md#generate-pdf-service-settings-generate-pdf-service-settings)：通过 PDF Generator 服务，现在在 JEE 上也支持使用 WebToPDF 路径将 HTML 文件转化为 PDF 文档。此功能是在现有的 Webkit 和 WebCapture（仅限 Windows）路径基础上的新增支持。此前 WebToPDF 路由已在 OSGi 上提供，并扩展到 JEE。现在，在 JEE 和 OSGi 平台上，PDF Generator 服务均支持以下跨不同操作系统的路由：
   * **Windows**：Webkit、WebCapture、WebToPDF
   * **Linux®**：Webkit、WebToPDF


## AEM 6.5 服务包 20 – 2024 年 2 月 22 日

### [!DNL Assets]

* Dynamic Media 现已支持 Apple iOS/iPadOS 的无损 HEIC 图像格式。请参阅 Dynamic Media 图像服务与渲染 API 中的 [fmt](https://experienceleague.adobe.com/zh-hans/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-is-http-fmt)。
* 多网站管理器（MSM）现已支持体验片段的结构，其中包括文件夹和子文件夹，可高效地将体验片段批量转出至 Live Copy。

### [!DNL Forms]

* **JEE 上的 AEM Forms 的事务报告**：JEE 上的 AEM Forms 引入了事务报告功能。该功能可对文档事务进行全面记录，例如转化、渲染和提交操作。此增强功能可提升工作效率，并有助于改进记录管理。该功能默认处于禁用状态。您可以在管理员 UI 中启用。
* **通过 ECDSA 支持增强安全性**：AEM Forms 现已在 JEE 和 OSGi 技术栈中全面支持椭圆曲线数字签名算法（ECDSA）。用户现在可以对 PDF 文档进行签名、认证和验证，从而显著提升安全性。支持的 EC 曲线算法包括：
   * ECDSA 椭圆曲线 P256 搭配 SHA256 摘要算法
   * ECDSA 椭圆曲线 P384 搭配 SHA384 摘要算法
   * ECDSA 椭圆曲线 P512 搭配 SHA512 摘要算法
* **Forms Designer 与 Windows 11 的无缝兼容性**：AEM Forms Designer 现已支持 Windows 11，确保顺利安装以及顺畅运行。用户可放心升级至 Windows 11，而无需重新安装 Forms Designer，也无需担心兼容性问题，从而保证工作流不受中断。
* **通过在 AEM Forms Designer 中使用自定义“字幕”角色来提升无障碍性**：AEM Forms Designer 现已支持一个名为“字幕”的自定义无障碍角色，使用户能够在 XDP 中创建个性化的字幕元素。该功能通过允许用户将自定义字幕集成到文档设计中，进一步提升了无障碍性，从而改善包容性和用户体验。

## AEM 6.5 服务包 19 – 2023 年 12 月 7 日

* 在 Sites 页面编辑器/图像组件中，用户现已可以引用来自远程 Assets 云服务的资产。（SITES-13448、SITES-13433）
* AEM 现已支持服务器端排序，在列表视图中可更快速地导航项目。项目节点会根据用户选择的列在显示到界面前完成排序。

### [!DNL Forms]

* **新的自适应表单核心组件**：新增了纵向选项卡、条款与条件以及复选框，以增强表单的可扩展性。
   * **[复选框组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox)**：基于核心组件的自适应表单现在包含复选框组件。通过它，用户可二选一，即选择或取消选择特定选项。它一般显示为一个小框，单击或点按它即可在选中和取消选中两种状态之间切换。复选框是一个常见的表单元素，用于提供是/否或真/假选择。

   * **[条款与条件组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions)**：基于核心组件的自适应表单现已包含条款与条件组件。表单作者可以在表单中添加此部分，用于向用户展示服务、产品或平台的条款、条件或法律协议。此组件旨在通知用户其提交表单即表示同意的规则、法规和义务。

     ![纵向选项卡、条款与条件及复选框组件](/help/forms/using/assets/forms-components.png)

   * **[纵向选项卡组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs)**：基于核心组件的自适应表单现在可将表单内容整理到纵向选项卡列表中，从而提供结构化的、可导航的布局。表单中的纵向选项卡通过简化导航和组织内容来提升用户体验。当表单包含多个部分或复杂信息时，该功能尤其有帮助。

* **[AEM Forms Designer 64 位版本](/help/forms/using/installing-configuring-designer.md)**：AEM Forms Designer 的 64 位版本带来更佳的性能、可扩展性和内存管理，以全面提升表单创建体验。利用 64 位架构，您可以轻松处理更大、更复杂的项目，确保无缝的设计工作流和优化的效率。利用此最新版本，提升您的表单设计能力并迎接 AEM Forms Designer 的未来。

* **[将自适应表单连接至 Microsoft® SharePoint 列表](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**：AEM Forms 提供开箱即用的集成功能，可将表单数据直接提交至 SharePoint 列表，从而利用 SharePoint 的列表功能。您可以将 Microsoft® SharePoint 列表配置为表单数据模型的数据源，并使用“通过表单数据模型提交”操作将自适应表单与 SharePoint 列表相连接。

* **[支持为自适应表单片段配置记录文档属性](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：现在，您可以在自适应表单编辑器中轻松自定义自适应表单片段及其字段。

* **64 位 XMLFM**：64 位版本的 XMLFM 提供更高的性能、可扩展性和优化的内存管理。这是首个在服务器端部署的原生 64 位服务。借助其相比于 32 位版本更强大的内存资源访问能力，64 位 XMLFM 能够无缝处理更大规模的渲染工作负载。这一里程碑不仅代表着性能的飞跃，同时还为 AEM Forms 服务器内的原生服务框架引入了关键增强功能。通过此次更新，AEM Forms 服务器已能够无缝支持任意 64 位原生服务。

## AEM 6.5 服务包 18 – 2023 年 8 月 24 日

* Assets，Dynamic Media - [为 Dynamic Media 视频提供多字幕和多音轨支持](/help/assets/video.md#about-msma)——现在您可以轻松为主视频添加多个字幕和多条音轨。此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的无障碍功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。
* Assets - 在搜索结果中，您现在可以直接导航到包含该资产的文件夹位置，以便执行各种资产管理任务。
* 内容片段中的 Sites Polaris 选择器性能已得到提升。
* 在 Sites 页面编辑器/图像组件中，用户现已可以引用来自远程 Assets 云服务的资产。
* 为了在系统中包含大量项目时能够快速在列表视图中找到项目，Adobe 现已支持服务器端排序。项目节点会在后台根据用户选择的列进行排序，然后才会在用户界面中呈现。
* AEM 6.5.18.0 支持 MongoDB 5.0 到 6.0。

### [!DNL Forms]

* **[通过规则编辑器中的自定义错误处理程序增强错误处理能力](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms)**——您现在可以在外部服务返回错误时调用自定义函数（使用客户端库）。并且，您可以向终端用户提供定制化响应。或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后台针对特定错误代码调用自定义工作流，或告知用户该服务当前不可用。

* **[增增强的 Adobe Sign 工作流步骤](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow-step-reference#sign-document-step)**——AEM 工作流中的 Adobe Sign 工作流步骤现已提供以下增强功能。

   * **基于政府身份证件的 Adobe Sign 身份验证增强安全性**——Adobe Acrobat Sign 的基于政府身份证件验证功能提供了额外的安全保障。用户可通过政府签发的身份证件（如驾驶证、国家身份证、护照）来验证其身份。通过利用可信身份证明文件，此增强功能将签名过程的可信度提高一级，使其成为需要更高的安全性、合规性和用户验证的场景的理想之选。

   * **通过审核记录提升 Adobe Sign 文档透明度**——借助审核记录功能，您可以深入了解 Adobe Sign 文档的完整生命周期。通过审核记录，您可以保留与文档相关的所有操作与交互的完整记录。这些操作和交互包括谁查看、编辑或签署了文档，以及每个事件的时间戳。此增强功能对于保持合规性、解决争议和确保数字协议的完整性至关重要。


   * **扩展协议接收人的角色设置，不再局限于签署人**——Adobe Acrobat Sign 现已支持将协议接收人的角色扩展到签署人之外，以更好地满足不同的工作流需求。启用此选项后，协议中的每个接收者均可单独配置其角色，其中签名者为默认角色。


* **[JEE 上的 AEM Forms 完整安装程序](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)**——此服务包提供 JEE 上的 AEM Forms 的完整安装程序，并支持多种全新的软件组合，其中包括：
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * Oracle WebLogic 14C（适用于 Windows Server 2022）
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC Connector 8

如果您正在安装或计划在 JEE 环境中使用 AEM 6.5 Forms 的最新软件，Adobe 建议使用 AEM 6.5.18.0 Forms on JEE 完整安装程序。有关已新增和已弃用软件的完整列表，请参阅 JEE 上的 AEM Forms 或 OSGi 上的 AEM Forms 的相关文档。

## AEM 6.5 服务包 17 – 2025 年 5 月 22 日

* **搜索体验增强** - 您现在可以对搜索结果中显示的资产快速执行以下操作：
   * 创建工作流
   * 创建一个版本
   * 关联或取消关联资产

  您无需导航到资源的位置并查看其属性即可执行这些操作。

* **Dynamic Media _快照_**功能可让您通过测试图像或 Dynamic Media URL 预览图像修饰符和智能成像优化效果——例如 WebP 或 AVIF 输出、带宽感知压缩以及设备像素比缩放。您可以立即比较每个设置对图像质量和文件大小的影响。
请参阅 [Dynamic Media 快照](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot)。
* **使用 Dynamic Media 的 DASH 流媒体**——为 Dynamic Media 视频传递中的自适应流媒体新增了协议（DASH——基于 HTTP 的动态自适应流媒体），并启用了 CMAF 支持。现已在所有地区开放使用。
* **Experience Manager Sites 和内容片段与 Assets 新一代 Dynamic Media 集成**——用户现在可以在 Experience Manager Sites 6.5 中使用其云托管资产。这些资产可以在本地部署实例或 Managed Services 实例中进行创作和传递。

### [!DNL Forms]

* **[在 AEM 页面编辑器中使用自适应表单](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**——您现在可以使用 AEM 页面编辑器快速创建多个表单，并将其添加到 Sites 页面中。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：
   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件，即可创建自适应表单。
   * 您还可以在 AEM Sites 编辑器中使用自适应表单向导，以独立于任何 Sites 页面的方式创建表单，从而灵活地在多个页面间重复使用这些表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。
* **[在 Experience Manager Forms 中支持 reCAPTCHA Enterprise](/help/forms/using/captcha-adaptive-forms.md)**——Experience Manager Forms 现已支持 reCAPTCHA Enterprise。除了现有的 Google reCAPTCHA v2 支持外，此功能还提供了针对欺诈活动和垃圾邮件的增强保护。
* **[在 Experience Manager Forms 中新增对 Adobe Acrobat Sign 政府版的支持](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**——AEM Forms 现已支持与 Adobe Acrobat Sign 政府版（符合 FedRAMP 标准）集成。此集成在提交自适应表单时，为与政府相关的帐户（政府部门和机构）提供了更高级别的合规性和安全性，以支持电子签名。通过与 Adobe Acrobat Sign 政府版的集成，Adobe 的合作伙伴和政府客户能够在自适应表单中使用电子签名，以满足最关键和最敏感的业务需求。这层额外的安全保障机制确保所有电子签名完全符合 FedRAMP Moderate 合规性，使 Adobe 的政府客户能够安心使用。
* **启用 Experience Manager Forms 与 Salesforce 的数据交换集成**——使用 OAuth 2.0 客户端凭据流程配置 Experience Manager Forms 与 Salesforce 应用程序之间的集成。此功能可实现应用程序的安全、直接身份验证和授权，并允许在无需用户参与的情况下实现无缝通信。
* **工作流引擎优化与功能增强**：通过减少工作流实例数量提升工作流引擎的性能。除 `COMPLETED` 和 `RUNNING` 状态值之外，工作流还支持三种新增的状态值：`ABORTED`、`SUSPENDED` 和 `FAILED`。

## AEM 6.5 服务包 16 – 2023 年 2 月 23 日

在 Dynamic Media 视频传递中推出了新的 DASH 协议（DASH，基于 HTTP 的动态自适应流播放），用于自适应码率流播放传输（启用了 CMAF [通用媒体应用格式]）。

* 自适应流播放（DASH/HLS）可确保终端用户获得更佳的视频观看体验。
* DASH 是自适应视频流的国际标准协议，已在业界被广泛采用。
* 目前已在亚太地区和北美地区上线；欧洲、中东和非洲地区即将推出。

### [!DNL Forms]

* [Headless 自适应表单](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-headless-adaptive-forms/using/overview)使开发人员能够创建、发布和管理交互式表单，这些表单可通过 API 进行访问和交互，而不是依赖传统的图形用户界面。

* [自适应表单核心组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/adaptive-forms/introduction#features)是一组 24 个开源、符合 BEM 标准的组件，其构建于 Adobe Experience Manager WCM 核心组件的基础之上。这些组件为开源组件，开发人员可以轻松进行自定义和扩展，以满足组织的特定需求。任何具备自定义 [WCM 核心组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/get-started/authoring)技能的人员，都能轻松对这些组件进行自定义和样式调整。

* OSGi 上的阅读器扩展服务现已提供单独选项，可在 PDF 上启用导入和导出使用权限，从而在 Adobe Acrobat Reader 中实现数据的导入或导出。
