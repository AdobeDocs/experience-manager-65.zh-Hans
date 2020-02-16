---
title: 生成XDP表单的HTML5预览
seo-title: 生成XDP表单的HTML5预览
description: LiveCycle Designer中的“预览HTML”选项卡可用于预览表单在浏览器中显示时的效果。
seo-description: LiveCycle Designer中的“预览HTML”选项卡可用于预览表单在浏览器中显示时的效果。
uuid: cbee956f-bf2d-40c5-8e03-58fce0fa215b
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 34e6d1bc-4eca-42dc-9ae5-9a2107fbefce
docset: aem65
translation-type: tm+mt
source-git-commit: 19299fb5fc764d0e71c0ea3a5ec2286183dd6861

---


# 生成XDP表单的HTML5预览{#generate-html-preview-of-an-xdp-form}

在AEM Forms Designer中设计表单时，除了预览表单的PDF再现外，您还可以预览表单的HTML5再现。 可使用“预 **览HTML** ”选项卡预览表单在浏览器中的显示效果。

## 在设计器中为XDP表单启用HTML预览 {#html-preview-of-forms-in-forms-designer}

要使设计人员能够生成XDP表单的HTML预览，请执行以下配置：

* 配置Apache Sling Authentication Service
* 禁用保护模式
* 提供AEM Forms服务器的详细信息

### 配置Apache Sling Authentication Service {#configure-apache-sling-authentication-service}

1. 转到在 `https://[server]:[port]/system/console/configMgr` OSGi上运行的AEM Forms，或
   `https://[server]:[port]/lc/system/console/configMgr` 在JEE上运行的AEM Forms。
1. 找到并单击 **Apache Sling Authentication service配置** ，以在编辑模式下将其打开。

1. 根据您是在OSGi还是JEE上运行AEM Forms，在“身份验证要求”字段中添 **加以下内容** :

   * JEE上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs
   * OSGi上的AEM Forms

      * -/content/xfaforms
      * -/etc/clientlibs/fd/xfaforms
   >[!NOTE]
   >
   >请勿复制粘贴“身份验证要求”字段中的指定值，因为该值可能会损坏该值中的特殊字符。 而是在字段中键入指定的值。

1. 在“匿名用户名”和“匿名用 **[!UICONTROL 户密码”字段]****[!UICONTROL 中分别指定用户名和密码]** 。 指定的凭据用于处理匿名身份验证并允许匿名用户访问。
1. Click **Save** to save the configuration.

### 禁用保护模式 {#disable-protected-mode}

默认 [情况下](../../forms/using/get-xdp-pdf-documents-aem.md) ，保护模式处于打开状态。 使其在生产环境中保持启用状态。 您可以为开发环境禁用它，以在设计中预览HTML5表单。 执行以下步骤以禁用它：

1. 以管理员身份登录到AEM Web Console。

   * OSGi上的AEM Forms的URL `https://[server]:[port]/system/console/configMgr`
   * JEE上的AEM表单的URL是 `https://[server]:[port]/lc/system/console/configMgr`

1. 打开 **[!UICONTROL 移动表单配置]** ，进行编辑。
1. 取消选择“ **[!UICONTROL 保护模式]** ”选项，然后单 **[!UICONTROL 击“保存”]**。

### 提供AEM Forms服务器的详细信息 {#provide-details-of-aem-forms-server}

1. 在设计器中，转到“工 **具** ”>“ **选项**”。
1. 在“选项”窗口中，选择“服 **务器选项** ”页，提供以下详细信息，然后单击“ **确定”**。

   * **服务器URL**:AEM Forms服务器URL。

   * **HTTP端口号**:AEM服务器端口。 默认值为 4502。
   * **** HTML预览上下文：用于呈现XFA表单的配置文件的路径。 以下默认配置文件用于在Designer中预览表单。 但是，您也可以指定自定义配置文件的路径。

      * `/content/xfaforms/profiles/default.html` （OSGi上的AEM Forms）

      * `/lc/content/xfaforms/profiles/default.html` （JEE上的AEM Forms）
   * **** Forms manager上下文：部署Forms Manager UI的上下文路径。 默认值为：

      * `/aem/forms` （OSGi上的AEM Forms）
      * `/lc/forms` （JEE上的AEM Forms）
   **** 注意：确保AEM Forms服务器已启动并正在运行。 HTML预览连接到CRX服务器以 *生成* 预览。

   ![AEM Forms Designer选项 ](assets/server_options.png)

   AEM Forms Designer选项

1. 要预览HTML格式的表单，请单击“预 **览HTML** ”选项卡。

   >[!NOTE]
   >
   >
   >
   >
   >    * 如果“HTML预览”选项卡关闭，则按F4可打开“预览HTML”选项卡。 还可以从“视图”菜单中选择“预览HTML”以打开“预览HTML”选项卡。
   >    * HTML预览不支持PDF文档，HTML预览仅适用于XDP文档。


   >[!CAUTION]
   >
   >要测试真正的最终用户体验，请在外部浏览器（Google Chrome、Microsoft Edge、Mozilla Firefox等）中预览表单。 每个浏览器都使用单独的引擎来渲染HTML，因此在设计人员和外部浏览器中的表单预览方式可能存在一些差异。

## 使用范例数据预览表单 {#to-preview-a-form-using-sample-data}

Designer允许您使用范例XML数据预览和测试表单。 建议您经常使用示例数据测试表单，以确保表单正确呈现。

如果您没有示例数据，设计人员可以创建它，您也可以自己创建它。 (请参 [阅自动生成样本数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7efe.2) , [以及创建样本数据以预览表单](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c136ae6f212a1f379c94-8000.2.html#WS92d06802c76abadb-728f46ac129b395660c-7eff.2)。)

使用示例数据源测试表单可确保映射数据和字段，并确保重复的子表单会如您期望的那样重复。 您可以创建平衡的表单布局，为每个对象提供显示合并数据的适当空间。

1. 选择“ **文件”>“表单属性**”。

1. 单击“ **预览** ”选项卡，在“数据文件”框中，键入测试数据文件的完整路径。 您还可以使用“浏览”按钮导航到文件。

1. 单击&#x200B;**确定**。下次在“预览HTML **** ”选项卡中预览表单时，范例XML文件中的数据值将显示在各个对象中。

## 预览位于存储库中的表单 {#html-preview-of-forms-in-forms-manager}

在AEM Forms中，您可以预览存储库中的表单和文档。 预览有助于准确了解表单的外观和行为，就像最终用户使用表单一样。

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
