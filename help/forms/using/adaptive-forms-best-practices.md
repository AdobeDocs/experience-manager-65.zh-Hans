---
title: 使用自适应表单的最佳实践
description: 介绍设置AEM Forms项目、开发自适应表单和优化AEM Forms系统性能的最佳实践。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components,Core Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 6ec4eca0c0ad5ecfe18ffc766e6415a0f48506a9
workflow-type: tm+mt
source-wordcount: '5963'
ht-degree: 0%

---

# 使用自适应表单的最佳实践 {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> Adobe建议使用现代的、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)  用于[创建新的自适应Forms](/help/forms/using/create-an-adaptive-form-core-components.md)  或[将自适应Forms添加到AEM Sites页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。 这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

## 概述 {#overview}

Adobe Experience Manager (AEM)表单可帮助您将复杂的交易转换为简单、愉快的数字体验。 但是，它需要齐心协力实施、构建、执行和维持高效且富有成效的AEM Forms生态系统。

本文档提供了表单管理员、作者和开发人员在使用AEM Forms（尤其是自适应表单组件）时可以从中受益的准则和建议。 该文档讨论了从设置表单开发项目到配置、自定义、创作和优化AEM Forms的最佳实践。 这些最佳做法共同为AEM Forms生态系统的整体性能作出贡献。

此外，对于一般AEM最佳实践，以下是一些推荐的读物：

* [最佳实践：部署和维护AEM](/help/sites-deploying/best-practices.md)
* [最佳实践：创作内容](/help/sites-authoring/best-practices.md)
* [最佳实践：管理AEM](/help/sites-administering/administer-best-practices.md)
* [最佳实践：开发解决方案](/help/sites-developing/best-practices.md)

## 设置和配置AEM Forms {#set-up-and-configure-aem-forms}

### 设置表单开发项目 {#setting-up-forms-development-project}

简化和标准化的项目结构可以显着减少开发和维护工作。 Apache Maven是用于构建AEM项目的开源工具。

* 使用Apache Maven `aem-project-archetype`创建和管理AEM项目的结构。 它可为您的AEM项目创建推荐的结构和模板。 此外，它还提供构建自动化和更改控制系统，以帮助管理项目。

   * 使用maven `archetype:generate`命令生成初始结构。
   * 使用maven `eclipse:eclipse`命令生成eclipse项目文件并将项目导入eclipse。

有关详细信息，请参阅[如何使用Apache Maven构建AEM项目](/help/sites-developing/ht-projects-maven.md)。

* FileVault工具或VLT可帮助您将CRX或AEM实例的内容映射到您的文件系统。 它提供变更控制管理操作，例如AEM项目内容的签入和签出。 请参阅[如何使用VLT工具](/help/sites-developing/ht-vlttool.md)。

* 如果您使用集成了Eclipse的开发环境，则可以使用AEM开发人员工具将Eclipse IDE与AEM实例无缝集成，以创建AEM应用程序。 有关详细信息，请参阅[适用于Eclipse的AEM开发人员工具](/help/sites-developing/aem-eclipse.md)。

* 请勿在/libs文件夹中存储任何内容或进行任何修改。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 在创建包以移动内容时，请确保包过滤器路径正确，并且只引用所需路径。

* 请勿在/libs文件夹中存储任何内容或进行任何修改。 在/app文件夹中创建叠加以扩展或覆盖默认功能。

* 为软件包定义正确的依赖关系，以强制预先确定的安装顺序/顺序。

* 请勿在/libs或/apps中创建任何可引用的节点。

### 规划创作环境 {#planning-for-authoring-environment}

设置AEM项目后，定义用于创作和自定义自适应表单模板和组件的策略。

* 自适应表单模板是一种专门的AEM页面，用于定义自适应表单的结构和页脚信息。 模板具有预配置的自适应表单布局、样式和基本结构。 AEM Forms提供了可用于创作自适应表单的开箱即用模板和组件。 但是，您可以根据需要创建自定义模板和组件。 建议收集在自适应表单中所需的其他模板和组件的要求。 有关详细信息，请参阅[自定义自适应表单和组件](/help/forms/using/adaptive-forms-best-practices.md#customize-components)。
* 建议使用表单管理器用户界面而不是CRX包管理器用户界面上传表单包，因为通过CRX包管理器上传包有时可能会导致异常。
* AEM Forms允许您基于以下表单模型创建自适应表单。 表单模型用作表单与AEM系统之间数据交换的接口，并为自适应表单内外的数据流提供基于XML的结构。 此外，表单模型以模式和XFA约束的形式对自适应表单施加规则和约束。

   * **无**：使用此选项创建的自适应表单不使用任何表单模型。 从此类表单生成的数据 XML 具有带字段和相应值的平面结构。
   * **XML或JSON架构**： XML和JSON架构表示组织中的后端系统生成或使用数据的结构。 您可以将架构关联到自适应表单，并使用其元素将动态内容添加到自适应表单。 架构的元素在内容浏览器的数据模型对象选项卡中可用，用于创作自适应表单。 您可以拖放架构元素来构建表单。
   * **XFA表单模板**：如果您在基于XFA的HTML5表单中有投资，则它是理想的表单模型。 它提供了一种将您的基于XFA的表单转换为自适应表单的直接方法。 任何现有XFA规则都会保留在关联的自适应表单中。 生成的自适应表单支持XFA构造，例如验证、事件、属性和模式。
   * **表单数据模型**：如果您希望集成后端系统(如数据库、Web服务和AEM用户配置文件)以预填充自适应表单并将提交的表单数据写回后端系统，则它是首选表单模型。 利用表单数据模型编辑器，可在可用于创建自适应表单的表单数据模型中定义和配置实体和服务。 有关详细信息，请参阅[AEM Forms数据集成](/help/forms/using/data-integration.md)。

请务必仔细选择不仅适合您的要求，而且能够扩大您对XFA和XSD资产（如果有）的现有投资的数据模型。 使用XSD模型创建表单模板，因为生成的XML包含架构定义的每个XPATH的数据。 使用XSD模型作为表单数据模型的默认选择也很有帮助，因为它将表单设计与处理和使用数据的后端系统分离，并且由于表单字段的一对一映射，它提高了表单的性能。 此外，还可以将该字段的BindRef设置为其数据值在XML中的XPATH。

有关详细信息，请参阅[创建自适应表单](/help/forms/using/creating-adaptive-form.md)。

* 自适应表单中包含一些常见部分。 您可以标识这些内容并定义策略以促进内容重用。 通过自适应表单，您可以创建独立的片段并在各个表单中重复使用。 您还可以将自适应表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的表单中。 它有助于减少创作时间并确保表单之间的一致性。 此外，使用片段使自适应表单变得轻量级，从而改进了创作体验，尤其是大型表单的创作体验。 有关详细信息，请参阅[自适应表单片段](/help/forms/using/adaptive-form-fragments.md)。

### 自定义自适应表单和组件 {#customize-components}

* AEM Forms提供了可用于创建自适应表单的现成自适应表单模板。 您还可以创建自己的模板。 AEM提供静态和可编辑的模板。

   * 静态模板由开发人员定义和配置。
   * 可编辑模板由作者使用模板编辑器创建。 利用模板编辑器，可在模板中定义基本结构和初始内容。 结构层中的任何修改都会反映在使用该模板的所有表单中。 初始内容可包括预配置的主题、预填充服务、提交操作等。 但是，可以使用表单编辑器为表单修改这些设置。 有关详细信息，请参阅[自适应表单模板](/help/forms/using/template-editor.md)。

* 若要设置特定字段或面板实例的样式，请使用[内联样式](/help/forms/using/inline-style-adaptive-forms.md)。 或者，您可以在CSS文件中定义类，并在组件的CSS Class属性中指定类名称。
* 在组件中包含客户端库，以便在使用该组件的自适应表单或片段中始终应用样式。 有关详细信息，请参阅[创建自适应表单页面组件](/help/forms/using/custom-adaptive-forms-templates.md)。
* 通过在自适应表单容器属性的CSS文件路径字段中指定客户端库的路径，应用客户端库中定义的样式来选择自适应表单。
* 要创建样式的客户端库，您可以在主题编辑器基本clientlib中或表单容器属性中配置自定义CSS文件。
* 自适应表单提供面板布局（如响应式、选项卡式、折叠和向导）以控制表单组件在面板中的布局方式。 您可以创建自定义面板布局，并使其可供表单作者使用。 有关详细信息，请参阅[为自适应表单创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md)。
* 您还可以自定义特定的自适应表单组件，如字段和面板布局。

   * 使用AEM的[叠加](/help/sites-developing/overlays.md)功能修改组件的副本。 不建议修改默认组件。
   * 要在/libs中自定义现成自适应表单组件的布局，除[默认布局](/help/forms/using/layout-capabilities-adaptive-forms.md)之外，还[创建自定义布局组件](/help/forms/using/custom-layout-components-forms.md)。
   * 通过创建自定义小部件或外观引入自定义交互。 不建议修改默认组件。 有关详细信息，请参阅[外观框架](/help/forms/using/introduction-widgets.md)。

* 有关处理PII数据的建议，请参阅[处理个人身份信息](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)。

### 创建表单模板

您可以使用&#x200B;**配置浏览器**&#x200B;中启用的表单模板创建自适应表单。 要启用表单模板，请参阅[创建自适应表单模板](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en)。

表单模板也可以从在另一台作者计算机上创建的自适应表单包上传。 通过安装[aemforms-references-*包](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en)，可以使用表单模板。 建议的一些最佳实践包括：

* 仅作者建议使用&#x200B;**nosamplecontent**&#x200B;运行模式，而不建议发布节点使用。
* 仅通过创作节点创作自适应表单、主题、模板或云配置等资产，这些节点可在配置的发布节点发布。
有关详细信息，请参阅[发布和取消发布表单和文档](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* 创作和发布需要Forms附加组件包来支持文档服务操作；因此，它可以被视为依赖项。
如果只需要Forms相关的示例模板、主题和DOR包，则可以从[aemforms-references-*包](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)下载它们。

有关详细信息，请参阅[自适应表单创作简介](/help/forms/using/introduction-forms-authoring.md)中的最佳实践。

## 创作自适应表单 {#author-adaptive-forms}

### 使用触控优化的UI进行创作 {#using-touch-optimized-ui-for-authoring}

* 使用侧栏中的对象浏览器快速访问表单层次结构中较深的字段。 您可以使用搜索框搜索表单或对象树中的对象，以便从一个对象导航到另一个对象。
* 若要在侧栏的组件浏览器中查看和编辑组件的属性，请选择该组件，然后单击![cmppr-1](assets/cmppr-1.png)。 也可以双击组件以在属性浏览器中查看其属性。
* 使用键盘快捷键可对表单执行快速操作。 请参阅[AEM Forms键盘快捷键](/help/forms/using/keyboard-shortcuts.md)。

* 建议仅在自适应表单页面中使用自适应表单组件。 组件依赖其父层次结构。 因此，请勿在AEM页面中使用它们。

另请参阅[自适应表单创作简介](/help/forms/using/introduction-forms-authoring.md)中的组件描述和最佳实践。

### 在自适应表单中使用规则 {#using-rules-in-adaptive-forms}

AEM Forms提供了一个[规则编辑器](/help/forms/using/rule-editor.md)，可让您创建规则以将动态行为添加到自适应表单组件。 使用这些规则，您可以评估条件并触发组件上的操作，例如显示或隐藏字段、计算值、动态更改下拉列表等。

规则编辑器提供了用于编写规则的可视编辑器和代码编辑器。 使用代码编辑器模式编写规则时，请考虑以下事项：

* 为表单字段和组件使用有意义、唯一的名称，以避免在编写规则时可能产生的任何冲突。
* 对组件使用`this`运算符以在规则表达式中引用自身。 这可确保即使组件名称发生更改，规则仍保持有效。 例如 `field1.valueCommit script: this.value > 10`。

* 引用其他表单组件时，请使用组件名称。 使用`value`属性获取字段或组件的值。 例如 `field1.value`。

* 按相对唯一层次结构引用组件以避免任何冲突。 例如 `parentName.fieldName`。

* 处理复杂或常用的规则时，请考虑将业务逻辑作为函数写入单独的客户端库中，以便您可以在自适应表单中指定并重用这些函数。 客户端库应为自包含库，并且不应具有任何外部依赖项，但jQuery和Underscore.js除外。 您还可以使用客户端库强制执行已提交表单数据的[服务器端重新验证](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form)。
* 自适应表单提供了一组API，您可以使用这些API与自适应表单通信并对自适应表单执行操作。 一些关键API如下所示。 有关详细信息，请参阅自适应JavaScript的[Forms库API参考](https://adobe.com/go/learn_aemforms_documentation_63)。

   * `guideBridge.reset()`：重置表单。
   * `guideBridge.submit()`：提交表单。
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`：将焦点设置为字段。
   * `guideBridge.validate(errorList, somExpression, focus)`：验证表单。
   * `guideBridge.getDataXML(options)`：以XML格式获取表单数据。
   * `guideBridge.resolveNode(somExpression)`：获取表单对象。
   * `guideBridge.setProperty(somList, propertyName, valueList)`：设置表单对象的属性。
   * 此外，您还可以使用以下字段属性：

      * `field.value`以更改字段的值。
      * `field.enabled`以启用/禁用字段。
      * `field.visible`以更改字段的可见性。

* 自适应表单作者可能需要编写JavaScript代码，才能在表单中构建业务逻辑。 虽然JavaScript功能强大且有效，但它有可能降低安全预期。 因此，您必须确保表单作者是受信任的角色，并且在表单投入生产之前具有审查和批准JavaScript代码的流程。 管理员可以根据用户组的角色或职能，限制用户组对规则编辑器的访问权限。 请参阅[向选定的用户组授予规则编辑器访问权限](/help/forms/using/rule-editor-access-user-groups.md)。
* 您可以在规则中使用表达式以使自适应表单成为动态表单。 所有表达式都是有效的JavaScript表达式，都使用自适应表单脚本模型API。 这些表达式返回某些类型的值。 有关表达式及其相关最佳实践的更多信息，请参阅[自适应表单表达式](/help/forms/using/adaptive-form-expressions.md)。

* 在使用规则编辑器创建规则时，Adobe建议比异步操作使用JavaScript同步操作。 强烈建议不要使用异步操作。 但是，如果您无法避免异步操作，则实施JavaScript关闭函数至关重要。 这样，您就可以有效地防止任何潜在的竞争情况，从而确保您的规则实施提供最佳性能并在整个过程中保持稳定性。

  例如，假设我们需要从外部API获取数据，然后根据该数据应用一些规则。 我们使用关闭来处理异步API调用，并确保在获取数据后应用规则。 以下是示例代码：

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  在此示例中，`fetchDataFromAPI`使用`setTimeout`模拟异步API调用。 在获取数据后，它会调用提供的回调函数，该函数是处理后续规则应用的闭包。 `ruleImplementation`函数包含规则逻辑。


### 使用主题 {#working-with-themes}

通过自适应主题，您可以创建可重复使用的样式，这些样式可以跨表单应用，以实现一致的外观和样式。 使用主题定义表单组件和面板的样式。 围绕主题的一些最佳实践如下：

* 使用资产库快速应用文本样式、背景和图像。 将样式添加到资产库时，该样式可用于其他主题以及表单编辑器的样式模式。
* 使用页面级别选择器应用全局设置，如字体和页面背景。
* 使用客户端库将现有样式或高级样式导入主题中。
* 可以覆盖表单样式图层中的特定字段、面板或按钮的样式。
* 如果主题不符合样式要求，则可以使用预定义类（如guideFieldNode、guideFieldLabel、guideFieldWidget和guidePanelNode）跨表单应用通用样式。

有关详细信息，请参阅[主题](/help/forms/using/themes.md)。

### 优化大型和复杂表单的性能 {#optimizing-performance-of-large-and-complex-forms}

在创作模式下或运行时加载大型表单时，表单作者和最终用户通常面临性能问题。 随着表单中对象（字段和面板）数量的增加，创作和运行时体验开始降级。 它还阻止多个作者同时协作和创作表单。

请考虑以下最佳实践以解决大型表单的性能问题：

* 建议使用XSD表单数据模型创建自适应表单，即使可能的情况下也将XFA转换为自适应表单。
* 仅包括自适应表单中从用户捕获信息的那些字段和面板。 请考虑将静态内容保持为最小或使用URL在单独的窗口中打开它们。
* 虽然每个表单都针对特定目的而设计，但大多数表单中都存在一些通用区段。 例如，个人详细信息、地址、雇用详细信息等。 为通用表单元素和节创建[自适应表单片段](/help/forms/using/adaptive-form-fragments.md)，并在表单间使用它们。 您还可以将现有表单中的面板另存为片段。 片段中的任何更改都会反映在所有关联的自适应表单中。 它促进了协作创作，因为多个作者可以同时处理构成表单的不同片段。

   * 在表单创作过程中，请考虑甚至为不可重用的部分创建表单片段。 随着表单的大小和复杂性的增加，将它们划分为片段可以显着简化创作过程并使表单更易于维护。 此方法允许您专注于更小的、更易于管理的表单部分，而不是一次处理整个表单。
   * 与自适应表单类似，建议使用片段容器对话框在客户端库中定义所有特定于片段的样式和自定义脚本。 此外，尝试创建不依赖于外部对象的自给自足的片段。
   * 避免使用跨片段脚本。 如果片段外有任何您必须引用的对象，请尝试将该对象作为父表单的一部分。 如果对象必须仍然驻留在另一个片段中，请在脚本中按其名称引用它。

* 使用自动保存并恢复可定期保存自适应表单，并允许用户稍后重新访问以完成表单。
* 配置片段以延迟加载。 在运行时，标记为延迟加载的片段仅在需要时才会呈现。 它显着缩短了大型表单的加载时间。 带有可重复面板的片段也支持此功能。 有关详细信息，请参阅[配置延迟加载](/help/forms/using/lazy-loading-adaptive-forms.md)。

   * 请勿在响应式网格布局或第一个面板中配置对片段的延迟加载。
   * 延迟加载的片段不支持文件附件和条款和条件组件。
   * 如果延迟加载面板中的某个值在表单的其他部分中使用，请将该值标记为“全局使用值”，以便在卸载包含的面板时使用该值。
   * 考虑为应根据条件显示或隐藏的片段编写可见性规则。
* 将&#x200B;**Apache Sling主Servlet**&#x200B;中每个请求&#x200B;**的**&#x200B;调用数的值设置为相当大的数值。 它允许Forms服务器进行其他调用。 配置显示默认值1500。 值“1500调用”适用于其他Experience Manager组件，如Sites和Assets。 自适应表单的默认值集为20000。 如果您在日志中遇到`too many calls`错误或表单无法呈现，请尝试将该值增大到较大的数字来解决问题。 如果调用的数量超过20000，则意味着表单非常复杂，在浏览器中呈现表单可能需要一些时间。 这仅在首次加载表单时发生，之后将缓存表单，并且一旦缓存表单，对性能没有重大影响。

### DOM大小注意事项和浏览器性能

在创建大型复杂自适应表单时，请务必考虑DOM大小对渲染和性能的影响：

* **DOM大小影响**：虽然AEM Forms中没有DOM大小的硬性限制，但过大会显着影响性能，尤其是在处理延迟加载的片段时。 大型DOM结构需要更多的内存和处理时间才能渲染和操作。

* **浏览器渲染差异**：渲染性能在不同的浏览器和设备上可能差别很大。 有些浏览器渲染引擎处理动态DOM更新的方式不同，对样式重新计算、重新流动和重新绘制的方式也不同。 对于动态加载的大型内容，这一点尤其明显。 在一些浏览器中，每次重大的DOM操作都会触发页面的完整布局重新计算和重绘，从而加剧大型或复杂表单的性能问题。

* **性能因素**：影响延迟加载性能的因素有多个：
   * 片段的大小和复杂性
   * 应用于元素的CSS样式
   * 动态更新触发的重排次数
   * 设备和浏览器功能

* **真实世界影响**：在观察到的情况下，DOM大小在400 KB左右的表单在某些浏览器上经历了最多15秒的大量渲染延迟。 这些延迟不仅由于片段大小，而且还与动态内容插入期间触发的CSS处理和页面重新流动相关。

**管理DOM大小的最佳实践：**

* 对于静态内容，请考虑使用AEM内容片段，而不是通过延迟加载动态插入大型HTML块。 此方法可以减少重新排程、重新绘制和JavaScript执行时间，从而提高整体页面加载性能。

* 当片段必须动态且延迟加载时，请将大型片段分解为更小、更易于管理的片段，并根据需要仅加载所需部分。

* 在适当时实施渐进式披露模式，仅在根据用户输入需要时显示其他表单字段。

* 跨多个浏览器和设备测试表单，尤其是使用延迟加载的片段时，以确保跨不同环境的一致性能。

* 监控和优化表单中使用的CSS，因为广泛或结构不佳的CSS可以显着增加渲染时间，尤其是在动态内容更新期间。

有关不同的浏览器渲染引擎如何处理DOM更新、重新排列和重绘的更多技术详细信息，请考虑探索浏览器引擎文档，如不同浏览器供应商提供的文档。

### 预填自适应表单 {#prefilling-adaptive-forms}

您可以使用从后端获取的数据预填充自适应表单字段，以帮助用户快速填写表单并避免键入错误。

* AEM Forms提供预填充服务，用于从预定义的数据XML文件中读取数据，并使用预填充XML文件中的内容预填充自适应表单的字段。
* 预填充数据XML必须与与自适应表单关联的表单模型的架构兼容。
* 在预填充XML中包括`afBoundedData`和`afUnBoundedData`部分，以便在自适应表单中预填充绑定和未绑定字段。

* 对于基于表单数据模型的自适应表单，AEM Forms提供现成的表单数据模型预填充服务。 预填充服务在自适应表单中查询数据模型对象的数据源，并在呈现表单时预填充字段值。
* 您还可以使用文件、crx、服务或http协议预填充自适应表单。
* AEM Forms支持自定义预填充服务，您可以将这些服务作为OSGi服务插入以预填充自适应表单。

有关详细信息，请参阅[预填自适应表单字段](/help/forms/using/prepopulate-adaptive-form-fields.md)。

### 签名和提交自适应表单 {#signing-and-submitting-adaptive-forms}

自适应表单需要提交操作来处理用户指定的数据。 提交操作确定使用自适应表单提交的数据上执行的任务。

* 在自适应表单中，有多个现成的提交操作。 有关详细信息，请参阅[配置提交操作](/help/forms/using/configuring-submit-actions.md)。
* 如果默认提交操作不符合您的用例，则可以编写自定义提交操作。 有关详细信息，请参阅[为自适应表单编写自定义提交操作](/help/forms/using/custom-submit-action-form.md)。
* 包括服务器端验证，以防止提交无效数据。

您可以在自适应表单中使用Adobe Sign的多签名体验。 在自适应表单中配置Adobe Sign时，请考虑以下事项。 有关详细信息，请参阅[在自适应表单中使用Adobe Sign](/help/forms/using/working-with-adobe-sign.md)。

* 仅在所有签名者对表单签名后，才提交启用Adobe Sign的自适应表单。 在所有签名者对表单进行签名之前，Forms会一直处于待处理签名状态。
* 您可以配置表单内签名体验或在提交时将签名者重定向到签名页面。
* 根据需要配置顺序或并行签名体验。

### 生成记录文档 {#generating-document-of-record}

记录文档(DoR)是自适应表单的拼合PDF版本，您可以打印、签名或存档。

* 根据自适应表单所基于的表单数据模型，您可以为DoR配置模板，如下所示：

   * **XFA表单模板**：使用关联的XDP文件作为DoR模板。
   * **XSD架构**：使用与自适应表单使用相同XML架构的关联XFA模板。
   * **无**：使用自动生成的DoR。

* 直接从自适应表单编辑器的“记录文档”选项卡配置页眉、页脚、图像、颜色、字体等。
* 使用`DoRService`以编程方式生成记录文档。
* 从记录文档排除隐藏字段。
* 使用`afAcceptLang`请求参数在另一个区域设置中查看DoR。

### 调试和测试自适应表单 {#debugging-and-testing-adaptive-forms}

[AEM Chrome插件](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/)是Google Chrome的浏览器扩展，提供了用于调试自适应表单的工具。 表单作者和开发人员可以使用这些工具执行以下操作：

* 确定瓶颈并优化表单渲染性能
* 调试表单中的关键字和bindRef错误
* 启用和配置日志
* 调试表单中的规则和脚本
* 探索和了解guideBridge API

有关详细信息，请参阅[AEM Chrome插件 — 自适应表单](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/)。

### 验证AEM服务器上的自适应表单 {#validating-adaptive-forms-on-aem-server}

需要服务器端验证，以防止任何绕过客户端验证的尝试以及任何可能危及数据提交和业务规则违规的行为。 服务器端验证通过加载所需的客户端库在服务器上执行。

* 在客户端库中包含用于验证自适应表单中表达式的函数，并在自适应表单容器对话框中指定客户端库。 有关详细信息，请参阅[服务器端重新验证](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p)。
* 服务器端验证将验证表单模型。建议为验证创建单独的客户端库，并且不要在同一客户端库中将其与HTML样式和DOM操作等其他内容混合。

### 本地化自适应表单 {#localizing-adaptive-forms}

AEM提供可用于本地化自适应表单的翻译工作流。 有关信息，请参阅[使用AEM翻译工作流本地化自适应表单](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

本地化自适应表单时的一些最佳实践如下：

* 将自适应表单片段用于各个表单中的常用元素并将片段本地化。 它确保您将片段本地化一次，并在使用本地化片段的所有表单中反映出来。
* 任何修改（如添加新组件或以本地化的形式应用脚本）都不会自动本地化。 因此，在本地化表单之前必须先完成该表单，以避免多个本地化周期。
* 使用`afAcceptLang`请求参数覆盖浏览器区域设置并以指定的区域设置呈现表单。 例如，无论浏览器设置中指定的区域设置如何，以下URL都会强制以日语区域设置呈现表单：

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms当前支持英语(en)、西班牙语(es)、法语(fr)、意大利语(it)、德语(de)、日语(ja)、葡萄牙语 — 巴西语(pt-BR)、中文(zh-CN)、中文 — 台湾(zh-TW)和韩语(ko-KR)本地化自适应表单内容。 但是，您可以在运行时为自适应表单添加新区域设置支持。 有关详细信息，请参阅[支持自适应表单本地化的新区域设置](/help/forms/using/supporting-new-language-localization.md)。

## 准备表单项目以进行生产 {#prepare-forms-project-for-production}

### 添加表单处理服务器 {#adding-forms-processing-server}

您可以配置另一个驻留在安全区域中的防火墙后面的AEM Forms服务器实例。 您可以将此实例用于：

* **批处理**：在重负载的批中循环或计划的作业。 例如，打印语句，生成对应，以及使用PDF Generator、Output和Assembler等文档服务。
* **存储PII数据**：将PII数据保存在处理服务器上。 如果您已在使用自定义存储提供程序存储PII数据，则不需要使用此功能。

### 将项目移动到其他环境 {#moving-project-to-another-environment}

您通常需要将AEM项目从一个环境移动到另一个环境。 迁移时要记住的一些关键事项如下：

* 备份现有客户端库、自定义代码和配置。
* 在新环境中以指定的顺序手动部署产品软件包和修补程序。
* 手动部署特定于项目的代码包和捆绑包，并将其作为单独的包或捆绑包部署到新的AEM服务器上。
* (*仅适用于JEE上的AEM Forms*)在Forms Workflow服务器上手动部署LCA和DSC。
* 使用[Export-Import](/help/forms/using/import-export-forms-templates.md)功能将资产移动到新环境。 您还可以配置复制代理并发布资产。
* 升级时，请将所有已弃用的API和功能替换为新的API和功能。

### 配置AEM {#configuring-aem}

以下是配置AEM以提高整体性能的一些最佳实践：

* 从Felix控制台为JavaScript和CSS启用HTML客户端库压缩。
* 在AEM Dispatcher上缓存`/etc.clientlibs/fd`中的所有客户端库和任何其他自定义客户端库，以提高已发布表单的响应速度和安全性。 有关详细信息，请参阅[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)。

* 不缓存`/content/forms/af/`和`/content/dam/formsanddocuments/*`路径。 有关配置自适应表单缓存的详细信息，请参阅[缓存自适应表单](/help/forms/using/configure-adaptive-forms-cache.md)。

* 通过Web服务器压缩模块启用HTML。 有关详细信息，请参阅[AEM Forms服务器的性能优化](/help/forms/using/performance-tuning-aem-forms.md)。
* 增加大型表单的每个请求配置的调用。 请参阅[优化大型复杂表单的性能](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms)。
* 创建由错误处理程序](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html)显示的[自定义错误页面。
* 安全的AEM Forms服务器。

   * 使用`nosamplecontent`运行模式以确保在生产服务器上没有部署示例内容和示例用户。 请参阅[在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md)。

* 将栈大小保持为最小8 GB。 有关其他设置，请参阅[AEM Forms服务器的性能优化](/help/forms/using/performance-tuning-aem-forms.md)。
* 使用服务用户会话而不是管理会话来执行服务级别任务。 有关详细信息，请参阅[服务身份验证](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html)。

>[!VIDEO](https://vimeo.com/)

### 为草稿和已提交的表单数据配置外部存储 {#external-storage}

在生产环境中，建议不要将提交的表单数据存储在AEM存储库中。 Forms Portal Store、Store Content和Store PDF的默认实施提交操作将表单数据存储在AEM存储库中。 这些提交操作仅用于演示目的。 此外，默认情况下，“保存并恢复”和“自动保存”功能使用入口存储。 因此，请考虑以下建议：

* **存储草稿数据**：如果使用自适应表单的草稿功能，则应实施自定义服务提供接口(SPI)，以将草稿数据存储到更安全的存储（如数据库）。 有关详细信息，请参阅将草稿和提交组件与数据库集成的[示例](/help/forms/using/integrate-draft-submission-database.md)。

* **存储提交数据**：如果您使用表单门户提交存储，则应该实施自定义SPI以将提交数据存储在数据库中。 有关示例集成，请参阅将草稿和提交组件与数据库](/help/forms/using/integrate-draft-submission-database.md)集成的[示例。

  您还可以编写自定义提交操作，将表单数据和附件存储在安全存储中。 有关详细信息，请参阅[为自适应表单编写自定义提交操作](/help/forms/using/custom-submit-action-form.md)。

* **草稿ID的长度**：将自适应表单另存为草稿时，将生成草稿ID以唯一标识草稿。 草稿ID字段的最小长度值为26个字符。 Adobe建议将草稿ID长度设置为26个或更多字符。

### 处理个人身份信息 {#handling-personally-identifiable-information}

组织面临的主要挑战之一是如何处理个人身份识别(PII)数据。 以下是将帮助您处理此类数据的一些最佳实践：

* 使用安全的外部存储（如数据库）存储草稿和已提交表单中的数据。 请参阅[为草稿和已提交的表单数据配置外部存储](/help/forms/using/adaptive-forms-best-practices.md#external-storage)。
* 使用条款和条件表单组件，在启用自动保存之前获得用户的明确同意。 在这种情况下，仅当用户同意条款和条件组件中的条件时才启用自动保存。

## 为自适应表单选择规则编辑器、代码编辑器或自定义客户端库 {#RuleEditor-CodeEditor-ClientLibs}

### 规则编辑器 {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

AEM Forms规则编辑器提供了一个用于创建和管理规则的可视化界面，无需进行大量编码。 这对于不具备高级编程技能但需要在表单中定义和维护业务规则的业务用户或表单设计人员特别有用，这里我们将讨论一些使用案例，其中规则编辑器允许您：

* <!-- Allows you --> 为表单定义业务规则，而无需大量的编程。
* <!-- Use the Rule Editor when you need --> 在表单中实施条件逻辑。 这包括显示或隐藏表单元素、根据特定条件更改字段值或动态更改表单的行为。
* <!--When you want --> 要对表单提交强制实施数据验证规则，可以使用规则编辑器来定义验证条件。
* <!-- When you need --> 要将表单与外部数据源(FDM)或服务集成，规则编辑器可帮助定义用于在表单交互期间获取、显示或处理数据的规则。
* <!-- If you want -->要创建响应用户操作的动态和交互式表单，您可以使用规则编辑器定义实时控制表单元素行为的规则。

规则编辑器适用于AEM Forms Foundation组件和核心组件。

### 代码编辑器 {#code-editor}

代码编辑器是Adobe Experience Manager (AEM) Forms中的一个工具，允许您编写自定义脚本和代码，以在表单中实现更复杂和高级的功能，这里我们将讨论一些用例：

* 需要实施超出AEM Forms规则编辑器功能的自定义客户端逻辑或行为时。 代码编辑器允许您编写JavaScript代码以处理复杂的交互、计算或验证。
* 如果您的表单需要服务器端处理或与外部系统集成，您可以使用代码编辑器编写自定义服务器端脚本。 您可以在代码编辑器中访问guideBridge API，以在表单事件和对象上实施任何复杂的逻辑。
* 当需要超出AEM Forms组件标准功能的高度自定义用户界面时，代码编辑器允许您实施自定义样式、行为，甚至创建自定义表单组件。
* 如果您的表单涉及异步操作（如异步数据加载），您可以使用代码编辑器通过自定义异步JavaScript代码管理这些操作。

请务必注意，使用代码编辑器需要很好地了解JavaScript和AEM Forms架构。 此外，在实施自定义代码时，请确保遵循最佳实践、遵守安全准则并彻底测试您的代码以防止生产环境中出现潜在问题。 您可以使用代码编辑器为FDM实施回调。

代码编辑器仅可用于AEM Forms Foundation组件。 对于自适应表单核心组件，您可以使用自定义函数创建自己的表单规则，如下节所述。

### 自定义函数 {#custom-client-libs}

在各种场景中，使用AEM Forms (Adobe Experience Manager Forms)中的自定义客户端库可能会有助于增强表单的功能、样式或行为。 以下是可能需要使用自定义客户端库的一些情况：

* 如果您的表单需要实施独特的设计或品牌策略，而这些设计或品牌策略超出了AEM Forms提供的默认样式选项的功能，则您可以选择创建自定义客户端库来控制外观。
* 当需要自定义客户端逻辑时，无法通过标准AEM Forms功能实现跨多个表单或行为的方法的可重用性。 这可能包括动态表单交互、自定义验证或与第三方库的集成。
* 通过优化和缩小客户端资源来提高表单性能。 自定义客户端库可用于捆绑和压缩JavaScript和CSS文件，从而缩短整个页面加载时间。
* 适用于需要集成未包含在默认JavaScript设置中的其他AEM Forms库或框架的情况。 增强型日期选取器、图表或其他交互式组件等功能可能需要此项。

在决定使用自定义客户端库之前，请务必考虑维护开销、与未来更新的潜在冲突以及遵守最佳实践的情况。 确保您的自定义项得到妥善的记录和测试，以避免在升级期间或与其他开发人员协作时出现问题。

>[!NOTE]
> 自定义函数适用于AEM Forms基础组件和核心组件。

**自定义函数的优势：**

**自定义函数**&#x200B;与&#x200B;**代码编辑器**&#x200B;相比具有显着的优势，因为它在内容和代码之间提供了清晰的区分，从而增强了协作并简化了工作流。 为获得以下优势，建议使用自定义函数：

* **无缝使用版本控制，如Git：**
   * 从内容中分离代码可显着减少内容管理期间的Git冲突，并提升组织良好的存储库。
   * 自定义函数对于有多个参与者同时工作的项目非常有用。

* **技术优势：**
   * 自定义函数提供了模块性和封装。
   * 模块可以独立开发、测试和维护。
   * 增强了代码的可重用性和可维护性。

* **高效开发流程：**
   * 模块化允许开发人员专注于特定功能。
   * 通过降低整个代码库的复杂程度来降低开发人员的负担，从而实现更有效的开发过程。



