---
title: 将 Search&Promote 功能添加到您的页面
seo-title: 将 Search&Promote 功能添加到您的页面
description: 在您的网站中集成 Search&Promote 功能后，您可以使用 Search&Promote 组件将相应功能添加到您的页面，例如关键字搜索、搜索结果页面、搜索优化以及横幅。
seo-description: 在您的网站中集成 Search&Promote 功能后，您可以使用 Search&Promote 组件将相应功能添加到您的页面，例如关键字搜索、搜索结果页面、搜索优化以及横幅。
uuid: 8cd3c143-cb0b-4eb0-931d-9d447ea3c950
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 968b9131-ccdf-4856-b504-bc1a44974980
docset: aem65
exl-id: cf5849c7-1c6a-46d8-9cc4-f1f20a507a0c
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 69%

---

# 将Search&amp;Promote功能添加到页面{#adding-search-promote-features-to-your-page}

要在您的网站中集成 Search&amp;Promote 功能，需使用 Search&amp;Promote 组件将以下功能添加到您的页面：

* 关键字搜索
* 搜索结果页面
* 搜索优化
* 横幅

仅当Adobe Experience Manager管理员已启用Search&amp;Promote功能时，才能使用这些功能。 请参阅[与AdobeSearch&amp;Promote集成](/help/sites-administering/search-and-promote.md)。

Search＆Promote 服务器上配置了一些 facet，这也是每个组件提供的信息。下表提供了每个组件的简要描述。后续部分详细介绍了这些组件的用法。

<table>
 <tbody>
  <tr>
   <th>Search&amp;Promote组件</th>
   <th>描述</th>
  </tr>
  <tr>
   <td>横幅</td>
   <td>显示横幅广告。 横幅的选择基于通过Search&amp;Promote收集的数据。<br /> </td>
  </tr>
  <tr>
   <td>痕迹导航</td>
   <td>显示搜索关键词以及用户应用于搜索结果的过滤器序列。</td>
  </tr>
  <tr>
   <td>复选框列表彩块化</td>
   <td>用于选择Facet以筛选搜索结果的复选框列表。</td>
  </tr>
  <tr>
   <td>下拉列表彩块化</td>
   <td>用于筛选搜索结果的Facet的下拉列表。</td>
  </tr>
  <tr>
   <td>链接列表彩块化</td>
   <td>用于筛选搜索结果的Facet链接列表。</td>
  </tr>
  <tr>
   <td>分页</td>
   <td>用于浏览搜索结果页面的控件。</td>
  </tr>
  <tr>
   <td>结果</td>
   <td>显示关键词搜索的结果。</td>
  </tr>
  <tr>
   <td>搜索</td>
   <td>向页面中添加搜索字段。</td>
  </tr>
 </tbody>
</table>

## 创建搜索结果页面 {#creating-the-search-results-page}

使用 WCM“网站”控制台可创建一个显示搜索结果的页面。如果使用相同的 Search&amp;Promote 服务，则使用任何搜索组件获取的搜索结果都可以显示在此页面上。

允许用户查看搜索结果的组件是“结果”和“分页”。**[!UICONTROL 结果]**&#x200B;组件在编辑或设计模式下没有可配置的属性。“结果”组件只会列出搜索结果，其中提供了指向其他页面的链接，并且还显示了搜索关键字的结果数量。

![srresultscomp](assets/srchresultscomp.png)

**[!UICONTROL 分页]**&#x200B;组件使用户能够浏览搜索结果的多个页面。用户可以查看页数、移到下一页或上一页、选择要打开的页面，或将所有结果合并到一个页面。

![分页](assets/srchpagination.png)

您可以在编辑模式下配置以下组件属性来控制运行时行为：

* 隐藏单个结果页面：如果要在搜索返回单个结果页面时隐藏页面导航控件，请选择此选项。
* 首次/最后隐藏：如果要阻止用户跳转到结果的第一页或最后一页，请选择此选项。
* “隐藏前一个/后一个”：确定用户是否可以浏览相对于当前页面的结果页面。
* “隐藏查看全部”：确定用户是否可以将所有搜索结果合并到单个页面。通常，提供分页数据可以更有效地使用服务器资源。如果要阻止在一条响应消息中传输大数据集，请选择此选项。

### 允许按彩块化筛选结果 {#enabling-the-filtering-of-results-by-facets}

您可以允许用户按 facet 筛选搜索结果。**[!UICONTROL 复选框列表Facet]**、**[!UICONTROL 下拉列表Facet]**&#x200B;和&#x200B;**[!UICONTROL 链接列表Facet]**&#x200B;组件允许用户选择一个或多个Facet进行筛选。 使用这些组件时，您还应包含&#x200B;**痕迹导航**&#x200B;组件。痕迹导航可指示当前使用的筛选器。

**[!UICONTROL 复选框列表Facet]**、**[!UICONTROL 下拉列表Facet]**&#x200B;和&#x200B;**[!UICONTROL 链接列表Facet]**&#x200B;组件各自具有您在&#x200B;**编辑**&#x200B;模式下配置的以下属性：

* **Facet 名称**：用于筛选器的 facet 名称。

**[!UICONTROL 复选框列表 Facet]** 组件会显示包含附带复选框的 facet 列表。使用&#x200B;**[!UICONTROL 复选框列表 Facet]**，用户可以查看包含多个 facet 项目的结果子集。例如，**可以使用“品牌”facet，因为多个品牌可提供相同类型的产品。**

每个与搜索结果关联的 facet 都会显示一个复选框。当用户选择某个复选框时，页面将重新加载以显示更新的结果集。所有复选框均会保留在页面上，以便客户可以随时在筛选器中添加或删除 facet：

![沙盒组件](assets/sandpcheckboxcomp.png)

**[!UICONTROL 下拉列表 Facet]** 组件使客户能够从下拉列表中选择一个 facet 项目。当您希望客户一次只关注一个 facet 项目时，此组件非常有用。例如，“专栏”facet 有助于客户能够按性别缩小产品搜索范围。John 要搜索“牛仔裤”**，然后在男士专栏中进行筛选。

下拉列表中填充了与所有搜索结果关联的 facet。在下拉列表中选择一个项目后，页面将重新加载以显示更新的结果集。下拉列表中的项目不会发生更改，以便客户可以随时切换 facet。

![沙滴管](assets/sandpdropdowndepartment.png)

**[!UICONTROL 链接列表 Facet]** 组件使客户能够将焦点逐步缩小到归类为多个 facet 成员或 facet 的项目。

facet 成员显示为链接列表。每个链接的文本是与当前搜索结果关联的 facet 成员的名称。当客户单击 facet 链接时，页面将重新加载以显示更新的结果集。链接列表会相应地更新，以便能够进一步缩小焦点。

![andlinklistcomp](assets/sandplinklistcomp.png)

当从其他类型的Search&amp;Promote组件应用过滤器时，列表中的链接也会发生更改。 使用多种类型的筛选器组件可以提供有效的筛选器组合。

**[!UICONTROL 痕迹导航]**&#x200B;组件使客户能够按照应用筛选器的顺序查看当前应用于搜索结果的筛选器。客户可以单击痕迹导航中的项目以还原到该筛选器组合。

![沙带结构组件](assets/sandpbreadcrumbcomp.png)

您可以在编辑模式下配置痕迹导航的以下属性，以便自定义该组件的外观：

* “分隔符”：定义用作各个痕迹导航之间的分隔符的字符或字符串。**[!UICONTROL 分隔符]**&#x200B;字段接受任何字符串作为输入。 默认设置为“>”（不带引号）
* “结尾分隔符”：定义要显示在痕迹导航末尾的字符或字符串。**[!UICONTROL Trailing Delimiter]**&#x200B;字段接受任何字符串作为输入。 此字段的默认设置为*blank*（即，痕迹导航行的末尾不显示任何内容）

### 添加搜索框 {#adding-search-boxes}

**[!UICONTROL 搜索]**&#x200B;组件允许客户执行关键词搜索。 将&#x200B;**[!UICONTROL Search]**&#x200B;组件添加到要提供搜索访问权限的每个页面。

在编辑模式下配置以下属性，以便控制运行时行为：

* “结果页面路径”：显示搜索结果的页面的路径。
* “启用自动完成”：如果选中，则当客户开始在搜索框中键入内容时，会显示建议的搜索关键字。

![sandsearchcomp](assets/sandpsearchcomp.png)

### 添加横幅 {#adding-banners}

**[!UICONTROL 横幅]**&#x200B;组件根据客户的Search&amp;Promote搜索显示横幅广告。 Search&amp;Promote 服务器上的逻辑会确定要显示的横幅。例如，搜索牛仔裤可能会显示与时装相关的横幅。在男士专栏中进行筛选可以进一步优化横幅的选择。

**[!UICONTROL 横幅]**&#x200B;组件提供了一个名为“横幅区域”的可配置属性。 在编辑模式下，选择其中一个属性值可指定横幅的显示方式。Search&amp;Promote 服务会确定您可以从中选择的值列表。

### Search&amp;Promote 搜索页面示例 {#example-search-promote-search-page}

下图显示了添加到页面以创建下面功能齐全的Search&amp;Promote结果页面的组件。

![1328213789109](assets/1328213789109.png) ![沙盒示例](assets/sandppageexample.png)
