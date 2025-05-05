---
title: 为自适应表单字段创建自定义外观
description: 在自适应Forms中自定义现成组件的外观。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 770e257a-9ffd-46a4-9703-ff017ce9caed
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# 为自适应表单字段创建自定义外观{#create-custom-appearances-for-adaptive-form-fields}

## 简介 {#introduction}

自适应表单使用[外观框架](/help/forms/using/introduction-widgets.md)来帮助您为自适应表单字段创建自定义外观，并提供不同的用户体验。 例如，使用切换按钮替换单选按钮和复选框，或使用自定义jQuery插件限制用户在电话号码或电子邮件ID等字段中输入。

本文档介绍如何使用jQuery插件为自适应表单字段创建这些替代体验。 此外，还展示了一个为数字字段组件创建自定义外观的示例，该组件显示为数字步进器或滑块。

让我们先看一下本文中使用的主要术语和概念。

**外观**&#x200B;指自适应表单字段各种元素的样式、外观和组织。 它通常包括标签、用于提供输入的交互式区域、帮助图标以及字段的简短和长描述。 本文讨论的外观定制适用于字段输入区域的外观。

**jQuery插件**&#x200B;提供基于jQuery构件框架的标准机制，以实施替代外观。

**ClientLib** AEM客户端处理中的客户端库系统，由复杂的JavaScript和CSS代码驱动。 有关更多信息，请参阅使用客户端库。

**Archetype**&#x200B;定义为Maven项目原始模式或模型的Maven项目模板工具包。 有关详细信息，请参阅原型简介。

**用户控件**&#x200B;引用包含字段值的小部件中的主元素，该主元素由外观框架用于绑定自定义小部件UI与自适应表单模型。

## 创建自定义外观的步骤 {#steps-to-create-a-custom-appearance}

创建自定义外观的高级别步骤如下：

1. **创建项目**：创建一个Maven项目，该项目生成内容包以在AEM上部署。
1. **扩展现有的构件类**：扩展现有的构件类并覆盖所需的类。
1. **创建客户端库**：创建`clientLib: af.customwidget`库并添加所需的JavaScript和CSS文件。

1. **生成并安装项目**：生成Maven项目并在AEM上安装生成的内容包。
1. **更新自适应表单**：更新自适应表单字段属性以使用自定义外观。

### 创建项目 {#create-a-project}

maven原型是创建自定义外观的起点。 要使用的原型的详细信息如下：

* **存储库**： https://repo1.maven.org/maven2/com/adobe/
* **项目ID**： custom-appearance-archetype
* **组ID**： com.adobe.aemforms
* **版本**： 1.0.4

执行以下命令以基于原型创建本地项目：

`mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

该命令从存储库下载Maven插件和原型信息，并根据以下信息生成项目：

* **groupId**：生成的Maven项目使用的组ID
* **artifactId**：生成的Maven项目使用的项目ID。
* **版本**：生成的Maven项目的版本。
* **包**：用于文件结构的包。
* **artifactName**：生成的AEM包的工件名称。
* **packageGroup**：生成的AEM包的包组。
* **widgetName**：用于引用的外观名称。

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

### 扩展现有构件类 {#extend-an-existing-widget-class}

创建项目模板后，根据需要进行以下更改：

1. 将第三方插件依赖关系包含在项目中。

   1. 将第三方或自定义jQuery插件放在`jqueryplugin/javascript`文件夹中，并将相关的CSS文件放在`jqueryplugin/css`文件夹中。 有关详细信息，请参阅`jqueryplugin/javascript and jqueryplugin/css`文件夹下的JS和CSS文件。

   1. 修改`js.txt`和`css.txt`文件以包含jQuery插件的任何其他JavaScript和CSS文件。

1. 将第三方插件与框架集成，以启用自定义外观框架与jQuery插件之间的交互。 只有在扩展或覆盖以下功能后，新小组件才能正常工作。

<table>
 <tbody>
  <tr>
   <td><strong>函数</strong></td>
   <td><strong>描述</strong></td>
  </tr>
  <tr>
   <td><code>render</code></td>
   <td>渲染函数为小部件的默认HTML元素返回jQuery对象。 默认的HTML元素应为可聚焦类型。 例如，<code>&lt;a&gt;</code>、<code>&lt;input&gt;</code>和<code>&lt;li&gt;</code>。 返回的元素用作<code>$userControl</code>。 如果<code>$userControl</code>指定上述约束，<code>AbstractWidget</code>类的函数将按预期工作，否则某些常用API（集中、单击）需要更改。 </td>
  </tr>
  <tr>
   <td><code>getEventMap</code></td>
   <td>返回将HTML事件转换为XFA事件的映射。 <br /> <code class="code">&lbrace;
      blur: XFA_EXIT_EVENT,
      &rbrace;</code><br />此示例显示<code>blur</code>是一个HTML事件，<code>XFA_EXIT_EVENT</code>是相应的XFA事件。 </td>
  </tr>
  <tr>
   <td><code>getOptionsMap</code></td>
   <td>返回一个映射，该映射提供更改选项时要执行的操作的详细信息。 键是提供给构件的选项，值是检测到选项更改时调用的函数。 该构件为所有常用选项（除<code>value</code>和<code>displayValue</code>之外）提供了处理程序。</td>
  </tr>
  <tr>
   <td><code>getCommitValue</code></td>
   <td>每当jQuery构件的值保存在XFA模型中（例如，在文本字段的退出事件中）时，jQuery构件框架都会加载函数。 该实施应返回保存在构件中的值。 将为处理程序提供选项的新值。</td>
  </tr>
  <tr>
   <td><code>showValue</code></td>
   <td>默认情况下，在输入事件的XFA中，将显示字段的<code>rawValue</code>。 调用此函数是为了向用户显示<code>rawValue</code>。 </td>
  </tr>
  <tr>
   <td><code>showDisplayValue</code></td>
   <td>默认情况下，在退出事件的XFA中，将显示字段的<code>formattedValue</code>。 调用此函数是为了向用户显示<code>formattedValue</code>。 </td>
  </tr>
 </tbody>
</table>

1. 根据需要更新`integration/javascript`文件夹中的JavaScript文件。

   * 将文本`__widgetName__`替换为实际的构件名称。
   * 从适当的现成可用构件类扩展构件。 在大多数情况下，它是与要替换的现有构件对应的构件类。 父类名称在多个位置使用，因此建议搜索文件中字符串`xfaWidget.textField`的所有实例，并将它们替换为使用的实际父类。
   * 扩展`render`方法以提供替代UI。 这是调用jQuery插件以更新UI或交互行为的位置。 `render`方法应返回用户控制元素。

   * 扩展`getOptionsMap`方法以覆盖由于小部件中的更改而受影响的任何选项设置。 函数将返回一个映射，该映射提供了在更改选项时执行的操作的详细信息。 键是提供给构件的选项，值是检测到选项更改时调用的函数。
   * `getEventMap`方法会将构件触发的事件映射到自适应表单模型所需的事件。 默认值映射默认小组件的标准HTML事件，如果触发了备用事件，则需要更新。
   * `showDisplayValue`和`showValue`应用display and edit picture子句，可以覆盖为具有替代行为。

   * 当发生`commit`事件时，`getCommitValue`方法由自适应表单框架调用。 通常，它是退出事件（除了下拉列表、单选按钮和复选框元素，在更改时会发生退出事件）。 有关详细信息，请参阅[自适应Forms表达式](../../forms/using/adaptive-form-expressions.md#p-value-commit-script-p)。

   * 模板文件提供了各种方法的实现示例。 删除不进行扩展的方法。

### 创建客户端库 {#create-a-client-library}

Maven原型生成的示例项目会自动创建所需的客户端库，并将其打包到具有类别`af.customwidgets`的客户端库中。 `af.customwidgets`中可用的JavaScript和CSS文件在运行时自动包含。

### 构建和安装 {#build-and-install}

要构建项目，请在shell上执行以下命令以生成需要安装在AEM服务器上的CRX包。

`mvn clean install`

>[!NOTE]
>
>maven项目引用POM文件中的远程存储库。 这仅供参考，根据Maven标准，存储库信息捕获到`settings.xml`文件中。

### 更新自适应表单 {#update-the-adaptive-form}

要将自定义外观应用于自适应表单字段，请执行以下操作：

1. 在编辑模式下打开自适应表单。
1. 打开要应用自定义外观的字段的&#x200B;**属性**&#x200B;对话框。
1. 在&#x200B;**样式**&#x200B;选项卡中，更新`CSS class`属性以`widget_<widgetName>`格式添加外观名称。 例如：**widget_numericstepper**

## 示例：创建自定义外观   {#sample-create-a-custom-appearance-nbsp}

现在，我们查看一个示例，该示例用于为显示为数值步进器或滑块的数字字段创建自定义外观。 执行以下步骤：

1. 执行以下命令可基于Maven原型创建本地项目：

   `mvn archetype:generate -DarchetypeRepository=https://repo1.maven.org/maven2/com/adobe/ -DarchetypeGroupId=com.adobe.aemforms -DarchetypeArtifactId=custom-appearance-archetype -DarchetypeVersion=1.0.4`

   它会提示您为以下参数指定值。
   *此示例中使用的值以粗体突出显示*。

   `Define value for property 'groupId': com.adobe.afwidgets`

   `Define value for property 'artifactId': customWidgets`

   `Define value for property 'version': 1.0.1-SNAPSHOT`

   `Define value for property 'package': com.adobe.afwidgets`

   `Define value for property 'artifactName': customWidgets`

   `Define value for property 'packageGroup': adobe/customWidgets`

   `Define value for property 'widgetName': numericStepper`

1. 导航到`customWidgets` （为`artifactID`属性指定的值）目录，然后执行以下命令以生成Eclipse项目：

   `mvn eclipse:eclipse`

1. 打开Eclipse工具并执行以下操作以导入Eclipse项目：

   1. 选择&#x200B;**[!UICONTROL 文件>导入>将现有项目导入Workspace]**。

   1. 浏览并选择执行`archetype:generate`命令的文件夹。

   1. 单击&#x200B;**[!UICONTROL 完成]**。

      ![eclipse-screenshot](assets/eclipse-screenshot.png)

1. 选择要用于自定义外观的构件。 此示例使用以下数字步进小组件：

   [https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html](https://www.jqueryscript.net/form/User-Friendly-Number-Input-Spinner-with-jQuery-Bootstrap.html)

   在Eclipse项目中，查看`plugin.js`文件中的插件代码，确保它符合外观要求。 在此示例中，外观满足以下要求：

   * 数值步进器应从`- $.xfaWidget.numericInput`扩展。
   * 小组件的`set value`方法会在焦点位于字段上之后设置值。 这是自适应表单小组件的强制要求。
   * 需要覆盖`render`方法才能调用`bootstrapNumber`方法。

   * 除了插件的主源代码之外，插件没有其他依赖项。
   * 该示例不会对步进器执行任何样式，因此无需其他CSS。
   * `$userControl`对象应对`render`方法可用。 它是使用插件代码克隆的`text`类型的字段。

   * 禁用字段时应禁用&#x200B;**+**&#x200B;和&#x200B;**-**&#x200B;按钮。

1. 将`bootstrap-number-input.js` （jQuery插件）的内容替换为`numericStepper-plugin.js`文件的内容。
1. 在`numericStepper-widget.js`文件中，添加以下代码以覆盖渲染方法以调用插件并返回`$userControl`对象：

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

1. 在`numericStepper-widget.js`文件中，覆盖`getOptionsMap`属性以覆盖访问选项，并在禁用模式下隐藏+和 — 按钮。

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

1. 保存更改，导航到包含`pom.xml`文件的文件夹，然后执行以下Maven命令来构建项目：

   `mvn clean install`

1. 使用AEM包管理器安装包。

1. 在要应用自定义外观的编辑模式下打开自适应表单，然后执行以下操作：

   1. 右键单击要应用外观的字段，然后单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以打开“编辑组件”对话框。

   1. 在样式选项卡中，更新&#x200B;**[!UICONTROL CSS类]**&#x200B;属性以添加`widget_numericStepper`。

您创建的新外观现在可供使用。
