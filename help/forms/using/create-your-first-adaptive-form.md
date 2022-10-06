---
title: “教程：创建您的第一个自适应表单”
seo-title: "Tutorial: Create your first adaptive form"
description: 了解如何创建业务类、交互式和响应式表单。
seo-description: Learn to create business class, interactive, and responsive forms.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
feature: Adaptive Forms
exl-id: 77a05f83-ac9a-4221-85ac-439e82623a28
source-git-commit: 471d7f48dc4653000b4852dbbeb886b05e28e644
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---

# 教程：创建您的第一个自适应表单 {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## 简介 {#introduction}

您是否在寻找适合移动设备的 **表单体验** 简化注册、增加参与度并缩短周转时间， **自适应表单** 非常适合你。 自适应表单可提供移动、自动化和分析友好的表单体验。 您可以轻松构建具有响应性和交互性的表单，使用自动化流程减少管理和重复性任务，并使用数据分析改进和个性化客户在您的表单上的体验。

本教程提供了用于创建自适应表单的端到端框架。 本教程分为一个用例和多个指南。 每个指南都可帮助您学习并将新功能添加到本教程中创建的自适应表单。 您在每个指南之后都有一个有效的自适应表单。 有关创建自适应表单的指南，请参阅。 随后的指南即将推出。 在本教程结束时，您将能够：

* 创建自适应表单和表单数据模型。
* 设置自适应表单的样式。
* 使用自适应表单规则编辑器来构建业务规则。
* 测试和发布自适应表单。

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

历程从学习用例开始：

网站为不同的客户提供一系列产品。 客户浏览门户，选择并订购产品。 每个客户都创建一个帐户并提供送货和帐单地址。 现有客户莎拉·罗丝正在寻求将她的送货地址添加到网站。 该网站提供在线表格以添加和更新送货地址。

网站在Adobe Experience Manager(AEM)上运行，并使用AEM [!DNL Forms] 用于数据捕获和处理。 地址添加和更新表单是自适应表单。 网站将客户详细信息存储在数据库中。 他们使用地址添加和更新表单来检索和显示可用地址。 他们还使用自适应表单来接受更新和新地址。

### 先决条件 {#prerequisite}

* 设置AEM创作实例。
* 安装 [AEM Forms附加组件](../../forms/using/installing-configuring-aem-forms-osgi.md) 在创作实例上。
* 从数据库提供程序获取JDBC数据库驱动程序（JAR文件）。 本教程中的示例基于 [!DNL MySQL] 数据库和使用 [!DNL Oracle's] [MySQL JDBC数据库驱动程序](https://dev.mysql.com/downloads/connector/j/5.1.html).

* 使用下面显示的字段设置包含客户数据的数据库。 数据库对于创建自适应表单并不是必需的。 本教程使用数据库来显示AEM的表单数据模型和持久性功能 [!DNL Forms].

![自适应格式数据](assets/adaptiveformdata.png)

## 步骤1:创建自适应表单 {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

自适应表单是新一代，具有吸引力、响应性、动态性和自适应性。 使用自适应表单，您可以提供个性化且有针对性的体验。 AEM [!DNL Forms] 提供拖放WYSIWYG编辑器以创建自适应表单。 有关自适应表单的更多信息，请参阅 [创作自适应表单简介](../../forms/using/introduction-forms-authoring.md).

目标：

* 创建允许客户添加送货地址的自适应表单
* 用于显示和接受客户信息的自适应表单的布局字段
* 创建提交操作以发送包含表单内容的电子邮件
* 预览和提交自适应表单

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## 步骤2:创建表单数据模型 {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

表单数据模型允许将自适应表单连接到不同的数据源。 例如，AEM用户配置文件、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库。 表单数据模型是业务实体和服务在连接数据源中提供的统一数据表示模式。 您可以将表单数据模型与自适应表单结合使用，以检索、更新、删除数据，并将数据添加到连接的数据源。

目标：

* 配置网站的数据库实例([!DNL MySQL] 数据库)作为数据源
* 使用创建表单数据模型 [!DNL MySQL] 数据库作为数据源
* 添加数据模型对象以形成数据模型
* 为表单数据模型配置读写服务
* 测试表单数据模型和配置有测试数据的服务

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## 步骤3:将规则应用于自适应表单字段 {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

自适应表单提供一个编辑器，用于在自适应表单对象上写入规则。 这些规则根据表单上的预设条件、用户输入和用户操作定义要在表单对象上触发的操作。 它有助于确保准确性并加快表单填写体验的速度。

目标：

* 创建规则并将其应用于自适应表单字段
* 使用规则触发表单数据模型服务以将数据更新到数据库

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## 步骤4:设置自适应表单的样式 {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

自适应表单提供主题和 [编辑者](../../forms/using/themes.md) 创建自适应表单的主题。 主题包含组件和面板的样式详细信息，您可以以不同的形式重复使用主题。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 将主题应用于表单时，指定的样式将反映在表单的相应组件上。 自适应表单还支持特定于表单的样式的内嵌样式。

目标：

* 将现成主题应用于自适应表单
* 使用主题编辑器创建自适应表单的主题
* 在自定义主题中使用Web字体

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## 步骤5:发布自适应表单 {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

您可以将自适应表单作为独立表单（单页应用程序）发布，并包含在AEM中 [站点页面](/help/forms/using/embed-adaptive-form-aem-sites.md)，或列在AEM上 [!DNL Site] 使用 [Forms门户](../../forms/using/introduction-publishing-forms.md).

目标：

* 将自适应表单作为AEM页面发布
* 在AEM中嵌入自适应表单 [!DNL Sites] 页面
* 将自适应表单嵌入到外部网页(在AEM外部托管的非AEM网页)

[![请参阅指南](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)
