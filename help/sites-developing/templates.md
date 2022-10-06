---
title: 模板
seo-title: Templates
description: 创建将用作新页面基础的页面时，会使用模板
seo-description: Templates are used when creating a page which will be used as the base for the new page
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# 模板{#templates}

模板在AEM的不同位置使用：

* When [创建需要选择模板的页面](#templates-pages);这将用作新页面的基础。 模板可定义生成页面的结构、任何初始内容以及 [组件](/help/sites-authoring/default-components.md) （设计属性）。

* When [创建内容片段时，您还需要选择模板](#templates-content-fragments). 此模板可定义结构、初始元素和变量。

详细介绍了以下模板：

* [页面模板 — 可编辑](/help/sites-developing/page-templates-editable.md)
* [页面模板 — 静态](/help/sites-developing/page-templates-static.md)
* [内容片段模板](/help/sites-developing/content-fragment-templates.md)
* [自适应模板渲染](/help/sites-developing/templates-adaptive-rendering.md)

## 模板 — 页面 {#templates-pages}

AEM现在提供两种用于创建页面的基本模板类型：

>[!NOTE]
>
>使用模板 [创建新页面](/help/sites-authoring/managing-pages.md#creating-a-new-page) （对页面作者而言）没有明显的差异，也没有显示正在使用的模板类型。

### 可编辑模板 {#editable-templates}

可编辑的模板现在被视为使用AEM进行开发的最佳实践。

可编辑模板的优势：

* 可以 [已创建](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 和 [编辑](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 的作者。

* 引入此模板后，您可以为使用该模板创建的任何页面定义以下内容：

   * 结构
   * 初始内容
   * 内容策略

* 创建新页面后，页面与模板之间会保持动态连接；这意味着对模板结构所做的更改将反映在使用该模板创建的任何页面上（不会反映对初始内容所做的更改）。
* 使用内容策略（从模板编辑器中编辑）来保留设计属性（在页面编辑器中不使用设计模式）。
* 存储在 `/conf`
* 请参阅 [可编辑的模板](/help/sites-developing/page-templates-editable.md) 以了解更多信息。

>[!NOTE]
>
>AEM社区文章介绍了如何使用可编辑的模板开发Experience Manager网站，请参阅 [使用可编辑的模板创建Adobe Experience Manager 6.5网站](https://helpx.adobe.com/experience-manager/using/first_aem64_website.html).

### 静态模板 {#static-templates}

静态模板:

* 必须由您的开发人员定义和配置。
* 这是AEM的原始模板系统，已推出多个版本。
* 静态模板是节点的层次结构，其结构与要创建的页面相同，但没有任何实际内容。
* 复制以创建新页面，此后不存在动态连接。
* 使用 [设计模式](/help/sites-authoring/default-components-designmode.md) 来保留设计属性。
* 存储在 `/apps`
* 请参阅 [静态模板](/help/sites-developing/page-templates-static.md) 以了解更多信息。

>[!NOTE]
>
>自AEM 6.5起，使用静态模板不被视为最佳实践。 请改用可编辑的模板。
>
>[AEM现代化](modernization-tools.md) 工具可以帮助您从静态模板迁移到可编辑的模板。

### 模板可用性 {#template-availability}

>[!CAUTION]
>
>AEM提供了多个属性来控制 **站点**. 但是，将它们组合在一起可能会导致非常复杂的规则，从而难以跟踪和管理。
>
>因此，Adobe建议您首先通过定义以下内容来简单操作：
>
>* 只有 `cq:allowedTemplates` 属性
>
>* 仅在站点根目录上
>
>有关示例，请参阅We.Retail: `/content/we-retail/jcr:content`
>
>属性 `allowedPaths`, `allowedParents`和 `allowedChildren` 也可以放置在模板上以定义更复杂的规则。 但是，如果可能， *多* 更简单地进一步定义 `cq:allowedTemplates` 网站子区域的属性（如果需要进一步限制允许的模板）。
>
>另一个优势是 `cq:allowedTemplates` 属性可由作者在 **高级** 选项卡 **页面属性**. 无法使用（标准）UI更新其他模板属性，因此需要开发人员为每次更改维护规则和代码部署。

在站点管理界面中创建新页面时，可用模板的列表取决于新页面的位置以及在每个模板中指定的放置限制。

以下属性确定模板是否 `T` 允许将新页面用作页面的子项 `P`. 以下每个属性都是一个包含零个或多个正则表达式的多值字符串，用于与路径匹配：

* 的 `cq:allowedTemplates` 属性 `jcr:content` 子节点 `P` 或 `P`.

* 的 `allowedPaths` 财产 `T`.

* 的 `allowedParents` 财产 `T`.

* 的 `allowedChildren` 模板的属性 `P`.

评价工作如下：

* 第一个非空 `cq:allowedTemplates` 属性，该属性在页面层次结构的升序时以开头 `P` 与 `T`. 如果没有值匹配， `T` 被拒绝。

* 如果 `T` 具有非空 `allowedPaths` 属性，但没有任何值与 `P`, `T` 被拒绝。

* 如果上述两个属性为空或不存在， `T` 被拒绝，除非它属于与 `P`. `T` 属于与 `P` 如果且仅当路径的第二级名称 `T` 与路径的第二级名称相同 `P`. 例如，模板 `/apps/geometrixx/templates/foo` 属于与页面相同的应用程序 `/content/geometrixx`.

* 如果 `T` 具有非空 `allowedParents` 属性，但没有任何值与 `P`, `T` 被拒绝。

* 如果的模板 `P` 具有非空 `allowedChildren` 属性，但没有任何值与 `T`, `T` 被拒绝。

* 在所有其他情况下， `T` 中的“禁止页面加载闪烁”。

下图描述了模板评估流程：

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子页面中使用的限制模板 {#limiting-templates-used-in-child-pages}

要限制可在给定页面下创建子页面的模板，请使用 `cq:allowedTemplates` 财产 `jcr:content` 用于指定允许作为子页面的模板列表的页面节点。 列表中的每个值都必须是允许的子页面模板的绝对路径，例如 `/apps/geometrixx/templates/contentpage`.

您可以使用 `cq:allowedTemplates` 模板上的属性  `jcr:content` 节点，以将此配置应用于使用此模板的所有新创建页面。

如果要添加更多约束（例如与模板层次结构有关的约束），可以使用 `allowedParents/allowedChildren` 属性。 然后，您可以明确指定从模板T创建的页面必须是从模板T创建的页面的父/子页面。

## 模板 — 内容片段 {#templates-content-fragments}

请参阅 [内容片段模板](/help/sites-developing/content-fragment-templates.md) 以了解完整信息。
