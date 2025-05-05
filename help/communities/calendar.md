---
title: 日历功能
description: 了解日历功能如何以日历格式提供社区活动信息。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# 日历功能 {#calendar-feature}

## 简介 {#introduction}

日历功能支持以日历格式向所有站点访客或仅登录站点访客（社区成员）提供社区事件信息，而只有授权成员才能添加事件。

文档的此部分描述

* 将日历功能添加到AEM站点
* `Calendar`组件的配置设置

## 向页面添加日历 {#adding-a-calendar-to-a-page}

要将`Calendar`组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Calendar`

并将其拖动到页面上的适当位置，例如相对于要供用户查看的功能的位置。

有关必要的信息，请访问[社区组件基础知识](/help/communities/basics.md)。

当包含[所需的客户端库](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side)时，`Calendar`组件的显示方式如下所示。

![日历组件](assets/calendar-component.png)

### 配置日历 {#configuring-calendar}

选择放置的`Calendar`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

![配置 — 日历](assets/configure-calendar1.png)

#### “设置”选项卡 {#settings-tab}

在&#x200B;**设置**&#x200B;选项卡下，指定是否允许将标记应用于日历条目。

* 每页&#x200B;**个事件**

  定义每页显示的事件数。 默认值为10。

* **已审核**

  如果选中，则必须先批准发布日历事件和评论，然后才能将其显示在发布网站上。 默认值为未选中。

* **已关闭**

  如果选中，则日历将针对新的事件条目和注释关闭。 默认值为未选中。

* **富文本编辑器**

  如果选中，则可以使用标记输入日历事件和注释。 默认值为选中。

* **允许标记**

  如果选中，则允许成员向其发布的事件添加标记标签（请参阅&#x200B;**标记字段**&#x200B;选项卡）。 默认值为选中。

* **允许文件上传**

  如果选中，则允许将文件附件添加到日历事件或注释中。 默认值为选中。

* **允许关注**

  如果选中，则允许成员关注发布到日历中的事件。 默认值为选中。

* **最大文件大小**

  仅在选中`Allow File Uploads`时才相关。 此字段限制已上传文件的大小（以字节为单位）。 默认值为104857600 (10 Mb)。

* **允许的文件类型**

  仅在选中`Allow File Uploads`时才相关。 包含“点”分隔符的逗号分隔文件扩展名列表。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则无法上载未指定的文件类型。 默认值为无指定以便允许所有文件类型。

* **附加图像文件大小上限**

  仅在选中允许文件上传时才相关。 上传的图像文件可以包含的最大字节数。 默认值为2097152 **&#x200B; &#x200B;**(2 Mb)。

* **允许的封面图像类型**

  以“点”分隔符分隔的图像文件扩展名列表。 默认值为`.jpg,.jpeg,.png,.gif,.bmp`。

* **允许线程回复**

  如果选中，则允许对发布到日历事件的评论进行回复。 默认值为选中。

* **允许用户删除评论和活动**

  如果选中，则允许成员删除他们发布的评论和日历事件。 默认值为选中。

* **允许投票**

  如果选中，请将“投票”功能与日历事件包含在内。 默认值为选中。

* **显示痕迹导航**

  在事件页面上显示痕迹导航。 默认值为选中。

* **日期范围筛选器**

  定义添加到当前日期的天数，以计算日历事件列表页面过滤器的“到”值。 默认数字为30。

* **允许精选内容**

  如果选中，该创意可标识为[精选内容](/help/communities/featured.md)。 默认值为未选中。

在&#x200B;**用户审核**&#x200B;选项卡下，指定如何管理发布的主题和回复（用户生成的内容）。 有关详细信息，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

#### “用户审核”选项卡 {#user-moderation-tab}

* **拒绝帖子**

  如果选中，则允许受信任的成员版主拒绝帖子，并阻止帖子出现在公共论坛中。 默认值为选中。

* **关闭/重新打开事件**

  如果选中，受信任成员审查方可以关闭事件以进一步编辑和注释，也可以重新打开事件。 默认值为选中。

* **标记帖子**

  如果选中，则允许成员将其他人的活动或评论标记为不适当。 默认值为选中。

* **标记原因列表**

  如果选中，则允许成员从下拉列表中选择将事件或评论标记为不适当的原因。 默认值为未选中。

* **自定义标记原因**

  如果选中，则允许成员输入他们自己的将事件或评论标记为不适当的原因。 默认值为未选中。

* **审核阈值**

  输入在通知审查方之前，事件或评论必须由成员标记的次数。 默认值为1（一次）。

* **标记限制**

  输入在将事件或评论从公开视图隐藏之前必须对其标记的次数。 如果设置为–1，则标记的主题或评论永远不会从公共视图中隐藏。 否则，此数字必须大于或等于审核阈值。 默认值为5。

#### “标记字段”选项卡 {#tag-field-tab}

在&#x200B;**标记字段**&#x200B;选项卡下，如果允许在&#x200B;**设置**&#x200B;选项卡下应用，则可能应用的标记将根据所选的命名空间而受限。

* **允许的命名空间**

  如果在&#x200B;**设置**&#x200B;选项卡下选中`Allow Tagging`，则相关。 可以应用的标记仅限于所选命名空间类别中的标记。 命名空间列表包括“标准标记”（默认命名空间）和“包括所有标记”。 默认设置为“无”复选框，这意味着允许使用所有命名空间。

* **建议限制**

  输入要显示为向论坛发布成员建议的标记数。 默认值为&#x200B;**-**&#x200B;1（无限制）。

>[!NOTE]
>
>访问[管理标记](/help/sites-administering/tags.md)，了解如何添加标记命名空间（分类）。

#### “翻译”选项卡 {#translation-tab}

在&#x200B;**翻译**&#x200B;选项卡下，如果为社区站点启用了翻译，则可以将翻译设置为翻译整个线程（事件和评论）而不是特定帖子。

* **全部翻译**

  如果选中，事件和注释将转换为用户的首选语言。 默认值为选中。

## 网站访客体验 {#site-visitor-experience}

在发布环境中，日历功能会显示一个搜索字段，其中包含默认日期范围以及属于该范围的任何日历事件。

选择日历事件后，将显示日历事件详细信息、说明和注释。

其他功能取决于网站访客是审查方、管理员、社区成员、拥有权限的成员还是匿名用户。

### 审查方和管理员 {#moderators-and-administrators}

当登录用户具有审阅人或管理员权限时，他们能够对发布到事件的所有日历事件和评论执行[审阅任务](/help/communities/moderate-ugc.md)（组件配置所允许）。

![审查方 — 视图](assets/moderators-view.png)

#### 成员 {#members}

当登录用户是社区成员或[特权成员](/help/communities/users.md#privileged-members-group)（取决于配置）时，他们能够选择`New Event`以创建和发布新的日历事件。

具体而言，他们可以：

* 创建日历事件
* Post日历事件的评论
* 编辑他们自己的日历事件或评论
* 删除他们自己的日历事件或评论
* 标记其他人的日历事件或评论

![create-event](assets/configure-calendar2.png)

![事件帖子](assets/configure-calendar3.png)

#### 匿名 {#anonymous}

未登录的网站访客只能读取发布的日历事件，如果支持则进行翻译，但不得添加事件或评论，也不得标记其他人的事件或评论。

![anonymous-user-view](assets/anonymous-user-view1.png)

## 附加信息 {#additional-information}

可在面向开发人员的[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)页面上找到更多信息。

有关审核日历事件和评论的信息，请参阅[审核用户生成的内容](/help/communities/moderate-ugc.md)。

有关标记日历事件和评论的信息，请参阅[标记用户生成的内容](/help/communities/tag-ugc.md)。

有关日历事件和注释的翻译，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。
