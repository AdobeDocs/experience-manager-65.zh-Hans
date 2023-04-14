---
title: AEM工作流中的变量
description: 创建变量，为变量设置值，然后在“或”拆分并转到AEM工作流步骤中使用该变量。
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
exl-id: c8aeceec-860c-49ee-b681-d7107e52020d
source-git-commit: 936b636819eaef595fcdf9f1f3446d4ac0c28b2f
workflow-type: tm+mt
source-wordcount: '2048'
ht-degree: 0%

---

# AEM工作流中的变量{#variables-in-aem-workflows}

工作流模型中的变量是一种根据值的数据类型来存储值的方法。 然后，您可以在任何工作流步骤中使用变量的名称来检索存储在变量中的值。 您还可以使用变量名称定义用于做出路由决策的表达式。

在AEM工作流模型中，您可以：

* [创建变量](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) 数据类型的值。
* [为变量设置值](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) 使用设置变量工作流步骤。
* [使用变量](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) 在OR拆分和转到AEM工作流步骤中，以便您定义用于执行路由决策的表达式。 您还可以在所有AEM Forms工作流步骤中使用变量。

以下视频演示了如何在AEM工作流模型中创建、设置和使用变量：

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

变量是 [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 界面。 您可以使用 [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 用于访问使用变量保存的元数据。

## 创建变量 {#create-a-variable}

您可以使用工作流模型Sidekick中提供的“变量”部分创建变量。 AEM工作流变量支持以下数据类型：

* **基元数据类型**:Long、Double、Boolean、Date和String
* **复杂数据类型**: [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) 和 [JSON](https://www.javadoc.io/doc/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>工作流仅支持ISO8601格式的日期类型变量。

有关AEM Forms工作流中可用的其他复杂数据类型，请参阅 [AEM Forms工作流中的变量](/help/forms/using/variable-in-aem-workflows.md). 使用ArrayList数据类型创建变量集合。 您可以为所有基元和复杂数据类型创建ArrayList变量。 例如，创建一个ArrayList变量并选择String作为子类型，以使用该变量存储多个字符串值。

要创建变量，请

1. 在AEM实例上，导航至工具>工作流>模型。
1. 点按 **[!UICONTROL 创建]** 并为工作流模型指定标题和可选名称。 选择模型并点按 **[!UICONTROL 编辑]**.
1. 点按工作流模型的Sidekick中提供的变量图标，然后点按 **[!UICONTROL 添加变量]**.

   ![添加变量](assets/variables_add_variable_new.png)

1. 在添加变量对话框中，指定名称，然后选择变量的类型。
1. 从 **[!UICONTROL 类型]** 下拉列表，并指定以下值：

   * 基元数据类型 — 为变量指定可选的默认值。
   * JSON或XML — 指定可选的JSON或XML架构路径。 当将此模式中可用的属性映射到另一个变量并将其存储到另一个变量时，系统将验证模式路径。
   * 表单数据模型 — 指定表单数据模型路径。
   * ArrayList — 为集合指定子类型。

1. 为变量指定可选描述，然后点按 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以保存更改。 变量显示在左侧窗格的可用列表中。

在创建变量时，请考虑以下实践：

* 根据工作流的需要创建任意数量的变量。 但是，为了节省数据库资源，请尽可能使用所需变量的最少数量，并重用变量。
* 变量区分大小写。 确保在工作流中使用相同的大小写引用变量。
* 避免在变量名称中使用特殊字符

## 设置变量 {#set-a-variable}

您可以使用设置变量步骤来设置变量的值并定义值的设置顺序。 变量按变量映射在设置变量步骤中列出的顺序进行设置。

变量值的更改仅影响发生更改的流程实例。 例如，当启动工作流并更改变量数据时，所做的更改仅会影响该工作流实例。 这些更改不会影响之前启动或稍后启动的工作流的其他实例。

根据变量的数据类型，您可以使用以下选项设置变量的值：

* **文字：** 当您知道要指定的确切值时，请使用选项。
* **表达式：** 根据表达式计算要使用的值时，请使用选项。 表达式在提供的表达式编辑器中创建。
* **JSON点表示法：** 使用选项从JSON或FDM类型变量中检索值。
* **XPATH:** 使用选项从XML类型变量中检索值。
* **相对于有效负载：** 当要保存到变量的值在相对于有效负载的路径上可用时，请使用选项。
* **绝对路径：** 当要保存到变量的值在绝对路径中可用时，请使用选项。

您还可以使用JSON点表示法或XPATH表示法来更新JSON或XML类型变量的特定元素。

### 添加变量之间的映射 {#add-mapping-between-variables}

要在变量之间添加映射，请执行以下操作：

1. 在工作流编辑页面上，点按工作流模型Sidekick中可用的步骤图标。
1. 拖放 **设置变量** 步骤至工作流编辑器，点按该步骤，然后选择 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) （配置）。
1. 在设置变量对话框中，选择 **[!UICONTROL 映射]** > **[!UICONTROL 添加映射]**.
1. 在 **映射变量** 部分，选择要存储数据的变量，选择映射模式，并指定要存储在变量中的值。 映射模式因变量类型而异。
1. 映射更多变量，以便创建有意义的表达式。 点按 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以保存更改。

### 示例1:查询XML变量以设置字符串变量的值 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

选择要存储XML文件的XML类型变量。 查询XML变量，为XML文件中可用的属性设置字符串变量的值。 使用 **为XML变量指定XPATH** 字段来定义要存储在字符串变量中的属性。

在本例中，选择 **格式数据** 用于存储 **cc-app.xml** 文件。 查询 **格式数据** 变量，以便您可以为 **emailaddress** 用于存储 **emailAddress** 属性 **cc-app.xml** 文件。

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "设置变量值")

### 示例2:使用表达式根据其他变量存储值 {#example2}

使用表达式计算变量的总和并将结果存储到变量中。

在此示例中，使用表达式编辑器定义表达式以计算 **资产成本** 和 **余额** 变量并将结果存储在 **totalvalue** 变量。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 使用表达式编辑器 {#use-expression-editor}

您还可以使用表达式在运行时计算变量的值。 变量提供用于定义表达式的表达式编辑器。

使用表达式编辑器可执行以下操作：

* 使用其他工作流变量、数字或数学表达式设置变量的值。
* 在数学表达式中使用工作流变量、字符串、数字或表达式
* 添加条件，以便设置变量值。
* 在条件之间添加运算符。

![表达式编辑器](assets/variables_expression_editor_new.png)

它基于自适应表单规则编辑器，并进行了以下更改。 变量中的规则编辑器：

* 不支持函数。
* 不提供用于查看规则摘要的UI
* 没有代码编辑器。
* 不支持启用和禁用对象的值。
* 不支持对象的设置属性。
* 不支持调用Web服务。

有关更多信息，请参阅 [自适应表单规则编辑器](/help/forms/using/rule-editor.md).

## 使用变量 {#use-a-variable}

您可以使用变量检索输入和输出或保存步骤结果。 工作流编辑器提供了两种类型的工作流步骤：

* 支持变量的工作流步骤
* 不支持变量的工作流步骤

### 支持变量的工作流步骤 {#workflow-steps-with-support-for-variables}

“转到”步骤或“拆分”步骤以及所有AEM Forms工作流步骤都支持变量。

#### 或拆分步骤 {#or-split-step}

“或拆分”(OR Split)在工作流中创建一个拆分，在该拆分之后，只有一个分支处于活动状态。 通过此步骤，您可以在工作流中引入条件处理路径。 您可以根据需要向每个分支添加工作流步骤。

您可以使用规则定义、ECMA脚本或外部脚本为分支定义路由表达式。

您可以使用变量通过表达式编辑器定义路由表达式。 有关在“或拆分”步骤中使用路由表达式的详细信息，请参阅 [或拆分步骤](/help/sites-developing/workflows-step-ref.md#or-split).

在本例中，在定义路由表达式之前，请使用 [示例2](/help/sites-developing/using-variables-in-aem-workflows.md#example2) 为 **totalvalue** 变量。 如果 **totalvalue** 变量大于50000。 同样，您可以定义一个规则，以在 **totalvalue** 变量小于50000。

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

同样，选择外部脚本路径或指定路由表达式的ECMA脚本以计算活动分支。 点按 **[!UICONTROL 重命名分支]** 指定分支的替代名称。

有关更多示例，请参阅 [创建工作流模型](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### 转至步骤 {#go-to-step}

的 **跳转步骤** 允许您根据路由表达式的结果，指定要在工作流模型中运行的下一步。

与“或拆分”步骤类似，您可以使用规则定义、ECMA脚本或外部脚本定义跳转步骤的路由表达式。

您可以使用变量通过表达式编辑器定义路由表达式。 有关在跳转步骤中使用路由表达式的详细信息，请参阅 [跳转步骤](/help/sites-developing/workflows-step-ref.md#goto-step).

![跳转规则](assets/variables_goto_rule1_new.png)

在此示例中，跳转步骤指定复查信用卡应用程序，如果 **actioncaped** 变量等于 **需要更多信息**.

有关在跳转步骤中使用规则定义的更多示例，请参阅 [模拟For环](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### 以Forms工作流为中心的工作流步骤 {#forms-workflow-centric-workflow-steps}

所有AEM Forms工作流步骤都支持变量。 有关更多信息，请参阅 [基于OSGi的以Forms为中心的工作流](/help/forms/using/aem-forms-workflow-step-reference.md).

### 不支持变量的工作流步骤 {#workflow-steps-without-support-for-variables}

您可以使用 [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 用于访问不支持变量的工作流步骤中的变量的界面。

#### 检索变量值 {#retrieve-the-variable-value}

要根据数据类型检索现有变量的值，请在ECMA脚本中使用以下API。

| 变量数据类型 | API |
|---|---|
| 基元（长、双精度、布尔、日期和字符串） | workItem.getWorkflowData()。getMetaDataMap()。get(variableName， type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData()。getMetaDataMap()。get(variableName， Packages.com.google.gson.JsonObject.class); |

有关AEM Forms工作流中可用的其他复杂变量数据类型的API的信息，请参阅 [AEM Forms工作流中的变量](/help/forms/using/variable-in-aem-workflows.md).

**示例**

使用以下API检索字符串数据类型的值：

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 更新变量值 {#update-the-variable-value}

要更新变量的值，请在ECMA脚本中使用以下API。

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**示例**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

更新 **薪金** 变量50000。

### 设置变量以调用工作流 {#apiinvokeworkflow}

您可以使用API设置变量并传递它们以调用工作流实例。

[workflowSession.startWorkflow](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) 使用model、wfData和metaData作为参数。 使用MetaDataMap为变量设置值。

在此API中， **variableName** 变量设置为 **值** 使用metaData.put(variableName， value);

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 编辑变量 {#edit-a-variable}

1. 在编辑工作流页面上，点按工作流模型Sidekick中可用的变量图标。 左窗格中的“变量”部分显示所有现有变量。
1. 点按 ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png) （编辑）图标。
1. 编辑变量信息并点按 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以保存更改。 您无法编辑 **[!UICONTROL 名称]** 和 **[!UICONTROL 类型]** 字段。

## 删除变量 {#delete-a-variable}

在删除变量之前，请从工作流中删除该变量的所有引用。 确保未在工作流中使用变量。

要删除变量，

1. 在编辑工作流页面上，点按工作流模型Sidekick中可用的变量图标。 左窗格中的“变量”部分显示所有现有变量。
1. 点按要删除的变量名称旁边的删除图标。
1. 点按 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png) 以确认和删除变量。
