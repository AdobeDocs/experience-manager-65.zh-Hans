---
title: 使用AEM翻译工作流将自适应表单和记录文档本地化
description: 了解如何使用AEM翻译工作流本地化自适应表单和记录文档。
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms,Foundation Components
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 20%

---

# 使用AEM翻译工作流将自适应表单和记录文档本地化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hans)，以[创建新的自适应表单](/help/forms/using/create-an-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

本地化的表单可帮助您跨地域提供更广泛的受众。 Adobe Experience Manager翻译工作流可帮助您本地化自适应表单及其记录文档。 您可以使用&#x200B;**机器翻译**&#x200B;或&#x200B;**人工翻译员**&#x200B;本地化自适应表单。

本文介绍了将AEM翻译工作流与自适应表单和记录文档结合使用的过程。

## 使用机器翻译本地化自适应表单和记录文档 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

机器翻译服务会立即以自适应表单和记录文档翻译您的内容。 AEM Forms已预配置为使用Microsoft Translator的试用版进行机器翻译。 执行以下步骤以启用自适应表单和记录文档的机器翻译：

1. 在AEM Forms UI上，选择一个表单，然后选择&#x200B;**添加词典**&#x200B;选项。
1. 在&#x200B;**将字典添加到翻译项目**&#x200B;屏幕中，选择&#x200B;**新建翻译项目**&#x200B;或&#x200B;**添加到现有翻译项目**&#x200B;选项。
1. 在&#x200B;**项目标题**&#x200B;字段中，指定标题。 例如，`Government Reference Site - German locale.`
1. 在&#x200B;**目标语言**&#x200B;字段中，指定区域设置（例如，`German(de)`），然后单击&#x200B;**完成**。 您可以指定多个区域设置。 表单已翻译为&#x200B;**目标语言**&#x200B;字段中指定的所有区域设置。
1. 在“添加的词典”对话框中，单击&#x200B;**打开项目**。 在“项目”屏幕中，打开新创建的项目。
1. 单击&#x200B;**翻译摘要**&#x200B;拼贴底部的&#x200B;**省略号**。 这将打开翻译摘要屏幕。
1. 单击&#x200B;**翻译摘要**&#x200B;屏幕顶部的&#x200B;**编辑**&#x200B;图标。 打开&#x200B;**翻译**&#x200B;选项卡，并在&#x200B;**翻译方法**&#x200B;屏幕中选择机器翻译。 选择适当的&#x200B;**翻译提供商**&#x200B;和&#x200B;**云配置**。 单击屏幕顶部的&#x200B;**完成**&#x200B;图标。
1. 在&#x200B;**翻译作业**&#x200B;拼贴上，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**开始**。 图块的状态将更改为“草稿”。 翻译完成后，状态将更改为&#x200B;**准备好审查**。 几分钟后刷新页面并验证状态。
1. 在&#x200B;**翻译作业**&#x200B;拼贴上的状态更改为&#x200B;**准备好审查**&#x200B;后，在浏览器窗口中打开表单。 此时将显示表单的本地化版本。

   >[!NOTE]
   >
   >* 在浏览器窗口中打开本地化的表单版本之前，请确保将浏览器的区域设置设置为与表单的区域设置相匹配。 例如，如果表单转换为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右至左(RTL)语言。 例如，希伯来语。

   除了自适应表单外，自动生成的记录文档也进行了本地化。

   有关记录文档设置和配置的更多信息，请参阅：

[记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[记录文档设置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定义记录文档的品牌信息](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)，并确保将浏览器区域设置设置为使用计算机语言将自适应表单本地化的相同语言。 浏览器区域设置有助于本地化记录文档中的品牌信息。
1. 要查看本地化的记录文档，请选择生成预览。 记录文档PDF在浏览器中生成并在新选项卡中打开。

## 使用人工翻译本地化自适应表单及其记录文档 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人工翻译中，内容将发送给翻译提供商并由专业翻译人员进行翻译。 完成后，将返回翻译的内容并将其导入 AEM。当您的翻译提供商与 AEM 集成时，内容会在 AEM 和翻译提供商之间自动发送。

对于翻译，包含XLIFF格式文件的词典将与专业翻译人员共享。 该词典包括适用于每种区域设置的单独的XLIFF文件。 每个XLIFF文件都包含将向最终用户显示的文本，以及相应的本地化文本的占位符。

执行以下步骤以使用人工翻译员本地化表单及其记录文档：

1. [将 AEM 连接到翻译服务提供商](/help/sites-administering/tc-tic.md)和[创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将语言母版页面关联到](/help/sites-administering/tc-tic.md)翻译服务和框架配置。

1. [标识要翻译的内容类型](/help/sites-administering/tc-rules.md)。

1. 通过创作语言母版并创建语言副本的根页面来[准备内容以进行翻译](/help/sites-administering/tc-prep.md)。

1. [创建翻译项目](/help/sites-administering/tc-manage.md)以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目[管理内容翻译过程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自适应表单组件不支持从右至左(RTL)语言。 例如，希伯来语。
>
