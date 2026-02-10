---
title: 自适应表单规则编辑器
description: 自适应表单规则编辑器允许您添加动态行为并将复杂逻辑构建到表单中，而无需编码或脚本。
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Adaptive Forms,Foundation Components
discoiquuid: 1b905e66-dc05-4f14-8025-62a78feef12a
docset: aem65
exl-id: c611a1f8-9d94-47f3-bed3-59eef722bf98
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: a0ef9925d1bcb84ea5bf733221875d0322cc6df1
workflow-type: tm+mt
source-wordcount: '6639'
ht-degree: 2%

---

# 自适应表单规则编辑器{#adaptive-forms-rule-editor}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-rules-and-use-expressions-in-an-adaptive-form/rule-editor.html) |
| AEM 6.5 | 本文 |

## 概述 {#overview}

Adobe Experience Manager Forms中的规则编辑器功能使表单业务用户和开发人员能够编写关于自适应表单对象的规则。 这些规则根据预设条件、用户输入和用户对表单的操作，定义要在表单对象上触发的操作。 它有助于进一步简化表单填写体验，确保准确性和速度。

规则编辑器提供了用于编写规则的直观且简化的用户界面。 规则编辑器为所有用户提供可视编辑器。 此外，仅对于表单超级用户，规则编辑器提供用于编写规则和脚本的代码编辑器。
<!-- Some of the key actions that you can perform on adaptive form objects using rules are:

* Show or hide an object
* Enable or disable an object
* Set a value for an object
* Validate the value of an object
* Execute functions to compute the value of an object
* Invoke a form data model service and perform an operation
* Set property of an object -->

规则编辑器取代了AEM 6.1 Forms及更早版本中的脚本编写功能。 但是，现有脚本将保留在新规则编辑器中。 有关在规则编辑器中使用现有脚本的更多信息，请参阅[规则编辑器对现有脚本的影响](#impact-of-rule-editor-on-existing-scripts)。

添加到forms-power-users组的用户可以创建新脚本并编辑现有脚本。 forms-users组中的用户可以使用脚本，但不能创建或编辑脚本。

## 了解规则 {#understanding-a-rule}

规则是操作和条件的组合。 在规则编辑器中，操作包括隐藏、显示、启用、禁用或计算表单中对象值等活动。 条件是对表单对象的状态、值或属性执行检查和操作而计算的布尔表达式。 根据通过评估条件返回的值（`True`或`False`）执行操作。

规则编辑器提供了一组预定义的规则类型（如When、Show、Hide、Enable、Disable、Set Value Of和Validate）以帮助您编写规则。 每种规则类型均允许您定义规则中的条件和操作。 本文档进一步详细说明了每种规则类型。

规则通常遵循下面的其中一个结构：

**Condition-Action**&#x200B;在此构造中，规则首先定义条件，然后定义要触发的操作。 这种构造与编程语言中的if-then语句类似。

在规则编辑器中，**When**&#x200B;规则类型强制使用condition-action结构。

**Action-Condition**&#x200B;在此构造中，规则首先定义要触发的操作，然后定义评估条件。 此结构的另一个变体是action-condition-alternate action ，它还会定义在条件返回False时要触发的替代操作。

规则编辑器中的“显示”、“隐藏”、“启用”、“禁用”、“设置值”和“验证”规则类型强制实施操作条件规则结构。 默认情况下，“显示”的替代操作是“隐藏”，“启用”的替代操作是“禁用”，反之亦然。 您不能更改默认替代操作。

>[!NOTE]
>
>可用的规则类型（包括在规则编辑器中定义的条件和操作）还取决于创建规则的表单对象的类型。 规则编辑器仅显示有效的规则类型和选项，用于为特定表单对象类型编写条件和操作语句。 例如，您看不到面板对象的“验证”、“设置值”、“启用”和“禁用”规则类型。

有关规则编辑器中可用规则类型的详细信息，请参阅规则编辑器中的[可用规则类型](#available-rule-types-in-rule-editor)。

### 选择规则结构的准则 {#guidelines-for-choosing-a-rule-construct}

虽然您可以使用任何规则构建来实现大多数用例，但以下是选择一种构建而不是另一种构建的一些准则。 有关规则编辑器中可用规则的更多信息，请参阅规则编辑器中的[可用规则类型](#available-rule-types-in-rule-editor)。

* 创建规则时，一个典型的经验法则是考虑您所编写规则的对象的上下文。 假定您要根据用户在字段A中指定的值隐藏或显示字段B。在这种情况下，您要评估字段A的条件，并根据它返回的值，触发字段B的操作。

  因此，如果您在字段B（评估条件的对象）上编写规则，请使用condition-action结构或When规则类型。 同样，在字段A上使用操作条件结构或显示或隐藏规则类型。

* 有时，您需要根据一个条件执行多个操作。 在这种情况下，建议使用条件 — 操作构造。 在此构造中，您可以计算一次条件并指定多个操作语句。

  例如，要根据检查用户在字段A中指定的值的条件隐藏字段B、C和D，请编写一条规则，其中在字段A上使用condition-action结构或When规则类型，并指定操作以控制字段B、C和D的可见性。否则，您需要在字段B、C和D上分别使用三个规则，其中每个规则都会检查条件，并显示或隐藏各自的字段。 在此示例中，在一个对象上编写When规则类型比在三个对象上编写Show或Hide规则类型更有效。

* 要根据多个条件触发操作，建议使用action-condition构造。 例如，要通过评估字段B、C和D的条件来显示和隐藏字段A，请在字段A上使用显示或隐藏规则类型。
* 如果规则包含一个条件的一个操作，则使用condition-action或action condition结构。
* 如果规则检查条件，并在字段中提供值或退出字段时立即执行操作，则建议在评估条件的字段中编写具有condition-action结构或When规则类型的规则。
* 当用户更改应用When规则的对象的值时，将评估When规则中的条件。 但是，如果您希望操作在服务器端更改时触发（例如在预填充值中），则建议编写一个When规则以在字段初始化时触发操作。
* 在编写下拉列表、单选按钮或复选框对象的规则时，表单中这些表单对象的选项或值会在规则编辑器中预填充。

## 规则编辑器中的可用运算符类型和事件 {#available-operator-types-and-events-in-rule-editor}

规则编辑器提供了以下逻辑运算符和事件，您可以使用这些运算符和事件创建规则。

* **等于**
* **不等于**
* **开头为**
* **结尾为**
* **包含**
* **为空**
* **不为空**
* **已选择：**&#x200B;当用户为复选框、下拉菜单单选按钮选择特定选项时，返回true。
* **已初始化（事件）：**&#x200B;当表单对象在浏览器中呈现时返回true。
* **Is Changed (event)：**&#x200B;当用户更改表单对象的输入值或选定选项时，返回true。

## 规则编辑器中的可用规则类型 {#available-rule-types-in-rule-editor}

规则编辑器提供了一组可用于编写规则的预定义规则类型。 让我们详细了解一下每种规则类型。 有关在规则编辑器中编写规则的更多信息，请参阅[编写规则](#write-rules)。

### 时间 {#whenruletype}

**When**&#x200B;规则类型遵循&#x200B;**condition-action-alternate action**&#x200B;规则结构，有时只遵循&#x200B;**condition-action**&#x200B;结构。 在此规则类型中，首先指定评估条件，然后指定满足该条件时要触发的操作(`True`)。 在使用When规则类型时，您可以使用多个AND和OR运算符来创建[嵌套表达式](#nestedexpressions)。

使用When规则类型，您可以评估表单对象的条件，并对一个或多个对象执行操作。

简单地说，典型的When规则的结构如下所示：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

对对象B采取行动2；
和
关于对象C的行动3；

_

当具有多值组件（如单选按钮或列表）时，在为该组件创建规则时，会自动检索选项并使这些选项可用于规则创建者。 您无需再次键入选项值。

例如，列表包含四个选项：红色、蓝色、绿色和黄色。 创建规则时，将自动检索选项（单选按钮）并使规则创建者可以使用此选项，如下所示：

![multivaluefcdisplaysoptions](assets/multivaluefcdisplaysoptions.png)

编写When规则时，可以触发Clear Value Of操作。 清除值操作清除指定对象的值。 通过在When语句中将Clear Value设置为选项，可以创建具有多个字段的复杂条件。

![clearvalueof](assets/clearvalueof.png)

**隐藏**&#x200B;隐藏指定的对象。

**显示**&#x200B;显示指定的对象。

**启用**&#x200B;启用指定的对象。

**禁用**&#x200B;禁用指定的对象。

**调用服务**&#x200B;调用表单数据模型中配置的服务。 选择“调用服务”操作时，会出现一个字段。 点按该字段时，会显示您的AEM实例上在所有表单数据模型中配置的所有服务。 选择表单数据模型服务时，会显示其他字段，您可以在其中映射具有指定服务的输入和输出参数的表单对象。 请参阅调用表单数据模型服务的示例规则。

除了表单数据模型服务之外，您还可以指定直接WSDL URL来调用Web服务。 但是，表单数据模型服务具有许多好处，并且推荐了调用服务的方法。

有关在表单数据模型中配置服务的更多信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

**设置值**&#x200B;计算并设置指定对象的值。 您可以将对象值设置为字符串、另一个对象的值、使用数学表达式或函数的计算值、对象的属性值或来自配置的表单数据模型服务的输出值。 选择Web服务选项时，该选项会显示您的AEM实例上在所有表单数据模型中配置的所有服务。 选择表单数据模型服务时，会显示其他字段，您可以在其中映射具有指定服务的输入和输出参数的表单对象。

有关在表单数据模型中配置服务的更多信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

**[!UICONTROL Set Property]**&#x200B;规则类型允许您根据条件操作设置指定对象的属性值。 您可以将属性设置为以下项之一：

* 可见（布尔值）
* dorExclusion（布尔型）
* chartType（字符串）
* title（字符串）
* 已启用（布尔值）
* 必填（布尔值）
* validationsDisabled（布尔型）
* validateExpMessage（字符串）
* 值（数字、字符串、日期）
* 项（列表）
* 有效（布尔值）
* errorMessage（字符串）

它可让您定义规则以动态地将复选框添加到自适应表单。 您可以使用自定义函数、表单对象或对象属性来定义规则。

![设置属性](assets/set_property_rule_new.png)

要基于自定义函数定义规则，请从下拉列表中选择&#x200B;**函数输出**，然后从&#x200B;**函数**&#x200B;选项卡中拖放自定义函数。 如果满足条件操作，则自定义函数中定义的复选框数将添加到自适应表单中。

要基于表单对象定义规则，请从下拉列表中选择&#x200B;**表单对象**，然后从&#x200B;**表单对象**&#x200B;选项卡中拖放表单对象。 如果满足条件操作，则表单对象中定义的复选框数将添加到自适应表单。

通过基于对象属性的设置属性规则，您可以根据自适应表单中包含的其他对象属性在自适应表单中添加复选框的数量。

下图描述了根据自适应表单中的下拉列表数量动态添加复选框的示例：

![对象属性](assets/object_property_set_property_new.png)

**清除值**&#x200B;清除指定对象的值。

**设置焦点**&#x200B;设置指定对象的焦点。

**保存表单**&#x200B;保存表单。

**提交Forms**&#x200B;提交表单。

**重置表单**&#x200B;重置表单。

**验证表单**&#x200B;验证表单。

**添加实例**&#x200B;添加指定可重复面板或表行的实例。

**删除实例**&#x200B;删除指定的可重复面板或表行的实例。

**导航到**&#x200B;导航到其他交互式通信、自适应表单、其他资产（如图像或文档片段）或外部URL。 有关详细信息，请参阅[将按钮添加到交互式通信](../../forms/using/create-interactive-communication.md#addbuttontothewebchannel)。

### 设置值 {#set-value-of}

**[!UICONTROL 规则类型的]**&#x200B;设置值允许您根据是否满足指定的条件来设置表单对象的值。 该值可以设置为另一个对象的值、文本字符串、从数学表达式或函数派生的值、另一个对象的属性的值或表单数据模型服务的输出。 同样，您可以检查组件、字符串、属性或从函数或数学表达式派生的值的条件。

“设置值”规则类型不适用于所有表单对象，例如面板和工具栏按钮。 标准的“设置值”规则具有以下结构：



将对象A的值设置为：

（字符串ABC）或
（对象C的对象属性X）或
（函数中的值）或
（数学表达式中的值）或
（数据模型服务或Web服务的输出值）；

时间（可选）：

（条件1和条件2和条件3）为TRUE；



以下示例将`dependentid`字段中的值作为输入，并将`Relation`字段的值设置为`Relation`表单数据模型服务的`getDependent`参数的输出。

![set-value-web-service](assets/set-value-web-service.png)

使用表单数据模型服务的设置值规则示例

>[!NOTE]
>
>此外，您可以使用规则的“设置值”从表单数据模型服务或Web服务的输出填充下拉列表组件中的所有值。 但是，请确保您选择的输出参数为数组类型。 数组中返回的所有值在指定的下拉列表中变为可用。

### 显示 {#show}

使用&#x200B;**Show**&#x200B;规则类型，您可以编写规则以根据条件是否满足来显示或隐藏表单对象。 Show规则类型还会触发Hide操作，以防条件不满足或返回`False`。

典型的显示规则的结构如下所示：



`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`



### 隐藏 {#hide}

与“显示”规则类型类似，您可以使用&#x200B;**隐藏**&#x200B;规则类型，根据是否满足条件来显示或隐藏表单对象。 如果条件不满足或返回`False`，隐藏规则类型还会触发“显示”操作。

典型的“隐藏”规则的结构如下所示：



`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`



### 启用 {#enable}

**启用**&#x200B;规则类型允许您根据条件是否满足来启用或禁用表单对象。 Enable规则类型也会在条件不满足或返回`False`时触发Disable操作。

典型的Enable规则的结构如下所示：



`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`



### 禁用 {#disable}

与“启用”规则类型类似，**禁用**&#x200B;规则类型允许您根据条件是否满足来启用或禁用表单对象。 Disable规则类型还会触发Enable操作，以防条件不满足或返回`False`。

典型的禁用规则的结构如下所示：



`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### 验证 {#validate}

**Validate**&#x200B;规则类型使用表达式验证字段中的值。 例如，您可以编写一个表达式来检查用于指定名称的文本框是否不包含特殊字符或数字。

典型的验证规则的结构如下所示：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合验证规则，则可以为用户显示验证消息。 您可以在侧边栏中组件属性的&#x200B;**[!UICONTROL 脚本验证消息]**&#x200B;字段中指定消息。

![脚本验证](assets/script-validation.png)

### 设置选项 {#setoptionsof}

**Set Options Of**&#x200B;规则类型允许您定义规则以将复选框动态添加到自适应表单。 您可以使用表单数据模型或自定义函数来定义规则。

要基于自定义函数定义规则，请从下拉列表中选择&#x200B;**函数输出**，然后从&#x200B;**函数**&#x200B;选项卡中拖放自定义函数。 自定义函数中定义的复选框数将添加到自适应表单中。

![自定义函数](assets/custom_functions_set_options_new.png)

要创建自定义函数，请参阅规则编辑器中的[自定义函数](#custom-functions)。

要根据表单数据模型定义规则，请执行以下操作：

1. 从下拉列表中选择&#x200B;**服务输出**。
1. 选择数据模型对象。
1. 从&#x200B;**显示值**&#x200B;下拉列表中选择一个数据模型对象属性。 自适应表单中的复选框数派生自数据库中为该属性定义的实例数。
1. 从&#x200B;**保存值**&#x200B;下拉列表中选择一个数据模型对象属性。

![FDM设置选项](assets/fdm_set_options_new.png)

## 了解规则编辑器用户界面 {#understanding-the-rule-editor-user-interface}

规则编辑器提供了一个全面而简单的用户界面来编写和管理规则。 您可以在创作模式下从自适应表单中启动规则编辑器用户界面。

要启动规则编辑器用户界面，请执行以下操作：

1. 在创作模式下打开自适应表单。
1. 选择要为其编写规则的表单对象，然后在组件工具栏中选择![edit-rules](assets/edit-rules.png)。 此时将显示规则编辑器用户界面。

   ![create-rules](assets/create-rules.png)

   此视图中列出了选定表单对象上的任何现有规则。 有关管理现有规则的信息，请参阅[管理规则](#manage-rules)。

1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;以编写新规则。 默认情况下，首次启动规则编辑器时会打开规则编辑器用户界面的可视化编辑器。

   ![规则编辑器UI](assets/rule-editor-ui.png)

让我们详细了解一下规则编辑器UI的每个组件。

### A.组件规则显示 {#a-component-rule-display}

显示自适应表单对象的标题（通过自适应表单对象启动规则编辑器）和当前选定的规则类型。 在上述示例中，规则编辑器从名为Salary的自适应表单对象启动，并且选定的规则类型是When。

### B.表单对象和功能 {#b-form-objects-and-functions-br}

规则编辑器用户界面左侧的窗格包含两个选项卡 — **[!UICONTROL Forms对象]**&#x200B;和&#x200B;**[!UICONTROL 函数]**。

“表单对象”选项卡显示自适应表单中包含的所有对象的分层视图。 它显示对象的标题和类型。 在编写规则时，可以将表单对象拖放到规则编辑器中。 在将对象或函数拖放到占位符中时，在创建或编辑规则时，占位符会自动采用相应的值类型。

应用了一个或多个有效规则的表单对象将标有绿点。 如果应用于表单对象的任意规则无效，则表单对象将标有黄点。

“函数”选项卡包含一组内置函数，例如“总和”、“最小值”、“最大值”、“平均值”、“数目”和“验证表单”。 您可以使用这些函数计算可重复面板和表格行中的值，并在编写规则时在操作和条件语句中使用它们。 但是，您也可以创建[自定义函数](#custom-functions)。

![函数选项卡](assets/functions.png)

>[!NOTE]
>
>您可以在Forms的“对象”和“函数”选项卡中对对象和函数名称和标题执行文本搜索。

在表单对象的左树中，您可以选择表单对象以显示应用于每个对象的规则。 您不仅可以浏览各种表单对象的规则，还可以复制粘贴表单对象之间的规则。 有关详细信息，请参阅[复制粘贴规则](#copy-paste-rules)。

### C.表单对象和功能切换 {#c-form-objects-and-functions-toggle-br}

点击切换按钮，可切换表单对象和功能窗格。

### D.可视规则编辑器 {#d-visual-rule-editor}

可视规则编辑器是规则编辑器用户界面的可视编辑器模式中用于编写规则的区域。 它允许您选择规则类型并相应地定义条件和操作。 在规则中定义条件和操作时，您可以从表单对象和函数窗格中拖放表单对象和函数。

有关使用可视规则编辑器的详细信息，请参阅[编写规则](#write-rules)。

### E.可视代码编辑器切换器 {#e-visual-code-editors-switcher}

表单超级用户组中的用户可以访问代码编辑器。 对于其他用户，代码编辑器不可用。 如果您拥有权限，则可以从可视编辑器模式切换到规则编辑器的代码编辑器模式，反之，可以使用规则编辑器右上方的切换器。 首次启动规则编辑器时，它将在可视编辑器模式下打开。 您可以在可视编辑器模式下编写规则，也可以切换到代码编辑器模式来编写规则脚本。 但请注意，如果修改规则或在代码编辑器中编写规则，则除非清除代码编辑器，否则无法切换回该规则的可视编辑器。

AEM Forms会跟踪您上次用于编写规则的规则编辑器模式。 当您下次启动规则编辑器时，它将在该模式下打开。 但是，您还可以配置默认模式以在指定模式下打开规则编辑器。 为此，请执行以下操作：

1. 转到位于`https://[host]:[port]/system/console/configMgr`的AEM Web控制台。
1. 单击以编辑&#x200B;**[!UICONTROL 自适应表单和交互式通信Web渠道配置]**。
1. 从&#x200B;**[!UICONTROL 默认模式下的规则编辑器]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 可视编辑器]**&#x200B;或&#x200B;**[!UICONTROL 代码编辑器]**

1. 单击&#x200B;**[!UICONTROL 保存]**。

### F.完成和取消按钮 {#f-done-and-cancel-buttons}

**[!UICONTROL 完成]**&#x200B;按钮用于保存规则。您可以保存不完整的规则。 但是，不完整部分无效，因此不会运行。 当您下次从同一表单对象启动规则编辑器时，会列出表单对象中已保存的规则。 您可以在该视图中管理现有规则。 有关详细信息，请参阅[管理规则](#manage-rules)。

使用&#x200B;**[!UICONTROL 取消]**&#x200B;按钮可放弃对规则所做的任何更改并关闭规则编辑器。

## 写入规则 {#write-rules}

您可以使用可视规则编辑器或代码编辑器编写规则。 首次启动规则编辑器时，它将在可视编辑器模式下打开。 您可以切换到代码编辑器模式并编写规则。 但请注意，如果在代码编辑器中编写或修改规则，则除非清除代码编辑器，否则无法切换到该规则的可视编辑器。 当您下次启动规则编辑器时，它将在您最后创建规则时使用的模式下打开。

我们首先看一下如何使用可视编辑器编写规则。

### 使用可视编辑器 {#using-visual-editor}

让我们了解如何使用以下示例表单在可视编辑器中创建规则。

![create-rule-example](assets/create-rule-example.png)

示例贷款申请表中的“贷款要求”部分要求申请人指定其婚姻状况、工资，如果已婚，还须指定其配偶的工资。 根据用户输入，规则将计算贷款资格金额，并显示在贷款资格字段中。 应用以下规则来实施方案：

* 配偶的“薪金”字段仅在婚姻状况为已婚时显示。
* 贷款资格金额为工资总额的50%。

执行以下步骤来编写规则：

1. 首先，根据用户为“婚姻状况”单选按钮选择的选项，编写规则以控制“配偶薪金”字段的可见性。

   以创作模式打开贷款申请表单。 选择&#x200B;**婚姻状况**&#x200B;组件并选择![编辑 — 规则](assets/edit-rules.png)。 接下来，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以启动规则编辑器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   在启动规则编辑器时，默认情况下会选中When规则。 此外，从中启动规则编辑器的表单对象（在本例中为“婚姻状况”）在When语句中指定。

   虽然不能更改或修改所选对象，但可以使用如下所示的规则下拉列表选择其他规则类型。 如果要在其他对象上创建规则，请选择“取消”以退出规则编辑器，然后从所需的表单对象中再次启动该编辑器。

1. 选择&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表并选择&#x200B;**[!UICONTROL 等于]**。 出现&#x200B;**[!UICONTROL 输入字符串]**&#x200B;字段。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在“婚姻状况”单选按钮中，**已婚**&#x200B;和&#x200B;**单身**&#x200B;选项分别分配了&#x200B;**0**&#x200B;和&#x200B;**1**&#x200B;值。 您可以在“编辑”单选按钮对话框的“标题”选项卡中验证分配的值，如下所示。

   规则编辑器中的![单选按钮值](assets/radio-button-values.png)

1. 在规则的&#x200B;**输入字符串**&#x200B;字段中，指定&#x200B;**0**。

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已将条件定义为`When Marital Status is equal to Married`。 接下来，定义此条件为True时要执行的操作。

1. 在Then语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 从“表单对象”选项卡中拖放&#x200B;**放置对象上的** Warbant Salary **字段，或选择此处**&#x200B;字段。 或者，选择&#x200B;**Drop对象或选择此处**&#x200B;字段，然后从弹出菜单中选择&#x200B;**Berpha Salary**&#x200B;字段，该字段列出了表单中的所有表单对象。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

   选择&#x200B;**完成**&#x200B;保存规则。

1. 如果婚姻状况为“单身”，请重复步骤1至5以定义另一个规则来隐藏“配偶薪金”字段。 规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您可以在“配偶薪金”字段编写一个“显示”规则，而不是在“婚姻状况”字段编写两个“何时规则”，以实施相同的行为。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接下来，编写规则以计算贷款资格金额（占总薪金的50%），并在“贷款资格”字段中显示。 要实现此目的，请在贷款资格字段中创建&#x200B;**设置值**。

   在创作模式下，选择&#x200B;**[!UICONTROL 贷款资格]**&#x200B;字段并选择![编辑规则](assets/edit-rules.png)。 接下来，选择&#x200B;**[!UICONTROL 创建]**&#x200B;以启动规则编辑器。

1. 从规则下拉列表中选择&#x200B;**[!UICONTROL 设置规则值]**。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 选择&#x200B;**[!UICONTROL 选择选项]**，并选择&#x200B;**[!UICONTROL 数学表达式]**。打开用于编写数学表达式的字段。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在表达式字段中：

   * 从Forms的“对象”选项卡中，选择或拖放第一个&#x200B;**放置对象中的** Salary **字段，或选择此处**&#x200B;字段。

   * 从&#x200B;**选择运算符**&#x200B;字段中选择&#x200B;**加号**。

   * 从Forms的“对象”选项卡中选择或拖放另一个&#x200B;**拖放对象中的** Berphor Salary **字段，或选择此处**&#x200B;字段。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下来，选择表达式字段周围的突出显示区域，并选择&#x200B;**扩展表达式**。

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在扩展表达式字段中，从&#x200B;**选择运算符**&#x200B;字段中选择&#x200B;**除以**，并从&#x200B;**选择选项**&#x200B;字段中选择&#x200B;**数字**。然后在数字字段中指定&#x200B;**2**。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以从“选择选项”字段中使用组件、函数、数学表达式和属性值来创建复杂表达式。

   接下来，创建一个条件，当该条件返回True时，表达式将执行。

1. 选择&#x200B;**添加条件**&#x200B;以添加When语句。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When语句中：

   * 从Forms对象选项卡中选择或拖放第一个&#x200B;**放置对象中的**&#x200B;婚姻状况&#x200B;**字段，或选择此处**&#x200B;字段。

   * 从&#x200B;**Select Operator**&#x200B;字段中选择i **等于**。

   * 在其他&#x200B;**放置对象中选择String或选择此处**&#x200B;字段，并在&#x200B;**输入字符串**&#x200B;字段中指定&#x200B;**已婚**。

   规则编辑器中的结果如下所示。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

   选择&#x200B;**完成**&#x200B;保存规则。

1. 重复步骤7至12，定义另一条规则，以计算婚姻状况为“单身”的贷款资格。 规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您可以使用设置值规则在您创建的When规则中计算贷款资格，以显示 — 隐藏“配偶薪金”字段。 当“婚姻状况”为“单身”时，生成的合并规则将在规则编辑器中显示如下。
>
>同样，您可以编写合并规则以控制“配偶薪金”字段的可见性，并在婚姻状况为“已婚”时计算贷款资格。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

### 使用代码编辑器 {#using-code-editor}

添加到表单超级用户组的用户可以使用代码编辑器。 规则编辑器会自动为您使用可视编辑器创建的任何规则生成JavaScript代码。 您可以从可视编辑器切换到代码编辑器以查看生成的代码。 但是，如果在代码编辑器中修改规则代码，则无法切换回可视编辑器。 如果更愿意在代码编辑器而不是可视编辑器中编写规则，则可以在代码编辑器中重新编写规则。 可视代码编辑器切换器可帮助您在这两种模式之间切换。

代码编辑器JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，都使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关自适应表单类、事件、对象和公共API的完整列表，请参阅自适应表单的[JavaScript库API参考](https://helpx.adobe.com/cn/experience-manager/6-5/forms/javascript-api/index.html)。

有关在代码编辑器中编写规则的准则的更多信息，请参阅[自适应表单表达式](/help/forms/using/adaptive-form-expressions.md)。

在规则编辑器中编写JavaScript代码时，以下可视提示可帮助您了解结构和语法：

* 语法高亮
* 自动缩进
* 表单对象、函数及其属性的提示和建议
* 自动完成表单组件名称和常用JavaScript功能

![javascriptruleeditor](assets/javascriptruleeditor.png)

#### 规则编辑器中的自定义函数 {#custom-functions}

>[!NOTE]
>
> 自定义函数必须与ECMAScript 5 (ES5)兼容。 Foundation Forms仅支持ES5；不支持使用较新的ECMAScript版本（ES6及更高版本），这可能会导致错误或意外行为。

除了在函数输出下列出的现成函数（如&#x200B;*和*&#x200B;之和）之外，您还可以编写您经常需要的自定义函数。 请确保您编写的函数伴有它上面的`jsdoc`。

需要随附`jsdoc`：

* 如果您需要自定义配置和描述。
* 因为有多种方法可以在`JavaScript,`中声明函数，而注释允许您跟踪这些函数。

有关详细信息，请参阅[usejsdoc.org](https://jsdoc.app/)。

支持的`jsdoc`标记：

* **专用**
语法： `@private`
专用函数未作为自定义函数包含在内。

* **名称**
语法： `@name funcName <Function Name>`
或者`,`您可以使用：`@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`。
  `funcName`是函数的名称（不允许有空格）。
  `<Function Name>`是函数的显示名称。

* **成员**
语法： `@memberof namespace`
将命名空间附加到函数。

* **参数**
语法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`。
显示函数使用的参数。 一个函数可以有多个参数标记，每个参数按其出现顺序对应一个标记。
  `{type}`表示参数类型。 允许的参数类型包括：

   1. 字符串
   1. 数字
   1. 布尔型
   1. 范围

  范围用于引用自适应表单的字段。 当表单使用延迟加载时，您可以使用`scope`访问其字段。 在加载字段时或字段标记为全局时，您可以访问这些字段。

  所有其他参数类型均归入上述参数类型之一。 不支持无。 确保选择以上类型之一。 类型不区分大小写。 参数`name`中不允许空格。`<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **返回类型**
语法： `@return {type}`
或者，您可以使用`@returns {type}`。
添加有关函数的信息，例如其目标。
  {type}表示函数的返回类型。 允许的返回类型包括：

   1. 字符串
   1. 数字
   1. 布尔型

  所有其他退货类型均归入上述任一类型下。 不支持无。 确保选择以上类型之一。 返回类型不区分大小写。

* **此**
语法： `@this currentComponent`

  使用@this引用编写了规则的自适应表单组件。

  以下示例基于字段值。 在以下示例中，规则隐藏了表单中的字段。 `this`的`this.value`部分引用了写入规则的基础自适应表单组件。

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function will be executed.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

>[!NOTE]
>
>使用自定义函数之前的注释进行摘要。 在遇到标记之前，摘要可以扩展到多行。 将大小限制为单个，以便在规则生成器中提供简要说明。

<!--
**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

Perform the following steps to create a client library and add it in the CRX repository.

1. Create a client library. For more information, see [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your adaptive form. It lets you use your custom function as a rule in your form. Perform the following steps to add the client library in your adaptive form.

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **Open**.
1. In the edit mode, select a component, then select ![field-level](assets/field-level.png) &gt; **Adaptive Form Container**, and then select ![cmppr](assets/cmppr.png).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules.png) to open the rule editor.
1. Select **Create Rule**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.
   [ ![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)Select **Done**. Your custom function is added.

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.
-->

您还可以在规则编辑器中使用自定义函数。 有关创建自定义函数的说明，请参阅文章[自适应Forms中的自定义函数](/help/forms/using/create-and-use-custom-functions.md)。

## 管理规则 {#manage-rules}

选择表单对象并选择![edit-rules1](assets/edit-rules1.png)时，会列出该对象上的任何现有规则。 您可以查看标题并预览规则摘要。 此外，您还可以通过UI展开和查看完整的规则摘要、更改规则的顺序、编辑规则以及删除规则。

![list-rules](assets/list-rules.png)

您可以对规则执行以下操作：

* **展开/折叠**：规则列表中的“内容”列显示规则内容。 如果整个规则内容在默认视图中不可见，请选择![expand-rule-content](assets/expand-rule-content.png)以展开它。

* **重新排序**：您创建的任何新规则都栈叠在规则列表的底部。 规则将从上到下执行。 顶部的规则首先运行，然后是相同类型的其他规则。 例如，如果您分别从顶部开始在第一个、第二个、第三个和第四个位置具有When、Show、Enable和When规则，则顶部的When规则将首先执行，然后是第四个位置的When规则。 然后，将执行显示和启用规则。
您可以通过点按![排序规则](assets/sort-rules.png)来更改规则的顺序，也可以将其拖放到列表中的所需顺序。

* **编辑**：要编辑规则，请选中规则标题旁边的复选框。 将显示用于编辑和删除规则的其他选项。 选择&#x200B;**编辑**&#x200B;以在可视或代码编辑器模式下在规则编辑器中打开选定的规则，具体取决于用于创建规则的模式。

* **删除**：要删除规则，请选择该规则并选择&#x200B;**删除**。

* **启用/禁用**：您可能需要临时暂停规则的使用。 您可以选择一个或多个规则，然后在操作工具栏中选择禁用以禁用这些规则。 如果禁用某个规则，则它不会在运行时执行。 要启用已禁用的规则，可以选择该规则并选择操作工具栏中的启用。 规则的状态列显示规则是启用还是禁用。

![disablerule](assets/disablerule.png)

## 复制粘贴规则 {#copy-paste-rules}

您可以将规则从一个字段复制粘贴到其他类似字段，以节省时间。

要复制粘贴规则，请执行以下操作：

1. 选择要从中复制规则的表单对象，然后在组件工具栏中选择![editrule](assets/editrule.png)。 此时将显示规则编辑器用户界面，其中选定了表单对象，并显示现有规则。

   ![复制规则](assets/copyrule.png)

   有关管理现有规则的信息，请参阅[管理规则](#manage-rules)。

1. 选中规则标题旁边的复选框。 此时会显示用于管理规则的其他选项。 选择&#x200B;**复制**。

   ![复制规则2](assets/copyrule2.png)

1. 选择要将规则粘贴到的其他表单对象，然后选择&#x200B;**粘贴**。 此外，您可以编辑规则以对其进行更改。

   >[!NOTE]
   >
   >仅当表单对象支持复制的规则事件时，才能将规则粘贴到另一个表单对象。 例如，按钮支持click事件。 您可以将包含点击事件的规则粘贴到按钮，但不能粘贴到复选框。

1. 选择&#x200B;**完成**&#x200B;保存规则。

## 嵌套表达式 {#nestedexpressions}

规则编辑器允许您使用多个AND和OR运算符创建嵌套规则。 您可以在规则中混合使用多个AND和OR运算符。

以下是嵌套规则的示例，该规则会在满足所需条件时向用户显示有关儿童监护权资格的消息。

![complexexpression](assets/complexexpression.png)

您还可以拖放规则中的条件以进行编辑。 选择并将鼠标悬停在条件前面的句柄（![句柄](assets/handle.png)）上。 指针变为手形符号后（如下所示），将条件拖放到规则中的任意位置。 规则结构会发生变化。

![拖放](assets/drag-and-drop.png)

## 日期表达式条件 {#dateexpression}

规则编辑器允许您使用日期比较来创建条件。

以下是一个示例条件，当房屋抵押贷款已被抵押时，该条件会显示一个静态文本对象，用户通过填写日期字段来表示该条件。

当用户填写的财产抵押日期为过去时，自适应表单会显示有关收入计算的说明。 以下规则将用户填写的日期与当前日期进行比较，如果用户填写的日期早于当前日期，则表单将显示文本消息（名为Income）。

![dateexpressioncondition](assets/dateexpressioncondition.png)

如果填写日期早于当前日期，则表单会显示如下文本消息（收入）：

![dateexpressionconditionmet](assets/dateexpressionconditionmet.png)

## 数字比较条件 {#number-comparison-conditions}

规则编辑器可让您创建比较两个数字的条件。

以下是一个示例条件，当申请人在其当前地址停留的月数小于36时，该条件将显示静态文本对象。

![numbercomparisoncondition](assets/numbercomparisoncondition.png)

当用户表示他在当前的居住地址居住不到36个月时，表格会显示通知，表明可能需要额外的居住证明。

![additionalproofrequested](assets/additionalproofrequested.png)

## 规则编辑器对现有脚本的影响 {#impact-of-rule-editor-on-existing-scripts}

在AEM 6.1 Forms功能包1之前的AEM Forms版本中，表单作者和开发人员用于在“编辑组件”对话框的“脚本”选项卡中编写表达式，以将动态行为添加到自适应表单。 “脚本”选项卡现在由规则编辑器替换。

必须在脚本选项卡中编写的任何脚本或表达式都可在规则编辑器中使用。 虽然无法在可视编辑器中查看或编辑脚本，但如果您是表单超级用户组的一部分，则可以在代码编辑器中编辑脚本。

## 示例规则 {#example}

### 调用表单数据模型服务 {#invoke}

考虑一个Web服务`GetInterestRates`，它将贷款金额、保有权和申请人的信用得分作为输入并返回包括EMI金额和利率的贷款计划。 使用Web服务作为数据源创建表单数据模型。 向表单模型添加数据模型对象和`get`服务。 该服务将显示在表单数据模型的“服务”选项卡中。 然后，创建一个自适应表单，其中包含数据模型对象中的字段，以捕获贷款金额、使用期和信用评分的用户输入。 添加触发Web服务获取计划详细信息的按钮。 输出将填充到相应的字段中。

以下规则显示了如何配置“调用服务”操作以完成示例场景。

![example-invoke-services](assets/example-invoke-services.png)

使用自适应表单规则调用表单数据模型服务

>[!NOTE]
>
>如果输入的类型为数组，则支持数组的字段在“输出”下拉部分下可见。

### 使用When规则触发多个操作 {#triggering-multiple-actions-using-the-when-rule}

在贷款申请表中，您要获取贷款申请人是否为现有客户。 根据用户提供的信息，客户ID字段应显示或隐藏。 此外，如果用户是现有客户，则还需要将焦点设置为“客户ID”字段。 贷款申请表包括以下组成部分：

* 单选按钮&#x200B;**您是现有Geometrixx客户吗？**&#x200B;提供“是”和“否”选项。 “是”的值为&#x200B;**0**，“否”的值为&#x200B;**1**。

* 用于指定客户ID的文本字段&#x200B;**Geometrixx客户ID**。

在用于实施此行为的单选按钮上编写When规则时，该规则在可视规则编辑器中如下所示。  ![when-rule-example](assets/when-rule-example.png)

可视编辑器中的规则

在示例规则中，When部分中的语句是条件，当返回True时，该条件将执行Then部分中指定的操作。

该规则在代码编辑器中如下所示。

![when-rule-example-code](assets/when-rule-example-code.png)

代码编辑器中的规则

### 在规则中使用函数输出 {#using-a-function-output-in-a-rule}

在采购订单表单中，您有下表，用户将在其中填写订单。 在此表中：

* 第一行是可重复的，因此用户可以订购多个产品并指定不同的数量。 其元素名称为`Row1`。
* 可重复行的“产品数量”列中的单元格的标题为“数量”。 此单元格的元素名称为`productquantity`。
* 表中的第二行是不可重复的，该行中“产品数量”列中的单元格的标题为“总数量”。

![example-function-table](assets/example-function-table.png)

**A.**&#x200B;行1 **B.**&#x200B;数量&#x200B;**C.**&#x200B;总数量

现在，您要在所有产品的“产品数量”列中添加指定数量，并在“总数量”单元格中显示总和。 可通过在“总数量”单元格中编写“设置值”规则来实现此目的，如下所示。

![example-function-output](assets/example-function-output.png)

可视编辑器中的规则

该规则在代码编辑器中如下所示。

![example-function-output-code](assets/example-function-output-code.png)

代码编辑器中的规则

### 使用表达式验证字段值 {#validating-a-field-value-using-expression}

在上一个示例中说明的采购订单表单中，您需要限制用户订购任何数量超过此10000价的产品。 为此，您可以编写验证规则，如下所示。

![example-validate](assets/example-validate.png)

可视编辑器中的规则

该规则在代码编辑器中如下所示。

![example-validate-code](assets/example-validate-code.png)

代码编辑器中的规则
