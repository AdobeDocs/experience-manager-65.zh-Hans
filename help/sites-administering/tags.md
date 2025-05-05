---
title: 管理标记
description: 了解如何在Adobe Experience Manager中管理标记。
contentOwner: Chiradeep Majumdar
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: content
content-type: reference
exl-id: ff041ef0-e566-4373-818e-76680ff668d8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 7%

---

# 管理标记 {#administering-tags}

标记是用于对网站中的内容进行分类的简单快捷方法。它们可以被视为关键字或标签（元数据），从而允许更快地找到作为搜索结果的内容。

在Adobe Experience Manager (AEM)中，标记可以是

* 页面的内容节点（请参阅[使用标记](/help/sites-authoring/tags.md)）

* 资源的元数据节点(请参阅[管理数字Assets的元数据](/help/assets/metadata.md))

除了页面和资源之外，标记还用于AEM Communities功能

* 用户生成的内容（请参阅[标记UGC）](/help/communities/tag-ugc.md)

* 启用资源（请参阅[标记启用资源](/help/communities/functions.md#catalog-function)）

## 标记功能 {#tag-features}

AEM中标记的部分功能包括：

* 标记可以分组到各种命名空间中。 此类层次结构允许构建分类。 这些分类在整个 AEM 中是全局性的。
* 新创建标记的主要限制是，它们必须在特定命名空间中是唯一的。
* 标记的标题不应包含标记路径分隔字符（如果存在，也不会显示）

   * 冒号`:` — 分隔命名空间标记
   * 正斜杠`/` — 分隔子标记

* 标记可由作者和网站访客应用。 在分配给页面或进行搜索时，所有形式的标记都可供选择，而无论标记创建者如何。
* “tag-administrators”组的成员以及对`/content/cq:tags`具有修改权限的成员可以创建标记并修改其分类。

   * 包含子标记的标记称为容器标记
   * 不是容器标记的标记称为叶标记
   * 标记命名空间是叶标记或容器标记

* 标记由[搜索组件](https://helpx.adobe.com/experience-manager/core-components/using/quick-search.html)使用，以便于查找内容。
* 标记由[Teaser组件](https://helpx.adobe.com/experience-manager/core-components/using/teaser.html)使用，该组件监视用户的标记云以提供目标内容。
* 如果标记是内容的一个重要方面

   * 确保将标记与使用它们的页面一起打包
   * 确保[标记权限](#setting-tag-permissions)启用读取访问权限

## 标记控制台 {#tagging-console}

“标记”控制台用于创建和管理标记及其分类。 一个目标是避免有许多与基本相同的内容相关的类似标记：例如，页面和页面或鞋和鞋。

标记的管理方法是：分组到命名空间，在创建新标记之前查看现有标记的使用情况，以及在不中断标记与当前引用内容之间的连接的情况下重新组织。

要访问“标记”控制台，请执行以下操作：

* 在作者上
* 使用管理权限登录
* 从全局导航

   * 选择&#x200B;**`Tools`**
   * 选择&#x200B;**`General`**
   * 选择&#x200B;**`Tagging`**

![managing_tags_usingthetagasministrationconsole](assets/managing_tags_usingthetagasministrationconsolea.png)

### 创建命名空间 {#creating-a-namespace}

要创建命名空间，请选择&#x200B;**`Create Namespace`**&#x200B;图标。

命名空间本身是一个标记，不包含任何子标记。 但是，要继续创建分类，请[创建子标记](#creating-tags)，这些子标记又可能是叶标记或容器标记。

![chlimage_1-183](assets/chlimage_1-183a.png) ![creating_tags_andnamespaces](assets/creating_tags_andnamespacesa.png)

* **标题**
  *（必需）*&#x200B;命名空间的显示标题。

* **名称**
  *（可选）*&#x200B;命名空间的名称。 如果未指定，则从标题创建有效的节点名称。 请参阅 [TagID](/help/sites-developing/framework.md#tagid)。

* **描述**
  *（可选）*&#x200B;命名空间的描述。

输入所需信息后

* 选择&#x200B;**创建**

### 标记操作 {#operations-on-tags}

选择命名空间或其他标记后，便可执行以下操作：

* [查看属性](#viewing-tag-properties)
* [引用](#showing-tag-references)
* [创建标记](#creating-tags)
* [编辑](#editing-tags)
* [移动](#moving-tags)
* [合并](#merging-tags)
* [发布](#publishing-tags)
* [取消发布](#unpublishing-tags)
* [删除](#deleting-tags)

![chlimage_1-184](assets/chlimage_1-184.png)

如果浏览器窗口不够宽，无法显示所有图标，则最右侧的图标将分组在&#x200B;**`... More`**&#x200B;图标下，该图标将在选中时显示隐藏操作图标的下拉列表。

![chlimage_1-185](assets/chlimage_1-185.png)

### 选择命名空间标记 {#selecting-a-namespace-tag}

在首次选中时，如果命名空间不包含任何标记，则属性将显示在右侧，否则子标记将显示。 所选的每个标记都会显示它所包含的标记，如果没有子标记，则会显示其属性。

要选择操作的标记，并多选，请仅选择标题旁边的图标。 选择标题将仅显示属性或打开标记以显示其内容。

![chlimage_1-186](assets/chlimage_1-186.png) ![chlimage_1-187](assets/chlimage_1-187.png)

### 查看标记属性 {#viewing-tag-properties}

![chlimage_1-188](assets/chlimage_1-188.png)

选择命名空间或其他标记后，选择&#x200B;**`View Properties`**&#x200B;图标将会显示有关`name`、上次编辑时间和引用数量的信息。 如果发布，则显示上次发布时间和发布者的ID。 此信息将显示在标记列左侧的列中。

![chlimage_1-189](assets/chlimage_1-189.png)

### 显示标记引用 {#showing-tag-references}

![chlimage_1-190](assets/chlimage_1-190.png)

选择命名空间或其他标记后，选择&#x200B;**引用**&#x200B;图标将标识已应用标记的内容。

初始显示是应用的标记计数。

![chlimage_1-191](assets/chlimage_1-191.png)

通过选择计数右侧的箭头，将列出参照名称。

将鼠标悬停在参照上时，参照的路径会显示为工具提示。

![chlimage_1-192](assets/chlimage_1-192.png)

### 创建标记 {#creating-tags}

![chlimage_1-193](assets/chlimage_1-193.png)

选择命名空间或其他标记（通过选择标题旁边的图标）时，可以通过选择&#x200B;**`Create Tag`**&#x200B;图标为当前标记创建子标记。

![chlimage_1-194](assets/chlimage_1-194.png)

* **标题**
*（必需） *标记的显示标题。

* **名称**
*（可选） *标记的名称。 如果未指定，则从标题创建有效的节点名称。 请参阅 [TagID](/help/sites-developing/framework.md#tagid)。

* **描述**
*（可选） *标记的描述。

输入所需信息后

* 选择&#x200B;**创建**

### 编辑标记 {#editing-tags}

![chlimage_1-195](assets/chlimage_1-195.png)

选择命名空间或其他标记后，可以通过选择&#x200B;**`Edit`**&#x200B;图标来更改标题、描述并提供标题的本地化设置。

进行编辑后，选择&#x200B;**保存**。

有关添加语言翻译的详细信息，请参阅[管理不同语言的标记](#managing-tags-in-different-languages)部分。

![chlimage_1-196](assets/chlimage_1-196.png)

### 移动标记 {#moving-tags}

![chlimage_1-197](assets/chlimage_1-197.png)

选择命名空间或其他标记后，选择&#x200B;**`Move`**&#x200B;图标将允许标记管理员和开发人员通过将标记移动到新位置或重命名标记来清理分类。 当所选标记是容器标记时，移动该标记也会移动所有子标记。

>[!NOTE]
>
>建议仅允许作者[编辑](#editing-tags)标记的`title`，而不允许移动或重命名标记。

![chlimage_1-198](assets/chlimage_1-198.png)

* **路径**
  *（只读）*&#x200B;选定标记的当前路径。

* **移至**
浏览到要在其中移动标记的新路径。

* **重命名为**
最初显示标记的当前`name`。 可以输入新的`name`。

* 选择&#x200B;**保存**

### 合并标记 {#merging-tags}

![chlimage_1-199](assets/chlimage_1-199.png)

当分类具有重复项时，可以使用合并标记。 当标记A合并到标记B时，所有使用标记A标记的页面都将使用标记B标记，并且标记A不再可用于作者。

选择命名空间或其他标记后，选择&#x200B;**合并**&#x200B;图标将打开一个面板，您可以在该面板中选择要合并到的路径。

![chlimage_1-200](assets/chlimage_1-200.png)

* **路径**
  *（只读）*&#x200B;选定要合并到其他标记的标记的路径。

* **合并到**
浏览以选择要合并到的标记的路径。

>[!NOTE]
>
>合并后，最初选择的&#x200B;**路径**&#x200B;将（实际上）不再存在。
>
>移动或合并引用的标记时，不会实际删除该标记，因此可以保留引用。

### 发布标记 {#publishing-tags}

![chlimage_1-201](assets/chlimage_1-201.png)

选择命名空间或其他标记后，选择&#x200B;**Publish**&#x200B;图标以在发布环境中激活该标记。 与页面内容类似，仅发布选定的标记，无论其是否为容器标记。

要发布分类（命名空间和子标记），最佳做法是创建命名空间的[包](/help/sites-administering/package-manager.md)（请参阅[分类根节点](/help/sites-developing/framework.md#taxonomy-root-node)）。 确保在创建包之前[将权限](#setting-tag-permissions)应用于命名空间。

### 取消发布标记 {#unpublishing-tags}

![chlimage_1-202](assets/chlimage_1-202.png)

选择命名空间或其他标记后，选择&#x200B;**取消发布**&#x200B;图标将在创作环境中取消激活该标记，并将其从发布环境中移除。 与`Delete`操作类似，如果所选标记是容器标记，则其所有子标记将在创作环境中停用，并从发布环境中移除。

### 删除标记 {#deleting-tags}

![chlimage_1-203](assets/chlimage_1-203.png)

选择命名空间或其他标记后，选择&#x200B;**删除**&#x200B;图标将从创作环境中永久移除该标记。 如果标记已发布，也会将其从发布环境中删除。如果所选标记是容器标记，则也将移除其所有子标记。

## 设置标记权限 {#setting-tag-permissions}

标记权限是[&#39;安全的（默认情况下）&#39;](/help/sites-administering/production-ready.md)；这是发布环境的最佳实践，它要求明确允许对标记具有读取权限。 基本上，这是通过在创作上设置权限后创建标记命名空间包，并在所有发布实例上安装该包来完成的。

* 在创作实例上

   * 使用管理权限登录
   * 访问[安全控制台](/help/sites-administering/security.md#accessing-user-administration-with-the-security-console)，

      * 例如，浏览到http://localhost:4502/useradmin

   * 在左窗格中，选择要为其授予[读取权限](/help/sites-administering/security.md#permissions)的组（或用户）
   * 在右侧窗格中，找到标记命名空间的&#x200B;**Path**

      * 例如，`/content/cq:tags/mycommunity`

   * 在&#x200B;**读取**&#x200B;列中选择`checkbox`
   * 选择&#x200B;**保存**

![chlimage_1-204](assets/chlimage_1-204.png)

* 确保所有发布实例都具有相同的权限

   * 一种方法是在“作者”上[创建命名空间包](/help/sites-administering/package-manager.md#package-manager)

      * 在`Advanced`选项卡上，为`AC Handling`选择`Overwrite`

   * 复制包

      * 从包管理器中选择`Replicate`

## 管理不同语言的标记 {#managing-tags-in-different-languages}

标记的`title`属性可以翻译成多种语言。 一旦翻译，可以根据用户语言或页面语言显示相应的标记`title`。

### 定义多种语言的标记标题 {#defining-tag-titles-in-multiple-languages}

以下介绍如何将&#x200B;**Animals**&#x200B;标记的`title`从英语翻译为德语和法语。

首先，选择&#x200B;**Stock Photography**&#x200B;命名空间下的标记，然后选择&#x200B;**`Edit`**&#x200B;图标（请参阅[编辑标记](#editing-tags)部分）。

通过“编辑标记”面板，可以选择标记标题将本地化的语言。

选择每种语言后，将出现一个文本输入框，可在其中输入翻译的标题。

输入所有翻译后，选择&#x200B;**保存**&#x200B;以退出编辑模式。

![chlimage_1-205](assets/chlimage_1-205.png)

通常，为标记选择的语言在可用时从页面语言中获取。 在其他情况下（例如，在表单或对话框中）使用[`tag`小组件](/help/sites-developing/building.md#tagging-on-the-client-side)时，标记语言取决于上下文。

“标记”控制台不使用页面语言设置，而是使用用户语言设置。 在“标记”控制台中，对于“Animals”标记，会向在其用户属性中将语言设置为法语的用户显示“Animaux”。

要向对话框添加新语言，请参阅[向编辑标记对话框添加新语言](/help/sites-developing/building.md#adding-a-new-language-to-the-edit-tag-dialog)。

>[!NOTE]
>
>标准页面组件中的标记云和meta关键字根据页面语言使用本地化的标记`titles`（如果可用）。

## 资源 {#resources}

* [为开发人员添加标记](/help/sites-developing/tags.md)

  有关标记框架和扩展以及在自定义应用程序中包括标记的信息。

* [经典UI标记控制台](/help/sites-administering/classic-console.md)
