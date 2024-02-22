---
title: Adobe Experience Manager 6.5版本中的关键功能和增强功能的汇总。
description: Adobe Experience Manager 6.5中比前八个Service Pack版本所具有的主要功能和增强功能的汇总列表。
content-type: reference
docset: aem65
feature: Release Information
role: User, Admin
source-git-commit: 4fab3f80e01c2b7c3e4ebdc4bffdedb6f5f39d11
workflow-type: tm+mt
source-wordcount: '2334'
ht-degree: 28%

---


# 主要功能和增强功能汇总

Adobe Experience Manager 6.5中针对前八个Service Pack版本的主要功能和增强功能的汇总列表。

另请参阅 [Adobe Experience Manager 6.5最新Service Pack发行说明](/help/release-notes/release-notes.md).

## AEM 6.5，Service Pack 18—2023年12月7日

* 允许站点页面编辑器/图像组件用户从远程AssetsCloud Service引用资源。 (SITES-13448和SITES-13433)
* AEM现在支持服务器端排序，从而加快列表视图中的项目导航速度。 项目节点在显示在界面中之前根据用户选择的列排序。

### [!DNL Forms]

* **新增自适应表单核心组件**：添加了垂直选项卡、条款和条件以及复选框以增强表单的可伸缩性。
   * **[复选框组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html)**：基于核心组件的自适应表单现在包含复选框组件。通过它，用户可二选一，即选择或取消选择特定选项。它一般显示为一个小框，单击或点按它即可在选中和取消选中两种状态之间切换。复选框是一个常见的表单元素，用于提供是/否或 true/false 选择。

   * **[条款和条件组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html)**：基于核心组件的自适应表单现在包含条款和条件组件。它允许Forms作者在表单中引入特定部分，向用户显示与服务、产品或平台的使用相关的条款、条件或法律协议。 此组件旨在通知用户其提交表单即表示同意的规则、法规和义务。

     ![垂直选项卡、条款和条件以及复选框组件](/help/forms/using/assets/forms-components.png)

   * **[垂直选项卡组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html)**：基于核心组件的自适应表单现在可将表单内容整理到选项卡垂直列表中，从而提供结构化的、可导航的布局。在表单中使用垂直选项卡可通过简化导航并改进表单内容的组织而增强整体用户体验，特别是在表单包含多个部分或复杂信息的情况下。

* **[AEM Forms Designer 64位版本](/help/forms/using/installing-configuring-designer.md)**：AEM Forms Designer的64位版本提供了增强的性能、可扩展性和内存管理，可增强您的表单创建体验。 利用 64 位架构，您可以轻松处理更大、更复杂的项目，确保无缝的设计工作流程和优化的效率。利用此最新版本，提升您的表单设计能力并迎接 AEM Forms Designer 的未来。

* **[将自适应Forms连接到Microsoft® SharePoint列表](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)**：AEM Forms提供了一个OOTB集成，可用于将表单数据直接提交到SharePoint List，让您能够使用SharePoint的“列表”功能。 您可以将Microsoft® SharePoint列表配置为表单数据模型的数据源，并使用使用表单数据模型提交操作将自适应表单与SharePoint列表连接起来。

* **[支持为自适应表单片段配置记录文档属性](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)**：您现在可以在自适应表单编辑器中轻松自定义自适应表单片段及其字段。

* **64位XMLFM**： XMLFM的64位迭代引入了更高的性能、可扩展性和更精细的内存管理。 它是第一个部署在服务器端的64位本机服务。 XMLFM 64位利用其固有的功能访问比32位对等项更大的内存资源，从而能够无缝处理更大的渲染工作负载。 这一里程碑不仅实现了性能的飞跃，而且还对AEM Forms服务器中的本机服务框架引入了关键增强功能。 此更新使AEM Forms Server能够无缝支持任何64位本机服务。

## AEM 6.5，Service Pack 18—2023年8月24日

* Dynamic Media的Assets - [Dynamic Media中支持视频的多字幕和多音频轨道](/help/assets/video.md#about-msma) — 您现在可以轻松地将多个字幕和多个音轨添加到主视频中。 此功能意味着全球观众都能看懂您的视频。只需自定义一个主视频，即可发布到多种语言的全球观众，并遵循不同地区的辅助功能准则。此外，作者从用户界面中的一个选项卡即可管理字幕和音轨。
* 资源 — 现在，您可以在搜索结果中导航到包含资源的文件夹位置，以便执行各种资源管理任务。
* 内容片段中的Sites Polaris选取器改进了性能。
* 允许站点页面编辑器/图像组件用户从远程AssetsCloud Service引用资源。
* 要在“列表”视图中快速查找项目（系统中可能有许多项目），Adobe现在支持服务器端排序。 项目节点在用户界面中呈现之前，会根据用户选择的列在后端进行排序。
* AEM 6.5.18.0支持MongoDB 5.0到6.0。

### [!DNL Forms]

* **[在规则编辑器中使用自定义错误处理程序增强了错误处理](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/standard-validation-error-messages-adaptive-forms.html)**  — 现在，您可以调用自定义函数（使用客户端库）来响应外部服务返回的错误。 而且，您可以为最终用户提供量身定制的响应。 或者，您可以针对服务返回的错误采取特定操作。例如，您可以在后端中调用自定义工作流以获取特定错误代码，或通知客户服务已中断

* **[增强的Adobe Sign工作流步骤](https://experienceleague.adobe.com/docs/experience-manager-65/forms/workflows/aem-forms-workflow-step-reference.html#sign-document-step)** - AEM Workflows中的Adobe Sign工作流步骤包含以下增强功能。

   * **通过基于Government ID的身份验证增强Adobe Sign的安全性** - Adobe Acrobat Sign基于Government ID的身份验证提供额外的验证层。 它允许用户使用政府颁发的ID（驾照、身份证、护照）进行身份认证。 通过利用可信身份证明文件，此增强将签名过程的可信度提高一级，使其成为需要更高的安全性、合规性和用户验证的场景的理想之选。

   * **Adobe Sign文档审核追踪的透明度增强**  — 使用审核记录功能可详细了解Adobe Sign文档的生命周期。 利用审核记录功能，您现在可保留与文档相关的所有操作和交互的全面记录。其中包括查看者、编辑者或签署文档者以及每个事件的时间戳等详细信息。此增强对于保持合规性、解决争议和确保数字协议的完整性至关重要。


   * **扩展了协议收件人的角色，而不只是签名者** - Adobe Acrobat Sign允许您扩展协议接受者的角色，而不只是签名者，以便更好地匹配他们的工作流要求。 启用后，协议中的每个收件人可以单独配置其角色，签名者是默认角色。


* **[AEM Forms on JEE完整安装程序](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms.html)** - Service Pack提供了AEM Forms on JEE的完整安装程序，以支持多种新软件组合，包括：
   * Microsoft® Windows Server 2022
   * Microsoft® Active Directory 2022
   * 在Windows Server 2022上OracleWebLogic 14C
   * Red Hat® JBoss® 7.4.10
   * MongoDB 6.0 <!-- it was previously MongoDB 4.4 -->
   * MySQL JDBC连接器8

如果您在JEE环境中安装或计划使用适用于AEM 6.5 Forms的最新软件，Adobe建议使用AEM 6.5.18.0 Forms on JEE完整安装程序。 要探索新添加和已弃用的软件的完整列表，请参阅JEE上的AEM Forms或OSGi上的AEM Forms的文档。

## AEM 6.5，Service Pack 17—2023年5月25日

* **搜索体验增强** - 您现在可以对搜索结果中显示的资源快速执行以下操作：
   * 创建工作流
   * 创建一个版本
   * 关联或取消关联资源

  您无需导航到资源的位置并查看其属性即可执行这些操作。
* **Dynamic Media _快照_**— 尝试使用测试图像或Dynamic Media URL，以查看各种图像修饰符的输出，并对文件大小（使用WebP和AVIF交付）、网络带宽和设备像素比进行智能成像优化。 请参阅 [Dynamic Media 快照。](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html)
* **使用Dynamic Media进行DASH流处理**  — 为Dynamic Media视频交付中的自适应流推出了新协议（DASH — 通过HTTP的动态自适应流）支持（启用了CMAF）。 现在所有地区均可用， [通过支持票证启用](/help/assets/video.md#enable-dash-on-your-account-enable-dash).
* **Experience Manager Sites和内容片段与资产新一代Dynamic Media的集成**  — 现在，Experience Manager Assetsas a Cloud Service的新一代Dynamic Media的用户可以使用这些云托管资源通过Experience Manager Sites 6.5的内部部署或Managed Services实例进行创作和交付。

### [!DNL Forms]

* **[AEM 页面编辑器中的自适应表单](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)**：您现在可以使用 AEM 页面编辑器快速创建多个表单并将其添加到您的 Sites 页面。通过使用该功能，内容作者可以使用自适应表单组件（包括动态行为、验证、数据集成、生成记录文档和业务流程自动化）的强大功能，在 Sites 页面内创建无缝的数据捕获体验。您可以：
   * 通过将表单组件拖放到 AEM Sites 编辑器或体验片段中的自适应表单容器组件来创建自适应表单。
   * 使用 AEM Sites 编辑器中的自适应表单向导创建独立于任何 Sites 页面的表单，让您可以自由地在多个页面中重复使用此类表单。
   * 将多个表单添加到 Sites 页面，简化用户体验并提供更大的灵活性。
* **[Experience Manager Forms中对reCAPTCHA Enterprise的支持](/help/forms/using/captcha-adaptive-forms.md)**：在Experience Manager Forms中增加了对reCAPTCHA Enterprise的支持，针对欺诈性活动和垃圾邮件提供了增强的保护，此外还有现有的Google reCAPTCHA v2支持。
* **[使用Experience Manager Forms为政府支持Adobe Acrobat Sign](/help/forms/using/adobe-sign-integration-adaptive-forms.md)**：AEM Forms现在与面向政府的Adobe Acrobat Sign集成（符合FedRAMP要求）。 此集成通过为政府关联帐户（政府部门和机构）提交自适应表单，为电子签名提供了高级的合规性和安全性。 与 Adobe Acrobat Sign 政府版的集成使 Adobe 的合作伙伴和政府客户能够在一些最关键和敏感的业务领域使用自适应表单中的电子签名功能。这层额外的安全保障机制确保所有电子签名完全符合 FedRAMP Moderate 合规性，使 Adobe 的政府客户能够安心使用。
* **启用Salesforce与Experience Manager Forms的集成以便进行数据交换**：使用OAuth 2.0客户端凭据流配置Experience Manager Forms与Salesforce应用程序之间的集成。 此功能支持对应用程序进行安全而直接的身份验证和授权，并允许无缝通信，而无需用户参与。
* **工作流引擎的优化和增强功能**：通过最大限度地减少工作流实例的数量来提高工作流引擎的性能。 此外 `COMPLETED` 和 `RUNNING` 对于状态值，工作流还支持三个新的状态值： `ABORTED`， `SUSPENDED`、和 `FAILED`.

## AEM 6.5，Service Pack 16—2023年2月23日

新协议DASH(Dynamic Adaptive Streaming over HTTP)支持在Dynamic Media视频交付（使用CMAF）中为自适应比特率流启动 [通用媒体应用程序格式] 已启用)。

* 自适应流(DASH/HLS)确保获得更好的视频最终用户观看体验。
* DASH是自适应视频流的国际标准协议，在业界得到广泛应用。
* 现在在亚太和北美提供（通过支持票证启用）；欧洲 — 中东 — 非洲即将推出。

请参阅 [在您的帐户上启用DASH](/help/assets/video.md#enable-dash).

### [!DNL Forms]

* [Headless自适应Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) 使您的开发人员能够创建、发布和管理可通过API（而不是通过传统的图形用户界面）访问和交互的交互式表单。

* [自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features) 一组基于Adobe Experience Manager WCM核心组件构建的24个开源、BEM兼容组件。 这些组件是开源的，使开发人员能够轻松地自定义和扩展这些组件，以满足其组织的特定需求。 具备自定义现有技能的人员 [WCM核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/authoring.html) 可以轻松自定义这些组件并设置其样式。

* OSGi上的Reader扩展服务现在提供了单独的选项，用于启用PDF的导入和导出使用权限，以便在Adobe Acrobat Reader中导入或导出数据。

## AEM 6.5，Service Pack 15—2022年11月24日

### [!DNL Forms]

* AEM Forms Designer现在在以下位置提供： [西班牙语区域设置](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).
* 您现在可以使用 [用于通过Microsoft® Office 365邮件服务器协议（SMTP和IMAP）进行身份验证的OAuth2](/help/forms/using/oauth2-support-for-mail-service.md).
* 您可以设置 [在服务器上重新验证](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br) 属性设置为true可标识要从服务器端记录文档排除的隐藏字段。
* AEM Forms Designer需要32位版本的Visual C++ 2019可再分发(x86)。

## AEM 6.5，Service Pack 14—2022年8月25日

仅错误修复。

## AEM 6.5，Service Pack 13—2022年5月26日

* 以自适应表单使用不可见CAPTCHA：现在，只有在可疑活动的情况下，您才可以使用不可见CAPTCHA显示CAPTCHA挑战。 如果未发现可疑活动，则不显示CAPTCHA质询。 它有助于评估人工表单的完成情况，而无需使用复选框要求，减少自定义工作，并改善最终用户体验。

* 添加了对在表单数据模型后处理中获取REST端点的响应标头的支持。

* 现在，在生成自适应表单翻译文件时，生成的XLIFF文件的文本序列与相应的自适应表单中的组件序列相同。

* 本地化自适应表单并对基础语言的文本进行微小更改时，所有其他语言的完整翻译都将丢失。 已在中修复此问题 [!DNL Experience Manager] 6.5.13.0。

* Forms的辅助功能改进：

   * 添加了对屏幕阅读器的支持，用于将表的标题和正文识别为连续和连接的实体。 它有助于屏幕阅读器正确导航表格。 (NPR-37139)
   * 添加了对屏幕阅读器的支持，允许在对话框打开之前停止在HTML工作区中导航。

## AEM 6.5，Service Pack 12—2022年2月24日

* 在配置远程 DAM 和 Sites 部署之间的连接后，远程 DAM 上的资源即可用于 Sites 部署。您现在可以对远程 DAM 资源或文件夹执行更新、删除、重命名和移动操作。更新会在 Sites 部署中自动提供，但会有一些延迟。
* 现在，默认情况下可以将Live Copy源推送转出到多个Live Copy，而无需使用Blueprint配置。
* 正在进行的异步操作的状态现在显示在用户界面中，以帮助防止用户意外触发同一路径上的多个异步操作。
* 为Analytics 2.0 API提供对基于IMS的身份验证的支持。
* API支持JSON选件类型体验片段。
* 现在为IMS中的删除选件（体验片段API）提供了选件请求。
* 内置存储库(Apache Jackrabbit Oak)仍为1.22.9。
