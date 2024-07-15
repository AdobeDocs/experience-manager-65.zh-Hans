---
title: 在AEM应用程序中生成标记
description: 以编程方式处理自定义AEM应用程序中的标记或扩展标记
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Developing,Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# 在AEM应用程序中生成标记{#building-tagging-into-an-aem-application}

对于以编程方式使用自定义AEM应用程序中的标记或扩展标记，本页介绍如何使用

* [标记API](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

那个和

* [标记框架](/help/sites-developing/framework.md)

有关标记的相关信息，请参阅：

* [管理标记](/help/sites-administering/tags.md)，了解有关创建和管理标记以及已对哪些内容应用标记的信息。
* [使用标记](/help/sites-authoring/tags.md)以获取有关标记内容的信息。

## 标记API概述 {#overview-of-the-tagging-api}

AEM中[标记框架](/help/sites-developing/framework.md)的实施允许使用JCR API管理标记和标记内容。 TagManager确保在`cq:tags`字符串数组属性上作为值输入的标记不会重复，它会删除指向不存在标记的TagID，并更新已移动或合并标记的标记ID。 TagManager使用JCR观察侦听器来还原任何不正确的更改。 主类位于[com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html)包中：

* JcrTagManagerFactory — 返回基于JCR的`TagManager`实现。 它是标记API的参考实施。
* `TagManager` — 允许按路径和名称解析和创建标记。
* `Tag` — 定义标记对象。

### 获取基于JCR的标签管理器 {#getting-a-jcr-based-tagmanager}

要检索TagManager实例，您必须具有JCR `Session`并调用`getTagManager(Session)`：

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

在典型的Sling上下文中，您还可以从`ResourceResolver`适应`TagManager`：

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### 检索标记对象 {#retrieving-a-tag-object}

通过解析现有标记或创建现有标记，可以通过`TagManager`检索`Tag`：

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

对于基于JCR的实现（将`Tags`映射到JCR `Nodes`），如果您有资源（例如`/content/cq:tags/default/my/tag`），则可以直接使用Sling的`adaptTo`机制：

```java
Tag tag = resource.adaptTo(Tag.class);
```

虽然标记只能从*资源（而非节点）进行转换，但标记可以同时*转换*为节点和资源：

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>无法直接从`Node`调整到`Tag`，因为`Node`未实现Sling `Adaptable.adaptTo(Class)`方法。

### 获取和设置标记 {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### 搜索标记 {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>要使用的有效`RangeIterator`为：
>
>`com.day.cq.commons.RangeIterator`

### 删除标记 {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### 复制标记 {#replicating-tags}

可以将复制服务(`Replicator`)与标记一起使用，因为标记的类型为`nt:hierarchyNode`：

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## 在客户端标记 {#tagging-on-the-client-side}

表单小组件`CQ.tagging.TagInputField`用于输入标记。 它有一个弹出菜单，用于从现有标记中进行选择，包括自动完成和许多其他功能。 其xtype为`tags`。

## 标记垃圾收集器 {#the-tag-garbage-collector}

标记垃圾收集器是一种后台服务，用于清理隐藏和未使用的标记。 隐藏和未使用的标记是`/content/cq:tags`以下的标记，这些标记具有`cq:movedTo`属性，未在内容节点上使用 — 它们的计数为零。 通过使用此延迟删除流程，不必在移动或合并操作过程中更新内容节点（即`cq:tags`属性）。 在更新`cq:tags`属性时（例如，通过页面属性对话框），`cq:tags`属性中的引用将自动更新。

默认情况下，标记垃圾回收器每天运行一次。 您可以在以下位置配置它：

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## 标记搜索和标记列表 {#tag-search-and-tag-listing}

搜索标记和标记列表的工作方式如下：

* 搜索TagID将搜索属性`cq:movedTo`设置为TagID并遵循`cq:movedTo` TagID的标记。

* 搜索标记“标题”只会搜索没有`cq:movedTo`属性的标记。

## 不同语言的标记 {#tags-in-different-languages}

如有关管理标记的文档中所述，在[管理不同语言的标记](/help/sites-administering/tags.md#managing-tags-in-different-languages)部分中，可以使用不同语言定义标记`title`。 然后，将区分语言的属性添加到标记节点。 此属性的格式为`jcr:title.<locale>`，例如，法语翻译为`jcr:title.fr`。 `<locale>`必须为小写的ISO区域设置字符串，并使用“_”而不是“ — ”，例如： `de_ch`。

将&#x200B;**Animals**&#x200B;标记添加到&#x200B;**Products**&#x200B;页面时，值`stockphotography:animals`将添加到节点/content/geometrixx/en/products/jcr：content的属性`cq:tags`。 将从标记节点中引用翻译。

服务器端API具有本地化的`title`相关方法：

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle（区域设置）
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle（区域设置）
   * getTitlePath（区域设置）

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath， Locale)
   * createTagByTitle(String tagTitlePath， Locale)
   * resolveByTitle(String tagTitlePath， Locale)

在AEM中，可以从页面语言或用户语言获取语言：

* 要在JSP中检索页面语言，请执行以下操作：

   * `currentPage.getLanguage(false)`

* 要在JSP中检索用户语言，请执行以下操作：

   * `slingRequest.getLocale()`

`currentPage`和`slingRequest`可通过[&lt;cq：definedObjects>](/help/sites-developing/taglib.md)标记在JSP中使用。

对于标记，本地化取决于上下文，因为标记`titles`能够以页面语言、用户语言或任何其他语言显示。

### 向“编辑标记”对话框添加新语言 {#adding-a-new-language-to-the-edit-tag-dialog}

以下过程介绍了如何向&#x200B;**标记编辑**&#x200B;对话框添加语言（芬兰语）：

1. 在&#x200B;**CRXDE**&#x200B;中，编辑节点`/content/cq:tags`的多值属性`languages`。

1. 添加`fi_fi`（表示芬兰语言环境）并保存更改。

现在，在&#x200B;**标记**&#x200B;控制台中编辑标记时，新语言（芬兰语）在页面属性的标记对话框和&#x200B;**编辑标记**&#x200B;对话框中可用。

>[!NOTE]
>
>新语言必须是AEM认可的语言之一。 也就是说，它必须作为`/libs/wcm/core/resources/languages`下的节点提供。

>[!CAUTION]
>
>通过官方更新包（包括Service Pack、Security Service Pack、Extended Feature Pack、Cumulative Feature Pack、修补程序等）安装与标记相关的现成内容，会将`/content/cq:tags`节点的languages属性重置为默认值。 因此，在安装之前，必须从属性中添加它。
