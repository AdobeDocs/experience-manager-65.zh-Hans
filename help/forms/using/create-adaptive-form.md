---
title: “教程：创建自适应表单”
seo-title: '"创建自适应表单"'
description: 了解如何创建、布局和预览自适应表单。 此外，了解如何配置提交操作。
seo-description: 了解如何创建、布局和预览自适应表单。 此外，了解如何配置提交操作。
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: 自适应表单
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 3%

---


# 教程：创建自适应表单{#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

本教程是[创建您的第一个自适应表单](/help/forms/using/create-your-first-adaptive-form.md)系列中的一个步骤。 建议按照时间顺序排列系列，以了解、执行和演示完整的教程用例。

## 关于教程{#about-the-tutorial}

自适应表单是新一代动态响应式表单。 您可以使用自适应表单来提供个性化体验。 您还可以将自适应表单与[!DNL Adobe Analytics]集成，以获取使用情况统计信息，与[!DNL Adobe Campaign]集成，以管理促销活动。 有关自适应表单功能的更多信息，请参阅[创作自适应表单简介](/help/forms/using/introduction-forms-authoring.md)。

在遵循正确的流程后，创建和管理表单会更加容易。 在本文中，您将学习如何：

* [创建允许客户添加送货地址的自适应表单](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [用于显示和接受客户信息的自适应表单的布局字段](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [创建提交操作以发送包含表单内容的电子邮件](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [预览和提交自适应表单](/help/forms/using/create-adaptive-form.md)

在文章末尾，您将拥有一个类似于以下内容的表单：\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 步骤1:创建自适应表单{#step-create-the-adaptive-form}

1. 登录到AEM创作实例，然后导航到&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。 默认URL为[http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)。
1. 点按&#x200B;**[!UICONTROL 创建]**，然后选择&#x200B;**[!UICONTROL 自适应表单]**。 此时会显示用于选择模板的选项。 点按&#x200B;**[!UICONTROL 空白]**&#x200B;模板以将其选中，然后点按&#x200B;**[!UICONTROL 下一个]**。

1. 出现&#x200B;**[!UICONTROL Add Properties]**&#x200B;选项。 **[!UICONTROL 标题]**&#x200B;和&#x200B;**[!UICONTROL 名称]**&#x200B;字段是必填字段：

   * **标题：** 在 `Add new or update shipping address` 标题字 **** 段中指定。标题字段指定表单的显示名称。 标题可帮助您识别AEM [!DNL Forms]用户界面中的表单。
   * **名称：** 在“ `shipping-address-add-update-form` 名称”字 **** 段中指定。“名称”字段指定表单的名称。 在存储库中创建具有指定名称的节点。 开始键入标题时，将自动生成名称字段的值。 您可以更改建议的值。 名称字段只能包含字母数字字符、连字符和下划线。 所有无效输入都将替换为连字符。

1. 点按&#x200B;**[!UICONTROL 创建]**。随即会创建一个自适应表单，并出现一个用于打开表单以进行编辑的对话框。 点按&#x200B;**[!UICONTROL 打开]** ，以在新选项卡中打开新创建的表单。 随即会打开表单进行编辑。 它还会显示侧栏，以根据需要自定义新创建的表单。

   有关自适应表单创作界面和可用组件的信息，请参阅[自适应表单创作简介](/help/forms/using/creating-adaptive-form.md)。

   ![新创建的自适应表单](assets/newly-created-adaptive-form.png)

## 步骤2:添加页眉和页脚{#step-add-header-and-footer}

AEM [!DNL Forms]提供了许多组件，用于显示自适应表单的信息。 页眉和页脚组件有助于为表单提供一致的外观。 标题通常包括公司徽标、表单标题和摘要。 页脚通常包括版权信息和指向其他页面的链接。

1. 点按![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png)。 此时会打开组件浏览器。 将&#x200B;**[!UICONTROL 标题]**&#x200B;组件从组件浏览器拖到自适应表单。
1. 点按&#x200B;**[!UICONTROL Logo]**。 此时会出现工具栏。 点按工具栏上的![aem_6_3_edit](assets/aem_6_3_edit.png)，键入&#x200B;**We.Retail**，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

1. 点按图像。 此时会出现工具栏。 点按![cmppr](assets/cmppr.png)。 将在屏幕左侧打开属性浏览器。 **** 浏览并上传徽标图像。点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 图像显示在标题上。

   如果您没有徽标，则可以点按获取文件以下载本文中使用的徽标。

[获取文件](assets/logo.png)

1. 将&#x200B;**[!UICONTROL 页脚]**&#x200B;组件从![treeexpandall](assets/treeexpandall.png)拖到自适应表单中。 此时，表单如下所示：

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 步骤3:添加组件以捕获和显示信息{#step-add-components-to-capture-and-display-information}

组件是自适应表单的构建基块。 AEM [!DNL Forms]提供了许多组件，用于在自适应表单中捕获和显示信息。 可以将组件从![treeexpandall](assets/treeexpandall.png)拖动到窗体中。 要了解可用组件和相应的功能，请参阅[创作自适应表单简介](/help/forms/using/introduction-forms-authoring.md)。

1. 将&#x200B;**[!UICONTROL 数字框组件]**&#x200B;拖动到自适应表单。 将其放在页脚组件之前。 打开组件的属性，将组件的&#x200B;**[!UICONTROL 标题]**&#x200B;更改为&#x200B;**`Customer ID`**，将&#x200B;**[!UICONTROL 元素名称]**&#x200B;更改为&#x200B;**`customer_ID`**，启用&#x200B;**[!UICONTROL 必填字段]**&#x200B;选项，启用&#x200B;**[!UICONTROL 使用HTML5数字输入类型]**&#x200B;选项，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。
1. 将三个文本框组件拖到自适应表单中。 将它们放在页脚组件之前。 为这些文本框设置以下属性。: 

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>文本框1<br/></b></td> 
      <td><b>文本框2<br/></b></td> 
      <td><b>文本框3</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>名称<br /> </td> 
      <td>配送地址</td> 
      <td>状态</td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_state</td> 
     </tr> 
     <tr> 
      <td>必填字段</td> 
      <td>启用</td> 
      <td>启用</td> 
      <td>启用</td> 
     </tr> 
     <tr> 
      <td>允许多行<br /> </td> 
      <td>已禁用</td> 
      <td>启用</td> 
      <td>已禁用</td> 
     </tr> 
    </tbody> 
   </table>

1. 将&#x200B;**[!UICONTROL 数字框]**&#x200B;组件拖动到页脚组件之前。 打开组件的属性，设置下表中列出的值，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 值 |
   |---|---|
   | 标题 | 邮政编码 |
   | 元素名称 | customer_ZIPCode |
   | 最大数字数量 | 6 |
   | 必填字段 | 启用 |
   | 显示图案类型 | 无模式 |

1. 将&#x200B;**[!UICONTROL Email]**&#x200B;组件拖动到页脚组件之前。 打开组件的属性，设置下表中列出的值，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 值 |
   |---|---|
   | 标题 | 电子邮件 |
   | 元素名称 | customer_Email |
   | 必填字段 | 启用 |

1. 将&#x200B;**[!UICONTROL 文件附件]**&#x200B;组件拖动到页脚组件之前。 打开组件的属性，设置下表中列出的值，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   <table> 
    <tbody> 
     <tr> 
      <td><b>属性</b></td> 
      <td><b>值</b></td> 
     </tr> 
     <tr> 
      <td>标题</td> 
      <td>政府批准的地址证明<br /> </td> 
     </tr> 
     <tr> 
      <td>元素名称</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>必填字段</td> 
      <td>启用</td> 
     </tr> 
    </tbody> 
   </table>

1. 将&#x200B;**[!UICONTROL 提交按钮]**&#x200B;组件拖到自适应表单中。 将其放在页脚组件之前。 打开组件的属性，将元素名称更改为`address_addition_update_submit`，点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。 表单的布局已完成，表单如下所示：

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 步骤4:为自适应表单{#step-configure-submit-action-for-the-adaptive-form}配置提交操作

当用户点按自适应表单上的“提交”按钮时，会触发提交操作。 您可以使用提交操作将表单数据保存到本地存储库、将表单数据发送到REST端点、将表单数据作为电子邮件发送，等等。 自适应表单提供了一些现成的提交操作。 有关详细信息，请参阅[配置Submit操作](/help/forms/using/configuring-submit-actions.md)。

使用以下步骤，您可以配置表单的电子邮件提交操作和演示提交操作：

1. 配置电子邮件服务器。 有关详细信息，请参阅[配置电子邮件通知](/help/sites-administering/notification.md)。


1. 点按内容浏览器中的&#x200B;**[!UICONTROL 表单容器]**，然后点按![cmpr](assets/cmppr.png)。 将在左侧打开属性浏览器。
1. 转到&#x200B;**[!UICONTROL Submission]** > **[!UICONTROL Submit Action]**。 选择&#x200B;**[!UICONTROL 发送电子邮件]**。 指定以下值，然后点按![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)。

   | 属性 | 值 |
   |--- |--- |
   | 发件人 | `donotreply@weretail.com` |
   | 收件人 | `${customer_Email}` |
   | 主题 | 确认：您已在We.Retail网站上添加送货地址。 |
   | 电子邮件模板 | `${customer_Name}`，添加以下地址作为您帐户的送货地址：<br>`${customer_Name}`、`${customer_Shipping_Address}`、`${customer_State}`、`${customer_ZIPCode}`<br>致敬，We.Retail |
   | 包含附件 | 启用 |

   您的表单已准备就绪。 现在，您可以预览表单并测试功能。 如果您使用了本教程中提到的名称，并在运行AEM [!DNL Forms]服务器的计算机上访问表单，则该表单位于[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。

## 步骤5:预览并提交自适应表单{#step-preview-and-submit-the-adaptive-form}

您可以使用&#x200B;**[!UICONTROL 预览选项]**&#x200B;来评估表单的外观和行为。 您可以在预览模式下提交表单，还可以检查对表单应用的验证。 例如，如果必填字段留空时显示错误。

自适应表单还提供了一个选项，用于模拟各种设备的表单体验。 例如，iPhone、iPad和Desktop。 您可以将&#x200B;**[!UICONTROL 预览]**&#x200B;和&#x200B;**[!UICONTROL 模拟器]** ![标尺](assets/ruler.png)选项结合使用，以预览不同屏幕大小的设备的表单。

1. 点按表单编辑器右侧的&#x200B;**[!UICONTROL 预览]**&#x200B;选项。 在预览模式下将打开表单。 如果您使用了本教程中提到的名称，则表单的预览URL为[http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 使用![标尺](assets/ruler.png)查看表单在各种设备上的显示方式。
1. 填写表单的字段，然后点按&#x200B;**[!UICONTROL Submit]**。 表单已提交，您将被重定向到默认的&#x200B;**感谢**&#x200B;页面。 您还可以指定自定义的感谢页面。 有关详细信息，请参阅[配置重定向页面](/help/forms/using/configuring-redirect-page.md)。

添加地址的自适应表单已准备就绪。 如果您使用了教程中提到的名称并在运行AEM Forms服务器的计算机上访问表单，则表单位于[http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)。
