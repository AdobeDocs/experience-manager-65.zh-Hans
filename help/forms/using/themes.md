---
title: 创建和使用主题
seo-title: 创建和使用主题
description: 您可以使用主题来风格化自适应表单或交互式通信并提供可视标识。 您可以跨任意数量的自适应表单或交互式通信共享主题。
seo-description: 您可以使用主题来风格化自适应表单或交互式通信并提供可视标识。 您可以跨任意数量的自适应表单或交互式通信共享主题。
uuid: 88b6b6fd-181b-48c5-ac15-2b37592bd14b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications
content-strategy: max-2018
discoiquuid: 770e9174-b648-462a-abe9-05fefa967d86
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# 创建和使用主题 {#creating-and-using-themes}

## 简介 {#introduction}

您可以创建并应用主题来使自适应表单或交互式通信风格化。 主题包含组件和面板的样式详细信息。 样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。 应用主题时，指定的样式会反映在相应的组件上。 在不引用自适应表单或交互通信的情况下独立地管理主题。

您可以：

* 创建主题
* 编辑和复制现有主题
* 下载现有主题并将其上传到AEM Forms服务器
* 管理主题的依赖关系

## 创建、下载或上传主题 {#creating-downloading-or-uploading-a-theme}

使用AEM Forms，您可以创建、下载或上传主题。 与表单、文档和字母等其他资产一样创建主题。 主题将另存为单独的实体，并包含表单等元属性。 主题是独立的实体，允许在多个自适应表单和交互式通信中重复使用。 您还可以将主题移到AEM Forms的其他实例并重复使用它。

### 创建主题 {#creating-a-theme}

执行以下步骤以创建主题：

1. 单击 **Adobe Experience Manager**，单击 **Forms**，然后单击 **主题**。

1. 在主题页面中，单击“ **创建”>“主题”**。
将启动用于创建主题的向导。

1. 在“创建主题”向导的“基本”选项卡中，提 **供主题****的“标题** ”和“名称”。 这些是必填字段。

1. 在“高级”选项卡中，您会获得两个字段：

   * **Clientlib位置**:存储主题的clientlib的存储库中的位置。

   * **Clientlib类别**:提供一个文本字段，用于输入主题的clientlib类别名称。

1. 单击 **创建** ，然后单击 **编辑** ，以在主题编辑器中打开主题，或单击 **完成** ，返回到主题页面。

### 下载主题 {#downloading-a-theme}

您可以将主题导出为zip文件，并在其他项目或AEM实例中使用这些文件。 下载主题：

1. 单击 **Adobe Experience Manager**，单击 **Forms**，然后单击 **主题**。

1. 在主题页面中，选 **择主题** ，然后单击 **下载**。 此时将显示一个包含主题详细信息的对话框。

1. 单击“ **下载**”。 主题将下载为zip文件。

>[!NOTE]
>
>如果您下载一个主题，该主题具有与其关联的自适应表单并且关联的自适应表单基于自定义模板，那么也请下载该自定义模板。 将下载的主题和自适应表单上传到AEM Forms服务器时，还需上传相关的自定义模板。

### 上传主题 {#uploading-a-theme}

您可以将创建的主题与项目上的样式预设结合使用。 您可以通过将其他人创建的主题包上传到您的项目来导入这些主题包。

要上传主题，请执行以下操作：

1. 单击 **Adobe Experience Manager**，单击 **Forms**，然后单击 **主题**。

1. 在主题页面中，单击创 **建>文件上传**。
1. 在“文件上传”提示中，浏览并选择计算机上的主题包，然后单击“上 **传”**。
上传的主题在主题页面中可用。

## 主题的元数据 {#metadata-of-a-theme}

列表主题的元属性（位于主题的属性页面中）。

<table>
 <tbody>
  <tr>
   <th><p><strong>ID</strong></p> <p> </p> </th>
   <th><strong>名称</strong></th>
   <th><strong>可编辑</strong></th>
   <th><strong>属性描述</strong></th>
  </tr>
  <tr>
   <td>1.</td>
   <td>标题</td>
   <td>是</td>
   <td>显示主题的名称。</td>
  </tr>
  <tr>
   <td>2.</td>
   <td>描述</td>
   <td>是</td>
   <td>主题说明。</td>
  </tr>
  <tr>
   <td>3.</td>
   <td>类型</td>
   <td>否</td>
   <td>
    <ul>
     <li>资产的类型。</li>
     <li>值始终为主题。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>4.</td>
   <td>创建时间</td>
   <td>否</td>
   <td>主题创建日期</td>
  </tr>
  <tr>
   <td>5.</td>
   <td>作者姓名</td>
   <td>是</td>
   <td>主题的作者。 在创建主题时计算。</td>
  </tr>
  <tr>
   <td>6.</td>
   <td>上次修改日期</td>
   <td>否</td>
   <td>上次修改主题的日期。</td>
  </tr>
  <tr>
   <td>7.</td>
   <td>状态</td>
   <td>否</td>
   <td>主题的状态（已修改／已发布）。</td>
  </tr>
  <tr>
   <td>8.</td>
   <td>按时发布</td>
   <td>是</td>
   <td>自动发布主题的时间。</td>
  </tr>
  <tr>
   <td>9.</td>
   <td>发布结束时间</td>
   <td>是</td>
   <td>是时候自动取消发布主题了。</td>
  </tr>
  <tr>
   <td>10.</td>
   <td>标记</td>
   <td>是</td>
   <td>附加到主题以用于改进搜索的标识的标签。</td>
  </tr>
  <tr>
   <td>11.</td>
   <td>引用</td>
   <td>链接</td>
   <td>
    <ul>
     <li>包含“引用者”部分。 列表使用主题的表单。</li>
     <li>由于主题不指任何其他资产，因此没有“引用”部分。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>12.</td>
   <td>Clientlib 位置</td>
   <td>是</td>
   <td>
    <ul>
     <li>“/etc”中用户定义的存储库路径，其中存储与此主题对应的clientlib。</li>
     <li>默认值- '/etc/clientlibs/fd/主题+主题资产的相对路径。</li>
     <li>如果位置不存在，则会自动生成文件夹层次结构。</li>
     <li>更改此值后，clientlib节点结构将移至输入的新位置。<br /> 注 <em><strong>意：</strong> 如果更改默认的clientlib位置，则在CRXDE存储库中，将 <code>crx:replicate, rep:write, rep:glob:*, rep:itemNames:: js.txt, jcr:read </code>其分 <code>forms-users</code> 配到新 <code>crx:replicate</code>位 <code>jcr:read </code>置和， <code>fd-service</code> 分配到新位置。 另外，通过添加 <code>deny jcr:addChildNodes</code><code>forms-user</code></em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>13.</td>
   <td>Clientlib 类别名称</td>
   <td>是</td>
   <td>
    <ul>
     <li>此主题的用户定义的clientlib类别名称。</li>
     <li>如果某些其他现有主题已使用该名称，则显示错误。</li>
     <li>默认值——使用主题位置计算。</li>
     <li>更改此值后，类别名称会在相应的clientlib节点上更新。 Updating Clientlib Category Name in the jsp files is not required because clientlib category name is used by reference.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## 关于主题编辑器 {#about-the-theme-editor}

AEM Forms随主题编辑器一起提供。 它是一个商业用户和Web设计人员／开发人员友好界面，它提供所需的功能，以便轻松指定各种自适应表单和交互式通信元素的样式。 创建主题时，它将作为单独的实体进行存储，如表单、交互通信、字母、文档片段和数据字典。

通过主题编辑器，您可以自定义主题中设置样式的组件的样式。 您可以自定义表单或交互式通信在设备上的显示方式。

主题编辑器分为两个面板：

* **Canvas** - Appears on the right side. 它显示了示例自适应表单或交互式通信，其中所有样式更改都可即时反映。 您还可以直接从画布中选择对象，以查找与其关联的样式，并编辑这些样式。 顶部的设备分辨率标尺将控制画布。 从标尺中选择分辨率断点可显示示例表单的预览或相应分辨率的交互式通信。 下面将详细介绍画 [布](../../forms/using/themes.md#using-canvas)。

* **侧栏**-显示在左侧。 它包含以下项目：

   * **选择器：** 显示为样式选择的组件及其可设置样式的属性。 选择器表示类型的所有组件。 如果您在主题中选择一个文本框组件来设置样式，则表单或交互式通信中的所有文本框都将继承该样式。 选择器允许您为样式选择通用组件或特定组件。 例如，字段组件是通用组件，文本框是特定组件。

      **样式通用组件：**字段可以是数字框字段（如年龄）或文本框字段（如地址）。
设置字段样式时，将设置所有字段（如年龄、名称、地址）的样式。

      **样式特定组件**:特定组件会影响特定类别的对象。 设置主题中数字框组件的样式时，只有样式中的数字框对象继承该样式。

      例如，文本框字段（如地址）的长度较长，数字框字段（如页面）的长度较短。 您可以选择一个数字框字段，缩短其长度并应用于表单。 Width of all numeric box fields is reduced in your form.

      当您使用特定的背景颜色自定义所有字段组件时，所有字段（如年龄、名称和地址）都将继承背景颜色。 When you select a numeric box, such as age, and reduce its width, width of all the numeric boxes such as age, number of people in a family is reduced. 文本框的宽度未更改。

   * **州：** 允许您自定义特定状态中对象的样式。 例如，您可以指定对象处于默认、焦点、禁用、悬停或错误状态时的外观。
   * **财产类别:** 样式属性分为多个类别。 例如，“尺寸和位置”、“文本”、“背景”、“边框”和“效果”。 在每个类别下，您提供样式信息。 例如，在“背景”下，可以提供“背景颜色”和“图像和渐变”。

   * **高级：** 允许您向对象添加自定义CSS，该对象将覆盖存在重叠时定义的可视控件属性。

   * **视图CSS**:允许您视图所选组件的CSS
   此外，在侧栏中，底部还有箭头。 单击箭头时，您还可以获得两个选项：模拟 **成功** 和模 **拟错误。** 这些选项以及上述选项将在下文中详细讨 [论](../../forms/using/themes.md#using-rail)。

[ 高亮 ![显示边栏和画布的主题编辑器。](assets/themes.png)](assets/themes-1.png) **A.** 提要 **栏B。** 画布

### 样式组件 {#styling-components}

You can use a theme in multiple adaptive forms and interactive communications, which imports the component formatting that you have specified in the theme. You can style various components such as titles, description, panels, fields, icons, and text boxes. Use widgets to configure component properties in a theme. Prior knowledge of CSS or LESS is not required but desired, though the CSS Overrides section lets you write CSS code or provide custom selectors. The CSS Overrides section appears when you select a component in the sidebar.

![Stylable components in the sidebar](assets/stylable-components.png)

Options in sidebar that let you select and style different components.

Clicking edit button against a component in the sidebar selects the component in Canvas, and lets you style the component using options in the sidebar.

Certain components like text box, numeric box, radio button, and check box are categorized under generic components like Field. For example, you want to customize styling of radio buttons. To select radio buttons for styling, select **Field > Widget > Radio Button**.

Click **EXPAND ALL** in the sidebar to view, select, and style categorized components that are not visible upfront.

### Styling panel layouts {#styling-panel-layouts-br}

AEM Forms中的主题支持在表单和交互式通信中的面板布局中设置元素样式。 支持在开箱即用的布局和自定义布局中设置元素样式。

现成面板包括：

* 左侧选项卡
* 顶部选项卡
* 折叠
* 响应
* 向导
* 移动布局

   * 标题中的面板标题
   * 标题中没有面板标题

选择器因每个布局而异。
从主题编辑器设置自定义布局的样式涉及：

* 为可设置样式的布局定义组件，为唯一标识这些组件的CSS选择器
* Defining the CSS properties that can be applied on these components
* Define the styling for these components interactively from the user interface

### Different styles for different screen sizes {#different-styles-for-different-screen-sizes-br}

Desktop and mobile layouts can have slightly or entirely different styles. For mobile devices, tablet and phone share similar layouts except for component sizes.

Use Theme Editor breakpoints to define alternate styling for different screen sizes. You can select a base device or resolution on which you start building the theme, and the styling variations for other resolutions are automatically generated. You can explicitly modify the styling for all the resolutions.

>[!NOTE]
>
>The theme is first created using a form or interactive communication, and then applied on different forms or interactive communications. The breakpoints used in theme creation can be different from the form or interactive communication on which the theme is applied. The CSS media queries are based on the form or interactive communication used in theme creation, and not the form or interactive communication on which the theme is applied.

### Styling properties context changes in sidebar on selecting objects {#styling-properties-context-changes-in-sidebar-on-selecting-objects}

在画布中选择组件时，其样式属性将列在提要栏中。 选择对象类型及其状态，然后提供其样式。

### 主题编辑器中最近使用的样式 {#recently-used-styles-in-theme-editor}

Theme editor caches upto 10 styles applied to a component. You can use the cached styles with other component of a theme. Recently-used styles are available right below the selected component in sidebar as a list box. 最初，最近使用的样式列表为空。

![资源库](assets/asset-library.png)

As you style a component, the styles are cached and listed in the list box. In this example, the label of the text box is styled to change the font size and color. 您可以按照类似的步骤选择图像或更改颜色以设置组件样式。 Observe how the style is cached and listed in the list box when the field label styling is changed.

![Font style cached for a component available for another](assets/font-style-cached.png)

In this example, style for the field label is changed, and when Responsive Panel Description is selected for style, a list entry is added in the asset library. The entry in the asset library can be used to change the style for Responsive Panel Description.

When a style is added in the asset library, it is available for other themes and in the [style mode](../../forms/using/inline-style-adaptive-forms.md) of the form editor or interactive communication editor UI. Similarly, when you use the style mode of the form editor or interactive communication editor UI to style a component, the style is cached and is available in themes.

通过资产库的加号按钮，您可以永久保存带有您提供的名称的样式。 The plus button saves the style even if you do not click the Save button in the sidebar to apply the style to a component. The plus button to save a style for later use is not available in the style mode.

![Providing a custom style name for asset libary](assets/custom-style-name.png)

When you provide a custom name for a style, the style is tied to a theme and is no longer available to other themes. 删除保存的样式：

1. 在“画布”工具栏上，单击“ **主题选项** ” ![](https://helpx.adobe.com/content/dam/help/en/aem-forms/6-2/theme-options.png) >“ **管理样式”**。
1. In the Manage Styles dialog, select a saved style, click **Delete**.

   ![Delete the saved style](assets/manage-styles.png)

### Live preview, save, and discard changes {#live-preview-save-and-discard-changes}

样式中所做的修改会立即反映在画布中加载的表单或交互式通信中。 Live preview lets you interactively define and see the impact of the styling. When you change the styling of a component, the **Done** button is enabled in the sidebar. To retain changes, use the **Done** button.

>[!NOTE]
>
>When an invalid character is entered in a field, the field boundary color changes to red and an error message is displayed at the top-left corner of the screen. For example, if you enter alphabets in a textbox which accepts numeric characters as inputs, the input box boundary color changed to red. You cannot save such a theme without resolving the error displayed on the top.

### 具有其他自适应表单或交互式通信的主题 {#theme-with-another-adaptive-form-or-interactive-communication}

When you create a theme, it is created with a form that is shipped with the Theme Editor. You provide styling for components in this form. Instead of the form that is shipped with the Theme Editor, you can select a form or interactive communication of your choice to provide styling and preview its results.

To replace the current form or interactive communication in Theme Editor Canvas:

1. In the THEME EDITOR panel, click **Theme Options** ![theme-options](assets/theme-options.png) > **Configure**.

1. 在“常规”选项卡中，浏览并选择“自适应表单/文档”字段的 **表单或交互式通信** 。

### 重做／撤消 {#redo-undo}

您可以撤消或重做意外发生的不需要的更改。 使用画布中的重做／撤消按钮。

![重做和撤消操作](assets/redo_undo_new.png)

画布中的撤消／重做按钮

在主题编辑器中设置组件样式时，将显示重做／撤消按钮。

## 使用主题编辑器 {#using-the-theme-editor}

通过主题编辑器，您可以编辑您创建或上传的主题。 导航到“表 **单和文档”>“主题”**，然后选择一个主题并将其打开。 主题将在主题编辑器中打开。

如上所述，主题编辑器有两个面板：提要栏和画布。
![主题编辑器](assets/theme-editor.png)

在主题编辑器中自定义文本框构件组件的成功状态样式。 组件在画布中处于选中状态，其状态在提要栏中处于选中状态。 侧栏中可用的样式选项用于自定义组件的外观。

### 使用画布 {#using-canvas}

主题是使用现成表单创建的，或者使用您选择的表单或交互式通信创建的。 画布显示用于创建主题的表单或交互式通信的预览，主题中指定了自定义设置。 表单上方的标尺用于根据设备的显示大小确定布局。

在画布工具栏中，您会看到：

* **切换侧面板**![切换侧面板](assets/toggle-side-panel.png):允许您显示或隐藏提要栏。
* **主题选项**![主题选项](assets/theme-options.png):提供三个选项

   * 配置：提供选项以选择预览表单或交互式通信、基本clientlib和typekit配置。
   * 视图主题CSS:为所选主题生成CSS。
   * 管理样式：提供用于管理文本和图像样式的选项
   * 帮助：运行主题编辑器的图像向导导览。

* **模拟器**![标尺](assets/ruler.png):模拟不同显示大小的主题外观。 显示大小在模拟器中被视为断点。 您可以选择断点并为其指定样式。 例如，桌面和平板电脑是两个断点。 可以为每个断点指定不同的样式。

在画布中选择组件时，您会在其顶部看到组件工具栏。 组件工具栏允许您选择组件或切换到通用组件。 例如，在面板中选择一个数字文本框。 您会在组件工具栏中看到以下选项：

* **数字框构件**:允许您选择组件以在提要栏中自定义其外观。
* **字段构件**:允许您选择用于样式的通用组件。 在此示例中，所有文本输入组件（文本框／数字框／数字步进器／日期输入）都被选中用于样式设置。

* ![field-level](assets/field-level.png):允许您切换到通用组件进行样式设置。 如果选择数字框并点按此图标，则会选择字段组件。 如果选择字段组件并点按此图标，则会选择面板。 如果继续点按此图标进行选择，则最后将选择样式布局。

>[!NOTE]
>
>组件工具栏中的可用选项因您选择的组件而异。

![组件工具栏](assets/overlay.png)

画布中数字框上的组件工具栏

### 使用提要栏 {#using-rail}

主题编辑器中的提要栏提供了自定义主题中组件样式和使用选择器的选项。 选择器允许您选择一组组件或单个组件，并可在提要栏中搜索选择器。 您可以为自定义组件编写选择器。

当您从提要栏的画布或选择器中选择组件时，提要栏会显示允许您为其自定义样式的所有选项。
以下是您在选择组件时在提要栏中看到的选项：

* 状态
* 属性表
* 模拟错误／成功

#### 状态 {#state}

状态是用户与组件交互的指示器。 例如，当用户在文本框中输入错误数据时，文本框的状态将变为错误状态。 通过主题编辑器，可指定特定状态的样式。

用于自定义状态样式的选项因不同组件而异。

#### 属性表 {#property-sheet}

<table>
 <tbody>
  <tr>
   <td><strong>属性</strong></td>
   <td><strong>用法</strong></td>
  </tr>
  <tr>
   <td><p>尺寸及位置</p> </td>
   <td><p>允许您设置主题中组件的对齐方式、大小、位置和置入样式。 </p> <p>您的选项包括显示设置、填充、边距、宽度、高度和Z索引。</p> <p>您还可以使用布局模式通过简单的拖放界面定义组件的宽度。 有关详细信息，请参 <a href="../../forms/using/resize-using-layout-mode.md">阅使用布局模式调整组件大小</a>。</p> </td>
  </tr>
  <tr>
   <td><p>文本</p> </td>
   <td><p>允许您自定义主题组件中的文本样式。</p> <p>例如，您希望更改在文本框中输入的文本的外观。</p> <p>您的选项包括字体系列、权重、颜色、大小、行高、文本对齐、字母间距、文本缩进、下划线、斜体、文本变换、垂直对齐、基线和方向。 </p> </td>
  </tr>
  <tr>
   <td><p>背景 </p> </td>
   <td><p>允许您使用图像或颜色填充组件的背景。 </p> </td>
  </tr>
  <tr>
   <td><p>边框</p> </td>
   <td><p>允许您选择组件边框的外观。 例如，您希望文本框有一个深红色的粗边框，边框带有虚线。 </p> <p>您的选项是边框的宽度、样式、半径和颜色。</p> </td>
  </tr>
  <tr>
   <td><p>效果</p> </td>
   <td><p>允许您向不透明度、混合模式和阴影等组件添加特殊效果。 </p> </td>
  </tr>
  <tr>
   <td><p>高级</p> </td>
   <td><p>允许您添加：</p>
    <ul>
     <li>用于在选 <code>::before</code> 择器 <code>::after</code> 中默认内容之后或之前添加内容的伪元素的属性，并设置其样式。<br /> 请参 <a href="https://www.w3schools.com/css/css_pseudo_elements.asp" target="_blank">阅CSS伪元素</a>。</li>
     <li>内嵌到组件的自定义CSS代码并编写自定义选择器。 </li>
    </ul> <p>添加自定义CSS代码时，它将覆盖您使用提要栏中的选项添加的自定义。 </p> </td>
  </tr>
 </tbody>
</table>

#### 模拟错误／成功 {#simulate-error-success}

“模拟错误”和“成功”选项位于提要栏底部。 您可以使用侧栏底部可见的显示／隐藏箭头查看它们。 使用主题编辑器，您可以设置组件的各种状态的样式。

例如，您在表单中添加一个数字字段，然后在主题编辑器中指定其样式。 当用户在字段中键入字母数字值时，您希望文本框的背景颜色发生更改。 在主题中选择数字字段，然后使用提要栏中的状态选项。 在提要栏中选择“错误”状态，并将背景颜色更改为红色。 要预览行为，您可以使用提要栏中的“模拟错误”选项。 “模拟错误”和“成功”选项的详细说明如下：

* **模拟成功**:允许您查看组件在指定成功状态的样式时的外观。 例如，在表单中，客户设置密码。 用户可以根据您提供的准则设置密码。 当用户根据您提供的所有准则键入密码时，文本框将变为绿色。 当文本框变为绿色时，它处于成功状态。 您可以为处于成功状态的组件指定样式，并使用“模拟成功”选项模拟其外观。

* **模拟错误**:允许您在为错误状态指定组件样式时查看组件的外观。 例如，在表单中，客户设置密码。 用户可以根据您提供的准则设置密码。 当用户键入的密码不符合您提供的所有准则时，文本框将变为红色。 当文本框变为红色时，它处于错误状态。 您可以为处于错误状态的组件指定样式，并使用“模拟错误”选项模拟其外观。

### 设置组件样式 {#styling-a-component}

例如，在表单中，您有两种类型的文本框：一个仅接受数字值，另一个只接受字母数字值。 您可以为仅接受数字值（数字框）的文本框自定义样式。

执行以下步骤以自定义特定组件（本例中的数字框）的样式：

1. 在主题编辑器中，选择画布中的数字框。
1. 选择数字框时，您会看到组件工具栏包含三个选项：

   * **数值框小组件**
   * **字段构件**![字段级别](assets/field-level.png)

1. 选择 **数字框构件**。
1. 提要栏标题将更改为数字框构件，并显示自定义其外观的选项。
使用 **提要栏中的“维度和位置** ”选项可自定义组件的大小。 确保状态为默 **认**。

选择组件工 **具栏中的字段构件**，而不是选择数 **** 字框构件，然后执行上述步骤。 当您为字段构件选 **项选择尺寸** ，除数字框外的所有文本框都具有相同的大小。

### 给定状态的样式字段 {#styling-fields-given-state}

使用组件工具栏，您还可以为组件的不同状态指定组件样式。 例如，如果某个组件被禁用，则它处于禁用状态。 可在主题编辑器中设置样式的组件的常用状态有：默认、焦点、禁用、错误、成功和悬停。 您可以在画布中选择组件，然后使用提要栏中的状态选项来自定义其外观。

执行以下步骤以自定义特定状态中的组件的样式：

1. 在画布中选择一个组件，然后从组件工具栏中选择相应的选项。
提要栏显示自定义组件样式的选项。
1. 在提要栏中选择一个状态。 例如，错误状态。
1. 使用提要栏中的 **边框、背景** 等选项自定义组件的外观。
1. 使用提 **要栏底部的** “模拟错误”选项查看样式在编辑中的外观。

在指定组件状态后自定义组件的样式时，仅针对指定状态显示组件的自定义。 例如，如果您在选择悬停状态时自定义组件的样式。 当您在已渲染的表单或应用主题的交互式通信中将指针移到组件上时，组件会显示自定义。

要模拟除错误和成功之外的状态行为，请使用预览模式。 要使用预览模式，请在页面 **工具栏** 中单击预览。

### 用于小型显示器的样式布局 {#styling-layouts-for-smaller-displays}

使用画布中的标尺为显示较小的设备选择断点。 在画布中单 ![击模拟器标尺](assets/ruler.png) ，以视图标尺和断点。 通过断点，您可以预览表单或交互式通信，以便显示与手机和平板电脑等不同设备相关的大小。 主题编辑器支持多种显示大小。

为不同断点设置组件样式：

1. 在画布中，选择标尺上方的断点。
断点表示移动设备及其显示大小。
1. 使用提要栏为所选显示大小自定义主题中表单或交互式通信组件的样式。
1. 确保保存自定义。

您可以为多个设备设计表单或交互式通信组件的样式。 适用于台式机和移动设备的表单和交互式通信组件可能具有不同的样式。

### 在主题中使用Web字体 {#using-web-fonts-in-a-theme}

您现在可以通过自适应表单或交互式通信使用Web服务中提供的字体。 现成的Typekit [（Adobe的Web字体服务）可](https://typekit.com/)用作配置。 要使用Typekit，请在其中创建工具包和字体，并从 [Typekit网站获取工具包ID](https://typekit.com/)。

执行以下步骤在AEM中配置Typekit:

1. 在创作实例中，单击 ![](assets/adobeexperiencemanager.png)adobeexperiencemanagerAdobe Experience Manager >工具锤 ![子](assets/hammer.png) >部署>云服务。
1. 在“云服 **务** ”页面上，导航至“第 **三方服务”** >“Typekit **”，然后单击“Typekit”****** 下的“立即配置”。 如果某个配置已可用，请单击 **+按钮** 以创建新实例。
1. 在“创 **建配置** ”对话框中，指定配置的标题，然后单击“创 **建”**。

   您将被重定向到配置页面。

1. 在出现的编辑组件对话框中，提供您的工具包ID，然后单击确 **定**。

请执行以下步骤配置主题以使用TypeKit配置：

1. 在创作实例中，在主题编辑器中打开一个主题。
1. 在主题编辑器中，导航到“主 **题选项** ” ![“主题选项](assets/theme-options.png) ” **>“配**&#x200B;置”。
1. 在Typekit **配置字段中** ，选择一个工具包，然后单击 **保存**。

   现在，您可以看到这些字体添加到主题的font-family属性中。

### 在主题编辑器中列出和选择字体 {#listing-and-selecting-fonts-in-theme-editor}

您可以使用主题配置服务向主题编辑器添加更多字体。 执行以下步骤以添加字体：

1. 使用管理权限登录到AEM Web Console。 AEM Web Console的URL为 `https://'[server]:[port]'/system/console/configMgr`。
1. 打开 **自适应表单主题配置服务**。

   ![theme-config](assets/theme-config.png)

1. 单击+，指定字体的名称，然后单击“保 **存”**。 该字体会添加并在主题编辑器中可用。

#### 在主题编辑器中选择字体 {#selecting-fonts-in-theme-editor}

您可以使用+按钮添加字体。 添加字体时，该字体会列在提要栏中。

![主题编辑器中列出的新字体](assets/theme-font.png)

除了主题配置选项之外，您还可以从主题编辑器本身添加字体。 在提要栏下方的字体系列字段中键入要使用的字体，然后按键盘上的返回键。

![在主题编辑器中键入和选择字体](assets/font-selection.png)

当您选择字体时，该字体会添加到字体系列列表下。 您可以使用主题编辑器中的“蒙版”选项来禁用或启用列出的字体。

![多字体](assets/multi-fonts.jpg)

您可以看到组件字体的更改。

“字体系列”字段支持多种字体。 键入字体时，浏览器会查找字体并将其应用到所选组件。 如果浏览器找不到字体，它会在系列中查找该字体旁边的字体。 您可以开始键入要查找的特定字体。 如果找不到要使用的字体，您可以在系列中键入通用字体并使用它。

#### 在主题编辑器中应用的蒙版样式 {#mask-styles-applied-in-theme-editor}

您可以遮住在主题中应用的样式。 在主题编辑器提要栏中，可以使用 ![toggle_](assets/toggle_eye.png)eyeicon禁用应用的样式。 例如，如果您以表单或交互式通信的形式更改维度组件，则可以使用属性左侧的遮罩按钮禁用它。 保存主题时，将保留选定的蒙版选项。

![主题编辑器提要栏中提供的遮罩选项](assets/mask-styles.png)

以下示例显示了主题中被遮罩和未被遮罩的样式。

![蒙版和未蒙版的样式](assets/mask2.png)

## 将主题应用于表单或交互式通信 {#applying-a-theme-to-a-form-or-interactive-communication-br}

要将主题应用于自适应表单，请执行以下操作：

1. 在编辑模式下打开表单。 要在编辑模式下打开表单，请选择一个表单，然后单击“打 **开”**。
1. 在编辑模式中，选择一个组件，单击 ![字段级别](assets/field-level.png) >自适 **应表单容器**，然后单 ![击cmppr](assets/cmppr.png)。

   您可以在提要栏中编辑表单的属性。

1. 在提要栏中，单击“样 **式”**。
1. 从“自适应表单主 **题”下拉菜单中选择您的主题** ，然后单击“完 **成**![”复选框](assets/check-button.png)。

要将主题应用于交互式通信，请执行以下操作：

1. 在编辑模式下打开您的交互式通信。 要在编辑模式下打开交互式通信，请选择一个表单，然后单击“打 **开”**。
1. 在编辑模式中，选择一个组件，单击 ![字段级别](assets/field-level.png) >**文档容器**，然后单 ![击cmppr](assets/cmppr.png)。

   您可以在提要栏中编辑表单的属性。

1. 在提要栏中，在**基本**下，从 **Theme** （主题）下拉菜单中选择您的主题，然后单击 **Done**![（完成）复选框](assets/check-button.png)

### 在运行时更改表单的主题 {#change-theme-of-a-form-at-runtime}

主题样式表单的不同组件。 您可以使用该 `themeOverride` 属性动态更改表单的主题。 表单的典型URL是：

`https://<server>:<port>/content/forms/af/test.html`

您可以使用themeOverride参数在运行时上应用一个主题。

`https://<server>:<port>/content/forms/af/test.html?themeOverride=/content/dam/formsanddocuments-themes/simpleEnrollmentTheme`

通过 `themeOverride` 此选项，您可以提供指向主题的路径。 它会更改表单的主题，并使用更新的样式刷新表单。

## 使用主题获取特定外观 {#specific-af-appearance}

借助AEM Forms以及默认的现成画布主题，还有许多其他主题。 如果要使用其他主题设计表单或交互式通信，并进行其他更改，请从“主题库”文件夹复制主题。 将复制的主题粘贴到“主题库”文件夹之外，然后根据所需的更改编辑复制的主题。

要复制主题，请执行以下步骤：

1. 在创作实例中，导航到 **Adobe Experience Manager > Forms >主题**。
1. 打开“主题库”文件夹。
1. 在“主题库”文件夹中，将指针悬停在相应的现成主题上，然后点按复 **制**。
1. 将复制的主题粘贴到“主题库”文件夹之外。
1. 自定义复制的主题。

自定义主题后，将其应用于表单或交互式通信。

>[!NOTE]
>
>请勿修改“主题库”文件夹中的可用主题。 此文件夹包含系统主题。 在安装AEM Forms的较新版本或热修复时，将覆盖您对这些主题所做的任何更改。

## 对其他自适应表单使用案例的影响 {#impact-on-other-adaptive-form-use-cases}

* **发布／取消发布表单：** 在发布表单时，应用到的主题也会发布（如果尚未发布）
* **导入／导出表单：** 导入或导出表单时，其关联的主题也会自动导入或导出。
* **表单的引用：** 表单引用中的“引用”部分包含一个额外的主题条目。
* **表单的上次修改时间：** 当关联的主题发生更改时更新。
* **A/B测试：** 在A/B测试中，您可以将不同的主题应用到表单的两个版本。 两个主题的信息分别存储在两个引导容器上。

## CSS生成序列 {#css-generation-sequence}

当您选择视图CSS时，主题编辑器会收集所有样式信息并构建CSS。 它按以下顺序收集信息：

1. 在主题的基本客户端库中定义的样式。
1. 用户定义的样式，使用提要栏中的属性指定。
1. 使用“CSS覆盖”选项提供的CSS样式。

例如，文本框在基本客户端库中的背景颜色为蓝色。 使用提要栏中的属性将其更改为粉红色。 生成CSS时，文本框的背景颜色显示为粉红色。 使用属性更改背景颜色后，另一位作者使用CSS覆盖选项将背景颜色文本框更改为白色。 生成CSS时，在生成的CSS中，背景颜色将显示为白色。

## 调试样式 {#debugging-styles}

在主题编辑器中指定组件样式时，将生成CSS。 设置通用组件的样式时，其中包含的多个组件也会设置样式。 例如，设置字段样式时，其中的文本框和标签也会设置样式。 设置字段中文本框的样式时，它会获得自己的CSS。 如果要调试为字段和组件生成的CSS，则主题编辑器提供允许您视图CSS的选项。

您可以使用以下选项查看生成的CSS:

* **视图提要栏中的CSS** 选项：在“主题”中选择组件时，可以在提要栏中看到“视图CSS”选项。 它显示生成的CSS，包括CSS的 `::before` 元素 `::after` 和伪元素。
* **视图画布工具栏中的“主题CSS** ”选项：在“画布”工具栏中，单 ![击“主题选项](assets/theme-options.png) ”>“ **视图主题CSS”**。 您可以查看在主题编辑器中定义的属性生成的整个主题CSS。

## 疑难解答、建议和最佳实践 {#troubleshooting-recommendations-and-best-practices}

* **避免使用其他主题的资源**

   编辑主题时，您可以浏览并添加来自其他主题的资产（如图像）。 例如，您正在编辑页面的背景。 例如，当您看到 **Page** ![edit-button](assets/edit-button.png)> Background **>** AddAddImage ********>浏览图像时，您会看到一个对话框，通过该对话框可以在其他主题中添加图像。

* 如果从其他主题中添加资产，并且移动或删除其他主题，您可能会遇到当前主题的问题。 建议您避免浏览和添加来自其他主题的资产。
* **使用基本clientlib、主题编辑器和内联样式**

   * **基本clientlib**:

      基本客户端库包含样式信息。 在主题的客户端库中使用样式信息。

      1. 导航到 **Experience Manager > Forms >主题**。
      1. 在主题页面中，选择一个主题，然后单击视图 **属性**。
      1. 在打开的“属性”页面中，单击“高 **级”**。
      1. 在“高级”选项卡的“Clientlib位置”字段中，浏览并选择要使用的客户端库。
      1. 单击&#x200B;**保存**。
      您在客户端库中指定的样式将导入使用该样式的主题中。 例如，指定文本框、数字框的样式，并在客户端库中切换。 在主题中导入客户端库时，将导入文本框、数字框和切换的样式。 然后，您可以使用主题编辑器设计其他组件的样式。
您还可以创建主题、创建主题的副本，然后修改复制的主题中为类似用例提供的样式。
请参阅 [使用主题获取特定外观](#specific-af-appearance)

   * **主题编辑器:**

      通过主题编辑器，您可以创建主题来设置表单或交互式通信的样式。 您可以在主题中指定组件的样式，从而在您开发的多个表单或交互式通信之间实现外观的一致性。 建议在主题中指定样式信息，然后将该主题应用于表单。

   * **内联样式：**

      处理表单时，您可以在表单或交互式通信多渠道编辑器中使用样式模式设置组件样式。 使用样式模式更改表单组件样式将覆盖在主题中指定的样式。 如果要更改特定表单的某些组件的样式，请参阅组件 [的内联样式](../../forms/using/inline-style-adaptive-forms.md)。


* **使用客户端库**

   如果要创建客户端库以导入样式信息，请参阅使 [用客户端库](/help/sites-developing/clientlibs.md)。 创建客户端库后，可以使用上述步骤将其导入主题中。

* **更改容器面板布局宽度**

   不建议更改容器面板布局宽度。 指定容器面板的宽度时，该面板会变为静态，并且不会适应不同的显示。

* **何时使用表单编辑器或主题编辑器处理页眉和页脚**

   如果要使用字体样式、背景和透明度等样式选项设置页眉和页脚的样式，请使用主题编辑器。
如果要提供徽标图像、页眉中的公司名称和页脚中的版权信息等信息，请使用表单编辑器选项。
