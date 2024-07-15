---
title: 升级自定义搜索Forms
description: 本文详细介绍了升级后自定义搜索表单正常运行所需的调整。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1797'
ht-degree: 2%

---

# 升级自定义搜索Forms{#upgrading-custom-search-forms}

在AEM 6.2中，Customized Search Forms在存储库中的存储位置已更改。 升级后，这些用户档案会从6.1中的以下位置移动：

* /apps/cq/gui/content/facets

到位于以下位置的新位置：

* /conf/global/settings/cq/search/facets

因此，升级后需要手动调整表单才能继续正常运行。

这适用于新的搜索Forms和已自定义的默认Forms。

有关详细信息，请参阅有关[搜索Facet](/help/assets/search-facets.md)的文档。

## 更改resourceType属性 {#changing-the-resourcetype-property}

除非另有说明，否则升级后需要执行的大多数调整都需要更改配置的自定义搜索Forms的`sling:resourceType`属性。 该操作是必需的，这样属性才能指向渲染脚本的正确位置。

您可以通过执行以下操作来更改属性：

1. 通过转到`https://server:port/crx/de/index.jsp`打开CRXDE Lite
1. 按照下面[自定义搜索Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms)列表中的指定，浏览到需要调整的节点位置。
1. 单击节点。 在右侧属性窗格中，单击并修改&#x200B;**sling：resourceType**&#x200B;属性。
1. 最后，按&#x200B;**全部保存**&#x200B;按钮保存更改。

## 自定义搜索Forms列表 {#list-of-custom-search-forms}

在下方，您将找到所有自定义Search Forms的列表以及升级后它们所需的修改。 他们引用`/conf/global/settings/cq/search/facets/sites/items`中的名称。

### 节点名称为“全文”的全文谓词 {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>6.1中默认搜索表单中的节点</td>
   <td>全文</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

在AEM 6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已由OmniSearch取代。 此谓词以编程方式跳过，可以删除。

**操作：**&#x200B;完全删除节点。

### 其他全文谓词 {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>在6.1中的默认搜索源中的节点</td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 路径浏览器谓词 {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>路径</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 标记谓词 {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>标记</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整&#x200B;**resourceType**&#x200B;属性（像上面所示的6.2位置中一样添加“**/coral**”）。

### 页面状态谓词 {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td>不适用</td>
  </tr>
 </tbody>
</table>

“页面状态”已被替换为两个“选项”属性谓词，一个用于publish，另一个用于LiveCopy状态。

**操作：**

* 删除`pagestatuspredicate`节点
* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * 至`/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 复制节点

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * 至`/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* 确保将`analyticspredicate`节点的`listOrder`属性设置为“**8**”。 这是避免冲突所必需的。

### 日期范围谓词 {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>日期范围谓词</td>
  </tr>
  <tr>
   <td>6.1中的资源类型</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 隐藏的筛选器 {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>类型</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;没有可调整的内容。

### 分析谓词 {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticsspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticsspredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 范围谓词 {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

>[!NOTE]
>
>注意：与6.1相反，范围谓词不再在搜索栏中呈现标记。

### 选项属性谓词 {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 滑块范围谓词 {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 组件谓词 {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 作者谓词 {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 模板谓词 {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>在6.1<br /> <br />中的默认搜索表单中的节点 </td>
   <td>不适用</td>
  </tr>
  <tr>
   <td><p>6.1中的资源类型</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>6.2中的资源类型</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

## 资产管理员搜索边栏 {#assets-admin-search-rail}

以下节点引用`/conf/global/settings/dam/search/facets/assets/items`中的名称

### 节点名称为“全文”的全文谓词 {#fulltext-predicate-with-node-name-fulltext-1}

| 6.1中默认搜索表单中的节点 | 全文 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| 6.2中的资源类型 | 不适用 |

在6.1中，标准全文谓词是搜索表单的一部分。 在6.2中，全文字段已由OmniSearch取代。 此谓词以编程方式跳过，可以删除。

**操作：**&#x200B;删除上述节点。

### 路径浏览器谓词 {#path-browser-predicates-1}

| 6.1中默认搜索表单中的节点 | 路径浏览器 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### Mime类型谓词 {#mime-type-predicates}

| 6.1中默认搜索表单中的节点 | mimetype |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）。

### 文件大小谓词 {#file-size-predicates}

| 6.1中默认搜索表单中的节点 | filesize |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**操作：**&#x200B;调整`resourceType`，如上面的6.2位置所示。

### 资产上次修改的谓词 {#asset-last-modified-predicates}

| 6.1中默认搜索表单中的节点 | assetlastmodifiedpredicate |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

操作：调整resourceType属性（像上面所示的6.2位置中那样添加“/coral”）。

### Publish谓词 {#publish-predicate}

| 6.1中默认搜索表单中的节点 | 发布 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**操作：**

* 调整`resourceType`属性（在上面所示的6.2位置中添加“**/coral**”）

* 添加值为`/libs/dam/options/predicates/publish`的`optionPaths`（类型为String）属性

* 添加布尔值为`true`的`singleSelect`属性。

### 状态谓词 {#status-predicates}

| 6.1中默认搜索表单中的节点 | 状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）

### 到期状态谓词 {#expiry-status-predicates}

| 6.1中默认搜索表单中的节点 | 过期状态 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）

### 元数据有效性谓词 {#metadata-validity-predicates}

| 6.1中默认搜索表单中的节点 | 元数据有效性 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）

### 评级谓词 {#rating-predicates}

| 6.1中默认搜索表单中的节点 | 评级 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）

### 方向谓词 {#orientation-predicate}

| 6.1中默认搜索表单中的节点 | 方向 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**操作：**

* 调整`resourceType`属性（在上面所示的6.2位置中添加“**/coral**”）

* 在同一节点上添加与`text`属性具有相同值的`fieldLabel`属性。

* 在同一节点上添加与`text`属性具有相同值的`emptyText`属性。

* 在同一节点上添加与`optionPaths`属性具有相同值的`rootPath`属性。

### 样式谓词 {#style-predicate}

| 6.1中默认搜索表单中的节点 | 样式 |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| 6.2中的资源类型 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**操作：**

* 调整`resourceType`属性（在上面所示的6.2位置中添加“**/coral**”）

* 在同一节点上添加与`text`属性具有相同值的`fieldLabel`属性。

* 在同一节点上添加与`text`属性具有相同值的`emptyText`属性。

* 在同一节点上添加与`optionPaths`属性具有相同值的`rootPath`属性。

### 视频格式谓词 {#video-format-predicates}

| 6.1中默认搜索表单中的节点 | videoFormat |
|---|---|
| 6.1中的资源类型 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| 6.2中的资源类型 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）

### Mainasset谓词 {#mainasset-predicate}

| 6.1中默认搜索表单中的节点 | mainasset |
|---|---|
| 6.1中的资源类型 | granite/ui/components/foundation/form/hidden |
| 6.2中的资源类型 | granite/ui/components/coral/foundation/form/hidden |

**操作：**&#x200B;调整`resourceType`属性（添加“**/coral**”，如上面所示的6.2位置）
