---
title: 创建节点
description: 了解如何通过从/libs复制所需的最少文件数并在/apps中编辑它们，使用自定义版本覆盖评论系统。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3d72cbdf-5eb4-477d-aa61-035a846f7dcb
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# 创建节点 {#create-nodes}

通过将所需的最少文件数从`/libs`复制到`/apps`并在`/apps`中修改它们，使用自定义版本覆盖评论系统。

>[!CAUTION]
>
>永远不会编辑/libs文件夹的内容，因为任何重新安装或升级操作都可能会删除或替换/libs文件夹，而/apps文件夹的内容保持不变。

在创作实例上使用[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)，首先在/apps文件夹中创建一条与/libs文件夹中覆盖组件的路径相同的路径。

要复制的路径为：

* `/libs/social/commons/components/hbs/comments/comment`

路径中的某些节点是文件夹，而某些节点是组件。

1. 浏览至[http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)
1. 创建`/apps/social`（如果尚不存在）
   * 选择`/apps`节点
   * **[!UICONTROL 创建>文件夹]**
      * 输入名称： `social`
1. 选择`social`节点
   * **[!UICONTROL 创建]** > **[!UICONTROL 文件夹]**
      * 输入名称： `commons`
1. 选择`commons`节点
   * **[!UICONTROL 创建>文件夹]**
      * 输入名称： `components`
1. 选择`components`节点
   * **[!UICONTROL 创建>文件夹]**。
      * 输入名称： `hbs`
1. 选择`hbs`节点
   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件]**
      * 输入标签： `comments`
      * 输入标题： `Comments`
      * 输入描述： `List of comments without showing avatars`
      * 超级类型： `social/commons/components/comments`
      * 输入组： `Communities`
      * 单击&#x200B;**[!UICONTROL 下一步]**，直到&#x200B;**[!UICONTROL 确定]**
1. 选择`comments`节点

   * **[!UICONTROL 创建]** > **[!UICONTROL 创建组件]**

      * 输入标签： `comment`
      * 输入标题： `Comment`
      * 输入描述： `A comment instance without avatars`
      * 超级类型： `social/commons/components/comments/comment`
      * 输入组： `.hidden`
      * 单击&#x200B;**[!UICONTROL 下一步]**，直到&#x200B;**[!UICONTROL 确定]**
   * 选择&#x200B;**[!UICONTROL 全部保存]**
1. 删除默认`comments.jsp`
   * 选择节点`/apps/social/commons/components/hbs/comments/comments.jsp`
   * 选择&#x200B;**[!UICONTROL 删除]**
1. 删除默认的comment.jsp
   * 选择节点`/apps/social/commons/components/hbs/comments/comment/comment.jsp`
   * 选择&#x200B;**[!UICONTROL 删除]**
   * 选择&#x200B;**[!UICONTROL 全部保存]**

>[!NOTE]
>
>要保留继承链，将叠加组件的`Super Type`（属性`sling:resourceSuperType`）设置为与要叠加的组件的`Super Type`相同的值，在本例中为：
>
>* `social/commons/components/comments`
>* `social/commons/components/comments/comment`

叠加图自己的`Type`（属性`sling:resourceType`）必须是相对自引用，以便在/apps中未找到的任何内容随后在/libs中查找。
* 名称：`sling:resourceType`
* 类型：`String`
* 值： `social/commons/components/hbs/comments`

1. 选择绿色`[+] Add`
   * 名称：`sling:resourceType`
   * 类型：`String`
   * 值： `social/commons/components/hbs/comments/comment`
1. 选择绿色`[+] Add`
   * 选择&#x200B;**[!UICONTROL 全部保存]**

![创建节点](assets/create-nodes.png)
