---
title: AEM 标记框架
description: 标记内容并使用AEM标记基础架构
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
feature: Developing,Tagging
exl-id: 53a37449-ef87-4fa6-82de-88fdc24cf988
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1637'
ht-degree: 0%

---


# AEM 标记框架 {#aem-tagging-framework}

标记允许对内容进行分类和组织。 标记可以按命名空间和分类法进行分类。 有关使用标记的详细信息：

* 有关将内容标记为内容作者的信息，请参阅文档[使用标记](/help/sites-authoring/tags.md)。
* 有关创建和管理标记以及已对哪些内容应用标记的管理员观点，请参阅文档[管理标记](/help/sites-administering/tags.md)。

本文重点介绍支持AEM中标记的基础框架以及如何作为开发人员使用它。

## 简介 {#introduction}

要标记内容并使用AEM标记基础架构，请执行以下操作：

* 标记必须作为类型`[cq:Tag](#tags-cq-tag-node-type)`的节点存在于[分类根节点下。](#taxonomy-root-node)

* 标记的内容节点的`NodeType`必须包含[`cq:Taggable`](#taggable-content-cq-taggable-mixin) mixin。
* [`TagID`](#tagid)已添加到内容节点的[`cq:tags`](#tagged-content-cq-tags-property)属性，并解析为类型为` [cq:Tag](#tags-cq-tag-node-type)`的节点。

## 标记：cq：Tag节点类型  {#tags-cq-tag-node-type}

标记声明在类型为`cq:Tag`的节点的存储库中捕获。

标记可以是简单单词（例如，`sky`），也可以表示分层分类（例如，`fruit/apple`，表示通用`fruit`和更具体的`apple`）。

标记由唯一的TagID标识。

标记具有可选的中继信息，例如标题、本地化的标题和描述。 如果存在，则应在用户界面中显示标题，而不是TagID。

标记框架还提供了将作者和网站访客限制为仅使用特定的预定义标记的功能。

### 标记特征 {#tag-characteristics}

* 节点类型为`cq:Tag`n
* 节点名称是[TagID](#tagid)的组件。
* [TagID](#tagid)始终包含[命名空间。](#tag-namespace)
* `jcr:title`属性（要在UI中显示的标题）是可选的。
* `jcr:description`属性是可选的。
* 当包含子节点时，该标记称为[容器标记。](#container-tags)
* 标记存储在名为[分类根节点的基本路径下的存储库中。](#taxonomy-root-node)

由于标记只是JCR节点，因此节点名称必须遵循[JCR命名约定。](naming-conventions.md)

### 标记 ID {#tagid}

TagID标识解析为存储库中标记节点的路径。

通常，TagID是以命名空间开头的简写TagID，也可以是从[分类根节点开始的绝对TagID。](#taxonomy-root-node)

当标记内容时，如果内容尚不存在，则会将`[cq:tags](#tagged-content-cq-tags-property)`属性添加到内容节点，并将TagID添加到属性的`String`数组值。

TagID包含[命名空间](#tag-namespace)，后跟本地TagID。 [容器标记](#container-tags)具有表示分类中层次结构顺序的子标记。 子标记可用于引用与任何本地TagID相同的标记。 例如，允许使用`fruit`标记内容，即使它是一个具有子标记的容器标记，如`fruit/apple`和`fruit/banana`。

### 分类根节点 {#taxonomy-root-node}

分类根节点是存储库中所有标记的基本路径。 分类根节点不能是`cq:Tag`类型的节点。

在AEM中，基路径为`/content/cq:tags`，根节点的类型为`cq:Folder`。

### 标记命名空间 {#tag-namespace}

命名空间允许您对事物进行分组。 最典型的使用案例是每个站点的命名空间（例如，公共、内部和门户）或大型应用程序(例如，WCM、Assets、社区)。 但命名空间可用于满足各种其他需求。 命名空间在用户界面中仅用于显示适用于当前内容的标记（即特定命名空间的标记）的子集。

标记的命名空间是分类子树中的第一个级别，它是[分类根节点](#taxonomy-root-node)正下方的节点。 命名空间是`cq:Tag`类型的节点，其父项不是`cq:Tag`节点类型。

所有标记都具有命名空间。 如果未指定命名空间，则将标记分配给默认命名空间，即TagID `default`，标题为`Standard Tags`，即`/content/cq:tags/default`。

### 容器标记 {#container-tags}

容器标记是`cq:Tag`类型的节点，包含任意数量的子节点和子节点类型，因此可以使用自定义元数据增强标记模型。

此外，分类法中的容器标记（或超级标记）充当所有子标记的包含项。 例如，使用`fruit/apple`标记的内容也被视为使用`fruit`标记。 也就是说，搜索标记为`fruit`的内容也会找到标记为`fruit/apple`的内容。

### 解析标记ID {#resolving-tagids}

如果TagID包含冒号(`:`)，则冒号会将命名空间与标记或子分类分开，该标记或子分类将以斜线(`/`)进一步分隔。 如果TagID没有冒号，则默认为默认命名空间。

标记的标准且唯一位置低于`/content/cq:tags`。

引用不存在的路径或不指向`cq:Tag`节点的路径的标记被视为无效并被忽略。

下表显示了一些示例TagID、其元素以及TagID如何解析为存储库中的绝对路径：

| 标记 ID | 命名空间 | 本地Id | 容器标记 | 叶标记 | 存储库绝对标记路径 |
|---|---|---|---|---|---|
| `dam:fruit/apple/braeburn` | `dam` | `fruit/apple/braeburn` | `fruit`、`apple` | `braeburn` | `/content/cq:tags/dam/fruit/apple/braeburn` |
| `color/red` | `default` | `color/red` | `color` | `red` | `/content/cq:tags/default/color/red` |
| `sky` | `default` | `sky` | 无 | `sky` | `/content/cq:tags/default/sky` |
| `dam:` | `dam` | 无 | 无 | 无，命名空间 | `/content/cq:tags/dam` |
| `/content/cq:tags/category/car` | `category` | `car` | `car` | `car` | `/content/cq:tags/category/car` |

### 标记标题本地化 {#localization-of-tag-title}

当标记包含可选标题字符串(`jcr:title`)时，可以通过添加属性`jcr:title.<locale>`来本地化显示的标题。

有关更多详细信息，请参阅以下文档：

* 不同语言的[标记](/help/sites-developing/building.md#tags-in-different-languages)，用于说明API的使用
* [管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)，其中介绍了标记控制台的使用

### 访问控制 {#access-control}

标记作为[分类根节点](#taxonomy-root-node)下的存储库中的节点存在。 通过在存储库中设置适当的ACL，可以允许或拒绝作者和网站访客在给定的命名空间中创建标记。

此外，拒绝某些标记或命名空间的读取权限会控制将标记应用于特定内容的能力。

典型实践包括：

* 允许`tag-administrators`组/角色对所有命名空间的写入权限（在`/content/cq:tags`下添加/修改）。 此组提供开箱即用的AEM。
* 允许用户/作者读取对他们应可读取的所有命名空间（大多数是所有）的访问权限。
* 允许用户/作者写入对标记应由用户/作者自由定义的命名空间的访问权限（在`/content/cq:tags/some_namespace`下添加节点）

## 可标记的内容：cq：Taggable Mixin {#taggable-content-cq-taggable-mixin}

对于要将标记附加到内容类型的应用程序开发人员，节点的注册([CND](https://jackrabbit.apache.org/jcr/node-type-notation.html))必须包含`cq:Taggable` mixin或`cq:OwnerTaggable` mixin。

继承自`cq:Taggable`的`cq:OwnerTaggable` mixin旨在指示内容可由所有者/作者分类。 在AEM中，它只是`cq:PageContent`节点的特性。 标记框架不需要`cq:OwnerTaggable` mixin。

>[!NOTE]
>
>建议仅在聚合内容项的顶级节点（或其`jcr:content`节点）上启用标记。 示例包括：
>
>* `jcr:content`节点类型为`cq:PageContent`且包含`cq:Taggable` mixin的页面(`cq:Page`)
>* Assets (`cq:Asset`)，其中`jcr:content/metadata`节点始终具有`cq:Taggable` mixin
>

### 节点类型表示法(CND) {#node-type-notation-cnd}

节点类型定义作为CND文件存在于存储库中。 CND表示法定义为[Jackrabbit文档](https://jackrabbit.apache.org/jcr/node-type-notation.html)的一部分。

AEM中包含的节点类型的基本定义如下：

```xml
[cq:Tag] > mix:title, nt:base
    orderable
    - * (undefined) multiple
    - * (undefined)
    + * (nt:base) = cq:Tag version

[cq:Taggable]
    mixin
    - cq:tags (string) multiple

[cq:OwnerTaggable] > cq:Taggable
    mixin
```

## 标记的内容：cq：tags属性 {#tagged-content-cq-tags-property}

`cq:tags`属性是一个`String`数组，用于在作者或网站访客将一个或多个标记ID应用于内容时存储这些标记ID。 仅当添加到使用`[cq:Taggable](#taggable-content-cq-taggable-mixin)` mixin定义的节点时，属性才有意义。

>[!NOTE]
>
>要使用AEM标记功能，自定义开发的应用程序不应定义`cq:tags`以外的标记属性。

## 移动和合并标记 {#moving-and-merging-tags}

以下说明使用[标记控制台](/help/sites-administering/tags.md)移动或合并标记时在存储库中产生的效果：

* 将标记A移动或合并到`/content/cq:tags`下的标记B中时：

   * 标记A未删除，因此获取了`cq:movedTo`属性。
   * 已创建标记B（如果发生了移动）并获取`cq:backlinks`属性。

* `cq:movedTo`指向标记B。

   * 此属性表示标记A已移动或合并到标记B中。移动标记B会相应地更新此属性。 标记A因此而隐藏，并仅保留在存储库中，以解决指向标记A的内容节点中的标记ID。标记垃圾回收器会删除标记A之类的标记，内容节点不再指向这些标记。

   * `cq:movedTo`属性的特殊值为`nirvana`。 该标记在删除标记时应用，但无法从存储库中删除，因为存在必须保留带有`cq:movedTo`的子标记。

  >[!NOTE]
  >
  >只有在满足以下任一条件时，`cq:movedTo`属性才会添加到移动或合并的标记中：
  >
  >1. 标记用在内容中（这意味着它包含引用）或
  >1. 标记具有已被移动的子项。

* `cq:backlinks`将引用保留在另一个方向。 也就是说，它会保留已移至标记B或与标记B合并的所有标记的列表。在移动/合并/删除标记B以及激活标记B时，这通常需要保持`cq:movedTo`属性为最新，在这种情况下，还必须激活其所有反向链接标记。

  >[!NOTE]
  >
  >只有在满足以下任一条件时，`cq:backlinks`属性才会添加到移动或合并的标记中：
  >
  >1. 标记用在内容中（这意味着它有引用）或
  >1. 标记具有已被移动的子项。

* 读取内容节点的`cq:tags`属性涉及以下分辨率：

   1. 如果`/content/cq:tags`下没有匹配项，则不会返回任何标记。

   1. 如果标记设置了`cq:movedTo`属性，则采用引用的标记ID。

      * 只要后续标记具有`cq:movedTo`属性，就重复此步骤。

   1. 如果后续标记没有`cq:movedTo`属性，则读取该标记。

* 要在移动或合并标记时发布更改，必须复制`cq:Tag`节点及其所有反向链接。 当在标记管理控制台中激活标记时，会自动执行此操作。

* 以后更新页面的`cq:tags`属性会自动清除旧引用。 之所以会触发此事件，是因为通过API解析已移动的标记会返回目标标记，从而提供目标标记ID。

>[!NOTE]
>
>标记的移动与标记的迁移不同。

## 标记迁移 {#tags-migration}

自Adobe Experience Manager 6.4起，标记存储在`/content/cq:tags`下，而以前的版本将标记存储在`/etc/tags`下。

从6.4之前的版本升级AEM系统时，必须将标记迁移到`/content/cq:tags`。 有关详细信息，请参阅AEM 6.5[&#128279;](/help/sites-deploying/all-repository-restructuring-in-aem-6-5.md#tags)中的常见存储库重构。
