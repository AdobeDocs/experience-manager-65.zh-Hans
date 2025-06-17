---
title: 为Adobe Experience Manager开发SPA
description: 本文介绍了在让前端开发人员为Adobe Experience Manager (AEM)开发SPA时应考虑的重要问题，并概述了AEM在AEM上部署开发的SPA时应牢记的有关SPA的架构。
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: c1429889-e2ed-4e2f-a45f-33f8a6a52745
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
source-git-commit: 1509ca884e2f9eb931fc7cd416801957459cc4a0
workflow-type: tm+mt
source-wordcount: '2018'
ht-degree: 5%

---


# 为 AEM 开发 SPA{#developing-spas-for-aem}

单页应用程序 (SPA) 可以为网站用户提供引人入胜的良好体验。开发人员希望能够使用SPA框架构建站点，而创作者则希望能够在Adobe Experience Manager (AEM)中顺畅地为使用此类框架构建的站点编辑内容。

本文介绍了在让前端开发人员为AEM开发SPA时应考虑的重要问题，并概述了AEM有关在AEM上部署SPA的架构。

{{ue-over-spa}}

## AEM的SPA开发原则 {#spa-development-principles-for-aem}

在 AEM 上开发单页应用程序时，假定前端开发人员在创建 SPA 时遵循标准最佳实践。作为前端开发人员，如果您遵循这些一般最佳实践和一些AEM特定原则，则您的SPA将可以使用[AEM及其内容创作功能](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)。

* **[可移植性](/help/sites-developing/spa-architecture.md#portability) -**&#x200B;与任何组件一样，组件应尽可能构建为可移植的。 应使用可移植且可重用的组件构建 SPA。
* **[AEM 推动站点结构](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)** – 前端开发人员创建组件并拥有其内部结构，但依赖 AEM 来定义站点的内容结构。
* **[动态呈现](/help/sites-developing/spa-architecture.md#dynamic-rendering)** – 所有呈现都应是动态的。
* **[动态路由](#dynamic-routing) -** SPA负责路由，AEM侦听该路由并根据其进行提取。 任何路由也应是动态的。

如果您在开发SPA时牢记这些原则，那么在启用所有受支持的AEM创作功能时，SPA将尽可能灵活且面向未来。

如果您不需要支持AEM创作功能，则可能需要考虑其他[SPA设计模型](/help/sites-developing/spa-architecture.md#spa-design-models)。

### 可移植性 {#portability}

与开发任何组件时一样，组件的设计应最大限度地提高可移植性。 应避免任何影响组件可移植性或重用的模式，以确保将来的兼容性、灵活性和可维护性。

生成的SPA应使用高度可移植和可重用的组件构建。

### AEM驱动器站点结构 {#aem-drives-site-structure}

前端开发人员必须自视为负责创建用于构建应用程序的SPA组件库。 前端开发人员对组件的内部结构具有完全控制权。 [但是，AEM始终拥有该站点的结构。](/help/sites-developing/spa-overview.md)

这意味着前端开发人员可以在组件的入口点之前或之后添加客户内容，并且还可以在组件内进行第三方调用。 例如，前端开发人员无法完全控制组件的嵌套方式。

### 动态渲染 {#dynamic-rendering}

SPA应仅依赖内容的动态渲染。 这是默认预期，AEM会获取并呈现内容结构的所有子项。

任何指向特定内容的显式渲染都被视为静态渲染，尽管受支持，但与AEM的内容创作功能不兼容。 这也不符合[可移植性](/help/sites-developing/spa-architecture.md#portability)的原则。

### 动态路由 {#dynamic-routing}

与渲染一样，所有路由也应是动态的。 在AEM中，[SPA应始终拥有路由](/help/sites-developing/spa-routing.md)，AEM会侦听该路由并根据其获取内容。

任何静态路由都违反了[可移植性原则](/help/sites-developing/spa-architecture.md#portability)，并由于与AEM的内容创作功能不兼容，而限制了作者。 例如，对于静态路由，如果内容作者想要更改路由或更改页面，则作者必须请求前端开发人员执行此操作。

## AEM 项目原型 {#aem-project-archetype}

任何 AEM 项目都应使用 [AEM 项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)，它支持使用 React 或 Angular 的 SPA 项目并利用 SPA SDK。

## SPA设计模型 {#spa-design-models}

如果遵循AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)中开发SPA的[原则，则您的SPA将可以使用所有受支持的AEM内容创作功能。

但是，在某些情况下，这并非完全必要。 下表概述了各种设计模型及其优点和缺点。

<table>
 <tbody>
  <tr>
   <th><strong>设计模型<br /> </strong></th>
   <th><strong>优点</strong></th>
   <th><strong>缺点</strong></th>
  </tr>
  <tr>
   <td>AEM用作headless CMS，而不使用<a href="/help/sites-developing/spa-reference-materials.md">SPA Editor SDK框架。</a></td>
   <td>前端开发人员可以完全控制应用程序。</td>
   <td><p>内容作者无法使用AEM的内容创作体验。</p> <p>如果代码包含静态引用或路由，则该代码不可移植或重用。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>前端开发人员使用SPA Editor SDK框架，但只向内容作者打开某些区域。</td>
   <td>开发人员通过仅在应用程序的受限区域中启用创作，来保持对应用程序的控制。</td>
   <td><p>内容作者仅限于AEM的一组有限内容创作体验。</p> <p>如果代码包含静态引用或路由，则代码存在不可移植或不可重用的风险。</p> <p>不允许使用模板编辑器，因此前端开发人员必须通过JCR维护可编辑的模板。</p> </td>
  </tr>
  <tr>
   <td>项目完全使用SPA Editor SDK，前端组件开发为库，应用程序的内容结构委派给AEM。</td>
   <td><p>该应用程序可重用和移植。</p> <p>内容作者可以使用AEM的内容创作体验编辑应用程序。<br /> </p> <p>SPA与模板编辑器兼容。</p> </td>
   <td><p>开发人员无法控制应用程序的结构和委派给AEM的内容部分。</p> <p>开发人员仍可以保留应用程序的区域，以便用于不应使用AEM创作的内容。</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>虽然AEM支持所有模型，但只有实施第三种(因此遵循AEM中推荐的[SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem))，内容作者才能在AEM中与已习惯的SPA内容交互并编辑其内容。

## 将现有SPA迁移到AEM {#migrating-existing-spas-to-aem}

通常，如果您的SPA遵循[适用于AEM的SPA开发原则](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)，则您的SPA将在AEM中工作并可使用AEM SPA编辑器进行编辑。

按照以下步骤操作，使现有SPA准备好与AEM配合使用。

1. **使JS组件模块化。**

   使它们能够按任何顺序、位置和大小呈现。
1. **使用Adobe SDK提供的容器将组件放在屏幕上。**

   AEM提供了一个页面和段落系统组件供您使用。
1. **为每个JS组件创建一个AEM组件。**

   AEM组件定义对话框和JSON输出。

## 面向前端开发人员的说明 {#instructions-for-front-end-developers}

让前端开发人员为AEM创建SPA的主要任务是就组件及其JSON模型达成一致。

下面概述了前端开发人员在为AEM开发SPA时需要执行的步骤。

1. **就组件及其JSON模型达成一致**

   前端开发人员和后端AEM开发人员需要就所需的组件和模型达成一致，以便从SPA组件到后端组件进行一对一匹配。

   仍需要AEM组件来提供“编辑”对话框和导出组件模型。

1. **在React组件中，通过`this.props.cqModel`**&#x200B;访问模型

   在同意组件且JSON模型就绪后，前端开发人员可以自由开发SPA，并且只需通过`this.props.cqModel`访问JSON模型即可。

1. **实施组件的`render()`方法**

   前端开发人员在他们认为合适的情况下实施`render()`方法，并且可以使用`cqModel`属性的字段。 这会输出插入到页面中的DOM和HTML片段。 这是在React中构建应用程序的标准方式。

1. **通过`MapTo()`**&#x200B;将组件映射到AEM资源类型

   映射存储组件类，并由提供的`Container`组件在内部使用，以根据给定的资源类型检索并动态实例化组件。

   这用作前端和后端之间的“粘合剂”，以便编辑器知道react组件对应于哪些组件。

   `Page`和`ResponsiveGrid`是扩展基`Container`的类的良好示例。

1. **将组件的`EditConfig`定义为参数`MapTo()`**

   只要尚未呈现或没有要呈现的内容，此参数是告诉编辑器应如何命名组件所必需的。

1. **为页面和容器扩展提供的`Container`类**

   页面和段落系统应该扩展此类，以便委派到内部组件的功能可按预期运行。

1. **使用HTML5 `History` API实施路由解决方案。**

   启用`ModelRouter`后，调用`pushState`和`replaceState`函数会触发向`PageModelManager`发出的获取缺少的模型片段的请求。

   `ModelRouter`的当前版本仅支持使用指向Sling模型入口点的实际资源路径的URL。 它不支持使用虚URL或别名。

   可以禁用`ModelRouter`或将其配置为忽略正则表达式列表。

## AEM不可知 {#aem-agnostic}

这些代码块说明了您的React和Angular组件如何不需要任何特定于Adobe或AEM的内容。

* JavaScript组件中的所有内容均与AEM无关。
* 但是，特定于AEM的是，必须使用MapTo帮助程序将JS组件映射到AEM组件。

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

`MapTo`帮助程序是允许后端和前端组件匹配在一起的“粘合剂”：

* 它告知JS容器（或JS段落系统）哪个JS组件负责渲染JSON中存在的每个组件。
* 它向JS组件渲染的HTML添加一个HTML数据属性，以便SPA编辑器知道在编辑组件时向作者显示哪个对话框。

有关使用`MapTo`和为常规AEM构建SPA的更多信息，请参阅所选框架的《快速入门指南》。

* [AEM中的SPA快速入门 — React](/help/sites-developing/spa-getting-started-react.md)
* [AEM - Angular中的SPA快速入门](/help/sites-developing/spa-getting-started-angular.md)

## AEM架构和SPA {#aem-architecture-and-spas}

使用SPA时，AEM的常规架构（包括开发、创作和发布环境）不会发生更改。 但是，了解SPA开发如何适应此架构很有帮助。

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **生成环境**

  这是签出SPA应用程序源和组件源的位置。

   * NPM clientlib生成器从SPA项目创建一个客户端库。
   * 该库由Maven获取，并由Maven Build插件与组件部署到AEM Author。

* **AEM作者**

  在AEM作者上创建内容，包括创作SPA。

  在创作环境中使用SPA编辑器编辑SPA时：

   1. SPA请求外部HTML。
   1. CSS已加载。
   1. 加载SPA应用程序的JavaScript。
   1. 执行SPA应用程序时，将请求JSON，以允许应用程序构建包含`cq-data`属性的页面的DOM。
   1. 此`cq-data`属性允许编辑器加载其他页面信息，以便它知道哪些编辑配置可用于组件。

* **AEM发布**

  在此处发布创作内容和编译的库（包括SPA应用程序工件、clientlibs和组件）以供公众使用。

* **Dispatcher / CDN**

  Dispatcher将用作网站访客的AEM的缓存层。

   * 处理请求的方式与在AEM创作实例中处理请求的方式类似，但不会请求页面信息，因为只有编辑器才需要这样做。
   * JavaScript、CSS、JSON和HTML已缓存，优化页面以实现快速交付。

>[!NOTE]
>
>在AEM内部，无需执行JavaScript构建机制或执行JavaScript本身。 AEM仅托管来自SPA应用程序的编译工件。

## 后续步骤 {#next-steps}

有关AEM中简单SPA的结构及其工作方式的概述，请参阅[React](/help/sites-developing/spa-getting-started-react.md)和[Angular](/help/sites-developing/spa-getting-started-angular.md)的快速入门指南。

有关创建您自己的SPA的分步指南，请参阅[AEM SPA编辑器快速入门 — WKND事件教程](https://helpx.adobe.com/cn/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)。

有关动态模型到组件映射及其在AEM中的SPA中的工作方式的更多详细信息，请参阅文章[SPA的动态模型到组件映射](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

如果您希望在AEM中为React或Angular以外的框架实施SPA，或者只是希望深入了解SPA SDK for AEM的工作方式，请参阅[SPA Blueprint](/help/sites-developing/spa-blueprint.md)文章。
