---
title: 多步表单序列简介
seo-title: Introduction to multi-step form sequence
description: 通过AEM Forms，您可以定义一系列表单面板，您希望用户在其中导航和填写自适应表单。
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 多步表单序列简介{#introduction-to-multi-step-form-sequence}

自适应表单使表单作者能够轻松创建多步数据捕获体验。 它内置支持创建多个面板并将每个面板与不同的导航模式关联。 表单作者可以对逻辑部分中的表单字段进行分组，并将组表示为面板。 使用面板布局可控制面板之间的整体导航。 作者可以选择以不同的布局来排列面板，例如，使用向导布局按顺序放置面板，或使用选项卡式布局以临时方式放置面板。 有关面板布局的信息，请参阅 [自适应表单的布局功能](../../forms/using/layout-capabilities-adaptive-forms.md).

在典型的表单填充体验中，涉及的步骤不止是捕获数据。 完整的表单提交可以包括其他步骤，例如以数字方式签署表单、验证表单中填写的信息、处理付款等。 它不同于不同的情况。

如果您的用例要求执行一组数据捕获步骤，或者存在需要遵循特定步骤的法规，AEM Forms将提供一种方法来跨表单强制实施该通用结构。 表单结构的有预谋实施定义表单的步骤顺序。 ![多步表单序列示例](assets/formpipeline.png)

多步表单序列示例

让我们举一个用例，您需要为表单创建填写、验证、签名和确认步骤的序列。 创建此类序列的步骤如下所示：

1. 定义表单模板并向其添加所需的面板。 请注意，序列中的每个步骤都应有一个面板。 但是，您可以在面板中包含子面板。

   在本例中，我们可以添加以下面板：

   * **填充**:它包含用于捕获数据的表单字段。 在此，您可以包含嵌套的子面板，以为不同类型的信息（如个人、家庭、财务等）创建部分。

   * **验证**:它包含 **验证** 可在基于XFA的自适应表单中使用的组件。 它以只读模式显示在“填充”面板中捕获的信息以进行验证。

   * **电子签名**:它包含 **Sign** 可在基于XFA的自适应表单中使用的组件。 它提供以下签名服务：

      * Adobe Document Cloud eSign服务
      * 连笔签名
   * **确认**:它包含 **概要** 组件，在用户签署表单后显示确认表单提交的消息并到达序列中的确认（摘要）步骤。 作者可以配置摘要组件的文本、显示感谢消息、显示指向生成PDF的链接，等等。


1. 将根面板的布局选择为 **[!UICONTROL 向导]**.
1. 完成其余步骤以创建表单模板。 有关更多信息，请参阅 [创建自定义自适应表单模板](../../forms/using/custom-adaptive-forms-templates.md).

在表单模板中定义表单序列后，您可以使用它创建将基本结构定义为就地序列的表单，不过您始终可以根据自己的要求自定义表单。
