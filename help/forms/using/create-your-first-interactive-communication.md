---
title: 教程 — 创建您的第一个交互式通信
description: 了解如何创建您的第一个交互式通信。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
feature: Interactive Communication
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 0%

---

# 教程：创建您的第一个交互式通信 {#tutorial-create-your-first-interactive-communication}

了解如何创建您的第一个交互式通信。

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

交互式通信可以集中管理安全、个性化的交互式信函的创建、编排和交付，例如业务信函、文档、对帐单、营销邮件、账单和欢迎资料包。 交互式通信可通过两种渠道提供：打印和Web。 Print channel用于创建PDF和纸张通信，而Web channel用于提供在线体验。

本教程提供了一个用于创建交互式通信的端到端框架。 本教程将组织为一个用例和多份指南。 每个指南都帮助您创建用作构建块的功能，以创建交互式通信。

下图说明了创建交互式通信所需的构建块。

![工作流](assets/workflow.gif)

在本教程结束时，您将能够：

* 创建构建基块（表单数据模型、文档片段和模板）
* 创建交互式通信
* 测试和发布交互式通信

## 用例 {#use-case}

历程从了解用例开始：

电信运营商每月通过电子邮件向客户发送账单。 账单是交互式通信。 该电子邮件包括：

* 受密码保护的PDF，在本教程中称为打印渠道。 它包括客户详细信息、账单详细信息、费用摘要、方便的账单支付方式和使用详细信息。
* 指向账单Web版本的链接，在本教程中称为Web渠道。 账单的Web版本，除了PDF版本中涵盖的详细信息之外，还提供使用详细信息的图形表示以及基于Adobe Target的个性化优惠。 Web版本还包含在线支付表单。 它有助于在不离开集成电路的情况下进行在线支付。
* 指向增值服务的链接，如在线存储、音乐订阅和点播视频订阅。

## 先决条件 {#prerequisites}

* 设置AEM创作实例。
* 安装 [AEM Forms加载项](/help/forms/using/installing-configuring-aem-forms-osgi.md) 在创作实例上
* 设置MYSQL数据库
* 从数据库提供程序获取JDBC数据库驱动程序（JAR文件）。 本教程中的示例基于MySQL数据库并使用Oracle的 [MySQL JDBC数据库驱动程序](https://dev.mysql.com/downloads/connector/j/5.1.html).

## 步骤1：规划交互式通信 {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

规划交互式通信的第一步是最终确定交互式通信的内容。 内容定稿后，您必须对其进行分析以确定创建交互式通信所需的各种资源类型。

**目标：**

为具有以下数据输入模式的交互式通信创建剖析：

* 静态文本
* 表单数据模型
* 代理 UI
* 条件数据
* 图像

[](/help/forms/using/planning-interactive-communications.md)

## 步骤2：创建表单数据模型 {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

表单数据模型允许您将交互式通信连接到不同的数据源。 例如，AEM用户配置文件、RESTful Web服务、基于SOAP的Web服务、OData服务和关系数据库。 表单数据模型是连接数据源中可用的业务实体和服务的统一数据表示架构。 您可以将表单数据模型与交互式通信结合使用，以从连接的数据源中检索数据。 有关表单数据模型的更多信息，请参阅 [AEM Forms数据集成](/help/forms/using/data-integration.md).

**目标：**

* 将数据库实例（MySQL数据库）配置为数据源
* 使用MySQL数据库作为数据源创建表单数据模型
* 将数据模型对象添加到表单数据模型
* 为表单数据模型配置读写服务
* 在数据模型对象之间创建关联
* 查看自动生成的示例数据
* 编辑示例数据
* 测试表单数据模型和已配置的服务（包含测试数据）

[](/help/forms/using/create-form-data-model0.md)

## 步骤3：创建文档片段 {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

文档片段是用于构成交互式通信的通信的可重用组件。 文档片段的类型有：文本、列表和条件。

**目标：**

* 创建文档片段
* 创建变量
* 创建和应用规则

[](/help/forms/using/create-document-fragments.md)

## 步骤4：创建模板 {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

要创建交互式通信，必须在AEM服务器上为打印和Web渠道提供模板。

打印渠道的模板在AdobeForms Designer中创建，并上传到AEM服务器。 然后，这些模板便可在创建交互式通信时使用。

Web渠道的模板是在AEM中创建的。 模板作者和管理员可以创建、编辑和启用Web模板。 创建并启用后，这些模板便可在创建交互式通信时使用。

**目标：**

* 使用AdobeForms Designer为打印渠道创建XDP模板
* 将XDP模板上传到AEM Forms服务器
* 为Web渠道创建和启用模板

[](/help/forms/using/create-templates-print-web.md)

## 步骤5：创建交互式通信 {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

为Web版本创建所有构建基块（如表单数据模型、文档片段和模板）后，即可开始创建交互式通信。

交互式通信可通过两种渠道提供：打印和Web。 您还可以创建以Print channel作为母版的交互式通信。 Web渠道的“打印为主文件”选项确保Web渠道的内容、继承和数据绑定派生自Print渠道。

**目标：**

* 为打印渠道创建交互式通信
* 为Web渠道创建交互式通信
* 创建Print和Web交互通信并将Print作为母版
* 在Web版本的交互式通信中创建动态表
* 在Web版本的交互式通信中创建图表
* 在Web版本的交互式通信中创建超链接

[](/help/forms/using/create-interactive-communication0.md)

## 步骤6：发布交互式通信 {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

使用打印和Web渠道创建和测试交互式通信后，即可发布这些资产。 本教程中描述的用例侧重于将这些资源与电子邮件客户端集成。 电子邮件客户端用作将交互式通信发送到多个电子邮件地址的桥梁。

**目标：**

* 将交互式通信与电子邮件客户端集成，以便能够向客户发送通信
* 将PDF文档作为附件包含（在打印渠道中创建的交互式通信）
* 包括指向交互式通信的Web版本的链接
