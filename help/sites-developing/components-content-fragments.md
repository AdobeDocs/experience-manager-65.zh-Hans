---
title: 内容片段的组件
description: Adobe Experience Manager (AEM)内容片段作为独立于页面的资源而创建和管理
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 内容片段的组件{#components-for-content-fragments}

## 用于片段创作的组件 {#components-for-fragment-authoring}

>[!CAUTION]
>
>不建议扩展或更改片段编辑器中使用的实际组件，因为它们仍然可能会发生更改。

查看[内容片段管理API — 客户端](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)。

## 用于页面创作的组件 {#components-for-page-authoring}

>[!CAUTION]
>
>现在建议使用[内容片段核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html)。 有关详细信息，请参阅[开发核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html)。
>
>此部分详细介绍为与内容片段（**常规**&#x200B;组中的&#x200B;**内容片段**）一起使用而交付的原始组件。

>[!NOTE]
>
>另请参阅[内容片段配置用于渲染的组件](/help/sites-developing/content-fragments-config-components-rendering.md)以了解更多信息。

Adobe Experience Manager (AEM)内容片段是[作为独立于页面的资源创建和管理的](/help/assets/content-fragments/content-fragments.md)。 它们允许您创建渠道中性内容，以及各种（特定于渠道的）变体。 [然后，您可以在创作内容页面时使用这些片段及其变体](/help/sites-authoring/content-fragments.md)。 您也可以[将现有内容片段资产从资产浏览器拖到页面](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)上（对于其他基于资产的组件，例如基础组件图像），从而使用现有内容片段资产。 现成的内容片段组件仅显示引用的内容片段的一个[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。 使用组件对话框，您可以定义要在页面上显示的[元素、变体和片段段落范围](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

>[!NOTE]
>
>此内容片段组件作为Article组件的增强版本引入到AEM 6.2中，该组件已弃用。

>[!NOTE]
>
>经典UI中不支持内容片段。

### 定义 {#definition}

**内容片段**&#x200B;组件用于保留对内容片段资源（有效地增强了文本资源）的引用。 内容片段的资源类型为：

`dam/cfm/components/contentfragment/contentfragment`

引用在属性中定义：

`fileReference`

只有触屏UI的编辑器完全支持内容片段组件，其中包括客户端库：

`cq.authoring.editor.plugin.cfm`

此库会向编辑器添加特定于内容片段的功能。 例如，支持在页面上添加和配置内容片段，支持在资产浏览器中搜索内容片段资产，以及在侧面板中搜索关联内容。

### 中间内容 {#in-between-content}

**内容片段** t组件允许您在显示的[元素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)的不同段落之间放置其他组件。 基本上，显示的元素由不同的段落组成（每个段落都标有一个回车符）。 在每个段落之间，您可以使用其他组件插入内容。

从技术角度来看，所显示元素的每个段落都位于其自身的parsys中，您在段落之间添加的每个组件都（在标题下）插入parsys中。

换句话说，如果内容片段组件的实例由三个段落组成，则组件在存储库中有三个不同的parsys。 添加到内容片段的所有中间内容实际上都位于这些parsys中。

在存储库中，中间内容是相对于其在整个段落结构中的位置存储的，也就是说，它未附加到实际的段落内容。

为了说明这一点，请考虑以下几点：

* 由三个段落组成的内容片段的实例
* 第二段之后已经插入了一些内容

   * 这意味着内容存储在第二个parsys中。

基本上，如果此实例的段落结构发生更改（通过更改显示的变体、元素或段落范围），它可能会影响在内容片段内容时显示的中间内容：

* 编辑，并在第二段之前添加另一段：

   * 中间内容在新创建的段落之后显示（第二个parsys现在保存新创建的段落）。

* 将编辑并删除第二段：

   * 中间内容显示在之前是第三段的段落之后（第二个parsys现在包含前三个段落）。

* 进行了配置，以便仅显示第一段：

   * 不显示中间内容（由于新配置，第二个Parsys不再呈现）。

### 自定义内容片段组件 {#customizing-the-content-fragment-component}

要使用现成的内容片段组件作为扩展的Blueprint，您应遵守以下合同：

* 重用HTL渲染脚本及其关联的POJO，以便查看中间内容功能的实施方式。
* 重用内容片段节点： `cq:editConfig`

   * `afterinsert`/`afteredit`/`afterdelete`侦听器用于触发JS事件。 这些事件在`cq.authoring.editor.plugin.cfm`客户端库中进行处理，以便在侧面板中显示关联的内容。
   * `cq:dropTargets`配置为支持拖动内容片段资产。
   * `cq:inplaceEditing`配置为支持在页面编辑器中创作内容片段。 片段就地编辑器在`cq.authoring.editor.plugin.cfm`客户端库中定义，允许快速链接在[片段编辑器](/help/assets/content-fragments/content-fragments-variations.md)中打开当前[元素/变体](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)。

### 呈现前资源重写 {#asset-rewriting-before-rendering}

内容片段管理使用内部渲染过程为页面生成最终HTML输出。 这由内容片段组件内部使用，也由在引用页面上更新引用片段的后台进程使用。

在内部，Sling重写器用于该渲染。 在`/libs/dam/config/rewriter/cfm`处找到相应的配置，如有必要，可以调整配置。 有关详细信息，请参阅[Apache Sling重写器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)。

>[!CAUTION]
>
>如果您确实要调整/叠加重写器的配置：
>
>* `/libs/dam/config/rewriter/cfm`
>
>然后`serializerType` **必须**&#x200B;更新为：
>
>* `serializerType="html5-serializer"`

现成的配置使用以下转换器：

* `transformer-cfm-payloadfilter` — 仅用于检索片段HTML的`body`部分(`<body>...</body>`)

* `transformer-cfm-parfilter` — 如果指定了段落范围，则过滤掉不需要的段落（对内容片段组件可以这样做）
* `transformer-cfm-assetprocessor` — 在内部用于检索嵌入到片段中的资源列表

呈现过程通过[`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html)公开，如有必要，自定义组件可以使用（例如）。
