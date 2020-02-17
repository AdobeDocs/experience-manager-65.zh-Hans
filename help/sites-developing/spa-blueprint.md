---
title: SPA Blueprint
seo-title: SPA Blueprint
description: 本文档描述了任何SPA框架在AEM中实施可编辑的SPA组件时应履行的与框架无关的一般合同。
seo-description: 本文档描述了任何SPA框架在AEM中实施可编辑的SPA组件时应履行的与框架无关的一般合同。
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# SPA Blueprint{#spa-blueprint}

要使作者能够使用AEM SPA编辑器编辑SPA的内容，SPA必须满足以下要求，本文档将对这些要求进行说明。

>[!NOTE]
>
>对于需要基于SPA框架的客户端渲染（例如“反应”或“角度”）的项目，建议使用SPA编辑器解决方案。

## 简介 {#introduction}

本文档描述任何SPA框架在AEM中实施可编辑的SPA组件时应履行的一般合同（即AEM支持层的类型）。

>[!NOTE]
>
>以下要求与框架无关。 如果满足这些要求，则可以提供由模块、组件和服务组成的框架特定层。
>
>**AEM中的React和Angular框架已满足这些要求。** 仅当您希望实施其他框架以与AEM一起使用时，此蓝图中的要求才相关。

>[!CAUTION]
>
>尽管AEM的SPA功能与框架无关，但目前仅支持React和Angular框架。

要使作者能够使用AEM页面编辑器编辑单页应用程序框架公开的数据，项目必须能够解释表示为AEM存储库中某个应用程序存储的数据的语义的模型结构。 为实现这一目标，提供了两个与框架无关的库：和 `PageModelManager` 那个 `ComponentMapping`。

### PageModelManager {#pagemodelmanager}

库 `PageModelManager` 作为NPM包提供，供SPA项目使用。 它随SPA提供，并充当数据模型管理器。

它代表SPA抽象了表示实际内容结构的JSON结构的检索和管理。 它还负责与SPA同步，以告知其何时必须重新渲染其组件。

查看NPM包 [@adobe/cq-spa-page-model-manager](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)

初始化应 `PageModelManager`用程序时，库首先加载提供的应用程序根模型（通过参数、元属性或当前URL）。 如果库确定当前页面的模型不是其获取的根模型的一部分，并将其作为子页面的模型包含在其中。

![page_model_consolidation](assets/page_model_consolidation.png)

### 组件映射 {#componentmapping}

该 `ComponentMapping` 模块作为NPM包提供给前端项目。 它存储前端组件，并为SPA提供了一种将前端组件映射到AEM资源类型的方法。 这样，在解析应用程序的JSON模型时，组件就可以动态解析。

模型中存在的每个项目都包含一个 `:type` 公开AEM资源类型的字段。 装载后，前端组件可以使用从基础库接收的模型片段来呈现自己。

#### 动态模型到组件映射 {#dynamic-model-to-component-mapping}

有关在AEM的Javascript SPA SDK中如何进行动态模型到组件映射的详细信息，请参阅SPA的 [动态模型到组件映射文章](/help/sites-developing/spa-dynamic-model-to-component-mapping.md)。

### 框架特定层 {#framework-specific-layer}

每个前端框架必须实现第三层。 第三个库负责与底层库进行交互，并提供一系列集成良好且易于使用的入口点以与数据模型交互。

本文件的其余部分描述了这一中间框架特定层的要求，并希望与框架无关。 通过遵守以下要求，可以为项目组件提供一个框架特定层以与负责管理数据模型的底层库交互。

## 一般概念 {#general-concepts}

### 页面模型 {#page-model}

页面的内容结构存储在AEM中。 页面模型用于映射和实例化SPA组件。 SPA开发人员创建映射到AEM组件的SPA组件。 为此，他们使用资源类型（或AEM组件的路径）作为唯一键。

SPA组件必须与页面模型同步，并相应地更新以更改其内容。 必须使用利用动态组件的模式来根据提供的页面模型结构动态实例化组件。

### 元字段 {#meta-fields}

页面模型利用JSON模型导出器，它本身基于 [Sling Model](https://sling.apache.org/documentation/bundles/models.html) API。 可导出的吊索模型显示以下字段列表，以便使底层库能解释数据模型：

* `:type`:AEM资源的类型（默认为资源类型）
* `:children`:当前资源的分层子项。 子项不是当前资源的内部内容的一部分（可以在表示页面的项目上找到）
* `:hierarchyType`:资源的分层类型。 当前 `PageModelManager` 支持页面类型

* `:items`:当前资源的子内容资源（嵌套结构，仅在容器中显示）
* `:itemsOrder`:子项的有序列表。 JSON映射对象不保证其字段的顺序。 通过使地图和当前阵列同时具有，API的用户具有这两种结构的优点
* `:path`:项目的内容路径（在表示页面的项目上显示）

另请参 [阅AEM Content services入门。](https://helpx.adobe.com/experience-manager/kt/sites/using/content-services-tutorial-use.html)

### 框架特定模块 {#framework-specific-module}

分离关注有助于促进项目实施。 因此，应提供特定于NPM的包。 此包负责聚合和公开基本模块、服务和组件。 这些组件必须封装数据模型管理逻辑并提供对项目组件期望的数据的访问。 该模块还负责过渡地暴露底层库的有用入口点。

为了促进库的互操作性，Adobe建议特定于框架的模块捆绑以下库。 如有必要，该层可以封装和调整底层API，然后将它们暴露到项目中。

* [@adobe/cq-spa-page-model-manager](https://www.npmjs.com/package/@adobe/cq-spa-page-model-manager)
* [@adobe/cq-spa-component-mapping](https://www.npmjs.com/package/@adobe/cq-spa-component-mapping)

#### 实施 {#implementations}

#### 反应 {#react}

npm模块： [@adobe/cq-react-editable-components](https://www.npmjs.com/package/@adobe/cq-react-editable-components)

#### 角度 {#angular}

npm模块：即将推出

## 主要服务和组件 {#main-services-and-components}

应按照每个框架的具体准则执行下列实体。 基于框架架构，实现方式可能差异很大，但必须提供描述的功能。

### 模型提供者 {#the-model-provider}

项目组件必须将模型片段的访问权限委派给模型提供者。 然后，模型提供者负责侦听对模型的指定片段所做的更改并将更新的模型返回到委托组件。

为此，模型提供者必须注册到 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`。 然后，当发生更改时，它接收并将更新的数据传递给委托组件。 根据惯例，将命名将携带模型片段的委托组件的可用属性 `cqModel`。 实施可免费向组件提供此属性，但应考虑到与框架架构的集成、可发现性和易用性等方面。

### 组件HTML修饰器 {#the-component-html-decorator}

组件修饰器负责使用页面编辑器所期望的一系列数据属性和类名称装饰每个组件实例的元素的外部HTML。

#### 组件声明 {#component-declaration}

以下元数据必须添加到项目组件生成的外部HTML元素中。 它们使页面编辑器能够检索相应的编辑配置。

* `data-cq-data-path`:相对于 `jcr:content`

#### 编辑功能声明和占位符 {#editing-capability-declaration-and-placeholder}

以下元数据和类名称必须添加到项目组件生成的外部HTML元素中。 它们使页面编辑器能够提供相关功能。

* `cq-placeholder`:用于标识空组件占位符的类名称
* `data-emptytext`:组件实例为空时叠加要显示的标签

**空组件占位符**

每个组件都必须扩展一个功能，当组件标识为空时，该功能将使用特定于占位符和相关叠加的数据属性和类名装饰外部HTML元素。

**论构件的虚性**

* 组件在逻辑上是空的吗？
* 当组件为空时，叠加应显示什么标签？

### 容器 {#container}

容器是用于包含和呈现子组件的组件。 为此，容器迭代其模 `:itemsOrder`型 `:items` 的 `:children` 属性和属性。

容器从库的存储中动态获取子组 ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` 件。 然后，容器使用“模型提供者”功能扩展子组件，最后将其实例化。

### 页面 {#page}

组 `Page` 件扩展组 `Container` 件。 容器是用于包含和呈现子组件（包括子页面）的组件。 为此，容器迭代其模 `:itemsOrder`型的 `:items`、 `:children` 和属性。 组 `Page` 件从ComponentMapping库的存储中动态获取子 [组件](/help/sites-developing/spa-blueprint.md#componentmapping) 。 负责 `Page` 实例化子组件。

### 响应式网格 {#responsive-grid}

响应式网格组件是一个容器。 它包含表示其列的模型提供者的特定变体。 响应式网格及其列负责用模型中包含的特定类名装饰项目组件的外部HTML元素。

响应式网格组件应预映射到其AEM对应组件，因为该组件复杂且很少进行自定义。

#### 特定模型字段 {#specific-model-fields}

* `gridClassNames:` 为响应式网格提供的类名
* `columnClassNames:` 为响应式列提供的类名

另请参阅npm资 [源@adobe/cq-react-editable-components#srccomponentsrespontedgridjsx](https://www.npmjs.com/package/@adobe/cq-react-editable-components#srccomponentsresponsivegridjsx)

#### 响应网格的占位符 {#placeholder-of-the-reponsive-grid}

SPA组件将映射到图形容器（如响应式网格），并且在创作内容时必须添加虚拟子占位符。 当页面编辑器创作SPA内容时，该内容会使用iframe嵌入到编辑器中，并且该属性会添加到该内容的 `data-cq-editor` 文档节点中。 当存 `data-cq-editor` 在属性时，容器必须包含HTMLElement，以表示将新组件插入页面时作者与之交互的区域。

例如：

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>该示例中使用的类名称当前为页面编辑器所必需。
>
>* `"new section"`:指示当前元素是容器的占位符
>* `"aem-Grid-newComponent"`:为布局创作标准化组件
>



#### Component Mapping {#component-mapping}

基础组 [件映射库及其功能](/help/sites-developing/spa-blueprint.md#componentmapping)`MapTo` 可被封装和扩展，以提供与当前组件类旁边提供的编辑配置相关的功能。

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

在上述实施中，项目组件在实际注册到组件映射存储之前以空虚功能进 [行扩展](/help/sites-developing/spa-blueprint.md#componentmapping) 。 这是通过封装和扩展库来 ` [ComponentMapping](/content.md#main-pars_header_906602219)` 引入对配置对象的支持来完 `EditConfig` 成的：

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## 与页面编辑器合同 {#contract-wtih-the-page-editor}

项目组件必须至少生成以下数据属性，以便编辑器能够与它们交互。

* `data-cq-data-path`:组件的相对路径， `PageModel` 如( `"root/responsivegrid/image"`)。 不应将此属性添加到页面。

总之，要让页面编辑器将项目组件解释为可编辑，项目组件必须遵守以下合同：

* 提供将前端组件实例关联到AEM资源的预期属性。
* 提供可创建空占位符的预期系列属性和类名称。
* 提供支持拖放资产的预期类名称。

### 典型HTML元素结构 {#typical-html-element-structure}

以下片段说明了页面内容结构的典型HTML表示形式。 以下是几个重要要点：

* 响应式网格元素具有前缀为 `aem-Grid--`
* 响应式列元素包含前缀为 `aem-GridColumn--`
* 响应式网格，也是父网格的列被封装，例如两个以前的前缀不出现在同一元素上
* 与可编辑资源对应的元素带有属 `data-cq-data-path` 性。 请参阅 [本文档的“与页面编辑器合同](#contract-wtih-the-page-editor) ”部分。

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## 导航和路由 {#navigation-and-routing}

应用程序拥有路由。 前端开发人员首先需要实现导航组件（映射到AEM导航组件）。 此组件将呈现要与一系列路由一起使用的URL链接，这些路由将显示或隐藏内容片段。

基础 [ 库及其模 `PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` [ModelRouter](/help/sites-developing/spa-routing.md)` 块（默认启用）负责预取和提供对与给定资源路径相关联的模型的访问。

两个实体与路由的概念有关，但 ` [ModelRouter](/help/sites-developing/spa-routing.md)` 只负责使加载的数据模型与当前应用状态 ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` 同步。

有关详细信息， [请参阅文章](/help/sites-developing/spa-routing.md) “SPA模型路由”。

## SPA实际操作情况 {#spa-in-action}

继续阅读AEM中的SPA快速入门文档，了解简单的SPA如何工作并亲自尝试 [SPA](/help/sites-developing/spa-getting-started-react.md)。

## 进一步阅读 {#further-reading}

有关AEM中SPA的详细信息，请参阅以下文档：

* [SPA创作概述](/help/sites-developing/spa-overview.md) ，了解AEM中SPA和通信模型的概述
* [AEM中的SPA快速入门](/help/sites-developing/spa-getting-started-react.md) ，了解简单SPA的指南及其工作方式
