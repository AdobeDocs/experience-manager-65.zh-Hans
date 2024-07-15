---
title: 使用审阅和审阅摘要（显示）
description: 了解如何将审阅和审阅摘要组件添加到页面。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# 使用审阅和审阅摘要（显示） {#using-reviews-and-reviews-summary-display}

`Reviews`组件是[注释](comments.md)和[评级](rating.md)的组合组件，可供使用。

`Reviews Summary (Display)`组件提供`Reviews`组件的活动或已关闭实例的摘要，以便在网站上的其他位置显示。

>[!NOTE]
>
>不支持评论的匿名发布。 网站访客必须注册（成为会员）并登录才能参与。 已登录的访客可随时更新其审核。

## 将审阅添加到页面 {#adding-a-review-to-a-page}

要在创作模式下将`Reviews`组件添加到页面，请使用组件浏览器找到`Communities / Reviews`并将其拖动到页面上的适当位置，例如相对于供用户查看的功能的位置。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](reviews-basics.md#essentials-for-client-side)时，`Reviews`组件的显示方式如下所示。

![create-review](assets/create-review.png)

## 配置审核 {#configuring-reviews}

选择放置的`Reviews`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置 — 新](assets/configure-new.png)

在&#x200B;**[!UICONTROL 允许的评级]**&#x200B;选项卡下，指定要向成员显示的完整评级列表。 第一个评级应为总体/综合评级，因为它是为`Review Summary (Display)`组件提供平均评级的评级。 默认配置中的后续两个评级应该使用不同的标题，而不是“子评级1”或“子评级2”。

![允许评级](assets/configure-review1.png)

* **[!UICONTROL 允许的评级]**

  成员可以选择的评级列表。

  使用向上箭头、向下箭头和删除按钮修改可见选择。

  单击&#x200B;**[!UICONTROL 添加项目]**&#x200B;以添加其他评级选择。

在&#x200B;**[!UICONTROL 必需评级]**&#x200B;选项卡下，重新输入评级所需&#x200B;**[!UICONTROL 允许评级]**&#x200B;列表中的项目。 如果仅在“允许的评级”选项卡上指定项目，则成员提交时可能会保留不标记该项目。

在网站上，必填评级标有星号。 如果某个项目是必需的且未标记，则会向该成员显示一条消息，并且在标记所有必需的评级之前，将拒绝提交。

![要求评级](assets/configure-review2.png)

* **[!UICONTROL 必需的评级]**

  允许的评级子集，指示所需的评级。

  使用向上箭头、向下箭头和删除按钮修改可见选择。

  单击&#x200B;**[!UICONTROL 添加项]**&#x200B;以添加其他响应选择。

>[!NOTE]
>
>如果在&#x200B;**[!UICONTROL 必需评级]**&#x200B;选项卡上输入的项未在&#x200B;**[!UICONTROL 允许的评级]**&#x200B;选项卡上指定，则该项不包括在要评级的项中。

在&#x200B;**[!UICONTROL 审核]**&#x200B;选项卡下，指定审核的处理方式。

![个评论](assets/configure-review3.png)

* **[!UICONTROL 允许回复]**

  如果选中，则允许回复审核。 默认值为未选中。

* **[!UICONTROL 已关闭]**

  如果选中，则对于新审阅和回复将关闭审阅。 默认值为未选中。

* **[!UICONTROL 允许文件上传]**

  如果选中，则允许上载文件附件以供审阅。 默认值为未选中。

* **最大文件大小**

  仅在选中&#x200B;**[!UICONTROL 允许文件上传]**&#x200B;时才相关。 此字段限制已上传文件的大小（以字节为单位）。 默认值为10 MB。

* **[!UICONTROL 最大消息长度]**

  可输入文本框的最大字符数。 默认值为4096个字符。

* **[!UICONTROL 允许的文件类型]**

  仅在选中&#x200B;**[!UICONTROL 允许文件上传]**&#x200B;时才相关。 包含“点”分隔符的逗号分隔文件扩展名列表。 例如，.jpg、.jpeg、.png、.doc、.docx、.pdf。 如果指定了任何文件类型，则不允许使用未指定的文件类型。 默认值为无指定以便允许所有文件类型。

* **[!UICONTROL 富文本编辑器]**

  如果选中，则可以使用标记输入帖子。 默认值为未选中。

* **[!UICONTROL 允许投票]**

  如果选中，请为主题加入投票功能。 默认值为未选中。

在&#x200B;**[!UICONTROL 用户审核]**&#x200B;选项卡下，指定如何管理已发布的审核。 有关详细信息，请参阅[审核用户生成的内容](moderate-ugc.md)。

![用户审核](assets/configure-review4.png)

* **[!UICONTROL 预审]**

  如果选中，审阅必须先获得批准，然后才能显示在发布网站上。 默认值为未选中。

* **[!UICONTROL 删除审核]**

  如果选中，则发布评论的成员可以将其删除。 默认值为未选中。

* **[!UICONTROL 拒绝审核]**

  如果选中，则允许审查方拒绝审核。 默认值为未选中。

* **[!UICONTROL 关闭/重新打开审核]**

  如果选中，则允许审查方关闭和重新打开审核。 默认值为未选中。

* **[!UICONTROL 标记审核]**

  如果选中，则允许成员将审核标记为不适当。 默认值为未选中。

* **[!UICONTROL 标记原因列表]**

  如果选中，则允许成员从下拉列表中选择将审核标记为不适当的原因。 默认值为未选中。

* **[!UICONTROL 自定义标记原因]**

  如果选中，则允许成员输入自己的原因以将审阅标记为不适当。 默认值为未选中。

* **[!UICONTROL 审核阈值]**

  输入在通知审查方之前，成员必须标记审阅的次数。 默认值为一次(1)。

* **[!UICONTROL 标记限制]**

  输入在将审阅从公开视图隐藏之前必须将其标记的次数。 此数字必须大于或等于&#x200B;**[!UICONTROL 审核阈值]**。 默认值为5。

### 向页面添加审核摘要（显示） {#adding-a-review-summary-display-to-a-page}

要将`Reviews Summary (Display)`组件添加到创作模式下的页面，请找到该组件

* `Communities / Reviews Summary (Display)`

并将其拖动到要显示活动或已关闭审阅摘要的页面上。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](reviews-basics.md#essentials-for-client-side)时，`Reviews Summary (Display)`组件的显示方式如下所示。

![审核摘要](assets/configure-review5.png)

>[!NOTE]
>
>“平均值”反映所汇总审阅的“允许的评级”选项卡上列出的第一个项目的投票数。

### 配置审阅摘要（显示） {#configuring-reviews-summary-display}

选择放置的`Reviews Summary (Display)`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置](assets/configure-new.png)

在&#x200B;**[!UICONTROL 审核摘要]**&#x200B;选项卡下

![审核摘要](assets/configure-review6.png)

* `Review Path`

  输入或浏览到`reviews`组件所放置的实例，这样您便可以总结出，例如，如果添加到[Geometrixx参与网站](getting-started.md)的网页，路径将为：

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  如果选中，则显示一个条形图，指示所总结的评论中有多少星级。 默认值为未选中。

### 更改为自定义审核类型 {#changing-to-a-custom-review-type}

审阅组件使用注释系统。

通过更改“注释资源类型”，注释系统不再使用缺省值生成注释的实例，而是由开发人员自定义（扩展）的实例。

当自定义资源类型已知时，输入[设计模式](../../help/sites-authoring/default-components-designmode.md)并双击放置的`Comments`组件以打开带有附加选项卡的对话框。

在&#x200B;**[!UICONTROL 资源类型]**&#x200B;选项卡下，为`Comments or Voting`组件的新实例指定自定义resourceType：

![评论投票](assets/configure-review7.png)

* **[!UICONTROL 评论资源类型]**

  导航到/apps中扩展`comment`组件的resourceType（单个注释）。 例如：`/apps/social/commons/components/hbs/comments/comment`。

  此资源标识访客发表评论时创建的UGC的resourceType。

* **[!UICONTROL 投票资源类型]**

  导航到/apps中扩展`voting`组件的resourceType。 例如：`/apps/social/components/hbs/voting`。

  此资源标识访客发表投票时创建的UGC的资源类型。

* **[!UICONTROL 注释系统资源类型]**

  导航到/apps中的扩展`comments`组件（注释系统）的resourceType。 留空，除非页面模板[在基础脚本中动态包含](scf.md#add-or-include-a-communities-component)注释系统，而不是作为资源（注释节点）添加到页面。 通过阅读有关[`{{include}}`帮助程序](handlebars-helpers.md#include)的信息了解详情。

## 网站访客体验 {#site-visitor-experience}

### 审查方和管理员 {#moderators-and-administrators}

当登录用户具有审阅人或管理员权限时，无论审阅的作者是谁，他们都能执行组件配置所允许的审阅任务。

### 成员 {#members}

当网站访客登录时，根据配置，他们可能：

* Post新审核
* 编辑他们自己的审核
* 删除他们自己的审核
* 标记其他人的审核评论

每个成员只允许一个评级。 会员可以随时变更等级。

### 匿名 {#anonymous}

未登录的网站访客只能读取已发布的评论，如果支持的话，可以翻译这些评论，但不得添加评级或评论，也不得标记其他人的评论意见。

## 附加信息 {#additional-information}

可在面向开发人员的[Review Essentials](reviews-basics.md)页面上找到更多信息。

有关审核已发布的评论，请参阅[审核用户生成的内容](moderate-ugc.md)。

有关已发布评论的翻译，请参阅[翻译用户生成的内容](translate-ugc.md)。
