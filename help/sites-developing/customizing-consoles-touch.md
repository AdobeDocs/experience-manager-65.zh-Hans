---
title: 自定义控制台
seo-title: 自定义控制台
description: AEM提供了各种机制，允许您自定义创作实例的控制台
seo-description: AEM提供了各种机制，允许您自定义创作实例的控制台
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 1%

---

# 自定义控制台{#customizing-the-consoles}

>[!CAUTION]
>
>本文档介绍如何在现代化的触屏优化UI中自定义控制台，并且不适用于经典UI。

AEM提供了各种机制，允许您自定义创作实例的控制台（和[页面创作功能](/help/sites-developing/customizing-page-authoring-touch.md)）。

* Clientlibs
Clientlibs允许您扩展默认实施以实现新功能，同时重用标准函数、对象和方法。 自定义时，您可以在`/apps.`下创建自己的clientlib。例如，它可以保存自定义组件所需的代码。

* 叠加
叠加基于节点定义，允许您将标准功能（在`/libs`中）与您自己的自定义功能（在`/apps`中）进行叠加。 在创建叠加时，不需要原始资源的1:1副本，因为Sling资源合并器允许继承。

这些控制台可以通过多种方式来扩展您的AEM控制台。 下面（在高级别）介绍了一些小的选择。

>[!NOTE]
>
>有关更多信息，请参阅：
>
>* 使用并创建[clientlibs](/help/sites-developing/clientlibs.md)。
>* 使用并创建[叠加](/help/sites-developing/overlays.md)。
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
[AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html)会话 — [AEM 6.0](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)的用户界面自定义中也介绍了本主题。

>[!CAUTION]
>
>***必须***&#x200B;不更改`/libs`路径中的任何内容。
>
>这是因为下次升级实例时，`/libs`的内容会被覆盖（当您应用修补程序或功能包时，很可能会被覆盖）。
>
>配置和其他更改的推荐方法是：
>
>1. 在`/apps`下重新创建所需项（即`/libs`中存在的项）
   >
   >
1. 在`/apps`中进行任何更改

>



例如，`/libs`结构中的以下位置可以覆盖：

* 控制台（任何基于Granite UI页面的控制台）；例如：

   * `/libs/wcm/core/content`

>[!NOTE]
>
>有关更多提示和工具，请参阅知识库文章[AEM TouchUI问题疑难解答](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)。

## 自定义控制台的默认视图{#customizing-the-default-view-for-a-console}

您可以自定义控制台的默认视图（列、卡片、列表）：

1. 您可以通过在下面叠加所需条目来重新排序视图：

   `/libs/wcm/core/content/sites/jcr:content/views`

   第一个条目将是默认条目。

   可用的节点与可用的视图选项相关联：

   * `column`
   * `card`
   * `list`

1. 例如，在列表的叠加中：

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   定义以下属性：

   * **名称**: `sling:orderBefore`
   * **类型**: `String`
   * **值**:  `column`

### 将新操作添加到工具栏{#add-new-action-to-the-toolbar}

1. 您可以构建自己的组件，并为自定义操作包含相应的客户端库。 例如，**提升到Twitter**&#x200B;操作位于：

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   然后，此组件可以连接到控制台上的工具栏项目：

   `/apps/<yourProject>/admin/ext/launches`

   例如，在选择模式下：

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 将工具栏操作限制为特定组{#restrict-a-toolbar-action-to-a-specific-group}

1. 您可以使用自定义渲染条件来覆盖标准操作，并强制规定在渲染之前必须满足的特定条件。

   例如，创建一个组件以根据组控制渲染条件：

   `/apps/myapp/components/renderconditions/group`

1. 要将这些操作应用到站点控制台上的创建站点操作，请执行以下操作：

   `/libs/wcm/core/content/sites`

   创建叠加：

   `/apps/wcm/core/content/sites`

1. 然后，为操作添加rendercondition:

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   使用此节点上的属性，您可以定义允许执行特定操作的`groups`;例如，`administrators`

### 自定义列表视图{#customizing-columns-in-the-list-view}中的列

>[!NOTE]
>
>此功能针对文本字段的列进行了优化；对于其他数据类型，可以在`/apps`中叠加`cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`。

要自定义列表视图中的列，请执行以下操作：

1. 覆盖可用列的列表。

   * 在节点上：

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 添加新列 — 或删除现有列。
   有关更多信息，请参阅[使用叠加（和Sling资源合并器）](/help/sites-developing/overlays.md)。

1. 可选：

   * 如果要插入其他数据，需要使用[](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 属性.

   例如，请参阅下面附加的类/包（从GitHub）。

1. 您现在可以在列表视图的列配置器中选择列。

### 筛选资源{#filtering-resources}

使用控制台时，常见的用例是用户必须从资源（例如页面、组件、资产等）中进行选择。 这可以采用列表的形式，例如，作者必须从中选择项目。

为了使列表保持为合理大小并且与用例相关，可以采用自定义谓词的形式实现过滤器。 有关详细信息，请参阅[本文](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)。
