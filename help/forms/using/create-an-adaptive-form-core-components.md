---
title: 如何创建自适应表单？
description: 了解如何使用 [!DNL Experience Manager Forms]创建自适应表单。 自适应Forms是响应式HTML5表单，可简化信息收集和处理。 深入了解如何基于表单数据模型和XML或JSON架构创建自适应表单。
Keywords: create adaptive form core component, create core component based adaptive form, creare adaptive form
products: SG_EXPERIENCEMANAGER/6.5/FORMS
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: ee596672-b0b5-42e9-a139-72f90287bf3b
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1794'
ht-degree: 33%

---

# 创建基于核心组件的自适应Forms {#creating-an-adaptive-form-core-components}


<span class="preview"> Adobe 建议使用核心组件[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)或[创建独立的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html?lang=zh-Hans) |
| AEM 6.5 | 本文 |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

自适应表单使您能够创建引人入胜、响应式、动态和自适应的表单。AEM Forms为商业用户提供了友好的UI，以便快速创建自适应Forms。 用户界面提供快速的选项卡导航，以轻松选择预配置的模板、样式、字段和提交选项以创建自适应表单。

在开始之前，了解可使用的表单组件类型：

* [自适应表单核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)：这些是标准化的数据捕获组件。对于您的数字注册体验，这些组件可以提供定制功能，缩短开发时间和降低维护成本。开发人员可以轻松地自定义这些组件并设置其样式。Adobe建议使用这些现代化的、可扩展的组件来开发自适应Forms。

* [自适应表单基础组件](creating-adaptive-form.md)：这些是经典（旧版）数据捕获组件。您可以继续使用这些组件来编辑您现有的基于基础组件的自适应表单。如果您正在创建表单，Adobe建议使用[自适应Forms核心组件](/help/forms/using/create-adaptive-form.md)创建自适应Forms。

## 先决条件

您需要以下项来创建自适应表单：

* **为您的环境启用自适应Forms核心组件**：需要AEM Archetype项目版本41或更高版本，才能[为您的环境启用核心组件](/help/forms/using/enable-adaptive-forms-core-components.md)。 在为您的环境启用核心组件时，会将&#x200B;**自适应Forms （核心组件）**&#x200B;模板和画布主题添加到您的环境中。

* **自适应表单模板**：模板提供基本结构并定义自适应表单的外观（版面和样式）。它的预格式化的组件包含某些属性和内容结构。它还提供用于定义主题和提交操作的选项。主题定义外观，提交操作定义在提交自适应表单时执行的操作。您还可以将[示例模板](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)部署到您的环境。 这些功能可帮助您迅速创建表单。

  >[!NOTE]
  >
  > 如果环境中没有&#x200B;**自适应表单（核心组件）**&#x200B;模板，请[为您的环境启用自适应表单核心组件](/help/forms/using/enable-adaptive-forms-core-components.md)。在为您的环境启用核心组件时，会将&#x200B;**自适应表单（核心组件）**&#x200B;模板添加到您的环境。

* **自适应表单主题**：主题包含组件和面板的样式详细信息。样式包括背景颜色、状态颜色、透明度、对齐方式和大小等属性。在应用主题时，指定的样式会反映在相应的组件上。在为环境启用核心组件时，默认会添加`Canvas`主题。 您可以[下载并自定义标准主题](create-or-customize-themes-for-adaptive-forms-core-components.md)。 对于现成的&#x200B;**主题**，您可以将[示例主题](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)部署到您的环境。 这些功能可帮助您开始设计表单的样式，并提供一个基础结构，以根据业务需求创建或自定义主题。

* **权限**：将用户添加到[!DNL forms-users]组。[!DNL forms-users]组的成员具有创建自适应表单的权限。有关特定于表单的用户组的详细列表，请参阅[组和权限](forms-groups-privileges-tasks.md)。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## 创建自适应表单 {#create-an-adaptive-form}

1. 登录到本地[AEM创作实例](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=zh-Hans#author-and-publish-installs)。

1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 创建自适应Forms]**。

1. 选择自适应Forms核心组件模板，然后单击&#x200B;**[!UICONTROL 下一步]**。

1. 出现&#x200B;**[!UICONTROL 添加属性]**。 指定以下属性字段的值。 标题和名称字段是必填字段：

   * **[!UICONTROL 标题：]**&#x200B;指定表单的显示名称。 标题可帮助您在 [!DNL Experience Manager Forms] 用户界面中标识表单。
   * **[!UICONTROL 名称：]**&#x200B;指定表单的名称。在存储库中创建具有指定名称的节点。在开始键入标题时，名称字段的值将自动生成。您可以更改建议的值。名称字段只能包含字母数字字符、连字符和下划线。
   * **[!UICONTROL 描述：]**&#x200B;指定有关表单的详细信息。
   * **[!UICONTROL 主题客户端库]：**&#x200B;指定自适应表单的主题。 默认情况下，选择`adaptiveform.theme.canvas3`主题。 您还可以从&#x200B;**[!UICONTROL 主题客户端库]**&#x200B;下拉菜单中选择其他主题。
   * **[!UICONTROL 配置容器：]**&#x200B;定义存储自适应Forms配置文件的位置。 这些配置文件包含与自适应Forms的行为和外观相关的设置和属性。
   * **[!UICONTROL 标记：]**&#x200B;指定用于唯一标识自适应表单的标记。 标记有助于搜索表单。 要创建标记，请在&#x200B;**[!UICONTROL 标记]**&#x200B;框中键入新标记名称。
1. 选择&#x200B;**[!UICONTROL 创建]**。创建自适应表单，并显示用于打开表单进行编辑的对话框。


1. 选择&#x200B;**[!UICONTROL 编辑]**&#x200B;以在新选项卡中打开新创建的表单。 将打开表单进行编辑，并显示模板中的可用内容。 它还会显示用于自定义新创建表单的边栏。


## 使用自适应Forms核心组件创建表单

打开表单进行编辑后，您可以使用可用的自适应Forms核心组件将表单字段添加到表单。 您可以拖放或使用+ [插入组件]选项将这些组件添加到表单中。 请参阅AEM核心组件文档，了解可用的[自适应Forms核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans#components)。 您还可以访问[https://aemcomponents.dev/](https://aemcomponents.dev/)以查看正在运行的可用核心组件。

## 配置自适应表单的提交操作 {#configure-submit-action-for-form}

提交操作允许您选择通过自适应表单捕获的数据的目标。 当用户单击自适应表单上的提交按钮时，会触发该事件。 自适应表单包括一些现成的提交操作。 您还可以扩展默认提交操作以创建自己的自定义提交操作。 要为表单配置提交操作，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/using/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。

1. 单击&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。

   ![单击扳手图标以打开“自适应表单容器”对话框来配置提交操作](/help/forms/using/assets/adaptive-forms-submit-message.png)

1. 根据要求选择并配置&#x200B;**[!UICONTROL 提交操作]**。有关提交操作的详细信息，请参阅[自适应表单提交操作](/help/forms/using/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 将用户重定向到页面或在提交表单时显示感谢消息

在提交表单时，您可以将用户重定向到其他网页或消息。 要重定向用户或配置感谢消息，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/using/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡。

   ![单击“扳手”图标以打开“自适应表单容器”对话框以配置重定向页面或感谢消息](/help/forms/using/assets/adaptive-forms-submit-message.png)

   * 要配置重定向URL，请在提交选项中，选择&#x200B;**[!UICONTROL 重定向到URL]**&#x200B;选项，然后浏览并选择AEM Sites页面或提供外部页面的URL。

   * 要配置自定义或感谢消息，请在“提交”选项中选择&#x200B;**[!UICONTROL 显示消息]**&#x200B;选项，然后在&#x200B;**[!UICONTROL 消息内容]**&#x200B;框中提供消息。 它是一个富文本框，您可以使用全屏选项查看所有可用的富文本项。

## 为自适应表单配置架构或表单数据模型 {#configure-schema-or-data-model-for-form}

您可以使用表单数据模型将表单连接到数据源，以根据用户操作来发送和接收数据。您还可以将表单连接到 JSON 架构，以接收预定义格式的提交数据。根据要求，将表单连接到 JSON 架构或表单数据模型：

* [创建JSON架构并上传到您的环境](/help/forms/using/adaptive-form-json-schema-form-model.md)
* [创建表单数据模型](/help/forms/using/create-form-data-models.md)

### 为表单配置JSON架构或表单数据模型

要为表单配置JSON架构或表单数据模型，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/using/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 打开&#x200B;**[!UICONTROL 数据模型]**&#x200B;选项卡。

   ![单击“扳手”图标以打开自适应表单容器对话框以配置JSON架构或表单数据模型](/help/forms/using/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根据您的要求，选择并配置JSON架构或表单数据模型：

   * 选择&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项时，请使用&#x200B;**[!UICONTROL 选择表单数据模型]**&#x200B;选项来选择预配置的表单数据模型。
   * 选择&#x200B;**[!UICONTROL 架构]**&#x200B;选项时，请使用&#x200B;**[!UICONTROL 架构]**&#x200B;选项为您的表单选择JSON架构。

1. 单击&#x200B;**[!UICONTROL 完成]**。

>[!NOTE]
>
> 您可以使用指南容器属性编辑自适应表单的JSON架构或表单数据模型。

## 配置预填充服务  {#configure-prefill-service-for-form}

您可以使用预填充服务使用现有数据自动填充自适应表单的字段。 当用户打开表单时，这些字段的值会预先填充。 您可以：

* [创建自定义预填充服务](/help/forms/using/prepopulate-adaptive-form-fields.md)
* [使用表单数据模型预填充服务](#fdm-prefill-service)

### 使用表单数据模型预填充服务预填充自适应表单的字段 {#fdm-prefill-service}

您可以使用表单数据模型预填充服务通过表单数据模型或自定义预填充服务预填充自适应表单的字段。 表单数据模型预填充服务使用配置的表单数据模型[&#128279;](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)的Get服务检索数据。 要对自适应表单使用表单数据模型预填充服务，请执行以下操作：

1. 打开内容浏览器，然后选择自适应表单的&#x200B;**[!UICONTROL 指南容器]**&#x200B;组件。
1. 单击指南容器属性![指南属性](/help/forms/using/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击自适应表单容器属性![自适应表单容器属性](/help/forms/using/assets/configure-icon.svg)图标。 此时将打开用于配置数据模型的自适应表单容器对话框。
   ![单击“扳手”图标以打开“自适应表单容器”对话框以配置重定向页面或感谢消息](/help/forms/using/assets/adaptive-forms-container-prefill-service.png)
1. 选择表单数据模型。 打开&#x200B;**[!UICONTROL 基本]**&#x200B;选项卡。 在预填充服务中，选择&#x200B;**[!UICONTROL 表单数据模型预填充服务]**。
1. 单击&#x200B;**[!UICONTROL 完成]**。 您的自适应表单现在配置为使用表单数据模型预填充。 您现在可以使用[规则编辑器](rule-editor.md)创建规则以预填充表单的字段。

## 如何重命名AEM自适应表单？{#rename-an-AEM-Adaptive-Form}

要重命名自适应表单，请执行以下步骤：

1. 在AEM Forms用户界面中选择自适应表单。
1. 单击位于上边栏上的&#x200B;**属性**。

   ![属性](/help/forms/using/assets/rename-form-properties.png)

1. 在&#x200B;**标题**&#x200B;选项卡中更改表单的名称，如下图所示。
1. 单击&#x200B;**保存并关闭**。

   ![重命名AEM自适应表单](/help/forms/using/assets/rename-form-title.png)


<!--
## Edit Form Model properties of an Adaptive Form {#edit-form-model}

1. Select the Adaptive Form and select ![Page information](/help/forms/using/assets/configure-icon.svg) > **[!UICONTROL Open Properties]**. The Form Properties page opens. 

1. Go to the **[!UICONTROL Form Model]** tab and choose a form model. If the Adaptive Form is without a form model, you have the freedom to choose either a JSON schema or a form data model. On the other hand, if the Adaptive Form is already based on a form model, you have the option to switch to another form model of the same type. For instance, if the form is using a JSON schema, you can easily switch to another JSON schema, and similarly if the form is using a Form Data Model, you can switch to another Form Data Model. 

1. Select **[!UICONTROL Save]** to save the properties.
-->

## 后续内容

* [使用规则编辑器向表单添加动态行为](rule-editor.md)
* [创建或自定义基于核心组件的自适应Forms的主题](create-or-customize-themes-for-adaptive-forms-core-components.md)


## 另请参阅

* [创建基于核心组件的自适应表单](create-an-adaptive-form-core-components.md)
* [创建自适应表单或将其添加到AEM Sites页面或体验片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [示例主题模板和表单数据模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hans)
