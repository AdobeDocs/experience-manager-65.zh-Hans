---
title: AEM Forms术语表
description: AEM Forms术语表提供了Adobe Experience Manager Forms (AEM Forms)中使用的主要术语、定义和概念的完整列表，可帮助用户了解并使用自适应表单和相关功能。
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 1%

---

# AEM Forms术语表

## [自适应表单](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

动态、响应式表单，可根据用户的设备和输入调整其布局和呈现，从而增强各种平台的用户体验。 包括条件逻辑、动态数据绑定和基于规则的行为。

## [自适应表单版本控制](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

能够使用JCR节点版本控制管理存储库中表单的多个版本。 确保审核跟踪和自适应表单的轻松回滚。

## [Adobe Analytics Forms集成](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

提供关于使用Adobe Analytics进行用户交互（例如，字段流失、每分区逗留时间）的详细见解，从而支持对表单设计进行数据驱动优化。

## [AEM Forms附加组件包](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

以包形式部署到Adobe Experience Manager (AEM)中的应用程序，包含由AEM Sling框架管理的服务（API提供程序）和Servlet或JSP。

## [JEE上的AEM Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

AEM Forms的一个部署选项，它利用Java Enterprise Edition (JEE)服务器，提供企业级可扩展性、事务管理和对复杂企业工作流的支持。

## [OSGi上的AEM Forms](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

OSGi环境上的AEM Forms是标准的AEM Author或AEM Publish，并在其上部署了AEM Forms包。 您可以在单个服务器环境、场设置和群集设置中在OSGi上运行AEM Forms。 集群设置仅可用于AEM Author实例。

## [AEM Forms中的Adobe Sign](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

用于安全无缝数字签名工作流的RESTful服务。 它使用基于OAuth的身份验证与AEM Forms集成，支持自动签名收集和实时跟踪。

## [AEM Forms Document Services 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

AEM Forms的Web层提供的API，可供基于HTTP的客户端远程使用，例如表单移动SDK。AEM Forms中的功能，可用于创建、组合、分发和存档PDF文档、添加数字签名以及解码条形码Forms。

| **服务名称** | **描述** | **文档链接** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **表单服务** | 使用模板和XML渲染PDF forms，集成表单数据以供导入/导出，并支持基于片段的渲染。 | [Forms服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **输出服务** | 通过将数据与PDF、PCL或PostScript等格式的模板合并来生成文档。 | [输出服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **汇编程序服务** | 合并、重新排列、验证和扩大PDF和XDP文档。 | [汇编程序服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **ConvertPDF服务** | 将PDF文档转换为PostScript或图像格式，如PNG、JPEG或TIFF。 | [ConvertPDF服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **条码式Forms服务** | 从TIFF和PDF文件中的条形码中提取数据，以自动执行数据捕获过程。 | [条码式Forms服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **DocAssurance服务** | 对PDF进行加密、解密、数字签名和应用文档安全策略。 | [DocAssurance服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **PDF Generator服务** | 将本机文件格式(例如：Microsoft Word、Excel)转换为PDF文档。 | [PDF Generator服务文档](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [Formsas a Cloud Service通信API](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Formsas a Cloud Service提供了用于管理表单和通信工作流的高级工具，支持无缝的数字表单创建、数据捕获和个性化通信。 Cloud Communication API通过HTTP提供安全的按需文档和批量文档生成、操作、验证以及与外部系统的集成，确保简化和安全操作。

| **服务名称** | **描述** | **文档链接** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **文档生成** | 将模板(XFA或PDF)与XML数据相结合，生成PDF和打印格式（如PS、PCL、DPL、IPL和ZPL格式）的文档。 | [文档生成文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#document-generation) |
| **文档操作** | 合并、重新排列PDF文档。 | [文档操作文档](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **文档转换** | 将PDF转换为PDF/A并检查PDF/A合规性。 | [文档转换文档](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **文档Assurance** | 添加或删除签名字段、签名、认证、加密、解密并为PDF文档应用使用权限。 | [文档Assurance文档](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **数字签名** | 集成Adobe Sign用于表单和文档的安全电子签名。 | [数字签名文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

用于创建、编辑和部署工作流以及管理以表单为中心的业务流程的桌面应用程序。 它提供了与后端服务和系统的集成。

## [原型](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/developing/archetype/overview)

AEM中的模板或模式，用于生成具有预定义结构的新项目，这有助于标准化、快速设置和遵守AEM开发最佳实践。

## [创作实例](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

内容创建者和管理员在发布内容之前设计、创建和管理内容的环境。 支持版本控制、预览和测试。

## [创作前端](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

用于在AEM Forms中创作和管理表单的用户界面。

## [自适应表单块](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

一种封装单元，它在逻辑上将相关的组件和元数据分组，以多步骤形式实现动态数据处理和易于扩展。

## [核心组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)

现成可重用的构建基块，用于创建表单，包括表单字段、布局容器、按钮和其他交互式元素。

## [通信管理](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

一个模块，使企业能够使用预定义的模板、规则和数据源创建、管理和提供个性化的通信。 包括信件模板、客户沟通和批量生成。

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

AEM中内置的Java Content Repository (JCR) ，用于存储结构化和非结构化数据，实现内容、模板和配置的分层存储。

## [自定义组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

扩展AEM Forms功能的定制组件，使用Sling模型、Sightly (HTL)和Java开发。 通常用于独特的业务逻辑或高级客户端交互。

## [自定义XCI（XML配置信息）](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

在Adobe Experience Manager (AEM) Forms中，管理员可以使用自定义XCI （XML配置信息）文件为表单和文档定义特定的呈现属性。 通过在管理控制台中配置XCI设置，您可以使用自定义选项覆盖系统默认值，确保量身定制的表单处理和呈现方式。

## [数据集成](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

将外部数据源（如数据库、Web服务或REST API）无缝集成到表单和工作流程中，以实现动态和个性化的用户体验。

## [数据源](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

用于将外部数据集成到表单中的接口，包括用于关系数据库的JDBC、用于Web服务的REST端点以及用于SAP系统的OData。 通过AEM Forms数据集成框架进行管理。

## [文档片段](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/lists)

文档的可重用组件，例如页眉、页脚、免责声明或条款，它们可以动态地包含在表单或通信中以确保一致性。

## [记录文档(DoR)](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

AEM Forms中的一项功能，可生成所提交表单的不可编辑的存档版本(通常采用PDF格式)，保留精确的内容和布局作为交易记录。

## [Edge Delivery Services](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/overview)

优化了AEM Forms的内容交付，确保减少表单、主题和客户端库等可供作者快速更新和发布内容的资产的延迟。

## [Forms集成](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/form-data-model/data-integration)

涉及使用OSGi包和连接器将AEM Forms连接到企业系统(例如SAP、Salesforce)，从而支持双向数据流和实时更新。

## [表单审核](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

工作流驱动功能，允许利益相关者在发布之前查看自适应表单、添加注释并批准更改。 使用AEM收件箱和任务管理。

## [表单数据模型(FDM)](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

一种表示层，用于将自适应表单连接到后端数据源，实现与RESTful Web服务、SOAP服务和OData的集成。 FDM允许表单作者将表单字段直接映射到后端数据结构，从而确保用户输入与外部系统的无缝同步。

## [表单本地化](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

自适应表单的过程，用于支持多种语言和区域设置，确保表单可供多种受众访问并且用户友好。

## [表单门户](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Forms Portal组件为Web开发人员提供了组件，以便在使用Forms (AEM)创作的网站上创建和自定义Adobe Experience Manager Portal。 它允许用户在Web和移动平台上高效地发现、访问和提交表单。

## [表单呈现和提交前端](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

AEM Forms中的最终用户界面，允许用户通过Web浏览器查看和提交表单。

## [表单集](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

以单个实体形式向用户展示的一组相关表单，可将复杂的数据收集流程细分为多个可管理的部分。

## [Forms Designer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

一个独立的应用程序，用于设计XDP表单的表单模板，并在AEM Forms中使用它来生成记录文档。

## [以Forms为中心的工作流](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

AEM Forms中管理业务流程（如文档审批、内容发布或用户通知）的一组自动或手动步骤。

## [交互式通信](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

用于管理高度个性化的多渠道通信的自定义实施。 它将来自各种来源（如CRM或ERP系统）的数据结合起来，以跨格式（如Web 、移动设备、电子邮件和打印）提供通信。

## [JCR （Java内容存储库）](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

一个分层的、基于标准的存储库，用于在AEM中存储内容、配置和元数据，支持结构化和非结构化数据存储。

## [封信](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

利用AEM Forms文档服务生成客户通信。 书信是使用XDP模板、数据模型和可重用片段的组合创建的，从而确保了在高容量情形下的可扩展性。

## [AEM Forms中的元数据](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

元数据支持高效的资源分类和检索。 AEM Forms包含每种资源类型的预定义元数据，并允许您进行自定义。 它还提供了用于无缝创建、管理和交换元数据的工具。

## [PDF Generator ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

AEM Forms中的一种工具，可将各种文件格式（例如：Word、Excel、PowerPoint）转换为PDF文档，并提供加密、水印和合并等功能。

## [Publish实例](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

AEM中向最终用户提供实时内容的环境。 它以优化的性能提供表单、页面和其他数字体验。

## [规则编辑器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

自适应Forms中的一种可视化工具，它允许创作者定义表单字段（如可见性、验证和数据预填充）的自定义规则和逻辑，而无需编码专业知识。

## [涂鸦签名](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

AEM Forms中的一项功能，允许用户使用鼠标或触屏设备直接在表单上绘制签名，从而以电子方式签署表单。

## [在AEM Forms中提交操作](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

在提交表单时执行的服务器端或客户端操作。 示例包括REST API调用、调用工作流或将数据写入JCR（Java内容存储库）。

## [主题](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

CSS驱动的样式框架应用于自适应表单，将LESS/SASS用于预处理器。 主题确保符合品牌准则和辅助功能标准，您可以自定义主题，更改其设计元素、布局、颜色、排版规则，有时还可以更改底层代码。

## [模板](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

自适应表单Blueprint包含结构元素（字段、布局）和预配置的脚本，您可以创建和自定义新模板或使用现有的现成模板。

## [Web层](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

包含基于通用服务和表单服务构建的JSP或servlet，可提供创作前端、表单呈现和提交前端以及REST API等功能。

## [XDP （XML数据包）](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

AEM Forms中使用的文件格式，用于设计和构建表单，支持动态内容和交互性时能够渲染为PDF或HTML。

## [XFA (XML Forms架构)](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

用于创建交互式和动态PDF forms的旧版技术。 XFA表单支持高级功能，例如动态布局调整、脚本编写以及与后端系统的无缝集成。

## [XML或JSON架构](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

一种标准化结构，用于定义表单和工作流程中XML或JSON数据的格式和组织。 这些架构可确保一致的数据处理，并实现与外部系统的互操作性。

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->
