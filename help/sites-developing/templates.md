---
title: 模板
description: 创建用作新页面基础的页面时，将使用模板。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# 模板{#templates}

模板在AEM中的各个时间点使用：

* [创建页面时，请选择模板](#templates-pages)。 此模板用作新页面的基础。 模板定义了页面的结构、任何初始内容以及可用的[组件](/help/sites-authoring/default-components.md)（设计属性）。

* [在创建内容片段时，您还应选择模板](#templates-content-fragments)。 此模板定义结构、初始元素和变体。

以下模板将详细介绍：

* [页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)
* [页面模板 — 静态](/help/sites-developing/page-templates-static.md)
* [内容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自适应模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板 — 页面 {#templates-pages}

AEM现在提供了两种用于创建页面的基本模板类型：

>[!NOTE]
>
>使用模板来[创建页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)时，没有可见差异（对页面作者而言），也未指示所使用的模板类型。

### 可编辑模板 {#editable-templates}

可编辑模板现在被视为使用AEM进行开发的最佳实践。

可编辑模板的优势：

* 可以由您的作者[创建](/help/sites-authoring/templates.md#creating-a-new-template-template-author)和[编辑](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)。

* 引入后，您可以为使用该模板创建的任何页面定义以下内容：

   * 结构
   * 初始内容
   * 内容策略

* 创建新页面后，页面和模板之间会保持动态连接。 此连接意味着对模板结构的更改会反映在使用该模板创建的任何页面上；对初始内容的更改不会反映在页面上。
* 使用内容策略（从模板编辑器编辑）来保留设计属性（不使用页面编辑器中的设计模式）。
* 存储在`/conf`下
* 有关详细信息，请参阅[可编辑模板](/help/sites-developing/page-templates-editable.md)。

>[!NOTE]
>
>请参阅[使用可编辑的页面模板开发Experience Manager站点](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=zh-Hans)。

### 静态模板 {#static-templates}

静态模板：

* 必须由开发人员定义和配置。
* AEM的原始模板系统已经有许多版本可用。
* 静态模板是指与要创建页面具有相同结构，但没有任何实际内容的节点的层次结构。
* 创建页面时复制了此变量，此后不存在动态连接。
* 使用[设计模式](/help/sites-authoring/default-components-designmode.md)保存设计属性。
* 存储在`/apps`下
* 有关详细信息，请参阅[静态模板](/help/sites-developing/page-templates-static.md)。

>[!NOTE]
>
>从AEM 6.5开始，使用静态模板不被视为最佳实践。 请改用可编辑的模板。
>
>[AEM现代化](modernization-tools.md)工具可以帮助您从静态模板迁移到可编辑模板。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供了多个属性以控制&#x200B;**站点**&#x200B;下允许的模板。 但是，将它们组合在一起可能会导致难以跟踪和管理的复杂规则。
>
>因此，Adobe建议您从定义以下内容开始：
>
>* 仅`cq:allowedTemplates`属性
>
>* 仅在站点根目录上
>
>有关示例，请参阅We.Retail： `/content/we-retail/jcr:content`
>
>属性`allowedPaths`、`allowedParents`和`allowedChildren`也可以放在模板上以定义更复杂的规则。 但是，如果可能的话，如果需要进一步限制允许的模板，在网站的子区域上定义其他`cq:allowedTemplates`属性会更简单&#x200B;*许多*。
>
>另一个优势是作者可以在&#x200B;**页面属性**&#x200B;的&#x200B;**高级**&#x200B;选项卡中更新`cq:allowedTemplates`属性。 无法使用（标准）UI更新其他模板属性，因此需要开发人员维护规则和每次更改的代码部署。

在站点管理界面中创建页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的版面限制。

以下属性确定模板`T`是否用于要作为页面`P`的子页面放置的新页面。 以下每个属性都是一个多值字符串，其中包含零个或多个用于与路径匹配的正则表达式：

* `P`的`jcr:content`子节点或`P`的上级的`cq:allowedTemplates`属性。

* `T`的`allowedPaths`属性。

* `T`的`allowedParents`属性。

* `P`模板的`allowedChildren`属性。

评估工作如下：

* 以`P`开头的页面层次结构升序时找到的第一个非空`cq:allowedTemplates`属性与`T`的路径匹配。 如果没有任何匹配的值，则会拒绝`T`。

* 如果`T`具有非空的`allowedPaths`属性，但没有值与`P`的路径匹配，则`T`被拒绝。

* 如果上述两个属性都为空或不存在，`T`将被拒绝，除非它与`P`属于同一应用程序。 当且仅当`T`路径的第二级名称与`P`路径的第二级名称相同时，`T`与`P`属于同一应用程序。 例如，模板`/apps/geometrixx/templates/foo`与页面`/content/geometrixx`属于同一应用程序。

* 如果`T`具有非空的`allowedParents`属性，但没有值与`P`的路径匹配，则`T`被拒绝。

* 如果`P`的模板具有非空的`allowedChildren`属性，但没有值与`T`的路径匹配，则`T`被拒绝。

* 在所有其他情况下，允许`T`。

下图描述了模板评估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 限制子页面中使用的模板 {#limiting-templates-used-in-child-pages}

要限制哪些模板可用于在给定页面下创建子页面，请使用页面`jcr:content`节点的`cq:allowedTemplates`属性指定允许作为子页面的模板列表。 列表中的每个值都必须是允许的子页面的模板的绝对路径，例如`/apps/geometrixx/templates/contentpage`。

您可以在模板的`jcr:content`节点上使用`cq:allowedTemplates`属性，将此配置应用于使用此模板的所有新创建的页面。

如果要添加更多约束（例如，关于模板层次结构），可以在模板上使用`allowedParents/allowedChildren`属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父项/子项。

## 模板 — 内容片段 {#templates-content-fragments}

请参阅[内容片段模板](/help/sites-developing/content-fragment-templates.md)。
