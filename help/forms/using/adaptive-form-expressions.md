---
title: 自适应表单表达式
description: 使用自适应表单表达式可添加自动验证、计算并打开或关闭部分的可见性。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2781'
ht-degree: 2%

---

# 自适应表单表达式{#adaptive-form-expressions}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

自适应表单为具有动态脚本编写功能的最终用户提供经过优化和简化的表单填写体验。 它允许您编写表达式以添加各种行为，如动态显示/隐藏字段和面板。 它还允许您添加计算字段、使字段只读、添加验证逻辑等。 动态行为基于用户输入或预填充的数据。

JavaScript是自适应表单的表达式语言。 所有表达式都是有效的JavaScript表达式，都使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关自适应表单类、事件、对象和公共API的完整列表，请参阅[自适应表单的JavaScript库API参考。](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/index.html)

## 编写表达式的最佳实践 {#best-practices-for-writing-expressions}

* 在编写表达式时，要访问字段和面板，您可以使用字段或面板的名称。 要访问字段的值，请使用value属性。 例如，`field1.value`
* 为表单中的字段和面板使用唯一名称。 它有助于避免在编写表达式时所使用的字段名称发生任何可能的冲突。
* 编写多行表达式时，请使用分号终止语句。

## 涉及重复面板的表达式的最佳实践 {#best-practices-for-expressions-involving-repeating-panel}

重复面板是使用脚本API或预填充数据动态添加或移除的面板的实例。 有关使用重复面板的详细信息，请参阅[创建具有可重复分区的表单](/help/forms/using/creating-forms-repeatable-sections.md)。

* 要创建重复面板，请在面板对话框中，打开设置，并将最大计数字段的值设置为大于1。
* 面板重复设置的最小计数值可以是一个或多个，但不能超过最大计数值。
* 当表达式引用重复面板的字段时，表达式中的字段名称解析为最接近的重复元素。
* 自适应表单提供了一些特殊函数来简化可重复面板的计算，例如sum、count、min、max、filter等。 有关函数的完整列表，请参阅[自适应表单的JavaScript库API参考](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/index.html)
* 用于处理重复面板的实例的API包括：

   * 要添加面板实例： `panel1.instanceManager.addInstance()`
   * 获取面板重复索引： `panel1.instanceIndex`
   * 获取面板的instanceManager： `_panel1 or panel1.instanceManager`
   * 要删除面板的实例： `_panel1.removeInstance(panel1.instanceIndex)`

## 表达式类型 {#expression-types}

在自适应表单中，您可以编写表达式以添加动态显示/隐藏字段和面板等行为。 您还可以编写表达式以添加计算字段、使字段只读、验证逻辑等。 自适应表单支持以下表达式：

* **[访问表达式](#access-expression-enablement-expression)**：启用/禁用字段。
* **[计算表达式](#calculate-expression)**：用于自动计算字段的值。
* **[单击表达式](#click-expression)**：处理按钮的单击事件操作。
* **[初始化脚本](#initialization-script)：**&#x200B;在初始化字段时执行操作。
* **[选项表达式](#options-expression)**：用于动态填充下拉列表。
* **[摘要表达式](#summary)**：用于动态计算折叠的标题。
* **[验证表达式](#validate-expression)**：验证字段。
* **[值提交脚本](#value-commit-script)：**，用于在字段值更改后更改表单组件。
* **[可见性表达式](#visibility-expression)**：用于控制字段和面板的可见性。
* **[步骤完成表达式](#step-completion-expression)**：用于防止用户进入向导的下一步。

### 访问表达式（启用表达式） {#access-expression-enablement-expression}

您可以使用访问表达式来启用或禁用字段。 如果表达式使用字段的值，则每当字段的值更改时，都会重新触发表达式。

**应用于**：字段

**返回类型**：表达式返回布尔值，表示该字段是启用还是禁用。 **true**&#x200B;表示该字段已启用，**false**&#x200B;表示该字段已禁用。

**示例**：要仅在&#x200B;**field1**&#x200B;的值设置为&#x200B;**X**&#x200B;时启用字段，访问表达式为： `field1.value == "X"`

### 计算表达式 {#calculate-expression}

计算表达式用于使用表达式自动计算字段的值。 通常，此类表达式使用其他字段的值属性。 例如，`field2.value + field3.value`。每当`field2`或`field3`的值更改时，就会重新触发表达式并重新计算该值。

**应用于**：字段

**返回类型**：表达式返回与显示表达式结果的字段（例如，小数）兼容的值。

**示例**：用于显示&#x200B;**field1**&#x200B;中两个字段之和的计算表达式是：
`field2.value + field3.value`

### 单击表达式 {#click-expression}

click表达式处理对按钮的单击事件执行的操作。 GuideBridge开箱即用地提供API来执行各种功能，例如提交和验证与单击表达式一起使用的功能。 有关API的完整列表，请参阅[GuideBridge API。](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)

**应用于**：按钮字段

**返回类型**： click表达式未返回任何值。 如果有任何表达式返回值，则忽略该值。

**示例**：若要在值为&#x200B;**AEM Forms**&#x200B;的按钮的点击操作中填充文本框&#x200B;**textbox1**，该按钮的点击表达式为`textbox1.value="AEM Forms"`

### 初始化脚本 {#initialization-script}

初始化自适应表单时会触发初始化脚本。 根据具体情况，初始化脚本的行为如下所示：

* 在呈现自适应表单时没有数据预填充，则初始化脚本在表单初始化后运行。
* 当自适应表单使用数据预填充呈现时，脚本在预填充操作完成后运行。
* 当触发自适应表单的服务器端重新验证时，执行初始化脚本。

**应用于：**&#x200B;字段和面板

**返回类型：**&#x200B;初始化脚本表达式未返回任何值。 如果有任何表达式返回值，则忽略该值。

**示例：**&#x200B;在数据预填充方案中，要在字段的值保存为null时用默认值`'Adaptive Forms'`填充字段，初始化脚本表达式为：
`if(this.value==null) this.value='Adaptive Forms';`

### 选项表达式 {#options-expression}

选项表达式用于动态填充下拉列表字段的选项。

**应用于**：下拉列表字段

**返回类型**：选项表达式返回字符串值的数组。 每个值都可以是一个简单的字符串，如&#x200B;**Male**，也可以是键=值对格式，如&#x200B;**1=Male**

**示例**：要根据其他字段的值填充字段的值，请提供简单的选项表达式。 例如，要根据在另一个字段中表示的&#x200B;**婚姻状况**&#x200B;填充字段&#x200B;**Number of Kids**，表达式为：

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

每当&#x200B;**wirtral_status**&#x200B;字段的值更改时，就会重新触发表达式。 您还可以从REST服务填充下拉列表。 有关详细信息，请参阅[动态填充下拉列表](../../forms/using/dynamically-populate-dropdowns.md)。

### 摘要表达式 {#summary}

摘要表达式可动态计算折叠布局面板的子面板的标题。 您可以在规则中指定摘要表达式，该表达式使用表单字段或自定义逻辑来评估标题。 表达式在表单初始化时执行。 如果您预填表单，则表达式会在预填数据后或表达式中使用的依赖字段的值发生更改时执行。

摘要表达式通常用于重复折叠布局面板的子面板，以便为每个子面板提供有意义的标题。

**适用于：**&#x200B;个面板，这些面板是布局配置为折叠的面板的直接子面板。

**返回类型：**&#x200B;表达式返回一个字符串，该字符串将成为折叠的标题。

**示例：** &quot;Account number ： &quot; + textbox1.value

### 验证表达式 {#validate-expression}

验证表达式用于使用给定表达式验证字段。 通常，此类表达式使用正则表达式以及字段值来验证字段。 将检索表达式，并在字段值发生任何更改时重新计算字段的验证状态。

**应用于**：字段

**返回类型**：表达式返回代表字段验证状态的布尔值。 值&#x200B;**false**&#x200B;表示该字段无效，**true**&#x200B;表示该字段有效。
**示例**：对于表示UK邮政编码的字段，验证表达式为：

(**this.value**&#x200B;和&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

在上例中，如果非空值与模式不匹配，表达式将返回&#x200B;**false**&#x200B;以指示该字段无效。

>[!NOTE]
>
>如果您为非必填或必填字段编写验证表达式，则无论字段的可见性状态如何，都将计算该表达式。 要停止验证隐藏字段，请将Initialization或Value Commit脚本中的validationsDisabled属性设置为true。 例如，`this.validationsDisabled=true`

### 值提交脚本 {#value-commit-script}

值提交脚本在以下情况下触发：

* 用户从UI更改字段的值。
* 字段的值会因其他字段中的更改而以编程方式更改。

**应用于：**&#x200B;字段

**返回类型：**&#x200B;值提交脚本表达式未返回任何值。 如果有任何表达式返回值，则忽略该值。

**示例：**&#x200B;若要在提交时将在字段中输入的字母的大小写转换为大写，值commit表达式为：
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>以编程方式更改字段的值时，您可以禁用值提交脚本的执行。 为此，请转到https://&#39;[服务器]：[端口]&#39;/system/console/configMgr并将&#x200B;**兼容性自适应Forms版本**&#x200B;更改为&#x200B;**AEM Forms 6.1**。 此后，仅当用户从UI更改字段的值时执行值提交脚本。

### 可见性表达式 {#visibility-expression}

“可见性”表达式用于控制字段/面板的可见性。 通常，可见性表达式使用字段的值属性，每当该值发生更改时都会重新触发。

**应用于**：字段和面板

**返回类型**：表达式返回布尔值，表示字段/面板是否可见。 **false**&#x200B;表示字段或面板不可见，而true表示字段或面板可见。

**示例**：对于仅当&#x200B;**field1**&#x200B;的值设置为&#x200B;**Male**&#x200B;时才变为可见的面板，可见性表达式为： `field1.value == "Male"`

### 步骤完成表达式 {#step-completion-expression}

步骤完成表达式用于防止用户进入向导布局的下一步。 当面板具有向导布局（一种每次显示一个步骤的多步表单）时，将使用这些表达式。 仅当当前部分中的所有必需值均已填写且有效时，用户才能移至下一步、面板或子部分。

**适用于**：项目布局设置为向导的面板。

**返回类型**：表达式返回布尔值，表示当前面板是否有效。 **True**&#x200B;表示当前面板有效，用户可以导航到下一个面板。

**示例**：在以各种面板组织的表单中，导航到下一个面板之前，将验证当前面板。 在这种情况下，将使用步骤完成表达式。 通常，这些表达式使用GuideBridge验证API。 步骤完成表达式的示例如下：
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## 自适应表单中的验证 {#validations-in-adaptive-form}

有多种方法可以将字段验证添加到自适应表单。 如果在字段中添加了验证检查，则&#x200B;**True**&#x200B;表示在该字段中输入的值有效。 **False**&#x200B;表示值无效。 如果您在字段中执行进出选项卡操作，则不会生成错误消息。

在字段中添加验证的方法包括：

### 必填 {#required}

若要将某个组件设为必需，在该组件的&#x200B;**编辑**&#x200B;对话框中，您可以选择选项&#x200B;**标题和文本>必需**。 您还可以添加相应的&#x200B;**必需消息**（可选）。

### 验证模式 {#validation-patterns}

字段有多个现成的验证模式。 要选择验证模式，请在组件的&#x200B;**编辑**&#x200B;对话框中，找到&#x200B;**模式**&#x200B;部分并选择&#x200B;**模式**。 您可以在&#x200B;**模式**&#x200B;文本框中创建自己的自定义验证模式。 仅当填写的数据符合验证模式时，才返回验证状态&#x200B;**True**，否则返回&#x200B;**False**。 要编写您自己的自定义验证模式，请参阅对HTML5表单的[Picture子句支持](/help/forms/using/picture-clause-support.md)。

### 验证表达式 {#validation-expressions}

字段的验证也可以使用不同字段上的表达式来计算。 这些表达式写入组件的&#x200B;**编辑**&#x200B;对话框的&#x200B;**脚本**&#x200B;选项卡的&#x200B;**验证脚本**&#x200B;字段中。 字段的验证状态取决于表达式返回的值。 有关如何编写此类表达式的信息，请参阅[验证表达式](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p)。

## 附加信息 {#additional-information}

### 使用字段显示格式 {#using-field-display-format}

显示格式可用于以不同的格式显示数据。 例如，您可以使用显示格式显示带有连字符的电话号码、邮政编码格式或日期选取器。 可以从组件的“编辑”对话框的&#x200B;**模式**&#x200B;部分中选择这些显示模式。 您可以编写与上述验证模式类似的自定义显示模式。

### GuideBridge - API和事件 {#guidebridge-apis-and-events}

GuideBridge是API的集合，可用于与浏览器内存模型中的自适应表单交互。 有关指南Bridge API、类方法、公开事件的详细介绍，请参阅[自适应表单的JavaScript库API参考。](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/index.html)

>[!NOTE]
>
>建议不要在表达式中使用GuideBridge事件侦听器。

#### 在各种表达式中使用GuideBridge {#guidebridge-usage-in-various-expressions}

* 要重置表单字段，您可以在按钮的点击表达式上触发`guideBridge.reset()` API。 同样，有一个提交API可以调用为click表达式&#x200B;`guideBridge.submit()`**。**

* 您可以使用`setFocus()` API在各种字段或面板中设置焦点（对于面板焦点自动设置为第一个字段）。 `setFocus()`提供多种导航选项，例如跨面板导航、上一个/下一个遍历、将焦点设置为特定字段等等。 例如，要移到下一个面板，您可以使用： `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* 要验证自适应表单或其特定面板，请使用`guideBridge.validate(errorList, somExpression).`

#### 在表达式外部使用GuideBridge  {#using-guidebridge-outside-expressions-nbsp}

您还可以在表达式之外使用GuideBridge API。 例如，您可以使用GuideBridge API设置托管自适应表单的页面HTML与表单模型之间的通信。 此外，您还可以设置来自托管表单的Iframe父级的值。

要将GuideBridge API用于上述示例，请捕获GuideBridge的一个实例。 要捕获实例，请侦听`window`对象的`bridgeInitializeStart`事件：

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>在AEM中，最好在clientLib中编写代码并将其包含在页面（页面的header.jsp或footer.jsp）中

要在初始化表单后使用GuideBridge（调度`bridgeInitializeComplete`事件），请使用`window.guideBridge`获取GuideBridge实例。 您可以使用`guideBride.isConnected` API检查GuideBridge初始化状态。

#### GuideBridge事件 {#guidebridge-events}

GuideBridge还为托管页面上的外部脚本提供了某些事件。 外部脚本可以侦听这些事件并执行各种操作。 例如，每当表单中的用户名发生更改时，页面标题中显示的名称也会更改。 有关此类事件的更多详细信息，请参阅[自适应表单的JavaScript库API参考。](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javascript-api/GuideBridge.html)

使用以下代码注册处理程序：

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### 为字段创建自定义模式 {#creating-custom-patterns-for-a-field}

如上所述，自适应表单允许作者提供验证模式或显示格式。 除了使用开箱即用模式之外，您还可以为自适应表单组件定义可重用的自定义模式。 例如，您可以定义文本字段或数字字段。 定义后，可在指定类型组件的所有表单中使用这些模式。 例如，您可以为文本字段创建自定义模式，并在其自适应表单的文本字段中使用该模式。 您可以通过访问组件的“编辑”对话框中的“模式”部分来选择自定义模式。 有关模式定义或格式的详细信息，请参阅HTML5表单[&#128279;](/help/forms/using/picture-clause-support.md)的Picture子句支持。

执行以下步骤可为特定字段类型创建自定义模式，并将其重复用于相同类型的其他字段：

1. 在创作实例上导航到CRXDE Lite。
1. 创建一个文件夹以保留您的自定义模式。 在/apps目录下，创建类型为sling：folder的节点。 例如，创建名为`customPatterns`的节点。 在此节点下，创建另一个类型为`nt:unstructed`的节点并将其命名为`textboxpatterns`。 此节点包含要添加的各种自定义模式。
1. 打开已创建节点的属性选项卡。 例如，打开`textboxpatterns`的“属性”选项卡。 将`guideComponentType`属性添加到此节点，并将其值设置为&#x200B;*fd/af/components/formatter/guideTextBox*。

1. 此属性的值因要定义模式的字段而异。 对于数值字段，`guideComponentType`属性的值为&#x200B;*fd/af/components/formatter/guideNumericBox*。 日期选取器字段的值为&#x200B;*fd/af/components/formatter/guideDatepicker*。
&quot;
1. 您可以通过为`textboxpatterns`节点分配属性来添加自定义模式。 添加具有名称（例如，`pattern1`）的属性，并将其值设置为要添加模式。 例如，添加值为Fax=text{99-999-9999999}的属性`pattern1`。 该模式适用于您在自适应Forms中使用的所有文本框。

   ![在CrxDe中为字段创建自定义模式](assets/creating-custom-patterns.png)

   创建自定义模式
