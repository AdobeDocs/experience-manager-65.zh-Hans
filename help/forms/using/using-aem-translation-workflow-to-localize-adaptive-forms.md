---
title: 使用AEM翻译工作流程本地化自适应表单和记录文档
seo-title: 使用AEM翻译工作流程本地化自适应表单和记录文档
description: 了解如何使用AEM翻译工作流本地化自适应表单和记录文档。
seo-description: 了解如何使用AEM翻译工作流本地化自适应表单和记录文档。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: 自适应表单
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# 使用AEM翻译工作流程本地化自适应表单和记录{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}的文档

本地化表单可帮助您跨地域提供更广的受众。 Adobe Experience Manager翻译工作流程可帮助您本地化自适应表单及其记录文档。 可以使用&#x200B;**机器翻译**&#x200B;或&#x200B;**人文翻译器**&#x200B;本地化自适应表单。

本文说明了将AEM翻译工作流与自适应表单和记录文档结合使用的过程。

## 使用机器翻译{#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}对自适应表单和记录文档进行本地化

机器翻译服务会立即以自适应形式和记录文档翻译您的内容。 AEM Forms已预配置为使用Microsoft Translator试用版进行机器翻译。 请执行以下步骤，为自适应表单和记录文档启用机器翻译：

1. 在AEM Forms UI中，选择一个表单，然后点按&#x200B;**添加词典**&#x200B;选项。
1. 在&#x200B;**将词典添加到翻译项目**&#x200B;屏幕中，选择&#x200B;**创建新翻译项目**&#x200B;或&#x200B;**添加到现有翻译项目**&#x200B;选项。
1. 在&#x200B;**项目标题**&#x200B;字段中，指定标题。 例如，`Government Reference Site - German locale.`
1. 在&#x200B;**目标语言**&#x200B;字段中，指定区域设置（例如`German(de)`），然后单击&#x200B;**完成**。 您可以指定多个区域设置。 表单将翻译为&#x200B;**目标语言**&#x200B;字段中指定的所有语言环境。
1. 在“已添加词典”对话框中，单击&#x200B;**打开项目**。 在“项目”屏幕中，打开新创建的项目。
1. 单击&#x200B;**翻译摘要**&#x200B;拼贴底部的&#x200B;**省略号**。 “翻译摘要”屏幕将打开。
1. 单击&#x200B;**翻译摘要**&#x200B;屏幕顶部的&#x200B;**编辑**&#x200B;图标。 打开&#x200B;**Translation**&#x200B;选项卡，并在&#x200B;**Translation Method**&#x200B;屏幕中选择Machine Translation。 选择相应的&#x200B;**转换提供程序**&#x200B;和&#x200B;**云配置**。 单击屏幕顶部的&#x200B;**完成**&#x200B;图标。
1. 在&#x200B;**转换作业**&#x200B;拼贴中，单击![aem62forms_downarrow](assets/aem62forms_downarrow.png)图标，然后单击&#x200B;**开始**。 拼贴的状态将更改为“草稿”。 翻译完成后，状态将变为&#x200B;**准备审阅**。 几分钟后刷新页面并验证状态。
1. 在状态变为&#x200B;**转换作业**&#x200B;拼贴上的&#x200B;**准备审阅**&#x200B;后，在浏览器窗口中打开表单。 将显示表单的本地化版本。

   >[!NOTE]
   >
   >* 在浏览器窗口中打开表单的本地化版本之前，请确保将浏览器的区域设置设置为与表单的区域设置匹配。 例如，如果表单已翻译为德语(de)语言，则将浏览器的区域设置设置为德语(de)。
   >* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。


   除了自适应表单外，自动生成的记录文档也已本地化。

   有关“记录”设置和配置的文档的详细信息，请参阅：

   [记录文档模板配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [文档录制设置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定义记录文档的品牌信](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 息，并确保将浏览器区域设置设置为您使用机器语言本地化自适应表单的同一语言。浏览器区域设置有助于在记录文档中本地化品牌信息。
1. 要视图记录的本地化文档，请点按生成预览。 录制PDF的文档将在您浏览器的新选项卡中生成并打开。

## 使用人文翻译{#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}对自适应表单及其记录文档进行本地化

在人文翻译中，内容将发送给翻译提供商，并由专业翻译人员进行翻译。 完成后，将返回译文内容并导入AEM。 将您的翻译提供商与AEM集成后，内容会在AEM和翻译提供商之间自动发送。

对于翻译，将与专业翻译人员共享包含XLIFF格式文件的词典。 词典包括每个区域设置的单独XLIFF文件。 每个XLIFF文件都包含将向最终用户显示的文本以及相应本地化文本的占位符。

使用“人文翻译员”，执行以下步骤来本地化表单及其记录文档:

1. [将AEM与您的翻译服务提供商](/help/sites-administering/tc-tic.md) 连接并 [创建翻译集成框架配置](/help/sites-administering/tc-tic.md)。

1. [将您的语言母版的页](/help/sites-administering/tc-tic.md) 面与翻译服务和框架配置关联。

1. [确定要翻译的](/help/sites-administering/tc-rules.md) 内容类型。

1. [通过创作语言主控](/help/sites-administering/tc-prep.md) 和创建语言副本的根页面，准备要翻译的内容。

1. [创建翻](/help/sites-administering/tc-manage.md) 译项目以收集要翻译的内容并准备翻译过程。

1. 使用翻译项目来管理[内容翻译过程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自适应表单组件不支持从右到左(RTL)语言。 例如，希伯来语。

>



