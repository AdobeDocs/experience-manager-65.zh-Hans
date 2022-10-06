---
title: 为自适应表单字段创建自定义外观
seo-title: Create custom appearances for adaptive form fields
description: 在自适应Forms中自定义现成组件的外观。
seo-description: Customize appearance of out-of-the-box components in Adaptive Forms.
uuid: 1aa36443-774a-49fb-b3d1-d5a2d5ff849a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d388acef-7313-4e68-9395-270aef6ef2c6
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
source-git-commit: 8a24ca02762e7902b7d0033b36560629ee711de1
workflow-type: tm+mt
source-wordcount: '1713'
ht-degree: 0%

---

# 为自适应表单字段创建自定义外观{#create-custom-appearances-for-adaptive-form-fields}

## 简介 {#introduction}

自适应表单可利用 [外观框架](/help/forms/using/introduction-widgets.md) 以帮助您为自适应表单字段创建自定义外观并提供不同的用户体验。 例如，将单选按钮和复选框替换为切换按钮，或使用自定义jQuery插件限制用户在电话号码或电子邮件ID等字段中的输入。

本文档介绍如何使用jQuery插件为自适应表单字段创建这些替代体验。 此外，它还显示一个示例，用于为数字字段组件创建自定义外观以显示为数字步进器或滑块。

让我们首先看一下本文中使用的关键术语和概念。

**外观** 指自适应表单字段各种元素的样式、外观和组织。 它通常包括标签、用于提供输入的交互区域、帮助图标以及字段的简短和长描述。 本文所讨论的外观定制适用于该字段输入区域的外观。

**jQuery插件** 提供基于jQuery小组件框架的标准机制来实施替代外观。

**ClientLib** 由复杂的JavaScript和CSS代码驱动的AEM客户端处理中的客户端库系统。 有关更多信息，请参阅使用客户端库。

**原型** Maven项目模板工具包，定义为Maven项目的原始模式或模型。 有关更多信息，请参阅原型简介。

**用户控制** 是指小组件中包含字段值的主元素，用于将自定义小组件UI与自适应表单模型绑定的外观框架。

## 创建自定义外观的步骤 {#steps-to-create-a-custom-appearance}

创建自定义外观的高级步骤如下所示：

1. **创建项目**:创建一个Maven项目，以生成要在AEM上部署的内容包。
1. **扩展现有小组件类**:扩展现有小组件类并覆盖所需的类。
1. **创建客户端库**:创建 `clientLib: af.customwidget` 库，并添加所需的JavaScript和CSS文件。

1. **构建和安装项目**:构建Maven项目，并在AEM上安装生成的内容包。
1. **更新自适应表单**:更新自适应表单字段属性以使用自定义外观。

### 创建项目 {#create-a-project}

Maven原型是创建自定义外观的起点。 要使用的原型的详细信息如下：

* **存储库**:https://repo1.maven.org/maven2/com/adobe/
* **项目ID**:custom-appearance-archetype
* **组ID**:com.adobe.aemforms
* **版本**:1.0.4

执行以下命令以基于原型创建本地项目：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

该命令从存储库下载Maven插件和原型信息，并根据以下信息生成项目：

* **groupId**:生成的Maven项目使用的组ID
* **artifactId**:生成的Maven项目使用的项目ID。
* **版本**:生成的Maven项目的版本。
* **软件包**:用于文件结构的包。
* **artifactName**:生成的AEM包的对象名称。
* **packageGroup**:生成的AEM包的包组。
* **widgetName**:用于引用的外观名称。

生成的项目具有以下结构：

```java
─<artifactId>

 └───src

     └───main

         └───content

             └───jcr_root

                 └───etc

                     └───clientlibs

                         └───custom

                             └───<widgetName>

                                 ├───common [client library - af.customwidgets which encapsulates below clientLibs]

                                 ├───integration [client library - af.customwidgets.<widgetName>_widget which contains template files for integrating a third-party plugin with Adaptive Forms]

                                 │   ├───css

                                 │   └───javascript

                                 └───jqueryplugin [client library - af.customwidgets.<widgetName>_plugin which holds the third-party plugins and related dependencies]

                                     ├───css

                                     └───javascript
```

### 扩展现有小组件类 {#extend-an-existing-widget-class}

创建项目模板后，根据需要进行以下更改：

1. 将第三方插件依赖项包含到项目中。

   1. 将第三方或自定义jQuery插件放置在 `jqueryplugin/javascript` 文件夹和 `jqueryplugin/css` 文件夹。 有关更多详细信息，请参阅 `jqueryplugin/javascript and jqueryplugin/css` 文件夹。

   1. 修改 `js.txt` 和 `css.txt` 文件，以包含jQuery插件的任何其他JavaScript和CSS文件。

1. 将第三方插件与框架集成，以启用自定义外观框架与jQuery插件之间的交互。 只有在您扩展或覆盖以下功能后，新小组件才能正常工作。

<table>
 <tbody>
  <tr>
   <td><strong>函数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>呈现函数返回小组件默认HTML元素的jQuery对象。 默认HTML元素应为可聚焦类型。 例如， <code>&lt;a&gt;</code>, <code>&lt;input&gt;</code>和 <code>&lt;li&gt;</code>. 返回的元素将用作 <code>$userControl</code>. 如果 <code>$userControl</code> 指定上述约束， <code>AbstractWidget</code> 类可按预期工作，否则某些常用API（焦点、单击）需要进行更改。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> <code class="code">{
      blur: XFA_EXIT_EVENT,
      }</code><br /> 此示例显示 <code>blur</code> 是HTML事件，并且 <code>XFA_EXIT_EVENT</code> 是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>返回一个映射，其中提供了有关更改选项时要执行的操作的详细信息。 键是提供给小组件的选项，值是每当检测到选项发生更改时调用的函数。 小组件为所有常用选项( <code>value</code> 和 <code>displayValue</code>)。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每当jQuery小组件的值保存在XFA模型中（例如，文本字段的退出事件）时，jQuery小组件框架便会加载该函数。 实施应返回小组件中保存的值。 处理程序将为选项提供新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>默认情况下，在XFA中，输入事件时， <code>rawValue</code> 的子代。 此函数被调用以显示 <code>rawValue</code> 。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>默认情况下，在退出时的XFA中， <code>formattedValue</code> 的子代。 此函数被调用以显示 <code>formattedValue</code> 。 </td>
  </tr>
 </tbody>
</table>

1. 在 `integration/javascript` 文件夹。

   * 替换文本 `__widgetName__` 以及实际的小组件名称。
   * 通过合适的现成小组件类扩展小组件。 在大多数情况下，它是与要替换的现有小组件对应的小组件类。 父类名称在多个位置使用，因此建议搜索字符串的所有实例 `xfaWidget.textField` ，并将其替换为使用的实际父类。
   * 扩展 `render` 方法来提供替代UI。 它是将从中调用jQuery插件以更新UI或交互行为的位置。 的 `render` 方法应返回用户控制元素。

   * 扩展 `getOptionsMap` 方法覆盖因小组件更改而受影响的任何选项设置。 函数会返回一个映射，该映射提供了在更改选项时要执行的操作的详细信息。 键是提供给小组件的选项，值是每当检测到选项发生更改时调用的函数。
   * 的 `getEventMap` 方法将小组件触发的事件与自适应表单模型所需的事件进行映射。 默认值映射默认小组件的标准HTML事件，如果触发替代事件，则需要更新。
   * 的 `showDisplayValue` 和 `showValue` 应用display and edit picture子句，并且可以被覆盖以具有替代行为。

   * 的 `getCommitValue` 方法在 `commit`事件。 通常，它是退出事件，但下拉列表、单选按钮和发生更改的复选框元素除外)。 有关更多信息，请参阅 [自适应Forms表达式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p).

   * 模板文件为各种方法提供了实施示例。 删除未扩展的方法。

### 创建客户端库 {#create-a-client-library}

由Maven原型生成的示例项目会自动创建所需的客户端库，并将它们包装到具有类别的客户端库中 `af.customwidgets`. 在 `af.customwidgets` 在运行时自动包含。

### 构建和安装 {#build-and-install}

要构建项目，请在shell中执行以下命令，以生成需要安装在AEM服务器上的CRX包。

`mvn clean install`

>[!NOTE]
>
>Maven项目引用POM文件内的远程存储库。 这仅供参考，并且根据Maven标准，存储库信息将在 `settings.xml` 文件。

### 更新自适应表单 {#update-the-adaptive-form}

要将自定义外观应用于自适应表单字段，请执行以下操作：

1. 在编辑模式下打开自适应表单。
1. 打开 **属性** 对话框。
1. 在 **样式** 选项卡，更新 `CSS class` 属性，以在 `widget_<widgetName>` 格式。 例如： **widget_numericstepper**

## 示例：创建自定义外观   {#sample-create-a-custom-appearance-nbsp}

现在，我们来看一个示例，以创建一个自定义外观，使数字字段显示为数字步进器或滑块。 执行以下步骤：

1. 执行以下命令以创建基于Maven原型的本地项目：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它会提示您为以下参数指定值。
   *此示例中使用的值以粗体突出显示*.

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 导航到 `customWidgets` (为 `artifactID` 属性)目录并执行以下命令以生成Eclipse项目：

   `mvn eclipse:eclipse`

1. 打开Eclipse工具，然后执行以下操作以导入Eclipse项目：

   1. 选择 **[!UICONTROL “文件”>“导入”>“将现有项目导入工作区”]**.

   1. 浏览并选择您执行的文件夹 `archetype:generate` 命令。

   1. 单击 **[!UICONTROL 完成]**.

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. 选择要用于自定义外观的小组件。 此示例使用以下数字步进小组件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse项目中，查看 `plugin.js` 文件以确保其符合外观要求。 在此示例中，外观满足以下要求：

   * 数字步进器应从 `- $.xfaWidget.numericInput`.
   * 的 `set value` 小组件的方法，可在焦点位于字段后设置值。 对于自适应表单小组件，这是一项强制要求。
   * 的 `render` 需要覆盖方法才能调用 `bootstrapNumber` 方法。

   * 除了插件的主源代码之外，该插件没有其他依赖项。
   * 该示例不对步进器执行任何样式，因此不需要其他CSS。
   * 的 `$userControl` 对象应可用于 `render` 方法。 它是 `text` 类型，使用插件代码克隆。

   * 的 **+** 和 **-** 在禁用字段时，应禁用按钮。

1. 替换 `bootstrap-number-input.js` 包含 `numericStepper-plugin.js` 文件。
1. 在 `numericStepper-widget.js` 文件中，添加以下代码以覆盖用于调用插件的render方法并返回 `$userControl` 对象：

   ```javascript
   render : function() {
        var control = $.xfaWidget.numericInput.prototype.render.apply(this, arguments);
        var $control = $(control);
        var controlObject;
        try{
            if($control){
            $control.bootstrapNumber();
            var id = $control.attr("id");
            controlObject = $("#"+id);
            }
        }catch (exc){
             console.log(exc);
        }
        return controlObject;
   }
   ```

1. 在 `numericStepper-widget.js` 文件，覆盖 `getOptionsMap` 属性覆盖访问选项，并在禁用模式下隐藏+和 — 按钮。

   ```javascript
   getOptionsMap: function(){
       var parentOptionsMap = $.xfaWidget.numericInput.prototype.getOptionsMap.apply(this,arguments),
   
       newMap = $.extend({},parentOptionsMap,
   
        {
   
              "access": function(val) {
              switch(val) {
                 case "open" :
                   this.$userControl.removeAttr("readOnly");
                   this.$userControl.removeAttr("aria-readonly");
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
                 case "nonInteractive" :
                 case "protected" :
                   this.$userControl.attr("disabled", "disabled");
                   this.$userControl.attr("aria-disabled", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
                case "readOnly" :
                   this.$userControl.attr("readOnly", "readOnly");
                   this.$userControl.attr("aria-readonly", "true");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',true);
                   break;
               default :
                   this.$userControl.removeAttr("disabled");
                   this.$userControl.removeAttr("aria-disabled");
                   this.$userControl.parent().find(".input-group-btn button").prop('disabled',false);
                   break;
             }
          },
      });
      return newMap;
    }
   ```

1. 保存更改，导航到包含 `pom.xml` ，然后执行以下Maven命令来构建项目：

   `mvn clean install`

1. 使用AEM包管理器安装包。

1. 在编辑模式下打开要应用自定义外观的自适应表单，然后执行以下操作：

   1. 右键单击要应用外观的字段，然后单击 **[!UICONTROL 编辑]** 打开编辑组件对话框。

   1. 在样式选项卡中，更新 **[!UICONTROL CSS类]** 添加属性 `widget_numericStepper`.

您刚刚创建的新外观现已可供使用。
