---
title: 自定义页面创作
description: Adobe Experience Manager (AEM)提供了各种机制，让您能够自定义页面创作功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 38%

---

# 自定义页面创作{#customizing-page-authoring}

>[!CAUTION]
>
>本文档介绍如何在现代的触屏UI中自定义页面创作，并且不适用于经典UI。

Adobe Experience Manager (AEM)提供了各种机制，允许您自定义创作实例的页面创作功能（和[控制台](/help/sites-developing/customizing-consoles-touch.md)）。

* Clientlibs

  Clientlibs允许您扩展默认实施以实现新功能，同时重用标准函数、对象和方法。 定制时，您可以在 `/apps.` 下创建自己的 clientlib。新的 clientlib 必须：

   * 取决于创作clientlib `cq.authoring.editor.sites.page`
   * 属于相应的`cq.authoring.editor.sites.page.hook`类别

* 叠加

  叠加基于节点定义，允许您用自己的自定义功能（在`/apps`中）叠加标准功能（在`/libs`中）。 创建叠加时不需要原始文件的1:1副本，因为[sling资源合并器](/help/sites-developing/sling-resource-merger.md)允许继承。

>[!NOTE]
>
>有关详细信息，请参阅[JS文档集](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)。

可以通过多种方式使用这些功能来扩展AEM实例中的页面创作功能。 下面介绍了所做的选择（在高级别）。

>[!NOTE]
>
>有关更多信息，请参阅以下内容：
>
>* 正在使用和创建[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用和创建[叠加图](/help/sites-developing/overlays.md)。
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM触屏UI的结构](/help/sites-developing/touch-ui-structure.md)，了解有关用于页面创作的结构区域的详细信息。
>


>[!CAUTION]
>
>***不要***&#x200B;更改`/libs`路径中的任何内容。
>
>原因在于`/libs`的内容在下次升级实例时被覆盖（在应用修补程序或功能包时很可能会被覆盖）。
>
>建议用于配置和其他更改的方法是：
>
>1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
>1. 在`/apps`中进行任何更改

## 添加新层（模式） {#add-new-layer-mode}

当您编辑页面的时候，有各种各样的[模式](/help/sites-authoring/author-environment-tools.md#page-modes)可用。这些模式是使用[层次](/help/sites-developing/touch-ui-structure.md#layer)来实施的。其允许访问同一页面内容的不同类型的功能。标准层包括：编辑、预览、批注、开发人员和定位。

### 层次示例：Live Copy 状态 {#layer-example-live-copy-status}

标准 AEM 实例提供 MSM 层。这会访问与[多站点管理](/help/sites-administering/msm.md)相关的数据，并在层次中突出显示它。

若要查看其实际操作情况，您可以编辑任何[We.Retail语言副本](/help/sites-developing/we-retail-globalized-site-structure.md)页面（或任何其他活动副本页面）并选择&#x200B;**活动副本状态**&#x200B;模式。

您可以在以下位置找到 MSM 层的定义（仅供参考）：

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 代码示例 {#code-sample}

这是一个示例包，显示如何创建层（模式），该层是用于MSM视图的新层。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-new-layer-mode项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 将新的选择类别添加到资源浏览器 {#add-new-selection-category-to-asset-browser}

资源浏览器会显示各种类型/类别的资源（例如图像和文档）。还可以按这些资源类别过滤资源。

### 代码示例 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 是一个示例包，其中显示了如何将群组添加到资源查找器。此示例会连接到 [Flickr &#x200B;](https://www.flickr.com)的公共流，并在侧面板中显示它们。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-extension-assetfinder-flickr项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 筛选资源 {#filtering-resources}

创作页面时，用户通常必须从资源（例如，页面、组件和资产）中进行选择。 这可以采用列表形式，例如，作者必须从中选择项目。

为了使列表保持合理的大小并且与用例相关，可以通过自定义谓词的形式实施筛选条件。例如，如果使用[`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui)组件允许用户选择特定资源的路径，则可以通过以下方式筛选显示的路径：

* 通过实施 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) 界面来实施自定义谓词。
* 指定谓词的名称，并在使用 `pathbrowser` 时引用该名称。

有关创建自定义谓词的详细信息，请参阅[为查询生成器实施自定义谓词计算器](/help/sites-developing/implementing-custom-predicate-evaluator.md)。

>[!NOTE]
>
>通过实施`com.day.cq.commons.predicate.AbstractNodePredicate`界面来实施自定义谓词同样适用于经典UI。
>
>有关在经典UI中实现自定义谓词的示例，请参阅[此知识库文章](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html)。

## 将新的操作添加到组件工具栏 {#add-new-action-to-a-component-toolbar}

每个组件（通常）都有一个工具栏，通过该工具栏可访问可对该组件执行的一系列操作。

### 代码示例 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 是一个示例包，其中展示了如何创建自定义工具栏操作，以呈现组件。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-extension-toolbar-screenshot项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 添加新的就地编辑器 {#add-new-in-place-editor}

### 标准就地编辑器 {#standard-in-place-editor}

在标准 AEM 安装中：

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   保存各种可用编辑器的定义。

1. 编辑器和可以使用它的每种资源类型（如在组件中）之间存在连接：

   * `cq:inplaceEditing`

     例如：

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 属性：`editorType`

           定义触发对该组件进行就地编辑时使用的内联编辑器的类型；例如，`text`, `textimage`, `image`, `title`。

1. 可以使用包含配置的`config`节点和包含必要插件配置详细信息的`plugin`节点来配置编辑器的其他配置详细信息。

   以下是为图像组件的图像裁剪插件定义长宽比的示例。 由于屏幕大小受限的可能性，裁切长宽比已移至全屏编辑器并且仅可在其中看到。

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >由 `ratio` 属性设置的 AEM 裁剪比例定义为&#x200B;**高度/宽度**。这与常见的宽高比的定义不同，这样做是出于对旧版兼容性的考虑。只要您清楚地定义 `name` 属性，页面创作用户便不会察觉到任何差异，因为您定义的名称才是 UI 中显示的内容。

#### 创建新的就地编辑器 {#creating-a-new-in-place-editor}

要实施新的就地编辑器（在您的 clientlib 中）：

>[!NOTE]
>
>例如，请参阅：
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 实施：

   * `setUp`
   * `tearDown`

1. 注册编辑器（包括构造函数）：

   * `editor.register`

1. 提供编辑器和可以使用它的每种资源类型（如在组件中）之间存在连接。

#### 用于创建新的就地编辑器的代码示例 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 是一个示例包，其中展示如何在 AEM 中创建就地编辑器。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-extension-inplace-editor项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 配置多个就地编辑器 {#configuring-multiple-in-place-editors}

可以配置组件，使其具有多个就地编辑器。 配置多个就地编辑器后，您可以选择相应的内容并打开相应的编辑器。 有关详细信息，请参阅[配置多个就地编辑器](/help/sites-developing/multiple-inplace-editors.md)文档。

## 添加新的页面操作。 {#add-a-new-page-action}

向页面工具栏中添加新的页面操作，例如&#x200B;**返回站点** （控制台）操作。

### 代码示例 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 是一个示例包，其中显示如何创建自定义标题栏操作，以跳回 Sites 控制台。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* 在GitHub上[打开aem-authoring-extension-header-backtosites项目](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 将项目下载为[ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 自定义激活请求工作流程程 {#customizing-the-request-for-activation-workflow}

开箱即用的工作流程程，**请求激活：**

* 当内容作者&#x200B;**没有**&#x200B;适当的复制权限，但&#x200B;**有** DAM 用户和作者的会员资格时，将会自动出现在适当的菜单上。

* 否则，不会显示任何内容，因为复制权限已被删除。

要在此类激活上自定义行为，您可以叠加&#x200B;**请求激活**&#x200B;工作流程程：

1. 在`/apps`中，覆盖&#x200B;**站点**&#x200B;向导：

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >它本身会覆盖以下常见实例：
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 根据需要更新[工作流模型](/help/sites-developing/workflows-models.md)和相关配置/脚本。
1. 从所有相关页面的所有相应用户中删除[`replicate`操作](/help/sites-administering/security.md#actions)的权限；在任何用户尝试发布（或复制）页面时，将此工作流作为默认操作触发。
