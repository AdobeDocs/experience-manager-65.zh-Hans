---
title: 在Adobe Experience Manager中编辑外部SPA
description: 本文档介绍了将独立SPA上传到Adobe Experience Manager实例、添加内容的可编辑部分以及启用创作的建议步骤。
exl-id: 25236af4-405a-4152-8308-34d983977e9a
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2391'
ht-degree: 0%

---

# 在Adobe Experience Manager中编辑外部SPA {#editing-external-spa-within-aem}

在决定外部SPA与Adobe Experience Manager (AEM)之间的集成级别时，您通常需要能够在AEM中编辑和查看SPA。

## 概述 {#overview}

本文档介绍了将独立SPA上传到AEM实例、添加内容的可编辑部分以及启用创作的建议步骤。

## 先决条件 {#prerequisites}

先决条件很简单。

* 确保AEM的实例正在本地运行。
* 使用[AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?#available-properties)创建基本AEM SPA项目。
   * 这构成了AEM项目的基础，该项目将进行更新以包含外部SPA。
   * 本文档中的示例使用[WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html#spa-editor)的起点。
* 准备好您想要集成的工作中的外部React SPA。

## 将SPA上传至AEM项目 {#upload-spa-to-aem-project}

首先，您需要将外部SPA上传到AEM项目。

1. 将`/ui.frontend`项目文件夹中的`src`替换为React应用程序的`src`文件夹。
1. 在`/ui.frontend/package.json`文件中包括应用`package.json`的任何其他依赖项。
   * 确保SPA SDK依赖项为[建议的版本](spa-getting-started-react.md#dependencies)。
1. 在`/public`文件夹中包括任何自定义项。
1. 包括在`/public/index.html`文件中添加的任何内联脚本或样式。

## 配置远程SPA {#configure-remote-spa}

现在，外部SPA是AEM项目的一部分，必须在AEM中对其进行配置。

### 包含AdobeSPA SDK包 {#include-spa-sdk-packages}

要利用AEM SPA功能，需要依赖以下三个软件包。

* [`@adobe/aem-react-editable-components`](https://github.com/adobe/aem-react-editable-components)
* [`@adobe/aem-spa-component-mapping`](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)
* [`@adobe/aem-spa-page-model-manager`](https://www.npmjs.com/package/@adobe/aem-spa-model-manager)

`@adobe/aem-spa-page-model-manager`提供用于初始化模型管理器以及从AEM实例检索模型的API。 然后，此模型可用于使用来自`@adobe/aem-react-editable-components`和`@adobe/aem-spa-component-mapping`的API呈现AEM组件。

#### 安装 {#installation}

运行以下npm命令以安装所需的包。

```shell
npm install --save @adobe/aem-spa-component-mapping @adobe/aem-spa-page-model-manager @adobe/aem-react-editable-components
```

### ModelManager初始化 {#model-manager-initialization}

在应用程序呈现之前，必须初始化[`ModelManager`](spa-blueprint.md#pagemodelmanager)以处理AEM `ModelStore`的创建。

这需要在应用程序的`src/index.js`文件中或在呈现应用程序根的位置完成。

为此，请使用`ModelManager`提供的`initializationAsync` API。

以下屏幕截图显示了如何在简单的React应用程序中启用`ModelManager`的初始化。 唯一的限制是必须在`ReactDOM.render()`之前调用`initializationAsync`。

![初始化ModelManager](assets/external-spa-initialize-modelmanager.png)

在此示例中，`ModelManager`已初始化，并创建了空的`ModelStore`。

`initializationAsync`可以选择接受`options`对象作为参数：

* `path` — 初始化时，将获取定义路径上的模型并将其存储在`ModelStore`中。 如果需要，这可用于在初始化时获取`rootModel`。
* `modelClient` — 允许提供负责提取模型的自定义客户端。
* `model` — 作为参数传递的`model`对象通常在使用[SSR.](spa-ssr.md)时填充

### AEM可授权的叶组件 {#authorable-leaf-components}

1. 创建/标识将为其创建可创作的React组件的AEM组件。 在此示例中，WKND项目使用文本组件。

   ![WKND文本组件](assets/external-spa-text-component.png)

1. 在SPA中创建简单的React文本组件。 在此示例中，已创建包含以下内容的新文件`Text.js`。

   ![Text.js](assets/external-spa-textjs.png)

1. 创建配置对象以指定启用AEM编辑所需的属性。

   ![创建配置对象](assets/external-spa-config-object.png)

   * 在AEM编辑器中打开时，`resourceType`是将React组件映射到AEM组件并启用编辑的必需项。

1. 使用包装函数`withMappable`。

   ![使用withMappable](assets/external-spa-withmappable.png)

   此包装函数将React组件映射到配置中指定的AEM `resourceType`，并在AEM编辑器中打开时启用编辑功能。 对于独立组件，它还会获取特定节点的模型内容。

   >[!NOTE]
   >
   >在此示例中，该组件有单独的版本：AEM封装和未封装的React组件。 显式使用组件时，需要使用包装的版本。 当组件成为页面的一部分时，您可以继续使用默认组件，就像当前在SPA编辑器中完成的那样。

1. 呈现组件中的内容。

   文本组件的JCR属性在AEM中如下所示。

   ![文本组件属性](assets/external-spa-text-properties.png)

   这些值将作为属性传递到新创建的`AEMText` React组件，并可用于呈现内容。

   ```javascript
   import React from 'react';
   import { withMappable } from '@adobe/aem-react-editable-components';
   
   export const TextEditConfig = {
       // Empty component placeholder label
       emptyLabel:'Text', 
       isEmpty:function(props) {
          return !props || !props.text || props.text.trim().length < 1;
       },
       // resourcetype of the AEM counterpart component
       resourceType:'wknd-spa-react/components/text'
   };
   
   const Text = ({ text }) => (<div>{text}</div>);
   
   export default Text;
   
   export const AEMText = withMappable(Text, TextEditConfig);
   ```

   这是完成AEM配置时组件的显示方式。

   ```javascript
   const Text = ({ cqPath, richText, text }) => {
      const richTextContent = () => (
         <div className="aem_text" id={cqPath.substr(cqPath.lastIndexOf('/') + 1)} data-rte-editelement dangerouslySetInnerHTML={{__html: text}}/>
      );
      return richText ? richTextContent() : (<div className="aem_text">{text}</div>);
   };
   ```

   >[!NOTE]
   >
   >在此示例中，已对渲染的组件进行了进一步的自定义以匹配现有的文本组件。 但是，这与AEM中的创作无关。

#### 将可创作组件添加到页面 {#add-authorable-component-to-page}

创建可创作的React组件后，即可在整个应用程序中使用它们。

让我们举一个示例页面，该页面需要添加WKND SPA项目中的文本。 对于此示例，您要显示文本“Hello World！” 在`/content/wknd-spa-react/us/en/home.html`。

1. 确定要显示的节点的路径。

   * `pagePath`：包含节点的页面，例如`/content/wknd-spa-react/us/en/home`
   * `itemPath`：页面中节点的路径，例如`root/responsivegrid/text`
      * 由页面上包含项目的名称组成。

   ![节点的路径](assets/external-spa-path.png)

1. 在页面的所需位置添加组件。

   ![将组件添加到页面](assets/external-spa-add-component.png)

   `AEMText`组件可以通过设置为属性的`pagePath`和`itemPath`值添加到页面的所需位置。 `pagePath`是必需属性。

#### 验证在AEM上编辑文本内容 {#verify-text-edit}

现在，在运行的AEM实例上测试该组件。

1. 从`aem-guides-wknd-spa`目录运行以下Maven命令以生成项目并将其部署到AEM。

```shell
mvn clean install -PautoInstallSinglePackage
```

1. 在您的AEM实例上，导航到`http://<host>:<port>/editor.html/content/wknd-spa-react/us/en/home.html`。

![在AEM中编辑SPA](assets/external-spa-edit-aem.png)

`AEMText`组件现在可在AEM上创作。

### AEM可创作页面 {#aem-authorable-pages}

1. 标识要在SPA中为创作添加的页面。 此示例使用`/content/wknd-spa-react/us/en/home.html`。
1. 为可创作页面组件创建文件（例如，`Page.js`）。 在这里，可以重复使用`@adobe/cq-react-editable-components`中提供的页面组件。
1. 在[AEM可创作叶组件](#authorable-leaf-components)部分中重复步骤4。 在组件上使用包装函数`withMappable`。
1. 与之前一样，将`MapTo`应用于页面中所有子组件的AEM资源类型。

   ```javascript
   import { Page, MapTo, withMappable } from '@adobe/aem-react-editable-components';
   import Text, { TextEditConfig } from './Text';
   
   export default withMappable(Page);
   
   MapTo('wknd-spa-react/components/text')(Text, TextEditConfig);
   ```

   >[!NOTE]
   >
   >在此示例中，使用的是未包装的React文本组件，而不是之前创建的已包装的`AEMText`。 这是因为当组件是页面/容器的一部分并且不是单独的一部分时，容器将负责递归映射组件并启用创作功能，并且每个子级不需要额外的包装器。

1. 要在SPA中添加可创作页面，请按照[将可创作组件添加到页面](#add-authorable-component-to-page)部分中的相同步骤操作。 但是，我们可以在此处跳过`itemPath`属性。

#### 验证AEM上的页面内容 {#verify-page-content}

要验证是否可以编辑页面，请按照[验证在AEM上编辑文本内容](#verify-text-edit)部分中的相同步骤操作。

![在AEM中编辑页面](assets/external-spa-edit-page.png)

该页面现在可以在具有布局容器和子文本组件的AEM上编辑。

### 虚拟叶组件 {#virtual-leaf-components}

在前面的示例中，我们使用现有AEM内容将组件添加到SPA。 但是，在某些情况下，内容尚未在AEM中创建，但需要内容作者稍后添加。 为了适应此要求，前端开发人员可以在SPA内的适当位置添加组件。 在AEM的编辑器中打开这些组件时，将显示占位符。 内容作者将内容添加到这些占位符中后，将在JCR结构中创建节点并保留内容。 创建的元件将允许与独立叶元件相同的一组操作。

在此示例中，我们重用了之前创建的`AEMText`组件。 我们希望在WKND主页上的现有文本组件下方添加新文本。 添加组分与添加普通叶组分相同。 但是，`itemPath`可以更新到需要添加新组件的路径。

由于新组件需要添加到`root/responsivegrid/text`处现有文本的下方，因此新路径将为`root/responsivegrid/{itemName}`。

```html
<AEMText
 pagePath='/content/wknd-spa-react/us/en/home'
 itemPath='root/responsivegrid/text_20' />
```

添加虚拟组件后，`TestPage`组件如下所示。

![正在测试虚拟组件](assets/external-spa-virtual-component.png)

>[!NOTE]
>
>确保配置中设置了`AEMText`组件的`resourceType`以启用此功能。

您现在可以按照[验证在AEM上编辑文本内容](#verify-text-edit)部分中的步骤将更改部署到AEM。 为当前不存在的`text_20`节点显示占位符。

![aem中的text_20节点](assets/external-spa-text20-aem.png)

当内容作者更新此组件时，将在`/content/wknd-spa-react/us/en/home`中的`root/responsivegrid/text_20`创建一个新的`text_20`节点。

![text20节点](assets/external-spa-text20-node.png)

#### 要求和限制 {#limitations}

添加虚拟叶组件有几项要求和一些限制。

* `pagePath`属性是创建虚拟组件的必需属性。
* 在`pagePath`中的路径中提供的页面节点必须存在于AEM项目中。
* 要创建的节点的名称必须在`itemPath`中提供。
* 可以在任何级别创建组件。
   * 如果在上一个示例中提供了`itemPath='text_20'`，则新节点将直接在页面`/content/wknd-spa-react/us/en/home/jcr:content/text_20`下创建
* 通过`itemPath`提供时，指向在其中创建新节点的节点的路径必须有效。
   * 在此示例中，`root/responsivegrid`必须存在，才能在其中创建新节点`text_20`。
* 仅支持创建叶组件。 未来版本将支持虚拟容器和页面。

### 虚拟容器 {#virtual-containers}

支持添加容器的功能，即使尚未在AEM中创建相应的容器。 概念和方法类似于[虚拟叶组件。](#virtual-leaf-components)

前端开发人员可以将容器组件添加到SPA内的适当位置，并且这些组件在AEM的编辑器中打开时将显示占位符。 然后，作者可以将组件及其内容添加到容器中，这将在JCR结构中创建所需的节点。

例如，如果`/root/responsivegrid`中已存在容器，并且开发人员想要添加新的子容器：

![容器位置](assets/container-location.png)

`newContainer`在AEM中尚不存在。

在AEM中编辑包含此组件的页面时，会显示容器的空占位符，作者可以在其中添加内容。

![容器占位符](assets/container-placeholder.png)

JCR](assets/container-jcr-structure.png)中的![容器位置

作者向容器添加子组件后，将使用JCR结构中的相应名称创建新容器节点。

包含内容的![容器](assets/container-with-content.png)

包含JCR](assets/container-with-content-jcr.png)内容的![容器

现在，可以根据作者的需要向容器中添加更多组件和内容，并且所做的更改将会保留。

#### 要求和限制 {#container-limitations}

添加虚拟容器有几项要求和一些限制。

* 用于确定可以添加哪些组件的策略将从父容器继承。
* 要创建的容器的直接父级必须已存在于AEM中。
   * 如果AEM容器中已存在容器`root/responsivegrid`，则通过提供路径`root/responsivegrid/newContainer`可创建新容器。
   * 但是`root/responsivegrid/newContainer/secondNewContainer`是不可能的。
* 一次只能虚拟创建一个新级别的组件。

## 其他自定义项 {#additional-customizations}

如果您按照前面的示例进行操作，则现在可以在AEM中编辑外部SPA。 但是，您可以进一步自定义外部SPA的其他方面。

### 根节点标识 {#root-node-id}

默认情况下，我们假定React应用程序在元素ID `spa-root`的`div`内呈现。 如有必要，可以自定义标记。

例如，假设我们有一个SPA，其中应用程序在元素ID `root`的`div`中呈现。 这需要在三个文件中反映出来。

1. 在React应用程序的`index.js`中（或调用`ReactDOM.render()`的位置）

   index.js文件](assets/external-spa-root-index.png)中的![ReactDOM.render()

1. 在React应用程序的`index.html`

   ![应用程序的index.html](assets/external-spa-index.png)

1. 在AEM应用程序的页面组件正文中，执行以下两个步骤：

   1. 为页面组件创建`body.html`。

   ![创建body.html文件](assets/external-spa-update-body.gif)

   1. 在新`body.html`文件中添加新的根元素。

   ![将根元素添加到body.html](assets/external-spa-add-root.png)

### 编辑带有路由的React SPA {#editing-react-spa-with-routing}

如果外部React SPA应用程序有多个页面，[它可以使用路由来确定要呈现的页面/组件](spa-routing.md)。 基本用例是将当前活动的URL与为路由提供的路径进行匹配。 要在此类启用路由的应用程序上启用编辑，需要转换要匹配的路径以适应AEM特定的信息。

在以下示例中，我们有一个包含两个页面的简单React应用程序。 要呈现的页面是通过将提供给路由器的路径与活动URL进行匹配来确定的。 例如，如果我们位于`mydomain.com/test`，则将呈现`TestPage`。

![在外部SPA中路由](assets/external-spa-routing.png)

要在此示例SPA的AEM中启用编辑，需要执行以下步骤。

1. 确定将用作AEM上的根的级别。

   * 对于我们的示例，我们将`wknd-spa-react/us/en`视为SPA的根。 这意味着该路径之前的所有内容仅是AEM页面/内容。

1. 在所需级别创建页面。

   * 在此示例中，要编辑的页面为`mydomain.com/test`。 `test`在应用程序的根路径中。 在AEM中创建页面时，也需要保留此设置。 因此，您可以在上一步中定义的根级别创建页面。
   * 创建的新页面必须与要编辑的页面具有相同的名称。 在此示例中，对于`mydomain.com/test`，创建的新页面必须为`/path/to/aem/root/test`。

1. 在SPA路由中添加帮助程序。

   * 新创建的页面将不会在AEM中呈现预期的内容。 这是因为路由器需要路径`/test`，而AEM活动路径为`/wknd-spa-react/us/en/test`。 要适应URL的AEM特定部分，我们需要在SPA端添加一些帮助程序。

   ![路由帮助程序](assets/external-spa-router-helper.png)

   * 由`@adobe/cq-spa-page-model-manager`提供的`toAEMPath`帮助程序可用于此目的。 当在AEM实例上打开应用程序时，它会转换为路由提供的路径，使其包括AEM特定的部分。 它接受三个参数：
      * 路由所需的路径
      * 编辑SPA的AEM实例的源URL
      * 第一步中确定的AEM上的项目根目录

   * 可以将这些值设置为环境变量，以获得更大的灵活性。

1. 验证是否在AEM中编辑页面。

   * 将项目部署到AEM并导航到新创建的`test`页面。 页面内容现在已呈现，并且AEM组件可供编辑。

## 框架限制 {#framework-limitations}

RemotePage组件希望该实施提供类似于此处](https://github.com/shellscape/webpack-manifest-plugin)所提供的[的资源清单。 但是，RemotePage组件仅经过测试可用于React框架（和通过remote-page-next组件的Next.js），因此不支持从其他框架(如Angular)远程加载应用程序。

## 其他资源 {#additional-resources}

以下参考资料可能有助于了解AEM上下文中的SPA。

* [AEM项目原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
* [WKND SPA项目](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/spa-editor/spa-editor-framework-feature-video-use.html?lang=zh-Hans)
* [在AEM中使用React快速入门SPA](spa-getting-started-react.md)
* [SPA参考资料（API参考）](spa-reference-materials.md)
* [SPA Blueprint和PageModelManager](spa-blueprint.md#pagemodelmanager)
* [SPA模型路由](spa-routing.md)
* [SPA和服务器端渲染](spa-ssr.md)
