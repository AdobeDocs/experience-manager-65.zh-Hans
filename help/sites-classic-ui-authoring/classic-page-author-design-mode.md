---
title: 在设计模式下配置组件
description: 现成安装AEM实例后，即可在sidekick中找到一组组件。 除此之外，还可以使用各种其他组件。 您可以使用设计模式启用/禁用此类组件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 在设计模式下配置组件{#configuring-components-in-design-mode}

现成安装AEM实例后，即可在sidekick中找到一组组件。

除此之外，还可以使用各种其他组件。 您可以使用设计模式来 [启用/禁用此类组件](#enabledisablecomponentsusingdesignmode). 启用并位于您的页面后，您可以使用设计模式来 [配置组件设计的各个方面](#configuringcomponentsusingdesignmode) 通过编辑属性参数。

>[!NOTE]
>
>编辑这些组件时务必谨慎。 设计设置通常是整个网站设计不可分割的一部分，因此它们只应由具有适当权限（和体验）的人员更改，通常是管理员或开发人员。 请参阅 [开发组件](/help/sites-developing/components.md) 以了解更多信息。

这实际上涉及添加或删除页面段落系统中允许的组件。 段落系统( `parsys`)是包含所有其他段落组件的复合组件。 段落系统允许作者向页面添加不同类型的组件，因为它包含所有其他段落组件。 每个段落类型都表示为一个组件。

例如，产品页面的内容可能包含包含以下内容的段落系统：

* 产品的图像（采用图像或文本段落的形式）
* 产品描述（作为文本段落）
* 带有技术数据的表格（作为表格段落）
* 表单用户填写（作为表单开头、表单元素和表单结束段落）

>[!NOTE]
>
>请参阅 [开发组件](/help/sites-developing/components.md#paragraphsystem) 和 [使用模板和组件的准则](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) 有关的详细信息 `parsys`.

## 启用/禁用组件 {#enable-disable-components}

在设计模式下，Sidekick被最小化，您可以配置可用于创作的组件：

1. 要进入设计模式，请打开页面进行编辑，并使用Sidekick图标：

   ![设计模式](do-not-localize/chlimage_1.png)

1. 单击 **编辑** 在段落系统(**杆件设计**)。

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. 此时将打开一个对话框，其中列出了Sidekick中显示的组件组及其包含的各个组件。

   根据需要选择添加或删除可在Sidekick中使用的组件。

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. 在设计模式下，Sidekick会最小化。 通过单击箭头，您可以最大化Sidekick并返回到编辑模式：

   ![Sidekick已最小化](do-not-localize/sidekick-collapsed.png)

## 配置组件设计 {#configuring-the-design-of-a-component}

在设计模式下，您还可以配置各个组件的属性。 每个组件都有自己的参数，以下示例显示了 **图像** 组件：

1. 要进入设计模式，请打开页面进行编辑，并使用Sidekick图标：

   ![设计模式 — Sidekick](do-not-localize/chlimage_1-1.png)

1. 您可以配置组件设计。

   例如，如果您单击 **编辑** 在图像组件上(**图像设计**)您可以配置特定于组件的参数：

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. 单击 **确定** 以保存更改。

1. 在设计模式下，Sidekick会最小化。 通过单击箭头，您可以最大化Sidekick并返回到编辑模式：

   ![Sidekick已最小化](do-not-localize/sidekick-collapsed-1.png)
