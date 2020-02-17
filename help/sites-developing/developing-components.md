---
title: 开发AEM组件
seo-title: 开发AEM组件
description: AEM组件用于保存、格式化和呈现网页上提供的内容。
seo-description: AEM组件用于保存、格式化和呈现网页上提供的内容。
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 开发AEM组件{#developing-aem-components}

AEM组件用于保存、格式化和呈现网页上提供的内容。

* 创作 [页面时](/help/sites-authoring/default-components.md)，组件允许作者编辑和配置内容。

   * 在构建 [Commerce](/help/sites-administering/ecommerce.md) Site时，组件可以从目录中收集和渲染信息。
See [Developing eCommerce](/help/sites-developing/ecommerce.md) for more information.

   * 在构建 [Communities站点时](/help/communities/author-communities.md) ，组件可以向访客提供信息并从访客那里收集信息。
See [Developing Communities](/help/communities/communities.md) for more information.

* 在发布实例中，组件会呈现您的内容，并根据您的要求向网站访问者展示它。

>[!NOTE]
>
>本页是文档 [AEM组件——基础知识的继续](/help/sites-developing/components-basics.md)。

>[!CAUTION]
>
>以下组 `/libs/cq/gui/components/authoring/dialog` 件仅用于编辑器（“创作”中的组件对话框）。 如果在其他位置使用它们（例如，在向导对话框中），它们的行为可能不如预期。

## 代码样本 {#code-samples}

此页提供为AEM开发新组件所需的参考文档（或指向参考文档的链接）。 有关 [一些实用示例，请参阅开发AEM组件](/help/sites-developing/developing-components-samples.md) -代码示例。

## 结构 {#structure}

AEM组件——基础知识页面中介绍了组 [件的基本结构](/help/sites-developing/components-basics.md#structure)。 该文档同时涵盖触屏优化UI和经典UI。 即使您不需要在新组件中使用经典设置，也可以在继承现有组件时了解这些设置。

## 扩展现有组件和对话框 {#extending-existing-components-and-dialogs}

根据要实现的组件，可能可以扩展或自定义现有实例，而不是从头开始定义和开发整个 [结构](#structure) 。

在扩展或自定义现有组件或对话框时，您可以复制或复制对话框所需的整个结构或结构，然后再进行更改。

### 扩展现有组件 {#extending-an-existing-component}

可以使用资源类型层次结构和相关的继 [承机制来扩展现有组件](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) 。

>[!NOTE]
>
>还可以使用基于搜索路径逻辑的叠加来重新定义组件。 但是，在这种情况下， [Sling Resource Mergare](/help/sites-developing/sling-resource-merger.md) （Sling资源合并）将不会触发，并 `/apps` 且必须定义整个叠加。

>[!NOTE]
>
>内容 [片段组件也可以自定义和扩展](/help/sites-developing/customizing-content-fragments.md) ，但必须考虑完整的结构以及与资产的关系。

### 自定义现有组件对话框 {#customizing-a-existing-component-dialog}

还可以使用Sling资源合并 *和定义属性* ，覆 [盖组件对话框](/help/sites-developing/sling-resource-merger.md)`sling:resourceSuperType`。

这意味着您只需重新定义所需的差异，而不是重新定义整个对话框(使用 `sling:resourceSuperType`)。 现在建议使用此方法来扩展组件对话框

有关更多 [详细信息，请参阅Sling Resource Mergare](/help/sites-developing/sling-resource-merger.md) 。

## 定义标记 {#defining-the-markup}

组件将使用 [HTML呈现](https://www.w3schools.com/htmL/html_intro.asp)。 您的组件需要定义需要的HTML，以获取所需的内容，然后根据需要在创作和发布环境中呈现它。

### 使用HTML模板语言 {#using-the-html-template-language}

The [HTML Templating Language (HTL)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), introduced with AEM 6.0, takes the place of JSP (JavaServer Pages) as the preferred and recommended server-side template system for HTML. 对于需要构建强大企业网站的Web开发人员，HTL有助于提高安全性和开发效率。

>[!NOTE]
>
>尽管HTL和JSP都可用于开发组件，但我们将在本页中用HTL说明开发，因为它是AEM的推荐脚本语言。

## 开发内容逻辑 {#developing-the-content-logic}

此可选逻辑选择和／或计算要呈现的内容。 它从具有相应Use-API模式的HTL表达式中调用。

将逻辑与外观分开的机制有助于阐明对给定视图所调用的内容。 它还允许同一资源的不同视图有不同的逻辑。

### 使用Java {#using-java}

[HTL Java Use-API使HTL文件能够访问自定义Java类中的帮助程序方法](https://helpx.adobe.com/experience-manager/htl/using/use-api-java.html)。 这允许您使用Java代码实现用于选择和配置组件内容的逻辑。

### 使用JavaScript {#using-javascript}

[HTL javaScript Use-API使HTL文件能够访问使用JavaScript编写的辅助代码](https://helpx.adobe.com/experience-manager/htl/using/use-api-javascript.html)。 这允许您使用JavaScript代码实现用于选择和配置组件内容的逻辑。

### 使用客户端HTML库 {#using-client-side-html-libraries}

现代网站严重依赖由复杂的JavaScript和CSS代码驱动的客户端处理。 组织和优化此代码的服务可能是一个复杂的问题。

为了帮助解决此问题，AEM提供了客户端库文件夹 ****，允许您在存储库中存储客户端代码，将其组织到类别中，并定义何时以及如何向客户端提供每类代码。 然后，客户端库系统负责在最终网页中生成正确的链接以加载正确的代码。

阅 [读使用客户端HTML库](/help/sites-developing/clientlibs.md) ，了解更多信息。

## 配置编辑行为 {#configuring-the-edit-behavior}

您可以配置组件的编辑行为，包括组件可用的操作、就地编辑器的特性以及与组件上的事件相关的监听器等属性。 该配置对于触屏优化UI和经典UI都是通用的，尽管具有某些特定差异。

通过 [在组件节点（类型）下添加类型的节点](/help/sites-developing/components-basics.md#edit-behavior) ，并通过添加特定属性和子节点来配置 `cq:editConfig``cq:EditConfig``cq:Component`组件的编辑行为。

## 配置预览行为 {#configuring-the-preview-behavior}

切换 [到“预览](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) ”模式时将设置 **** WCM模式Cookie，即使页面未刷新也是如此。

对于渲染对WCM模式敏感的组件，需要定义这些组件以具体刷新它们，然后依赖cookie的值。

>[!NOTE]
>
>在触屏优化UI中，只有值和 `EDIT` 用 `PREVIEW` 于 [WCM模式Cookie](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/WCMMode.html) 。

## 创建和配置对话框 {#creating-and-configuring-a-dialog}

对话框用于允许作者与组件进行交互。 使用对话框允许作者和／或管理员编辑内容、配置组件或定义设计参数(使用“设 [计”对话框](#creating-and-configuring-a-design-dialog))

### Coral UI和Granite UI {#coral-ui-and-granite-ui}

[Coral UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) 和 [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 定义了AEM的现代外观。

[Granite UI提供了在创作环境中创建对话框所需的大量基本组件（构件）](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 。 必要时，您可以扩展此选择并 [创建自己的构件](#creatinganewwidget)。

有关使用Coral和Granite资源类型开发组件的详细信息，请参阅：使 [用Coral/Granite资源类型构建Experience manager组件](https://helpx.adobe.com/experience-manager/using/aem64_coral_resourcetypes.html)。

有关完整详细信息，请参阅：

* Coral UI

   * 在所有云解决方案中提供一致的UI
   * [AEM触屏优化UI的概念- Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Coral UI 指南](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html)

* Granite UI

   * 提供打包到Sling组件中的Coral UI标记，用于构建UI控制台和对话框
   * [AEM触屏优化UI的概念- Granite UI](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>[!NOTE]
>
>由于Granite UI组件的性质（以及与ExtJS构件的不同），组件与触屏优化UI和经典UI的交互方式存在一 [些差异](/help/sites-developing/developing-components-classic.md)。

### 创建新对话框 {#creating-a-new-dialog}

触屏优化UI的对话框：

* 名称 `cq:dialog`。
* 定义为具有 `nt:unstructured` 属性集的 `sling:resourceType` 节点。

* 位于其节点 `cq:Component` 下，并位于其组件定义旁。
* 基于其内容结构和属性在服务器端呈现（作为Sling组件） `sling:resourceType` 。
* 使用Granite UI框架。
* 包含描述对话框中字段的节点结构。

   * 这些节点 `nt:unstructured` 具有所需的属 `sling:resourceType` 性。

示例节点结构可能是：

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

自定义对话框与开发组件类似，因为对话框本身是组件（即组件脚本呈现的标记以及客户端库提供的行为／样式）。

有关示例，请参阅：

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>如果组件没有为触屏优化UI定义对话框，则经典UI对话框将用作兼容性层内的回退。 要自定义此类对话框，您需要自定义经典UI对话框。 请参 [阅经典UI的AEM组件](/help/sites-developing/developing-components-classic.md)。

### 自定义对话框字段 {#customizing-dialog-fields}

>[!NOTE]
>
>请参阅：
>
>* “自定义对话框字段”上 [的AEM Gems会话](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。
>* 代码示例——如何自定义 [对话框字段中介绍的相关示例代码](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)。
>



#### 创建新字段 {#creating-a-new-field}

触屏优化UI的构件作为Granite UI组件实现。

要创建在触屏优化UI的组件对话框中使用的新构件，您需 [要创建新的Granite UI字段组件](/help/sites-developing/granite-ui-component.md)。

>[!NOTE]
>
>有关Granite UI的完整详细信息，请参阅 [Granite UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。

如果您将对话框视为表单元素的简单容器，那么您还可以将对话框内容的主要内容显示为表单字段。 创建新表单字段需要您创建资源类型；这等同于创建新组件。 为了帮助您完成该任务，Granite UI提供了一个要继承的通用字段组件(使用 `sling:resourceSuperType`):

`/libs/granite/ui/components/coral/foundation/form/field`

更具体地说，Granite UI提供了一系列适用于对话框（或更一般地，以表单形式）的字段 [组件](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)。

>[!NOTE]
>
>这与经典UI不同，在经典UI中，构件由节点表示，每个节点都具有特定的 `cq:Widgets` 节点，以便 `xtype` 与其相应的ExtJS构件建立关系。 从实施角度看，这些构件是由ExtJS框架在客户端呈现的。

创建资源类型后，可以通过在对话框中添加新节点来实例化字段，该节点的属性引用您刚 `sling:resourceType` 刚引入的资源类型。

#### 为样式和行为创建客户端库 {#creating-a-client-library-for-style-and-behavior}

如果要为组件定义样式和行为，可创建专用客户端库 [以定义自定义](/help/sites-developing/clientlibs.md) CSS/LESS和JS。

要仅为组件对话框加载客户端库（即不会为其他组件加载），您需要将对话框的属性 `extraClientlibs`** **设置为刚刚创建的客户端库的类别名称。 如果客户端库很大，且／或您的字段特定于该对话框并且在其他对话框中不需要，则建议这样做。

要为所有对话框加载客户端库，请将客户端库的category属性设置为 `cq.authoring.dialog`。 这是显示所有对话框时默认包含的客户端库的类别名称。 如果客户端库很小，且／或字段是通用的，并且可能会在其他对话框中重复使用，您就希望这样做。

有关示例，请参阅：

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * 由代码示 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 扩展（继承自）字段 {#extending-inheriting-from-a-field}

根据您的要求，您可以：

* 通过组件继承( `sling:resourceSuperType`)扩展给定的Granite UI字段
* 通过遵循构件库API（JS/CSS继承），从基础构件库中扩展给定构件（对于Granite UI，这是Coral UI）

#### 访问对话框字段 {#access-to-dialog-fields}

您还可以使用渲染条件( `rendercondition`)来控制谁有权访问对话框中的特定选项卡／字段；例如：

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### 处理字段事件 {#handling-field-events}

现在，处理对话框字段上的事件的方法已在自定义客 [户端库中的监听器中完成](#listeners-in-a-custom-client-library)。 这与在内容结构中设置监听器的 [旧方法相比有所改变](#listenersinthecontentstructureclassicui)。

#### 自定义客户端库中的监听器 {#listeners-in-a-custom-client-library}

要将逻辑注入您的领域，您应：

1. 使用给定的CSS类（挂接）标记您 *的字段*。
1. 在客户端库中定义一个挂钩该CSS类名的JS监听器（这可确保您的自定义逻辑仅作用于您的字段，并且不会影响同一类型的其他字段）。

要实现此目的，您需要了解要与之交互的底层构件库。 请参阅 [Coral UI文档](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/coral-ui/coralui3/index.html) ，以确定要对哪个事件做出反应。 这与您过去使用ExtJS必须执行的过程非常相似：查找给定构件的文档页面，然后检查其事件API的详细信息。

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * 由代码示 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### 内容结构中的监听器 {#listeners-in-the-content-structure}

在具有ExtJS的经典UI中，通常在内容结构中具有给定构件的监听器。 在触屏优化UI中实现相同的功能是不同的，因为JS监听器代码（或任何代码）在内容中都不再定义。

内容结构描述了语义结构；它不应（必须）暗示基础构件的性质。 如果内容结构中没有JS代码，则无需更改内容结构即可更改实施详细信息。 换句话说，您无需触摸内容结构即可更改构件库。

### 字段验证 {#field-validation}

#### 必填字段 {#mandatory-field}

要将给定字段标记为必填字段，请在字段的内容节点上设置以下属性：

* 名称: `required`
* 类型: `Boolean`

有关示例，请参阅：

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### 字段验证(Granite UI) {#field-validation-granite-ui}

Granite UI和Granite UI组件（等效于构件）中的字段验证是使用 `foundation-validation` API完成的。 [有关详细信息，请 `foundation-valdiation` 参阅Granite文档。](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

有关示例，请参阅：

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * 由代码示 [例提供](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## 创建和配置设计对话框 {#creating-and-configuring-a-design-dialog}

当组件具有可在设计模式下编辑的设计详细信息时，将提供“设 [计”对话框](/help/sites-authoring/default-components-designmode.md)。

该定义与用于编辑内容的对 [话框的定义非常相似](#creating-a-new-dialog)，区别在于它被定义为节点：

* Node name: `cq:design_dialog`
* 类型: `nt:unstructured`

## 创建和配置就地编辑器 {#creating-and-configuring-an-inplace-editor}

就地编辑器允许用户直接在段落流中编辑内容，无需打开对话框。 例如，标准文本组件和标题组件都有一个就地编辑器。

对于每个组件类型，就地编辑器并非必需／有意义的。

有关详 [细信息，请参阅扩展页面创作——添加新的就地编辑器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) 。

## 自定义组件工具栏 {#customizing-the-component-toolbar}

组 [件工具栏](/help/sites-developing/touch-ui-structure.md#component-toolbar) ，让用户能够访问组件的一系列操作，如编辑、配置、复制和删除。

有关详 [细信息，请参阅扩展页面创作——向组件工具栏添加新操作](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) 。

## 为引用边栏配置组件（借入／借出） {#configuring-a-component-for-the-references-rail-borrowed-lent}

如果新组件引用了来自其他页面的内容，则您可以考虑是否希望它影响引用边栏的“借 **阅内容** ”和“借阅内容 ****[****](/help/sites-authoring/basic-handling.md#references)”部分。

现成的AEM只检查引用组件。 要添加组件，您需要配置OSGi捆绑 **WCM创作内容引用配置**。

在定义中创建一个新条目，指定您的组件以及要检查的属性。 例如：

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services. See [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

## 启用组件并将其添加到段落系统 {#enabling-and-adding-your-component-to-the-paragraph-system}

开发组件后，需要启用该组件以在相应的段落系统中使用，以便在所需的页面上使用它。

这可以通过以下任一方式实现：

* 编辑 [特定页面时](/help/sites-authoring/default-components-designmode.md) ，使用“设计”模式。
* [在模 `components` 板的段落系统中定义属性](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system)。

## Configuring a Paragraph System so that Dragging an Asset Creates a Component Instance {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM提供了在页面上配置段落系统的可能性，当用户将（适当）资产拖动到该页面的实例上时 [](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) （而不是始终需要将空组件拖动到页面上），将自动创建新组件的实例。

可以配置此行为以及所需的资产与组件关系：

1. 根据页面设计的段落定义。 例如：

   * `/etc/designs/<myApp>/page/par`
   创建新节点：

   * 名称: `cq:authoring`
   * 类型: `nt:unstructured`


1. 在此下，创建一个新节点以保存所有资产到组件映射：

   * 名称: `assetToComponentMapping`
   * 类型: `nt:unstructured`

1. 对于每个资产到组件映射，请创建一个节点：

   * 名称：文本；建议名称指示资产和相关组件类型；例如，图像
   * 类型: `nt:unstructured`
   每个组件都具有以下属性：

   * `assetGroup`:

      * 类型: `String`
      * 值：相关资产所属的组；例如， `media`
   * `assetMimetype`:

      * 类型: `String`
      * 值：相关资产的mime类型；示例 `image/*`
   * `droptarget`:

      * 类型: `String`
      * 值：落靶；例如， `image`
   * `resourceType`:

      * 类型: `String`
      * 值：相关组件资源；例如， `foundation/components/image`
   * `type`:

      * 类型: `String`
      * 值：例如， `Images`






有关示例，请参阅：

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-project-archetype项目](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/archive/master.zip)

>[!NOTE]
>
>现在，使用核心组件和可编辑模板时，可以在UI中轻松配置组 [件实例的自](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) 动创建。 有关定 [义与给定媒体类型自动关联的组件的详细信息](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) ，请参阅创建页面模板。

## 使用AEM Brackets扩展 {#using-the-aem-brackets-extension}

AEM Brackets扩 [展提供了一个平滑的工作流](/help/sites-developing/aem-brackets.md) ，用于编辑AEM组件和客户端库。 它基于 [Brackets代码编](https://brackets.io/) 辑器。

扩展：

* 简化同步（无需Maven或File Vault），以帮助提高开发人员效率，并帮助AEM知识有限的前端开发人员参与项目。
* 提供一 [些HTL支持](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) ，这是专为简化组件开发和提高安全性而设计的模板语言。

>[!NOTE]
>
>建议使用Brackets创建组件。 它取代了为经典UI设计的CRXDE Lite —— 创建组件功能。

## 从经典组件迁移 {#migrating-from-a-classic-component}

将设计用于经典UI的组件迁移到可与触屏优化UI一起使用的组件（单独或联合使用）时，应考虑以下问题：

* HTL

   * 使用 [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) 不是强制性的，但如果您的组件需要更新，那么现在是考虑从JSP迁移到HTL [的理想时机](/help/sites-developing/components-basics.md#htl-vs-jsp)。

* 组件

   * 迁移 [ 使用经 `cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code) 典UI特定功能的代码
   * RTE插件，有关详细信息，请 [参阅配置富文本编辑器](/help/sites-administering/rich-text-editor.md)。
   * [迁移 `cq:listener` 使用](#migrating-cq-listener-code) 经典UI特定函数的代码

* 对话框

   * 您需要创建一个新对话框以在触屏优化UI中使用。 但是，出于兼容性考虑，当未为触屏优化UI定义对话框时，触屏优化UI可以使用经典UI对话框的定义。
   * 提供 [了对话框转换工具](/help/sites-developing/dialog-conversion.md) ，以帮助您扩展现有组件。
   * [将ExtJS映射到Granite UI组件](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) ，可方便地概述ExtJS xtypes和节点类型及其等效的Granite UI资源类型。
   * 自定义字段，有关详细信息，请参阅自定义对话框字段上的AEM Gems [会话](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。
   * 从类型迁移到 [Granite UI验证](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * 使用JS监听器，有关详细信息，请参 [阅处理字段事件](#handling-field-events) ，以及自定义对话框字段的AEM Gems [会话](https://docs.adobe.com/content/ddc/en/gems/customizing-dialog-fields-in-touch-ui.html)。

### 迁移cq：监听器代码 {#migrating-cq-listener-code}

如果迁移的项目是为经典UI设计的，则代码（和与组件相关的客户端库）可能使用特定于经典UI的函数(如 `cq:listener``CQ.wcm.*`)。 对于迁移，必须使用触屏优化UI中的等效对象／函数更新此类代码。

如果您的项目已完全迁移到触屏优化UI，您需要替换此类代码以使用与触屏优化UI相关的对象和功能。

但是，如果您的项目在迁移期间（通常情况）必须同时满足经典UI和触屏优化UI的需求，则您需要实现一个切换以区分引用相应对象的单独代码。

此切换机制可实现为：

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## 对组件进行文档化 {#documenting-your-component}

作为开发人员，您希望轻松访问组件文档，以便快速了解：

* 描述
* 预期用途
* 内容结构和属性
* 暴露的API和扩展点
* 等等

因此，很容易将您在组件本身中拥有的任何现有文档标记公开。

您只需在组件结构中 `README.md` 放置一个文件。 此标记随后将显示在组件控 [制台中](/help/sites-authoring/default-components-console.md)。

![chlimage_1-7](assets/chlimage_1-7.png)

支持的标记与内容片段的标 [记相同](/help/assets/content-fragments-markdown.md)。
