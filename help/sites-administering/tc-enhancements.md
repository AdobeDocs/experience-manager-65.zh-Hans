---
title: 翻译增强功能
seo-title: Translation Enhancements
description: AEM中的翻译增强功能。
seo-description: Translation enhancements in AEM.
uuid: 0563603f-327b-48f1-ac14-6777c06734b9
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 42df2db3-4d3c-4954-a03e-221e2f548305
feature: Language Copy
exl-id: 2011a976-d506-4c0b-9980-b8837bdcf5ad
source-git-commit: 3de9f3c97b99644297a2f07344f6aebae1c5ae83
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 10%

---

# 翻译增强功能{#translation-enhancements}

本页介绍对AEM翻译管理功能的增量增强和改进。

## 翻译项目自动化 {#translation-project-automation}

添加了用于提高翻译项目工作效率的选项，例如自动提升和删除翻译启动项，以及计划翻译项目的定期执行。

1. 在您的翻译项目中，单击或点按 **翻译摘要** 拼贴。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到 **高级** 选项卡。 在底部，您可以选择 **自动提升翻译启动项**.

   ![screen_shot_2018-04-19at223430](assets/screen_shot_2018-04-19at223430.jpg)

1. （可选）您可以选择是否在收到翻译内容后自动提升和删除翻译启动项。

   ![screen_shot_2018-04-19at224033](assets/screen_shot_2018-04-19at224033.jpg)

1. 要选择翻译项目的定期执行，请在下方选择带下拉菜单的频率 **重复翻译**. 定期项目执行将在指定的时间间隔内自动创建和执行翻译作业。

   ![screen_shot_2018-04-19at223820](assets/screen_shot_2018-04-19at223820.jpg)

## 多语言翻译项目 {#multilingual-translation-projects}

可以在翻译项目中配置多种目标语言，以减少创建的翻译项目总数。

1. 在翻译项目中，单击或点按 **翻译摘要** 拼贴。

   ![screen_shot_2018-04-19at222622](assets/screen_shot_2018-04-19at222622.jpg)

1. 切换到 **高级** 选项卡。 您可以在 **目标语言**.

   ![screen_shot_2018-04-22at212601](assets/screen_shot_2018-04-22at212601.jpg)

1. 或者，如果您通过站点中的引用边栏启动翻译，请添加语言并选择 **创建多语言翻译项目**.

   ![screen_shot_2018-04-22at212941](assets/screen_shot_2018-04-22at212941.jpg)

1. 将在项目中为每种目标语言创建翻译作业。 可以在项目中逐个启动这些任务，也可以通过在项目管理员中全局执行项目来同时执行这些任务。

   ![screen_shot_2018-04-22at213854](assets/screen_shot_2018-04-22at213854.jpg)

## 翻译内存更新 {#translation-memory-updates}

已翻译内容的手动编辑可以同步回翻译管理系统 (TMS) 以训练其翻译记忆库。

1. 在站点控制台中，更新翻译页面中的文本内容后，选择 **更新翻译内存**.

   ![screen_shot_2018-04-22at234430](assets/screen_shot_2018-04-22at234430.jpg)

1. 列表视图显示每个已编辑的文本组件的源和翻译的并排比较。选择应同步到翻译记忆库的翻译更新，然后选择 **更新内存**.

   ![screen_shot_2018-04-22at235024](assets/screen_shot_2018-04-22at235024.jpg)

AEM 会将选定的字符串发送回翻译管理系统。

* 该操作可更新已配置翻译管理系统(TMS)的翻译内存中现有字符串的翻译。
* 它不会创建新的翻译作业。
* 它会通过AEM转换API将字符串的值对及其转换发送回TMS。
* 此功能要求翻译管理系统配置为与AEM一起使用。

## 多个级别的语言副本 {#language-copies-on-multiple-levels}

语言根现在可以分组到节点下，例如按区域，同时仍被识别为语言副本的根。

![screen_shot_2018-04-23at144012](assets/screen_shot_2018-04-23at144012.jpg)

>[!CAUTION]
>
>仅允许一个级别。例如，以下内容将不允许“es”页面解析为语言副本：
>
>* `/content/we-retail/language-masters/en`
>* `/content/we-retail/language-masters/americas/central-america/es`
>
>此 `es` 将不会检测到语言副本，因为它是2个级别（美洲/中美洲），而不是 `en` 节点。

>[!NOTE]
>
>语言根可以具有任何页面名称，而不只是语言的ISO代码。 AEM将始终先检查路径和名称，但如果页面名称无法识别语言，则AEM将检查页面的cq:language属性以获取语言标识。

## 翻译状态报表 {#translation-status-reporting}

现在，可以在站点列表视图中选择一个属性，以显示页面是否已翻译、正在翻译或尚未翻译。 要显示它，请执行以下操作：

1. 在站点中，切换到 **列表视图。**

   ![screen_shot_2018-04-23at130646](assets/screen_shot_2018-04-23at130646.jpg)

1. 单击或点按 **查看设置**.

   ![screen_shot_2018-04-23at130844](assets/screen_shot_2018-04-23at130844.jpg)

1. 检查 **已翻译** 复选框下方 **翻译** 然后点按/单击 **更新**.

   ![screen_shot_2018-04-23at130955](assets/screen_shot_2018-04-23at130955.jpg)

您现在可以看到 **已翻译** 列，显示页面的翻译状态。

![screen_shot_2018-04-23at133821](assets/screen_shot_2018-04-23at133821.jpg)
