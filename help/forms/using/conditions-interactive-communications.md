---
title: 交互式通信条件
description: 创建和编辑要在交互式通信中使用的条件片段 — 条件是用于构建交互式通信的四种文档片段类型之一。 其他三个是文本、列表和布局片段。
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 1%

---

# 交互式通信条件{#conditions-in-interactive-communications}

创建和编辑要在交互式通信中使用的条件片段 — 条件是用于构建交互式通信的四种文档片段类型之一。 其他三个是文本、列表和布局片段。

## 概述 {#overview}

条件是可以包含在交互式通信中的文档片段。 其他文档片段为[文本](../../forms/using/texts-interactive-communications.md)、列表和布局片段。 条件允许您根据提供的数据和规则定义一个或多个上下文资产，这些上下文资产将包含在交互式通信中。

示例：

* 在信用卡报表中，根据客户的信用卡类型，显示信用卡年费及信用卡影像。
* 在保险费到期提醒中，显示基于客户所在州税款的计税结果。

条件中的资产，该条件基于应用的规则和传递到规则的值渲染。 条件中的规则可以检查以下数据类型中的值：

* 关联的表单数据模型的属性
* 您在条件中创建的任何变量
* 字符串
* 数字
* 数学表达式
* 日期

## 创建条件 {#createcondition}

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 条件]**。
1. 指定以下信息：

   * **[!UICONTROL 标题]**： （可选）输入条件的标题。 标题不需要是唯一的，并且可以包含特殊字符和非英语字符。 条件由它们的标题（如果可用）引用，例如在缩略图和属性中。
   * **[!UICONTROL 名称]**：文件夹中条件的唯一名称。 文件夹中不能存在任何状态下具有相同名称的两个文档片段（文本、条件或列表）。 在“名称”字段中，只能输入英语字符、数字和连字符。 根据“标题”字段自动填充“名称”字段。 在“标题”字段中输入的特殊字符、空格、数字和非英语字符将在“名称”字段中替换为连字符。 虽然“标题”字段中的值会自动复制到“名称”，但您可以编辑该值。

   * **[!UICONTROL 描述]**：键入文档片段的描述。
   * **[!UICONTROL 表单数据模型]**： （可选）选择“表单数据模型”单选按钮以根据表单数据模型创建条件。 选择“表单数据模型”单选按钮时，会显示&#x200B;**[!UICONTROL 表单数据模型]**&#x200B;字段。 浏览并选择表单数据模型。 在为交互式通信创建条件时，请确保使用与要在交互式通信中使用的数据模型相同的数据模型。 有关表单数据模型的详细信息，请参阅[数据集成](../../forms/using/data-integration.md)。

   * **[!UICONTROL 标记]**： （可选）要创建自定义标记，请在文本字段中输入值，然后选择“输入”。 保存此条件时，将创建新添加的标记。

1. 选择&#x200B;**[!UICONTROL 下一步]**。

   此时将显示“创建条件”页。

   ![createcondition](assets/createcondition.png)

1. 选择&#x200B;**[!UICONTROL 添加Assets]**。

   此时会显示“选择Assets”页面，其中显示了可在条件中添加的可用文本、列表、条件和图像。

   >[!NOTE]
   >
   >“选择Assets”页面中仅显示基于无、新创建的资源和基于FDM的资源（使用与正在创建的条件相同的FDM创建）。

1. 选择要包含在条件中的相应资源，然后选择&#x200B;**[!UICONTROL 完成]**。

   此时会显示“创建条件”页面，其中列出了已添加的资源。

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   您可以使用以下选项管理条件中的资源：

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A]拒绝更改。**选择此图标可拒绝您对条件中的资产和规则所做的更改。
   **[B]接受更改。**选择此图标以接受您在条件中的资产和规则中所做的更改。
   **[C]重复资产。**选择此图标以创建资产的副本以及条件中应用的规则（如果有）。 然后，您可以继续编辑重复资产的规则和资产。 复制资产对于创建类似规则以根据特定上下文显示替代资产非常有用。
   **[D]节目预览。**选择此图标可在“创建\编辑条件”页面中显示资源的预览。
   **“服务器”重新排序。**&#x200B;选择并按住此图标可拖放资源以在条件中重新排序。

   您可以选择以下选项来指定条件在运行时的工作方式：

   * **已禁用多个结果评估\已启用多个结果评估**：启用此选项（显示为“已启用多个结果评估”）时，将评估所有规则，结果将是所有真实规则的总和。 如果禁用此选项（显示为“已禁用多个结果评估”），则仅评估发现为true的第一个规则，并成为条件的输出。

   * **分页符**：选择此选项（![分页符](assets/break.png)）可在条件的资源之间添加分页符。 如果未选择此选项(![nobreak](assets/nobreak.png))，则如果某个条件溢出到打印输出中的下一页，则整个条件将移至下一页，而不是该条件中的资产之间的页面中发生中断。

1. 选择&#x200B;**[!UICONTROL 创建规则]**&#x200B;以根据需要添加用于显示或隐藏资产的规则。 要在规则中使用变量，请参阅[创建变量](#variables)。 有关详细信息，请参阅[将规则添加到条件](#ruleeditor)。

   创建的规则将显示在创建条件屏幕的RULE列中。

   ![createconditionscreenrulesadded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >您可以在条件中插入已应用规则或重复应用的资产。

1. 选择&#x200B;**[!UICONTROL 保存]**。

   条件已创建。 现在，您可以在创建交互式通信时继续使用条件作为构建块。

   >[!NOTE]
   >
   >要保存新条件或编辑后的条件，您必须为条件中添加的每个资产至少具有一个规则。

## 编辑条件 {#edit-a-condition}

可以使用以下步骤编辑条件。 您还可以通过在弹出菜单中选择编辑片段，从交互式通信中编辑条件。

1. 选择&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL 文档片段]**。
1. 导航到条件并将其选定。
1. 选择&#x200B;**[!UICONTROL 编辑]**。
1. 在条件中进行所需的更改。 有关可在条件中更改的信息的详细信息，请参阅[创建条件](#createcondition)。
1. 选择&#x200B;**[!UICONTROL 保存]**，然后选择&#x200B;**[!UICONTROL 关闭]**。

## 在条件中创建规则 {#ruleeditor}

在条件中使用规则编辑器，可以创建规则以根据&#x200B;**预设条件**&#x200B;显示或隐藏资源。 这些条件可以基于以下基础构建：

* 字符串
* 数字
* 数学表达式
* 日期
* 关联的表单数据模型的属性
* 您已创建的任何[变量](#variables)

### 在条件中创建规则 {#create-rule-in-condition}

1. 创建或编辑条件时，为相关资产选择![ruleeditoricon](assets/ruleeditoricon.png) （规则编辑器）图标。

   此时将显示“创建规则”对话框。 除了字符串、数字、数学表达式和日期之外，规则编辑器中还提供以下内容来创建规则语句：

   * 关联的表单数据模型的属性
   * 您已创建的任何[变量](#variables)。

   ![createruledialog](assets/createruledialog.png)

   选择要评估的适当选项。

   >[!NOTE]
   >
   >不支持使用收藏集属性创建显示资产的规则。

1. 选择相应的运算符以计算规则，例如“等于”、“包含”和“开头为”。
1. 插入求值表达式、字符串、数据模型属性、变量或日期。

   ![策略类型为标准时显示资源的规则](assets/ruleincondition.png)

   在策略类型为标准时显示资源的规则

   * 创建或编辑规则时，您还可以选择![icon_resize](assets/icon_resize.png) （调整大小）以展开“创建规则”/“编辑规则”对话框。 展开的完整窗口对话框允许您创建[变量](#variables)来构造规则。 再次选择调整大小以返回常规的“创建规则”对话框。

   * 您还可以在规则中创建多个条件。

1. 选择&#x200B;**[!UICONTROL 完成]**。

   该规则将应用于资源。

## 在条件中创建和使用变量 {#variables}

在条件中创建或编辑规则时，您可以选择![icon_resize](assets/icon_resize.png) （调整大小）以展开“创建规则\编辑规则”对话框。 通过展开的全窗口对话框，您可以：

* 在规则中创建和使用变量
* 在规则中拖放表单数据模型的属性和变量

再次选择调整大小以返回到“创建规则\编辑规则”对话框。

### 创建变量 {#create-variables}

1. 在条件中创建或编辑规则时，您可以选择![icon_resize](assets/icon_resize.png) （调整大小）以展开“创建规则\编辑规则”对话框。

   此时将出现“已展开，全窗口”对话框。

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. 在左窗格中，选择&#x200B;**[!UICONTROL 变量]**。

   此时将显示“变量”窗格。

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. 选择&#x200B;**[!UICONTROL 创建]**。

   此时将显示“创建变量”窗格。

1. 输入以下信息并选择&#x200B;**[!UICONTROL 创建]**：

   * **[!UICONTROL 名称]**：变量的名称。
   * **[!UICONTROL 描述]**： （可选）输入有关变量的描述。
   * **[!UICONTROL 类型]**：选择变量的类型： String、Number、Boolean或Date。
   * **[!UICONTROL 仅允许特定值]**：对于String和Number变量，您可以确保代理从代理UI中占位符的特定值集中进行选择。 要指定值集，请选择此选项，然后指定&#x200B;**[!UICONTROL 值]**&#x200B;字段中允许使用逗号分隔的值。

1. 选择&#x200B;**[!UICONTROL 创建]**。

   随即会创建变量并将其列在“变量”窗格中。

1. 要在规则中插入变量，请将该变量拖放到规则中某个选项的占位符中。
1. 构造有效规则后，选择&#x200B;**[!UICONTROL 完成]**。

   如有必要，请继续在条件中进行进一步更改并保存。
