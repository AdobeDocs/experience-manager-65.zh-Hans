---
title: 使用（已弃用）涂写签名将电子签名应用于表单
seo-title: 使用（已弃用）涂写签名将电子签名应用于表单
description: 使用涂写对表单进行签名
seo-description: 使用涂写对表单进行签名
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
translation-type: tm+mt
source-git-commit: 92a64c8a1ba38f592d18355b8233cb79a2575301

---


# 使用（已弃用）涂写签名将电子签名应用于表单{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

您可以使用（已弃用） **Scribble Signature** （涂写签名）组件和 **** Signature Step（签名步骤）组件在自适应表单上绘制（涂写）签名。 签名步骤组件显示自适应表单的PDF版本。 您需要启用记录文档选项或基于表单模板的自适应表单才能使用签名步骤组件。

这两个组件都提供一个窗口，用于对表单进行签名，如下所示。 您还可以单击地理位 ![置图标aem_6_3_geolocation](assets/aem_6_3_geolocation.png) ，以向签名添加地理位置。

![“涂写签名”对话框](assets/scribble-signature.png)

## 配置自适应表单以使用涂写签名 {#configure-an-adaptive-form-to-use-scribble-signature}

1. 创建启用记录文档选项或基于表单模板的自适应表单。 有关分步信息，请参阅创 [建自适应表单](../../forms/using/creating-adaptive-form.md)。
1. 将“涂写签名”组件从组 **件浏览器拖放到自适应表单** 。
1. 点按配 **置**![配置](assets/configure.png) 图标。 它打开属性浏览器并显示“涂写签名”组件的属性。 配置“涂写签名”组件的属性。
1. 将签名步骤组件从组件浏览器拖放到自适应表单。

   >[!NOTE]
   >
   >签名步骤组件占用表单的全宽。 建议在包含签名步骤组件的部分上不要包含任何其他组件。

1. 在内容浏览器中，点按表 **单容器**，然后点按配 **置**![](/help/forms/using/assets/configure.png) 图标。 它打开属性浏览器并显示自适应表单容器属性。 导航到“自 **适应表单容器** ”>“ **电子签名** ”，然后取消选择“ **启用Adobe Sign** ”选项。 点按完 ![成aem_6_3_forms_save图标](assets/aem_6_3_forms_save.png) ，以保存更改。

   >[!NOTE]
   >
   >当您将签名步骤组件添加到自适应表单时，将自动选择“启用Adobe签名”选项。

1. 点按配 **置**![配置](assets/configure.png) 图标。 它打开属性浏览器并显示签名步骤属性。 配置以下属性：

   * **元素名称**:指定组件的名称。

   * **** 标题：指定组件的唯一标题。
   * **** 模板消息：指定加载签名PDF时要显示的消息。 Adobe sign服务需要一些时间来准备和加载签名PDF。
   * **** 签名服务：选择“涂 **写签名** ”选项。

   * **CSS类**:指定客户端库的CSS类（如果有）。 建议使用主 [题](../../forms/using/themes.md)[和内联样](../../forms/using/inline-style-adaptive-forms.md) 式，而不是CSS类。
   点按完 ![成aem_6_3_forms_save图标](assets/aem_6_3_forms_save.png) ，以保存更改。 签名配置成功。

   现在，当您填写表单时，将显示PDF版本的自适应表单，并提供对PDF文档进行签名的选项。 有关详细信息，请参 [阅使用涂写签名对自适应表单进行签名](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)。

## 使用涂写签名对自适应表单进行签名 {#sign-an-adaptive-form-using-scribble-signature}

1. 在您填写自适应表单并到达签名步骤页面后，将显示签名屏幕。

   ![EchoSign页面的签名屏幕](assets/esignscribblesign.jpg)

1. 单击“ **[!UICONTROL 签名]**”。 出现“涂写符号”对话框。 对表单进行签名，然后单 ![击“完成aem_6_3_forms_save](assets/aem_6_3_forms_save.png) ”图标以保存签名。

   ![“涂写签名”对话框](assets/scribblewidget.jpg)

1. 单击“完成”以完成签名过程。

   ![完成签名过程](assets/scribblecomplete.jpg)

签名将添加到表单，表单控件将移到下一个面板。

