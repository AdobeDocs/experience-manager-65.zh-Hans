---
title: 工作流步骤参考
seo-title: Workflow Step Reference
description: 工作流步骤参考
seo-description: null
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: 768576e300b655962adc3e1db20fc5ec06a5ba6c
workflow-type: tm+mt
source-wordcount: '3246'
ht-degree: 2%

---

# 工作流步骤参考 {#workflow-step-reference}

工作流模型由各种类型的一系列步骤组成。 根据类型，可以使用参数和脚本配置和扩展这些步骤，以提供所需的功能和控制。

>[!NOTE]
>
>此部分介绍标准工作流步骤。
>
>有关模块特定的步骤，请参阅以下步骤：
>
>* [AEM Forms工作流步骤参考](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [使用媒体处理程序和工作流处理资产](/help/assets/media-handlers.md)
>


## 步骤属性 {#step-properties}

每个步骤组件都有 **步骤属性** 对话框，用于定义和编辑所需的属性。

### 步骤属性 — “常用”选项卡 {#step-properties-common-tab}

以下属性的组合适用于 **常用** 选项卡：

* **标题**
步骤的标题。

* **描述**
步骤的描述。

* **工作流暂存**

   要应用 [阶段](/help/sites-developing/workflows.md#workflow-stages) 中。

* **超时**

   步骤“超时”的时间段。
您可以在以下两种方式中进行选择： **关闭**, **立即**, **1小时**, **6小时**, **12小时**, **24小时**.

* **超时处理程序**

   在步骤超时时控制工作流的处理程序。 例如，`Auto Advancer`

* **处理程序前进**

   选择此选项可在执行后自动将工作流推进到下一步。 如果未选择，则实施脚本必须处理工作流进度。

### 步骤属性 — “用户/组”选项卡 {#step-properties-user-group-tab}

以下属性适用于 **用户/组** 选项卡：

* **通过电子邮件通知用户**

   * 当工作流到达该步骤时，您可以通过向参与者发送电子邮件来通知他们。
   * 如果启用，则会向属性定义的用户发送电子邮件 **用户/组**，或在定义了群组时发送给群组的每个成员。

* **用户/组**

   * 通过下拉选择框，您可以导航到某个用户或组并将其选中。
   * 如果您将步骤分配给特定用户，则只有该用户才能对该步骤执行操作。
   * 如果您将步骤分配给整个组，则当工作流到达此步骤时，此组中的所有用户都将在其 **工作流收件箱**.
   * 请参阅 [参与工作流](/help/sites-authoring/workflows-participating.md) 以了解更多信息。

## AND 拆分 {#and-split}

的 **和拆分** 在工作流中创建拆分，在该拆分之后，两个分支都处于活动状态。 您可以根据需要向每个分支添加工作流步骤。 此步骤允许您在工作流中引入多个处理路径。 例如，您可以允许并行执行某些审核步骤，从而节省时间。

![wf-26](assets/wf-26.png)

### 和拆分 — 配置 {#and-split-configuration}

要配置拆分，请执行以下操作：

* 编辑 **和拆分属性**:

   * **拆分名称**:为说明性目的指定名称
   * 选择所需的分支数量；2、3、4或5。

* 根据需要将工作流步骤添加到分支。

   ![wf-27](assets/wf-27.png)

## 容器步骤 {#container-step}

容器步骤启动作为子工作流执行的另一个工作流模型。

此容器允许您重复使用工作流模型以实施常见的步骤序列。 例如，翻译工作流模型可用于多个编辑工作流。

![wf-28](assets/wf-28.png)

### 容器步骤 — 配置 {#container-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **容器**

   * **子工作流**:选择要启动的工作流。

## 跳转步骤 {#goto-step}

的 **跳转步骤** 允许您指定要在工作流模型中执行的下一步。 您可以指定规则定义、外部脚本或ECMA脚本作为路由表达式，以评估工作流模型的下一步。

* 如果指定的条件为true，则 **跳转步骤** 完成并工作流引擎执行指定的步骤。
* 如果指定的条件不为true，则 **跳转步骤** 完成，普通路由逻辑确定要执行的下一步。

的 **跳转步骤** 允许您在工作流模型中实施高级路由结构。 例如，要实施循环，请 **跳转步骤** 可定义为执行工作流中的前一步骤，其中路由表达式评估循环条件。

### 转到步骤 — 配置 {#goto-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **目标步骤**:选择在评估路由表达式的条件后要执行的步骤。
   * **路由表达式**:选择规则定义、外部脚本或ECMA脚本，以确定是否执行 **目标步骤**.

      * **规则定义：** 使用 [表达式编辑器](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 来定义规则。
      * **外部脚本：** 外部脚本的路径。
      * **ECMA脚本**:用于确定是否执行 **跳转步骤**.

#### 模拟用于循环的 {#simulating-a-for-loop}

模拟“for loop”要求您保持已发生循环迭代次数的计数：

* 计数通常表示在工作流中执行操作的项目的索引。
* 计数将作为循环的退出条件进行评估。

例如，要实施对多个JCR节点执行操作的工作流，可以使用循环计数器作为节点的索引。 要保留计数，请存储 `integer` 值。 要递增计数并将计数与退出条件进行比较，请使用 **跳转步骤**.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 使用规则定义模拟for循环 {#simulateforloop}

您还可以使用规则定义作为路由表达式来模拟for循环。 [创建 **计数** 变量](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 长数据类型。 使用 **表达式** 作为 **[设置变量](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 设置 **计数** 变量 **计数+ 1** 每次执行 **设置变量** 中。

![模拟for循环](assets/variable_use_case_count_new.png)

在 **跳转步骤**，使用 **设置变量** 作为 **目标步骤** 和 **计数&lt; 5** 作为路由表达式。

![模拟for环的条件](assets/variable_use_case_count1_new.png)

的 **设置变量** 步骤会重复运行，从而增加 **计数** 变量的值，直到值达到5。

## OR 拆分 {#or-split}

的 **或拆分** 在工作流中创建拆分，之后只有一个分支处于活动状态。 通过此步骤，您可以在工作流中引入条件处理路径。 您可以根据需要向每个分支添加工作流步骤。

>[!NOTE]
>
>请参阅 [或拆分步骤](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=en#use-a-variable)

![使用OR拆分进行分支](assets/variables_orsplit_new.png)

### OR拆分 — 配置 {#or-split-configuration}

要配置拆分，请执行以下操作：

* 编辑 **或拆分属性**:

   * **通用**

      * 指定拆分名称。
   * **分支(*x)***

      * **添加分支：** 在步骤中添加更多分支。
      * **选择路由表达式**:要评估活动分支，请选择路由表达式。 可能的值包括：规则定义、外部脚本和ECMA脚本。
      * **单击以添加表达式**:如果选择 **规则定义** 作为路由表达式。
      * **脚本路径**:包含脚本的文件的路径，在您选择 **外部脚本** 作为路由表达式。
      * **脚本**:在框中添加脚本，以在选择 **ECMA脚本** 作为路由表达式。
      * **默认路由**:如果有多个分支，则遵循默认分支。 您只能指定一个分支作为默认分支。

   >[!NOTE]
   >
   >    * 每次根据路由表达式计算一个分支。
   >    * 分支从上到下进行评估。
   >    * 将执行计算为true的第一个脚本。
   >    * 如果没有分支的计算结果为true，则工作流不会前进。


   >[!NOTE]
   >
   >请参阅 [为OR拆分定义规则](/help/sites-developing/workflows-models.md#defineruleecmascript).

* 根据需要将工作流步骤添加到分支。

## 参与者步骤和选择者 {#participant-steps-and-choosers}

### 参与者步骤 {#participant-step}

A **参与者步骤** 允许您为特定操作分配所有权。 仅当用户手动确认该步骤时，工作流才会继续。 当您希望某人对工作流执行操作时，会使用此工作流。 例如，审核步骤。

虽然与用户授权不直接相关，但在分配操作时必须考虑用户授权；用户必须有权访问工作流有效负载页面。

#### 参与者步骤 — 配置 {#participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)

>[!NOTE]
>
>在以下情况下，始终会通知工作流启动器：
>
>* 工作流已完成（已完成）。
>* 工作流已中止（终止）。
>


>[!NOTE]
>
>必须配置某些属性才能启用电子邮件通知。 您还可以自定义电子邮件模板或为新语言添加电子邮件模板。 要在AEM中配置电子邮件通知，请参阅 [配置电子邮件通知](/help/sites-administering/notification.md#configuringemailnotification).

### 对话框参与者步骤 {#dialog-participant-step}

使用 **对话框参与者步骤** 从分配了工作项的用户那里收集信息。 此步骤对于收集稍后在工作流中使用的少量数据非常有用。

完成该步骤后， **完成工作项** 对话框包含您在对话框中定义的字段。 在字段中收集的数据将存储在工作流有效负载的节点中。 随后，后续工作流步骤可以从存储库中读取值。

要配置该步骤，请指定要将工作项分配到的组或用户，以及对话框的路径。

#### 对话框参与者步骤 — 配置 {#dialog-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **对话框**

   * **对话框路径**:的对话框节点的路径 [对话框创建](#dialog-participant-step-creating-a-dialog).

#### 对话框参与者步骤 — 创建对话框 {#dialog-participant-step-creating-a-dialog}

要创建对话框，必须创建对话框：

* 确定结果数据的位置 [存储在有效负载中](#dialog-participant-step-storing-data-in-the-payload).
* [定义对话框；包括定义用于收集和保存数据的字段](#dialog-participant-step-dialog-definition).

#### 对话框参与者步骤 — 在有效负载中存储数据 {#dialog-participant-step-storing-data-in-the-payload}

您可以在工作流有效负荷或工作项元数据中存储小组件数据。 的格式 `name` 小组件节点的属性决定数据存储的位置。

* **使用有效负载存储数据**

   * 要将小组件数据作为工作流有效负载的属性进行存储，请对小组件节点name属性的值使用以下格式：
      `./jcr:content/nodename`

   * 数据存储在 `nodename` 有效负载节点的属性。 如果节点不包含该属性，则会创建该属性。
   * 当与有效负载一起存储时，使用相同有效负载的对话框的后续使用将覆盖属性的值。

* **将数据与工作项一起存储**

   * 要将小组件数据存储为工作项元数据的属性，请对name属性的值使用以下格式：
      `nodename`

   * 数据存储在 `nodename` 工作项的属性 `metadata`. 如果以后将对话框与相同的有效负载一起使用，则会保留数据。

#### 对话框参与者步骤 — 对话框定义 {#dialog-participant-step-dialog-definition}

1. **对话框结构**

   对话框参与者步骤的对话框与为创作组件而创建的对话框类似。 它们存储在以下位置：

   `/apps/myapp/workflow/dialogs`

   标准触屏UI的对话框具有以下节点结构：

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >请参阅 [创建和配置对话框](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **对话框路径属性**

   的 **对话框参与者步骤** 具有 **对话框路径** 资产(与 [参与者步骤](#participant-step))。 的值 **对话框路径** 属性是 `dialog` 的子代码。

   例如，对话框包含在名为 `EmailWatch` 节点中存储的值：

   `/apps/myapp/workflows/dialogs`

   对于触屏优化UI，会将以下值用于 **对话框路径** 属性：

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **示例对话框定义**

   以下XML代码段表示用于存储 `String` 值 `watchEmail` 有效负载内容的节点。 标题节点表示 [文本字段](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 组件：

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   在触屏优化UI中，此示例会生成如下对话框：

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 动态参与者步骤 {#dynamic-participant-step}

的 **动态参与者步骤** 组件类似于 **[参与者步骤](#participant-step)** 在运行时自动选择参与者时的差异。

要配置该步骤，请选择 **参与者选择器** 用于标识要将工作项分配到的参与者，以及对话框。

#### 动态参与者步骤 — 配置 {#dynamic-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参与者选择器**

   * **参与者选择器**:的名称 [您创建的参与者选择器](#developingtheparticipantchooser).
   * **参数**:任何必需的参数。
   * **电子邮件**:是否应向用户发送电子邮件通知。

* **对话框**

   * **对话框路径**:的对话框节点的路径 [对话框(与 **对话框参与者步骤**)](#dialog-participant-step-creating-a-dialog).

#### 动态参与者步骤 — 开发参与者选择器 {#dynamic-participant-step-developing-the-participant-chooser}

创建参与者选择器。 因此，您可以使用任何选择逻辑或条件。 例如，您的参与者选择者可以选择工作项目最少的用户（在组内）。 您可以创建任意数量的参与者选择器，以用于 **动态参与者步骤** 组件。

创建OSGi服务或ECMAScript，以选择用户将工作项分配到的。

* **ECMAscript**

   脚本必须包含名为getParticiant的函数，该函数将用户ID作为 `String` 值。 将自定义脚本存储在 `/apps/myapp/workflow/scripts` 文件夹或子文件夹。

   标准AEM实例中包含一个示例脚本：

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   >
   >请勿在 `/libs` 路径。
   >
   >
   >原因是 `/libs` 在下次升级实例时被覆盖（在应用修补程序或功能包时可能会被覆盖）。

   此脚本将选择工作流启动器作为参与者：

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   >
   >的 **工作流启动器参与者选择器** 组件 **动态参与者步骤** 并使用此脚本作为步骤实施。

* **OSGi服务**

   服务必须实施 [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 界面。 界面定义以下成员：

   * `SERVICE_PROPERTY_LABEL` 字段：使用此字段可指定参与者选择器的名称。 该名称显示在 **动态参与者步骤** 属性。

   * `getParticipant` 方法：将动态解析的主体ID返回为 `String` 值。
   >[!CAUTION]
   >
   >的 `getParticipant` 方法返回动态解析的主体id。 此ID可以是组ID或用户ID。
   >
   >
   >但是，组ID只能用于 **参与者步骤**，返回参与者列表时。 对于 **动态参与者步骤**，则会返回空列表，不能用于委派。

   使实施可用于 **动态参与者步骤** 组件中，将您的Java™类添加到导出服务的OSGi包中，然后将该包部署到AEM服务器。

   >[!NOTE]
   >
   >**随机参与者选择器** 是选择随机用户( `com.day.cq.workflow.impl.process.RandomParticipantChooser`)。 的 **随机参与者选择** r步骤组件示例扩展 **动态参与者步骤** 并使用此服务作为步骤实施。

#### 动态参与者步骤 — 参与者选择器服务示例 {#dynamic-participant-step-example-participant-chooser-service}

以下Java™类实现 `ParticipantStepChooser` 界面。 类返回启动工作流的参与者的名称。 该代码使用与示例脚本(`initiator-participant-chooser.ecma`)。

的 `@Property` 注释设置 `SERVICE_PROPERTY_LABEL` 字段 `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

在 **动态参与者步骤** 属性对话框， **参与者选择器** 列表包含项目 `Workflow Initiator Participant Chooser (script)`，表示此服务。

启动工作流模型时，日志会指示启动工作流的用户的ID以及为该工作项分配的用户的ID。 在本例中， `admin` 用户启动了工作流。

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 表单参与者步骤 {#form-participant-step}

的 **表单参与者步骤** 在打开工作项时显示表单。 当用户填写并提交表单时，字段数据将存储在工作流有效负载的节点中。

要配置该步骤，请指定要将工作项分配到的组或用户，以及表单的路径。

>[!CAUTION]
>
>本节介绍 [用于页面创作的基础组件的Forms部分](/help/sites-authoring/default-components-foundation.md#form).

#### 表单参与者步骤 — 配置 {#form-participant-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* [用户/组](#step-properties-user-group-tab)
* **表单**

   * **表单路径**:路径 [创建的表单](#form-participant-step-creating-the-form).

#### 表单参与者步骤 — 创建表单 {#form-participant-step-creating-the-form}

创建用于 **表单参与者步骤** 正常。 但是，表单参与者步骤的表单必须具有以下配置：

* 的 **表单开始** 组件必须具有 **操作类型** 属性设置为 `Edit Workflow Controlled Resource(s)`.
* 的 **表单开始** 组件必须具有 `Form Identifier` 属性。
* 表单组件必须具有 **元素名称** 属性设置为存储字段数据的节点的路径。 路径必须在工作流有效负载内容中找到节点。 值使用以下格式：

   `./jcr:content/path_to_node`

* 表单必须包含 **工作流提交按钮** 组件。 您不会配置组件的任何属性。

工作流的要求决定了字段数据存储的位置。 例如，字段数据可用于配置页面内容的属性。 的以下值 **元素名称** 属性将字段数据存储为 `redirectTarget` 属性 `jcr:content` 节点：

`./jcr:content/redirectTarget`

在以下示例中，字段数据用作 **文本** 有效负载页面上的组件：

`./jcr:content/par/text_3/text`

第一个示例可用于 `cq:Page` 组件呈现。 仅当有效负载页面包含 **文本** ID为 `text_3`.

表单可以位于存储库中的任意位置，但必须授权工作流用户读取表单。

### 随机参与者选择器 {#random-participant-chooser}

的 **随机参与者选择器** 步骤是参与者选择器，用于将生成的工作项分配给从列表中随机选择的用户。

![wf-31](assets/wf-31.png)

#### 随机参与者选择器 — 配置 {#random-participant-chooser-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **参数**

   * **参与者**:指定可供选择的用户列表。 要将用户添加到列表，请单击 **添加项目** 并键入用户节点或用户ID的主路径。 用户的顺序不会影响为工作项目分配的可能性。

### 工作流发起者参与人选择器 {#workflow-initiator-participant-chooser}

的 **工作流启动器参与者选择器** 步骤是一个参与者选择器，用于将生成的工作项分配给启动工作流的用户。 除 **常用** 属性。

#### 工作流启动器参与者选择器 — 配置 {#workflow-initiator-participant-chooser-configuration}

要配置该步骤，请使用以下选项卡进行编辑：

* [通用](#step-properties-common-tab)

## 流程步骤 {#process-step}

A **流程步骤** 执行ECMAScript或调用OSGi服务以执行自动处理。

![wf-32](assets/wf-32.png)

### 流程步骤 — 配置 {#process-step-configuration}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](#step-properties-common-tab)
* **进程**

   * **进程**:要执行的进程实施。 使用下拉菜单选择ECMAScript或OSGi服务。 有关信息:

      * 标准ECMAScript和OSGi服务，请参阅 [用于流程步骤的内置流程](/help/sites-developing/workflows-process-ref.md).
      * 为流程步骤创建ECMAScript，请参阅 [使用ECMAScript实施流程步骤](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * 为流程步骤创建OSGi服务，请参阅 [使用Java™类实施流程步骤](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).
   * **处理程序高级**:选择此选项可在执行后自动将工作流推进到下一步。 如果未选择，则实施脚本必须处理工作流进度。
   * **参数**:要传递到进程的参数。


## 设置变量 {#set-variable}

通过设置变量步骤，您可以设置变量的值并定义值的设置顺序。 变量按变量映射在设置变量步骤中列出的顺序进行设置。

![添加映射以设置变量](assets/set_variable_addmappingnew.png)

### 设置变量 — 配置 {#setvariable}

要配置该步骤，请编辑并使用以下选项卡：

* [通用](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **映射**

   * **选择变量：** 使用此选项可选择一个变量以设置其值。
   * **选择映射模式：**  要设置变量的值，请选择映射模式。 根据变量的数据类型，您可以使用以下选项设置变量的值：

      * **文字：** 当您知道要指定的确切值时，请使用选项。
      * **表达式：** 根据表达式计算要使用的值时，请使用选项。 表达式在提供的表达式编辑器中创建。
      * **JSON点表示法：** 使用选项从JSON或FDM类型变量中检索值。
      * **XPATH:** 使用选项从XML类型变量中检索值。
      * **相对于有效负载：** 当要保存到变量的值在相对于有效负载的路径上可用时，请使用选项。
      * **绝对路径：** 当要保存到变量的值在绝对路径中可用时，请使用选项。
   * **指定值：** 要映射到变量，请指定一个值。 在此字段中指定的值取决于映射模式。
   * **添加映射：** 使用此选项可添加更多映射来设置变量的值。
