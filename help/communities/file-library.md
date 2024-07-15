---
title: 文件库功能
description: 文件库功能允许登录的网站访客上传、管理和下载文件。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# 文件库功能{#file-library-feature}

## 简介 {#introduction}

文件库功能为已登录站点访客（社区成员）提供了一个在社区站点中上传、管理和下载文件的位置。

此文档的此部分描述了：

* 向AEM站点添加文件库功能。
* `File Library`组件的配置设置。

### 将文件库添加到页面 {#adding-a-file-library-to-a-page}

要将`File Library`组件添加到创作模式下的页面，请找到该组件：

* `Communities / File Library`

并将其拖动到页面上的适当位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/essentials-file-library.md#essentials-for-client-side)时，它就是`File Library`组件的显示方式：

![file-library1](assets/file-library1.png)

### 配置文件库 {#configuring-file-library}

选择放置的`File Library`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置 — 新](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### “评论”选项卡 {#comments-tab}

在&#x200B;**备注**&#x200B;选项卡下，指定是否显示已上传文件的备注以及如何显示：

* **允许对文件进行评论**

  如果选中，则允许对已上传的文件添加注释。 默认值为未选中。

* 每页&#x200B;**条评论**

  限制每页显示的评论数和显示的回复数。 默认值为&#x200B;**10**。

* **最大文件大小**

  此值限制上传的文件大小。 默认限制为104857600 (10 MB)。

* **最大消息长度**

  可输入文本框的最大字符数。 默认值为4096个字符。

* **允许的文件类型**

  包含“点”分隔符的逗号分隔文件扩展名列表。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许指定任何文件类型。 默认值未指定，因此允许所有文件类型。

* **富文本编辑器**

  如果选中，则可以使用标记输入注释。 默认值为未选中。

* **删除评论**

  如果选中，则允许用户删除自己的注释。 默认值为选中。

* **允许标记**

  如果选中，将启用向文件添加标记的功能。 默认值为未选中。

* **允许的命名空间**

  如果选中“允许标记”，则可用标记将仅限于已勾选的命名空间。 如果未选中任何命名空间，则允许使用所有命名空间。 默认值为全部命名空间。

* **建议限制**

  如果选中“允许标记”，则此设置将限制要显示的建议标记数。 如果设置为–1，则无限制。 默认值为–1。

* **允许投票**

  如果选中，则启用投票给文件的功能。 默认值为未选中。

* **允许关注**

  如果选中，请为博客文章加入以下功能，以便成员能够[收到新帖子的通知](/help/communities/notifications.md)。 默认值为未选中。

* **启用提及功能**

  如果启用，则允许注册社区用户标识其他注册成员（使用名字、姓氏、用户名），并使用通用@user-name语法标记它们。 标记的用户会收到有关其提及的通知。

* **最大提及次数**

  限制帖子中允许的最多提及次数。 默认值为10。

* **UI提及模式**

  指定允许的模式字符串，以便在帖子中标记(@mention)已注册的用户。 例如：`~{{familyName}}{{givenName}}`。

* **允许线程回复**

  如果选中，则允许回复已发布的评论。 默认值为未选中。

#### “用户审核”选项卡 {#user-moderation-tab}

在&#x200B;**用户审核**&#x200B;选项卡下，如果允许评论，请配置审核评论：

* **预审**

  如果选中，评论必须先获得批准，然后才能显示在发布网站上。 默认值为未选中。

* **删除评论**

  如果选中，发布评论的访客可以根据需要删除评论。 默认值为选中。

* **拒绝评论**

  如果选中，则允许受信任成员审查方拒绝评论。 默认值为未选中。

* **关闭/重新打开评论**

  如果选中，则允许受信任成员审查方关闭和重新打开注释。 默认值为未选中。

* **标记评论**

  如果选中，则允许访客将评论标记为不适当。 默认值为未选中。

* **标记原因列表**

  如果选中，则允许访客从下拉列表中选择将评论标记为不适当的原因。 默认值为未选中。

* **自定义标记原因**

  如果选中，则允许访客输入将评论标记为不适当的原因。 默认值为未选中。

* **审核阈值**

  输入当访客对评论进行标记的次数达到此值后通知审查方。 默认值为一次(**1**)。

* **标记限制**

  输入在将评论从公开视图隐藏之前必须对其标记的次数。 此数字必须大于或等于&#x200B;**审核阈值**。 默认值为5。

### “排序设置”选项卡 {#sort-settings-tab}

排序依据

设置为默认

### 附加信息 {#additional-information}

更多信息可在[File Library Essentials](/help/communities/essentials-file-library.md)页面上找到开发人员。

有关审核已发布的主题和评论，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记已发布的主题和评论，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。
