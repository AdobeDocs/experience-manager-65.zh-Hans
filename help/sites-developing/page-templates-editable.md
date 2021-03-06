---
title: 页面模板 — 可编辑
seo-title: Page Templates - Editable
description: 已引入可编辑的模板，允许非开发人员创建和编辑模板，提供可保留与从这些模板创建的任何页面动态连接的模板，并使页面组件更加通用
seo-description: Editable templates have been introduced to, allow non-developers to create and edit templates, provide templates that retain a dynamic connection to any pages created from them, and make the page component more generic
uuid: 61791960-fdef-4e49-878a-11fdf1d4f0ab
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 1099cc44-de6d-499e-8b52-f2f5811ae086
docset: aem65
exl-id: dcb66b6d-d731-493e-8936-12d529f6cbde
source-git-commit: 2801ef5ec5ed7b01f4eb046baa439f6d5de56b75
workflow-type: tm+mt
source-wordcount: '3249'
ht-degree: 9%

---

# 页面模板 — 可编辑 {#page-templates-editable}

已为以下对象引入了可编辑的模板：

* 允许专门的作者 [创建和编辑模板](/help/sites-authoring/templates.md).

   * 这种专业作者被称为 **模板作者**
   * 模板作者必须是 `template-authors` 群组。

* 提供模板，以保留与从这些模板创建的任何页面的动态连接。 这可确保模板的任何更改都反映在页面本身中。
* 使页面组件更加通用，以便无需自定义即可使用核心页面组件。

使用可编辑的模板，可在组件中分隔出用于创建页面的片段。 您可以在UI中配置组件的必要组合，从而无需为每个页面变体开发新的页面组件。

>[!NOTE]
>
>[静态模板](/help/sites-developing/page-templates-static.md) 也可用。

本文档：

* 概述如何创建可编辑的模板

   * 有关详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md)

* 描述创建可编辑模板所需的管理员/开发人员任务
* 描述可编辑模板的技术基础

本文档假定您已经熟悉创建和编辑模板。 请参阅创作文档 [创建页面模板](/help/sites-authoring/templates.md)，其中详细介绍了向模板作者显示的可编辑模板的功能。

>[!NOTE]
>
>在新项目中设置可编辑的页面模板时，以下教程可能也很有意义：
>[AEM Sites入门第2部分 — 创建基页和模板](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part2.html)

## 创建新模板 {#creating-a-new-template}

可编辑的模板主要通过 [模板控制台和模板编辑器](/help/sites-authoring/templates.md) 模板作者。 本节概述了此过程，并随后介绍了在技术层面发生的情况。

有关如何在AEM项目中使用可编辑模板的信息，请参阅 [使用Lazybone创建AEM项目](https://helpx.adobe.com/experience-manager/using/aem_lazybones.html).

创建新的可编辑模板时，您需要执行以下步骤：

1. 创建 [模板文件夹](#template-folders). 这不是强制性的，但建议使用最佳实践。
1. 选择 [模板类型](#template-type). 此操作将复制以创建 [模板定义](#template-definitions).

   >[!NOTE]
   >
   >提供了一系列现成的模板类型。 您还可以 [创建您自己的特定于网站的模板类型](/help/sites-developing/page-templates-editable.md#creating-template-types) （如果需要）。

1. 配置新模板的结构、内容策略、初始内容和布局。

   **结构**

   * 利用结构，可为模板定义组件和内容。
   * 不能在生成页面上移动在模板结构中定义的组件，也不能从任何生成页面中删除这些组件。

      * 如果您是在We.Retail示例内容以外的自定义文件夹中创建模板，则可以选择基础组件或使用 [核心组件](https://helpx.adobe.com/experience-manager/core-components/using/developing.html).
   * 如果要使页面作者能够添加和删除组件，请在模板中添加段落系统。
   * 可以解锁组件，然后再将其锁定，以便定义初始内容。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   有关结构的技术详细信息，请参阅 [结构](/help/sites-developing/page-templates-editable.md#structure) 在本文档中。

   **策略**

   * 内容策略可定义组件的设计属性。

      * 例如，可用的组件或最小/最大尺寸。
   * 这些属性适用于模板（和使用模板创建的页面）。

   有关模板作者如何定义策略的详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   有关策略的技术详细信息，请参阅 [内容策略](/help/sites-developing/page-templates-editable.md#content-policies) 在本文档中。

   **初始内容**

   * 初始内容定义在首次基于模板创建页面时显示的内容。
   * 然后，页面作者可以编辑初始内容。

   有关模板作者如何定义结构的详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   有关初始内容的技术详细信息，请参阅 [初始内容](/help/sites-developing/page-templates-editable.md#initial-content) 在本文档中。

   **布局**

   * 您可以为各种设备定义模板布局。
   * 模板的响应式布局与页面创作时的响应式布局功能相同。

   有关模板作者如何定义模板布局的详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   有关模板布局的技术详细信息，请参阅 [布局](/help/sites-developing/page-templates-editable.md#layout) 在本文档中。

1. 启用模板，然后为特定内容树启用它。

   * 可以启用或禁用模板，以使其对页面作者可用或不可用。
   * 可以使模板可用于或不可用于某些页面分支。

   有关模板作者如何启用模板的详细信息，请参阅 [创建页面模板](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   有关启用模板的技术详细信息，请参阅 [为我们启用和允许模板](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)本文档中的e

1. 使用它创建内容页面。

   * 使用静态模板和可编辑的模板创建新页面的过程没有明显的区别，也没有孰优孰劣之分。
   * 对于页面作者而言，该创建过程一目了然。

   有关页面作者如何使用模板创建页面的详细信息，请参阅 [创建和组织页面](/help/sites-authoring/managing-pages.md#templates).

   有关使用可编辑模板创建页面的技术详细信息，请参阅 [生成内容页面](/help/sites-developing/page-templates-editable.md#resultant-content-pages) 在本文档中。

>[!TIP]
>
>切勿在模板中输入任何需要国际化的信息。出于内部化目的， [核心组件的本地化功能](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html) 。

>[!NOTE]
>
>模板是简化页面创建工作流的强大工具。不过，太多的模板会让作者不知所措，并使页面创建变得混乱。一个好的经验法则是将模板的数量保持在 100 个以内。
>
>由于潜在的性能影响，Adobe 建议不要使用超过 1000 个模板。

>[!NOTE]
>
>编辑器客户端库假定存在 `cq.shared` 命名空间，如果不存在JavaScript错误，则使用 `Uncaught TypeError: Cannot read property 'shared' of undefined` 结果。
>
>所有示例内容页面都包含 `cq.shared`，因此基于这些内容的任何内容都会自动包含 `cq.shared`. 但是，如果您决定从头开始创建自己的内容页面，而不基于示例内容，则必须确保包含 `cq.shared` 命名空间。
>
>请参阅 [使用客户端库](/help/sites-developing/clientlibs.md) 以了解更多信息。

## 模板文件夹 {#template-folders}

要组织模板，您可以使用以下文件夹：

* **全局**
* 特定于网站创建的用于组织模板的特定于网站的文件夹，其帐户具有管理员权限。

>[!NOTE]
>
>即使您可以嵌套文件夹，当用户在 **模板** 控制台以平面结构呈现。

在标准 AEM 实例中，“模板”控制台中已存在&#x200B;**全局**&#x200B;文件夹。此文件夹会保存默认模板，如果在当前文件夹中没有找到策略和/或模板类型，则此文件夹可以充当备用。您可以将默认模板添加到此文件夹或创建新文件夹（推荐）。

>[!NOTE]
>
>最佳做法是创建新文件夹来保存自定义模板，而不使用全局文件夹。

>[!CAUTION]
>
>文件夹必须由具有 `admin` 权限。

模板类型和策略将按照以下优先顺序继承到所有文件夹：

1. 当前文件夹。
1. 当前文件夹的父项。
1. `/conf/global`
1. `/apps`
1. `/libs`

将创建所有允许条目的列表。 如果有任何配置重叠( `path`/ `label`)，则只会向用户显示最接近当前文件夹的实例。

要创建新文件夹，您可以执行以下操作之一：

* 以编程方式或使用CRXDE Lite
* 使用配置浏览器

## 使用 CRXDE Lite {#using-crxde-lite}

1. 可以采用编程方式或通过CRXDE Lite为实例创建新文件夹（在/conf下）。

   必须使用以下结构：

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. 然后，您可以在文件夹根节点上定义以下属性：

   `<your-folder-name> [sling:Folder]`

   名称: `jcr:title`

   * 类型: `String`

   * 值：要显示在 **模板** 控制台。

1. 在 *添加* 的权限(例如， `content-authors`)，您现在需要为作者分配组并定义所需的访问权限(ACL)，以便在新文件夹中创建模板。

   的 `template-authors` 组是需要分配的默认组。 请参阅以下部分 [ACL和组](/help/sites-developing/page-templates-editable.md#acls-and-groups) 以了解详细信息。

   请参阅 [访问权限管理](/help/sites-administering/user-group-ac-admin.md#access-right-management) 以了解有关管理和分配访问权限的完整详细信息。

### 使用配置浏览器 {#using-the-configuration-browser}

1. 转到 **全局导航** -> **工具** > **配置浏览器**.

   现有文件夹将列在左侧，包括 **全球** 文件夹。

1. 单击&#x200B;**创建**。
1. 在 **创建配置** 对话框需要配置以下字段：

   * **标题**:为配置文件夹提供标题
   * **可编辑的模板**:勾号，允许在此文件夹中编辑模板

1. 单击 **创建**

>[!NOTE]
>
>在配置浏览器中，您可以编辑全局文件夹并激活 **可编辑的模板** 选项，但建议不要使用此文件夹创建模板。
>
>请参阅 [配置浏览器](/help/sites-administering/configurations.md) 文档以了解更多信息。

### ACL和组 {#acls-and-groups}

创建模板文件夹（通过CRXDE或使用配置浏览器）后，必须为模板文件夹的相应组定义ACL，以确保适当的安全性。

的模板文件夹 [We.Retail参考实施](/help/sites-developing/we-retail.md) 例子。

#### 模板作者组 {#the-template-authors-group}

的 `template-authors` 组是用于管理模板访问权限的组，其标准中包含AEM，但为空。 必须将用户添加到项目/站点的组。

>[!CAUTION]
>
>的 `template-authors` 组 *仅* 适用于必须能够创建新模板的用户。
>
>编辑模板非常强大，如果未正确完成，现有模板可能会被破坏。 因此，此角色应该重点突出，并且仅包含符合条件的用户。

下表详细列出了进行模板编辑所需的权限。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>模板作者<br /> </td>
   <td>读、写、复制</td>
   <td>在特定于站点的模板中创建、读取、更新、删除和复制模板的模板作者 <code>/conf</code> 空间</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在渲染页面时必须读取模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>激活页面时，replicateContent作者需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读、写、复制</td>
   <td>在特定于站点的模板中创建、读取、更新、删除和复制模板的模板作者 <code>/conf</code> 空间</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在渲染页面时必须读取策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>模板作者</td>
   <td>读取</td>
   <td>模板作者基于其中一种预定义的模板类型创建新模板。</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不得访问模板类型</td>
  </tr>
 </tbody>
</table>

此默认 `template-authors` 组仅涵盖项目设置，其中 `template-authors` 允许成员访问和创作所有模板。 对于更复杂的设置，在设置中需要多个模板作者组来分隔对模板的访问权限，必须创建更多自定义模板作者组。 但是，模板作者组的权限将保持不变。

#### /conf/global下的旧版模板 {#legacy-templates-under-conf-global}

模板不应再存储在 `/conf/global`但是，对于某些旧版安装，此位置中可能仍存在模板。 只有在此类旧情况下，才应满足以下条件 `/conf/global` 路径进行显式配置。

<table>
 <tbody>
  <tr>
   <th>路径</th>
   <th>角色/组</th>
   <th>权限<br /> </th>
   <th>描述</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>模板作者</td>
   <td>读、写、复制</td>
   <td>在中创建、读取、更新、删除和复制模板的模板作者 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在渲染页面时必须读取模板</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面的模板</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>读、写、复制</td>
   <td>在中创建、读取、更新、删除和复制模板的模板作者 <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>读取</td>
   <td>匿名Web用户在渲染页面时必须读取策略</td>
  </tr>
  <tr>
   <td>内容作者</td>
   <td>复制</td>
   <td>内容作者在激活页面时需要激活页面模板的策略</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>模板作者</td>
   <td>读取</td>
   <td>模板作者基于其中一种预定义的模板类型创建新模板</td>
  </tr>
  <tr>
   <td>匿名Web用户</td>
   <td>无</td>
   <td>匿名Web用户不得访问模板类型</td>
  </tr>
 </tbody>
</table>

## 模板类型 {#template-type}

创建新模板时，您需要指定模板类型：

* 模板类型有效地为模板提供模板。 创建新模板时，将使用所选模板类型的结构和初始内容创建新模板。

   * 将复制模板类型以创建模板。
   * 复制后，模板与模板类型之间的唯一连接便是用于获取信息的静态引用。

* 模板类型允许您定义：

   * 页面组件的资源类型。
   * 根节点的策略，用于定义模板编辑器中允许的组件。
   * 建议为响应式网格定义断点，并在模板类型上的设置移动模拟器。 这是可选的，因为配置也可以在单个模板上定义(请参阅 [模板类型和移动设备组](/help/sites-developing/page-templates-editable.md#p-template-type-and-mobile-device-groups-br-p))。

* AEM提供了一小部分现成的模板类型，如“HTML5页面”和“自适应表单页面”。

   * 在 [We.Retail](/help/sites-developing/we-retail.md) 示例内容。

* 模板类型通常由开发人员定义。

现成模板类型存储在以下位置：

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>您不得在 `/libs` 路径。 这是因为 `/libs` 在下次升级实例时被覆盖（在应用修补程序或功能包时可能会被覆盖）。

您特定于网站的模板类型应存储在以下可比位置：

* `/apps/settings/wcm/template-types`

自定义模板类型的定义应存储在用户定义的文件夹中（推荐），或者存储在 `global`. 例如：

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>模板类型必须遵循正确的文件夹结构(即 `/settings/wcm/...`)，否则将找不到模板类型。

### 模板类型和移动设备组 {#template-type-and-mobile-device-groups-br}

的 [设备组](/help/sites-developing/mobile.md#device-groups) 用于可编辑的模板（设置为属性的相对路径） `cq:deviceGroups`)定义哪些移动设备在中可用作模拟器 [布局模式](/help/sites-authoring/responsive-layout.md) 页面创作的页面。 此值可设置为两个位置：

* 在可编辑的模板类型上
* 在可编辑的模板上

创建新的可编辑模板时，该值会从模板类型复制到单个模板。 如果未在类型上设置值，则可以在模板上设置该值。 创建模板后，类型对模板的继承就不存在。

>[!CAUTION]
>
>的值 `cq:deviceGroups` 必须设置为相对路径，如 `mobile/groups/responsive` 而不是作为绝对路径，例如 `/etc/mobile/groups/responsive`.

>[!NOTE]
>
>使用 [静态模板](/help/sites-developing/page-templates-static.md)，的值 `cq:deviceGroups` 可以在站点的根位置设置。
>
>使用可编辑的模板，此值现在存储在模板级别，而在页面根级别不受支持。

### 创建模板类型 {#creating-template-types}

如果已创建可用作其他模板基础的模板，则可以将此模板复制为模板类型。

1. 与创建任何可编辑模板一样创建模板 [如此处所述](/help/sites-authoring/templates.md#creating-a-new-template-template-author)，用作模板类型的基础。
1. 使用CRXDE Lite，从 `templates` 节点 `template-types` 节点下 [模板文件夹](/help/sites-developing/page-templates-editable.md#template-folders).
1. 从 `templates` 节点下 [模板文件夹](/help/sites-developing/page-templates-editable.md#template-folders).
1. 在位于 `template-types` 节点，删除全部 `cq:template` 和 `cq:templateType` `jcr:content` 属性。

您还可以使用GitHub上提供的可编辑模板示例作为基础，开发您自己的模板类型。

GITHUB上的代码

您可以在GitHub上找到此页面的代码

* [在GitHub上打开aem-sites-example-custom-template-type项目](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* 将项目下载为 [ZIP文件](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/archive/master.zip)

## 模板定义 {#template-definitions}

可编辑模板的定义已存储 [用户定义的文件夹](/help/sites-developing/page-templates-editable.md#template-folders) （推荐）或 `global`. 例如：

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

模板的根节点类型为 `cq:Template` 骨架结构为：

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

主要元素包括：

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:content {#jcr-content}

此节点包含模板的属性：

* **名称**: `jcr:title`

* **名称**: `status`

   * **类型**: `String`

   * **值**: `draft`, `enabled` 或 `disabled`

### 结构 {#structure}

定义生成页面的结构：

* 与初始内容( `/initial`)。
* 对结构所做的更改将会反映在使用该模板创建的任何页面中。
* 的 `root` ( `structure/jcr:content/root`)节点定义将在生成页面中可用的组件列表。

   * 无法在任何生成页面上移动或删除在模板结构中定义的组件。
   * 解锁组件后， `editable` 属性设置为 `true`.

   * 解锁已包含内容的组件后，此内容将被移动到 `initial` 分支。

* 的 `cq:responsive` 节点包含响应式布局的定义。

### 初始内容 {#initial-content}

定义新页面在创建时将包含的初始内容：

* 包含 `jcr:content` 节点。
* 与结构合并( `/structure`)。
* 如果初始内容在创建后发生更改，则不会更新任何现有页面。
* 的 `root` 节点包含一个组件列表，用于定义将在生成页面中可用的组件。
* 如果在结构模式下将内容添加到组件，并且该组件随后被解锁（反之亦然），则此内容将用作初始内容。

### 布局 {#layout}

When [编辑可定义布局的模板](/help/sites-authoring/templates.md)，使用 [标准响应式布局](/help/sites-authoring/responsive-layout.md) 也可以 [已配置](/help/sites-administering/configuring-responsive-layout.md).

### 内容策略 {#content-policies}

内容（或设计）策略可定义组件的设计属性。例如，可用的组件或最小/最大尺寸。这些属性适用于模板（和使用模板创建的页面）。可以在模板编辑器中创建和选择内容策略。

* 资产 `cq:policy`，在 `root` 节点
   `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
为页面的段落系统提供对内容策略的相对引用。

* 资产 `cq:policy`，在下的组件显式节点上 `root`，则提供各个组件的策略链接。

* 实际策略定义存储在以下位置：
   `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>策略定义的路径取决于组件的路径。 `cq:policy` 包含对配置本身的相对引用。

>[!NOTE]
>
>从可编辑模板创建的页面在页面编辑器中不提供设计模式。
>
>的 `policies` 可编辑模板的树的层次结构与静态模板的设计模式配置在以下位置相同：
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>为每个页面组件定义了静态模板的设计模式配置。

### 页面策略 {#page-policies}

页面策略允许您定义 [内容策略](#content-policies) 对于页面（主parsys），在模板或生成页面中。

### 启用和允许模板使用 {#enabling-and-allowing-a-template-for-use}

1. **启用模板**

   模板必须通过以下任一方式启用，才能使用：

   * [启用模板](/help/sites-authoring/templates.md#enablingatemplateauthor) 从 **模板** 控制台。

   * 在 `jcr:content` 节点。

      * 例如，在：
         `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * 定义属性：

         * 名称：状态
         * 类型：字符串
         * 值: `enabled`

1. **允许的模板**

   * [在上定义允许的模板路径 **页面属性**](/help/sites-authoring/templates.md#allowing-a-template-author) 子分支的相应页面或根页面的名称。
   * 设置属性：
      `cq:allowedTemplates`
在 
`jcr:content` 所需分支的节点。
   例如，值为：

   `/conf/<your-folder>/settings/wcm/templates/.*`

## 生成内容页面 {#resultant-content-pages}

从可编辑模板创建的页面：

* 创建时使用的是从中合并的子树 `structure` 和 `initial` 在模板中

* 对模板和模板类型中包含的信息进行引用。 这是通过 `jcr:content` 的节点：

   * `cq:template`
提供对实际模板的动态引用；允许将对模板所做的更改反映在实际页面上。

   * `cq:templateType`
提供对模板类型的引用。

![chlimage_1-71](assets/chlimage_1-71.png)

上图显示了模板、内容和组件如何相互关联：

* 控制器 —  `/content/<my-site>/<my-page>`
引用模板的生成页面。 内容控制着整个过程。 根据定义，访问相应的模板和组件。

* 配置 —  `/conf/<my-folder>/settings/wcm/templates/<my-template>`
的 [模板和相关内容策略](#template-definitions) 定义页面配置。

* 模型 — OSGi包 [OSGi包](/help/sites-deploying/osgi-configuration-settings.md) 实施功能。

* 查看 —  `/apps/<my-site>/components`
在创作和发布环境中，内容都由 [组件](/help/sites-developing/components.md).

渲染页面时：

* **模板**:

   * 的 `cq:template` 其属性 `jcr:content` 将引用节点以访问与该页面对应的模板。

* **组件**:

   * 页面组件将合并 `structure/jcr:content` 模板的树 `jcr:content` 页面树。

   * 页面组件将仅允许作者编辑已标记为可编辑的模板结构的节点（以及任何子节点）。
   * 在页面上渲染组件时，该组件的相对路径将从 `jcr:content` 节点；同一条路 `policies/jcr:content` 随后将搜索模板的节点。

      * 的 `cq:policy` 此节点的属性指向实际的内容策略（即它包含该组件的设计配置）。

      * 这样，您就可以拥有多个重复使用相同内容策略配置的模板。
