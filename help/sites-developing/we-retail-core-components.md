---
title: 在We.Retail中试用核心组件
description: 了解如何使用We.Retail在Adobe Experience Manager中试用核心组件。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# 在We.Retail中试用核心组件{#trying-out-core-components-in-we-retail}

核心组件是灵活的新式组件，具有轻松的扩展性并允许轻松集成到项目中。 核心组件是围绕几个主要设计原则构建的，例如HTL、开箱即用的可用性、可配置性、版本控制和可扩展性。 We.Retail构建于核心组件之上。

## 正在尝试 {#trying-it-out}

1. 使用We.Retail示例内容启动Adobe Experience Manager (AEM)，并打开[组件控制台](/help/sites-authoring/default-components-console.md)。

   **全局导航>工具>组件**

1. 在组件控制台中打开边栏，您可以筛选特定组件组。 核心组件可在以下位置找到：

   * `.core-wcm`：标准核心组件
   * `.core-wcm-form`：表单提交核心组件

   选择`.core-wcm`。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 所有核心组件都名为&#x200B;**v1**，这反映了此核心组件的第一个版本。 今后将发布常规版本，这些版本与AEM的版本兼容，并且允许轻松升级，以便您能够利用最新功能。
1. 单击&#x200B;**文本(v1)**。

   查看该组件的&#x200B;**资源类型**&#x200B;是`/apps/core/wcm/components/text/v1/text`。 核心组件位于`/apps/core/wcm/components`下，且按组件进行版本控制。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 单击&#x200B;**文档**&#x200B;选项卡以查看组件的开发人员文档。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 返回到组件控制台。 筛选组&#x200B;**We.Retail**&#x200B;并选择&#x200B;**Text**&#x200B;组件。
1. 查看&#x200B;**资源类型**&#x200B;在`/apps/weretail`下按预期指向组件，但&#x200B;**资源超级类型**&#x200B;指向核心组件`/apps/core/wcm/components/text/v1/text`。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 单击&#x200B;**实时使用情况**&#x200B;选项卡以查看将在哪些页面上使用此组件。 单击前&#x200B;**感谢**&#x200B;页以编辑该页。

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. 在感谢页面上，选择文本组件，并在该组件的“编辑”菜单中，单击取消继承图标。

   [We.Retail具有全局化网站结构](/help/sites-developing/we-retail-globalized-site-structure.md)，内容通过称为继承[&#128279;](/help/sites-administering/msm.md)的机制从语言母版推送到活动副本。 因此，必须取消继承，用户才能手动编辑文本。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 单击&#x200B;**是**&#x200B;确认取消。

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. 取消继承并选择文本组件后，即可使用更多选项。 单击&#x200B;**编辑**。

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. 您现在可以看到哪些编辑选项可用于文本组件。

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. 从&#x200B;**页面信息**&#x200B;菜单中，选择&#x200B;**编辑模板**。
1. 在页面的模板编辑器中，单击页面&#x200B;**布局容器**&#x200B;中文本组件的&#x200B;**策略**&#x200B;图标。

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. 利用核心组件，模板作者可以配置哪些属性可供页面作者使用。 这些功能包括允许的粘贴源、格式选项和可用的段落样式等功能。

   此类设计对话框可用于许多核心组件，并与模板编辑器携手工作。 启用后，作者可以通过组件编辑器使用它们。

   ![chlimage_1-172](assets/chlimage_1-172.png)

## 更多信息 {#further-information}

有关核心组件的更多信息，请参阅创作文档[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)以了解核心组件的功能概述，并参阅开发人员文档[开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html)以了解技术概述。

此外，您可能希望进一步调查[可编辑模板](/help/sites-developing/we-retail-editable-templates.md)。 有关可编辑模板的完整详细信息，请参阅创作文档[创建页面模板](/help/sites-authoring/templates.md)或开发人员文档页面[模板 — 可编辑](/help/sites-developing/page-templates-editable.md)。
