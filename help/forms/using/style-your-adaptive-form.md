---
title: 设置自适应表单的样式
description: 了解如何创建自定义主题、设置单个组件的样式以及在主题中使用Web Fonts。
topic-tags: introduction
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2038'
ht-degree: 8%

---

# 设置自适应表单的样式 {#do-not-publish-style-your-adaptive-form}

了解如何创建自定义主题、设置单个组件的样式以及在主题中使用Web Fonts。

![主页图像](do-not-localize/08-style_your_adaptiveformmain.png)

本教程是[创建您的第一个自适应表单](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html)系列中的步骤。 Adobe建议您按照时间顺序跟踪系列，以了解、执行和演示完整的教程用例。

## 关于教程  {#about-the-tutorial}

您可以使用主题为自适应表单提供独特的外观和样式。 您可以应用自适应表单编辑器提供的现成主题，或创建自己的自定义主题。 AEM [!DNL Forms]提供[主题编辑器](https://helpx.adobe.com/cn/experience-manager/6-3/forms/using/themes.html)以创建自定义主题。 单个主题可以为在移动设备、平板电脑或桌面上打开的相同自适应表单提供不同的外观。 使用主题编辑器不需要预先了解CSS或LESS，但需要使用。

在本教程结束时，您应该能够执行以下操作：

* 将现成的主题应用于自适应表单
* 使用主题编辑器为自适应表单创建主题
* 为单个组件设置样式
* 附加部分：在自定义主题中使用Web Fonts

完成本教程后，您的表单应类似于以下内容：

![带有自定义主题的表单](assets/styled-adaptive-form.png)

## 开始之前 {#before-you-start}

在本地计算机上下载下面给定的标题样式和徽标图像。 `shipping-address-add-update-form`自适应表单的页眉使用页眉样式和徽标图像。 标题样式图像显示在标题的右侧。

[获取文件](assets/header-style.png)

[获取文件](assets/logo-1.png)

## 步骤1：将主题应用于自适应表单 {#step-apply-a-theme-to-your-adaptive-form}

自适应表单编辑器提供了多个现成的主题。 如果您计划不使用自适应表单的自定义样式，则还可以使用现成的主题发布自适应表单。 主题与自适应表单无关。 您可以将同一主题应用于多个自适应表单。

**要将主题应用于自适应表单：**

1. 打开自适应表单进行编辑。

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 打开&#x200B;**[!UICONTROL 自适应表单容器]**&#x200B;的属性。 在属性浏览器中，导航到&#x200B;**[!UICONTROL 基本]** > **[!UICONTROL 自适应表单主题]**。 **[!UICONTROL 自适应表单主题]**&#x200B;字段列出了所有现成的主题和自定义主题。 默认情况下，将应用画布主题。
1. 从&#x200B;**[!UICONTROL 自适应表单主题]**&#x200B;字段中选择主题。 例如，**调查主题**。 选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，以便应用所选主题。

   ![带有默认主题的自适应表单](assets/default-adaptive-form.png)

   **图：** *带有默认主题的自适应表单*

   带有调查主题的![自适应表单](assets/adaptive-form-with-survey-theme.png)

   **图：** *带有调查主题的自适应表单*

## 第2步：更新您的自适应表单 {#step-update-your-adaptive-form}

以上显示的设计要求更改现有自适应表单的占位符文本和徽标。

**要更新您的自适应表单：**

1. 更改标题的现有徽标和文本。 要删除徽标，请执行以下操作：

   1. 在表单编辑器中打开表单。

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 选择[!UICONTROL 标头]组件中的徽标图像，然后选择![cmppr](assets/cmppr.png) **[!UICONTROL 属性]**。 在[!UICONTROL image]属性中，选择X以删除现有的徽标图像。
   1. 选择&#x200B;**[!UICONTROL 上传]**，选择logo.png，然后选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)以保存更改。 图像下载到[开始](/help/forms/using/style-your-adaptive-form.md#before-you-start)之前。
   1. 选择标题文本`We.Retail`，然后选择![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**。 将标题文本更改为`we retail`。 仅对`we retail`中的`we`应用粗体格式。

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 移除标题并添加占位符文本：

   1. 选择“客户ID”字段，然后选择![cmppr](assets/cmppr.png)属性。
   1. 将&#x200B;**[!UICONTROL 标题]**&#x200B;字段的内容复制到&#x200B;**[!UICONTROL 占位符文本]**&#x200B;字段。
   1. 删除&#x200B;**[!UICONTROL Title]**&#x200B;字段的内容，然后选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
   1. 对表单中的所有文本框、数字框和电子邮件字段重复前三个步骤。

      ![已更新自适应表单](assets/updated-adaptive-form.png)

## 步骤3：为自适应表单创建自定义主题 {#step-create-a-custom-theme-for-your-adaptive-form}

您可以使用[主题编辑器](/help/forms/using/themes.md)创建自定义主题。 主题编辑器是一个功能强大的WYSIWYG编辑器。 它是一种将CSS应用于自适应表单的各种组件的可视化方法。 它提供更细化的控件，用于设置自适应表单的组件和面板的样式。

主题是一个单独的实体，如自适应表单。 它包含自适应表单的组件和面板的样式(CSS)。 样式包括CSS属性，例如背景颜色、状态颜色、透明度、对齐方式和大小。 应用主题时，指定的样式将应用于自适应表单的相应组件。

在本教程中，您将设置页眉和页脚、文本和数字组件、附件组件和按钮的样式。 让我们从创建主题开始：

### 创建主题 {#create-a-theme}

1. 登录到AEM创作实例并导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 主题]**。 默认URL为[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes)。
1. 选择&#x200B;**[!UICONTROL 创建]**&#x200B;并选择&#x200B;**[!UICONTROL 主题]**。 此时将显示[!UICONTROL 创建主题]页面，其中包含创建主题所需的字段。 **[!UICONTROL Title]**&#x200B;和&#x200B;**[!UICONTROL Name]**&#x200B;字段是必填字段：

   * **标题：**&#x200B;指定主题的标题。 例如，**全局主题。**&#x200B;标题可帮助您从主题列表中识别主题。
   * **名称：**&#x200B;指定主题的名称。 例如，**Global-Theme。**&#x200B;在存储库中创建具有指定名称的节点。 当您开始键入标题时，将自动生成“名称”字段的值。 您可以更改建议的值。名称字段只能包含字母数字字符、连字符和下划线。所有无效的输入都将替换为连字符。

1. 选择&#x200B;**[!UICONTROL 创建]**。将创建一个主题，并出现一个对话框以打开表单进行编辑。 选择&#x200B;**[!UICONTROL 打开]**&#x200B;以在新选项卡中打开新创建的主题。 主题将在主题编辑器中打开。 对于样式，主题编辑器使用AEM [!DNL Forms]随附的现成自适应表单。

   有关使用主题编辑器UI的信息，请参阅[关于主题编辑器](/help/forms/using/themes.md#aboutthethemeeditor)。

1. 选择&#x200B;**[!UICONTROL 主题选项]** ![主题选项](assets/theme-options.png) > **[!UICONTROL 配置]**。 在&#x200B;**[!UICONTROL 预览表单]**&#x200B;字段中，选择&#x200B;**shipping-address-add-update-form**&#x200B;自适应表单，选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)，然后选择&#x200B;**[!UICONTROL 保存]**。 现在，主题编辑器配置为使用您自己的自适应表单，而不是默认的自适应表单。 选择&#x200B;**[!UICONTROL 取消]**&#x200B;以返回主题编辑器。

   ![自定义主题](assets/custom-theme.png)

   **图：** *具有shipping-address-add-update-form自适应表单的主题编辑器*

   ![create-a-theme](assets/create-a-theme.png)

   **图：** *带有默认表单的自适应表单*

### 样式页眉和页脚 {#style-header-and-footer}

页眉和页脚为自适应表单提供一致且独特的外观。 通常，页眉包含组织的徽标和名称，页脚包含版权信息，并且这些信息和信息在组织的多个表单中保持相同。 要设置shipping-address-add-update-form自适应表单的页眉和页脚的样式，请执行以下操作：

1. 在“选择器”面板中导航&#x200B;**[!UICONTROL Header]** > **[!UICONTROL Text]**&#x200B;选项。 “选择器”面板位于主题编辑器的左侧。 如果该面板不可见，请选择![切换侧面板](assets/toggle-side-panel.png)切换侧面板。

1. 在&#x200B;**[!UICONTROL 文本]**&#x200B;折叠面板中设置以下属性，然后选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 价值 |
   |---|---|
   | 字体系列 | Arial® |
   | 字体颜色 | FFFFFF |
   | 字体大小 | 54像素 |

1. 选择[!UICONTROL 标头]构件并选择&#x200B;**[!UICONTROL 标头]**。 用于设置标题小组件样式的选项显示在左侧。 展开&#x200B;**[!UICONTROL Dimension和位置]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL 高度]**&#x200B;设置为`120px`，然后选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 展开标题小组件的&#x200B;**[!UICONTROL 背景]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL 背景颜色]**&#x200B;设置为`F6921E.`

   将鼠标悬停在&#x200B;**[!UICONTROL 图像和渐变]** > **[!UICONTROL +添加]**&#x200B;上，选择&#x200B;**[!UICONTROL 图像]**。 设置以下属性并选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 价值 |
   |---|---|
   | 图像 | 上传header-style.png。 图像下载到[开始](/help/forms/using/style-your-adaptive-form.md#before-you-start)之前。 |
   | 位置 | 右下 |
   | 并排显示 | 不重复 |

1. 在主题编辑器中，选择标题中的徽标，然后选择&#x200B;**[!UICONTROL 标题徽标]**。 展开“Dimension和位置”折叠面板，设置以下属性并选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>边距</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>上：1.5雷姆</li> 
        <li>底部：-35像素</li> 
        <li>左： 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>提示：</strong>选择<img src="assets/link.png">链接图标为每个字段提供不同的值。<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>高度</td> 
      <td>4.75雷姆</td> 
     </tr> 
    </tbody> 
   </table>

1. 选择页脚小组件并选择&#x200B;**[!UICONTROL 页脚]**。 展开&#x200B;**[!UICONTROL 背景]**&#x200B;折叠面板，将&#x200B;**[!UICONTROL 背景颜色]**&#x200B;设置为`F6921E`，然后选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

### 设置数据捕获组件的样式，并将背景应用于自适应表单 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

您可以在自适应表单中使用多个组件来捕获数据。 例如，文本框和数字框。 您可以为所有数据捕获组件提供相同的样式，或者为每个组件提供单独的样式。 在本教程中，相同的样式将应用于数字框（客户ID、邮政编码）和文本框（客户ID、姓名、送货地址、州、电子邮件）。 设置数据捕获组件的样式：

1. 选择&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段并选择&#x200B;**[!UICONTROL 字段小组件]**&#x200B;选项。 设置以下属性并选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>可折叠项</b></td> 
      <td><b>属性</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径 </td> 
      <td> 
       <ul> 
        <li>顶部： 7像素<br /> </li> 
        <li>右： 7像素<br /> </li> 
        <li>底部： 7像素<br /> </li> 
        <li>左： 7像素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18像素</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>宽度</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>左：10雷姆</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 选择&#x200B;**[!UICONTROL 客户ID]**&#x200B;字段上方的空白区域，然后选择&#x200B;**[!UICONTROL 响应面板容器]**。 将&#x200B;**[!UICONTROL Background]** > **[!UICONTROL Background Color]**&#x200B;设置为F1F2F2。 选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   ![响应面板容器](do-not-localize/responsive-panel-container.png)

### 设置按钮的样式 {#style-the-buttons}

您可以使用自定义主题将相同的样式应用于自适应表单的所有按钮，并使用[内联样式](/help/forms/using/inline-style-adaptive-forms.md)将样式应用于特定按钮。 设置按钮样式：

1. 选择&#x200B;**[!UICONTROL 提交]**&#x200B;按钮并选择&#x200B;**[!UICONTROL 按钮]**&#x200B;选项。 设置以下属性并选择![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>可折叠项</b></td> 
      <td><b>属性</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框<br /> </td> 
      <td>边框颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径 </td> 
      <td> 
       <ul> 
        <li>顶部： 7像素<br /> </li> 
        <li>右： 7像素<br /> </li> 
        <li>底部： 7像素<br /> </li> 
        <li>左：7像素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>文本<br /> </td> 
      <td>字体系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18像素</td> 
     </tr> 
    </tbody> 
   </table>

1. [将自定义主题](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)全局主题应用于您的自适应表单。 如果样式未反映在自适应表单上，请清理浏览器缓存并重试。

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 步骤4：设置单个组件的样式 {#step-style-individual-components}

某些样式仅适用于特定组件。 此类组件在自适应表单编辑器中设置样式。

1. 打开自适应表单进行编辑。 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 在顶部栏上，选择&#x200B;**[!UICONTROL 样式]**&#x200B;选项。

   ![style-option](assets/style-option.png)

1. 选择&#x200B;**[!UICONTROL 附加]**&#x200B;按钮并选择![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 在&#x200B;**[!UICONTROL Dimension和位置]**&#x200B;折叠面板中设置以下属性：

   | 属性 | 价值 |
   |---|---|
   | 浮点数 | 左 |
   | 宽度 | 10% |

1. 选择&#x200B;**[!UICONTROL 政府批准的地址验证]**&#x200B;选项，然后选择![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 设置以下属性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>可折叠项</b></td> 
      <td><b>属性</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>浮点数</td> 
      <td>左</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>宽度</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>左：10像素</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>尺寸及位置</td> 
      <td>高度</td> 
      <td>40像素</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置<br /> </td> 
      <td>边距</td> 
      <td><br /> 
       <ul> 
        <li>右：2分米</li> 
        <li>左：10雷姆 </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框宽度</td> 
      <td>1像素</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框样式</td> 
      <td>实线</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框半径</td> 
      <td>7像素</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体系列</td> 
      <td>Arial®</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体颜色</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>字体大小</td> 
      <td>18像素</td> 
     </tr> 
     <tr> 
      <td>文本</td> 
      <td>行高</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 选择&#x200B;**[!UICONTROL 提交]**&#x200B;按钮并选择![aem_6_3_edit](assets/aem_6_3_edit.png)图标。 设置以下属性：

   <table> 
    <tbody> 
     <tr> 
      <td><b>可折叠项</b></td> 
      <td><b>属性</b></td> 
      <td><b>价值</b></td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>浮点数</td> 
      <td>右</td> 
     </tr> 
     <tr> 
      <td>Dimension和位置</td> 
      <td>边距</td> 
      <td> 
       <ul> 
        <li>上：5分</li> 
        <li>右：14雷姆</li> 
        <li>底部：20像素</li> 
        <li>左： 20像素<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>背景</td> 
      <td>背景颜色</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>边框</td> 
      <td>边框颜色</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 步骤5：附加部分：在自定义主题中使用Web Fonts {#step-bonus-section-using-web-fonts-in-a-custom-theme}

您可以使用各种字体设计自适应表单。 在查看自适应表单的所有设备上可能没有用于设计自适应表单的字体。 您可以使用Web字体服务将所需的字体交付给目标设备。

[!DNL Adobe Fonts]是Web Fonts服务。 您可以在自适应表单中配置并使用服务。 要在自适应表单中使用[!DNL Adobe Fonts]，请执行以下操作：
1. 浏览[Adobe库](https://fonts.adobe.com/)并选择字体以设置表单的样式。
<!--
>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] is now called Adobe Fonts and is included with Creative Cloud and other subscriptions. [Learn more](https://fonts.adobe.com/).-->

>[!NOTE]
>
> 可添加标记或筛选器以优化字体列表。

1. 单击&lt;/>按钮将系列添加到Web项目中，以防您找到所需的字体。

   ![select-font-from-font-library](assets/select-font-from-font-library.png)

   出现“Add fonts to a web project（将字体添加到Web项目）”对话框。

   >[!NOTE]
   >
   > 只有在Web项目中具有&lt;/>按钮时，才能添加字体。

2. 命名您的Web项目。
3. 选中复选框以选择要包括的字体粗细和样式。

   ![添加字体库](assets/add-a-font-window.png)

4. 选择&#x200B;**单击**&#x200B;以创建项目。
5. 从屏幕复制嵌入代码和URL。
   ![嵌入代码和URL](assets/font-add-url.png)

6. 单击&#x200B;**完成**&#x200B;以关闭Web项目窗口。
7. 登录AEM实例并转到URL `http://server:port/crx/de/index.jsp#`
8. 在CRXDE中创建文件夹结构，例如`/apps/[fontslibrary]/[customlibrary(clientlibrary)]`。
9. 转到新创建的`clientlibs`文件夹并添加`allowProxy`和`categories`属性。
10. 导航到`/apps/[fontslibrary]/[customlibrary(clientlibrary)]`并创建css文件夹。
11. 转到创建的CSS文件夹并创建一个文件。 例如，创建一个文件作为`fonts.css`，并粘贴嵌入代码以及URL。
    ![文件夹结构](/help/forms/using/assets/fonts-add-in-crxde.png)
12. 保存更改。

>[!NOTE]
>
> 要在自适应表单中使用添加的自定义字体，请确保&#x200B;**[!UICONTROL 客户端库类别]**&#x200B;中的客户端库名称与clientlib文件夹的“类别”选项中指定的名称一致。

自适应表单现在可通过以下自定义字体客户端库访问包含的字体。


<!--
Create Adobe Fonts Configuration

1. To create a API Token, go to **login** > **API Token** > **Make me a new API token**.

   ![API token](/help/forms/using/assets/fonts-api-token.png)

2. Once, you click **Make me a new API token**, a new token is generated. 
3. Copy the generated token for future use.
4. Now login to your AEM  author instance. On the author instance, go to **[!UICONTROL Tools]**>**[!UICONTROL Cloud Services]**> **[!UICONTROL Adobe Fonts]**.
5. Select the configuration container and click **Create**. **[UICONTROL Create Adobe Fonts Configuration]** screen appears.
    ![API token](/help/forms/using/adobe-font-configuration-screen.png)

6. Spceify the name and paste the API token in the **[!UICONTROL Kit ID]** textbox.
7. Click **Create**.



The fonts added to the **[!UICONTROL Adobe Fonts]** are available for selection in the **[!UICONTROL Text]** accordion of all the components.
1. In the theme editor, navigate to **[!UICONTROL Theme Options]** ![theme-options](assets/theme-options.png) > **[!UICONTROL Configure]**. 
2. In the **[!UICONTROL Adobe Fonts Configuration]** field, select the kit, and click **[!UICONTROL Save]**.


1. Create an [Adobe Fonts](https://fonts.adobe.com/?ref=tk.com) account, create a kit, add font Myriad Pro to the kit, publish the kit, and obtain the Kit ID. It is required to use [!DNL Adobe Fonts] (Web Fonts) in an adaptive form. 
1. In the AEM [!DNL Forms] Server, navigate to ![adobeexperiencemanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. Now, open a configuration folder. If a configuration is already available, click the **[!UICONTROL Create]** button to create an instance.

   On the Create Configuration dialog, specify a **Title** for the configuration, and click **[!UICONTROL Create]**. You are redirected to the configuration page. In the [!UICONTROL Edit Component] dialog that appears, provide your **Kit ID** and click **[!UICONTROL OK]**. -->


