---
title: 内联条件，并在Interactive Communications和Letters中重复
seo-title: 内联条件，并在Interactive Communications和Letters中重复
description: 使用内联条件并在交互通信和字母中重复，您可以创建高度上下文化和结构良好的通信。
seo-description: 使用内联条件并在交互通信和字母中重复，您可以创建高度上下文化和结构良好的通信。
uuid: 32b48a8b-431d-4f9c-9f51-8e7e9ac624a0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications
discoiquuid: bbaba39b-e15a-4143-b6fc-7789fa2917b4
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 内联条件，并在Interactive Communications和Letters中重复{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## 内联条件 {#inline-conditions}

AEM Forms允许您在文本模块中使用内联条件，以自动呈现取决于与表单数据模型（在交互通信中）或数据字典（在字母中）关联的上下文或数据的文本。 内联条件根据条件评估为true或false显示特定内容。

条件对表单数据模型／数据字典或最终用户提供的数据值执行计算。 使用内联条件，您可以节省时间并减少人为错误，同时创建高度上下文化和个性化的交互式通信／字母。

有关详细信息，请参阅：

* [创建交互式通信](../../forms/using/create-interactive-communication.md)
* [通信管理概述](/help/forms/using/cm-overview.md)
* [交互通信中的文本](../../forms/using/texts-interactive-communications.md)

### 示例：使用规则在交互式通信中条件化内联文本 {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

要在交互通信中对句子、段落或文本字符串进行条件化，可以在相应的文本文档片段中创建规则。 以下示例使用规则仅向交互通信的美国接收方显示免费电话号码。

有关详细信息，请参阅在交互通信中的文本 [中以文本创建规则](../../forms/using/texts-interactive-communications.md)。

在交互通信中包含文本片段后，代理使用代理UI准备交互通信后，将评估接收者的（表单数据模型）数据，并且该文本仅显示给美国的接收者。

### 示例：在字母中使用内联条件来呈现相应的地址 {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

通过在相应的文本模块中插入内联条件，可以在字母中插入内联条件。 以下示例使用两个条件在基于DD元素“性别”的字母中评估和显示相应的地址，即Sir或Ma&#39;am。 使用类似的步骤，您可以创建其他条件。

>[!NOTE]
>
>如果您的现有资产包含旧条件／重复表达式（6.2 SP1 CFP 4之前），则资产将显示旧的条件语法和重复。 但是，旧的条件／重复操作起作用。 新条件／重复表达式和旧条件／重复表达式相互兼容，以创建新旧条件／重复表达式的嵌套混合。

1. 在相关文本模块中，选择要条件化并点按条件的文本部分 **。**

   ![1_selecttext](assets/1_selecttext.png)

   出现“条件”(Condition)对话框，其中显示一个空条件。

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >无法保存空或无效的条件表达式。 必须有一个有效的条件表达式才能 `${}` 保存表达式。

1. 执行以下操作以构建一个条件，用于评估所选／条件化文本是否显示在字母中，然后点按复选标记以保存表达式：

   双击DD元素以在条件中插入它。 插入相应的运算符，并在对话框中构建以下条件。

   ```java
   ${DD_creditcard_Gender=="Male"}
   ```

   有关创建表达式的详细信息，请参阅在 **Expression builder中使用表达式创建器创建表达式** 和远程 [函数](../../forms/using/expression-builder.md)。 数据字典中的元素必须支持表达式中指定的值。 有关详细信息，请参 [阅数据字典](../../forms/using/data-dictionary.md)。

   插入条件后，您可以将鼠标悬停在条件左侧的手柄上以查看条件。 您可以点按手柄以查看条件的弹出菜单，该菜单允许您编辑或删除条件。

   ![3_straphandle](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. 通过选择文本插入类似条件 `Ma'am`。

   ```java
   ${DD_creditcard_Gender == "Female"}
   ```

1. 预览相关字母，并注意文本会根据内联条件呈现。 您可以使用以下方式输入DD元素“性别”的值：

   * 在预览带有样本数据的字母时，基于相关数据字典创建的样本XML数据文件。
   * 附加到相关数据字典的XML数据文件。
   有关详细信息，请参 [阅数据字典](../../forms/using/data-dictionary.md)。

   ![5_leteroutput](assets/5_letteroutput.png)

## 重复 {#repeat}

您的交互式通信／信函中可能包含动态信息，例如信用卡对帐单中的事务处理，其实例或发生情况可能会随每个生成的信函而不断变化。 使用重复，您可以在文本文档片段中设置和构造此类动态信息。

此外，您可以在重复构造中指定规则／条件，以对在交互通信／字母中呈现的信息／条目进行条件化。

### 示例：在交互通信中使用重复设置信用卡交易的格式、结构和显示信用卡交易列表 {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例介绍了使用重复功能在交互式通信中构造和渲染信用卡交易的步骤。

1. 在基于表单数据模型的文本文档片段中，插入相关的表单数据模型对象（和标签所需的嵌入文本，如本例所示）:

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >可重复内容必须至少包含“集合”类型的一个属性。

1. 选择要应用重复的内容。

   ![2_selection](assets/2_selection.png)

1. 点按重复。

   此时将显示重复对话框。

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 选择换行作为分隔符，然后根据需要点按添加条件以创建规则。 您还可以使用文本作为分隔符，并指定要用作分隔符的文本字符。

   此时将显示创建规则对话框。

1. 创建一个规则以显示日期为2018年2月28日之后的事务处理，以便在交互通信中仅包含3月的事务处理。

   >[!NOTE]
   >
   >此示例假定代理将在2018年3月底创建该语句。 否则，您可以创建另一条规则，以在2018年3月之前包括事务处理，以排除2018年3月之后的事务处理。

   ![4_createrule](assets/4_createrule.png)

1. 保存条件／规则，然后保存重复。 条件重复将应用于选定内容。

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   在鼠标移过时，文本文档片段会显示条件以及应用于内容的重复操作中使用的分隔符。

1. 保存文本文档片段并预览相关的交互式通信。 根据表单数据模型中的数据，对元素应用的重复操作将呈现与预览中的以下内容类似的事务详细信息：

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 示例：在信件中重复使用，以设置格式、结构和显示信用卡交易列表 {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下示例提供了使用重复功能在信函中构造和呈现信用卡交易的步骤。 使用类似的步骤，您可以在不同的场景中使用重复。

1. 打开（在编辑或创建时）包含DD元素的文本模块，这些元素可呈现重复／动态数据并在DD元素周围嵌入所需的文本。 例如，文本模块具有以下DD元素，用于在信用卡上创建交易对帐单：

   ```
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   这些DD元素会显示信用卡上进行的事务处理列表，其中包含以下信息：

   事务处理日期、事务处理金额和事务处理类型（借项或贷项）

1. 在DD元素中嵌入文本，使语句更易读，如：

   ![1_repeat](assets/1_repeat.png)

   ```
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   但是，尚未完成呈现格式良好的语句的任务。 如果根据目前所做的工作渲染字母，则其显示如下：

   ![1-1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   要重复静态文本和DD元素，您需要应用重复，如后续步骤中所述。

1. 选择静态文本以及要重复的DD元素，如下所示：

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 点按 **重复**。 出现“重复”对话框，其内嵌条件为空。

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 如果需要，插入一个条件以选择性地呈现事务，例如呈现大于50美分的事务金额：

   ```
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   否则，如果您不需要选择性地呈现信息（此处的事务），请在对话框中删除以下内容，将条件保留为空： `${}`. 如果重复表达式窗口为空（不需要重复时不包含${}），或当它包含有效的重复条件时，将启用保存重复表达式。

1. 选择分隔符以设置动态文本的格式，然后点按复选标记以保存：

   * **换行**:在输出字母中的每个事务条目后插入换行符。
   * **文本**:在输出字母中的每个事务条目之后插入指定的文本字符。
   插入条件后，重复文本将以红色突出显示，并在其左侧显示一个手柄。 可将鼠标悬停在重复项左侧的手柄上以查看重复构造。

   ![4_repeat_strapdetail](assets/4_repeat_hoverdetail.png)

   您可以点击手柄以查看重复的弹出菜单，该菜单允许您编辑或删除重复构造。

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 预览相关字母，并注意文本会根据重复内容进行渲染。 您可以使用以下方式输入DD元素的值：

   * 在预览带有样本数据的字母时，基于相关数据字典创建的样本XML数据文件。
   * 附加到相关数据字典的XML数据文件。
   有关详细信息，请参 [阅数据字典](https://helpx.adobe.com/aem-forms/6-2/data-dictionary.html)。

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   静态文本与事务详细信息一起重复。 重复静态文本由此过程中对文本应用的重复而方便。 条件${DD_creditcard_TransactionAmount > 0.5}可确保在信函中不呈现低于USD .5的事务。

   >[!NOTE]
   >
   >您只能在创建或编辑相关文本模块时插入条件并重复上述操作。 在预览字母时，尽管您可以编辑文本模块，但无法插入条件或重复执行此操作。

## 使用内联条件并重复——某些用例 {#using-inline-condition-and-repeat-some-use-cases}

### 在条件内重复 {#repeat-within-condition}

您可能需要在某个条件内使用重复。 通过“对应管理”，您可以在内联条件构造中使用重复。

例如，在某个条件（格式为绿色）中重复以下内容（格式为红色）。

当重复操作呈现信用卡交易时，条件${DD_creditcard_nooftransactions > 0}确保仅在至少有一次交易时才呈现重复构造。

![repeatwincondition](assets/repeatwitincondition.png)

同样，根据您的要求，您可以创建：

* 一个条件内的一个或多个条件
* 重复内的一个或多个条件
* 条件和在条件或重复项中重复的组合

### 内联条件为空 {#empty-inline-condition}

您可能需要稍后插入空的内联条件并嵌入文本和DD元素。 通信管理允许您这样做。

![emptycondition](assets/emptycondition.png)

但是，建议您尽可能首先在文本模块中插入文本和DD元素，并采用预期的格式（如项目符号），然后应用内联条件。
