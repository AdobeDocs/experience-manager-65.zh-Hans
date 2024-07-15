---
title: 审核社区内容
description: 了解如何审核用户生成的内容，以便您能够识别积极的贡献并限制消极的贡献，例如垃圾邮件和辱骂性语言。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 2%

---

# 审核社区内容 {#moderating-community-content}

## 概述 {#overview}

社区内容，也称为用户生成内容(UGC)，是在成员（登录网站访客）通过与以下社区组件之一交互而发布已发布社区网站中的内容时创建的：

* [博客](/help/communities/blog-feature.md)：成员发表博客文章或评论。
* [日历](/help/communities/calendar.md)：成员发布日历事件或评论。
* [评论](/help/communities/comments.md)：成员发布评论或回复评论。

* [论坛](/help/communities/forum.md)：成员发布新主题或回复主题。
* [构思](/help/communities/ideation-feature.md)：成员发布构思或评论。
* [QnA](/help/communities/working-with-qna.md)：成员创建问题或回答问题。
* [评论](/help/communities/reviews.md)：成员在对项目进行评级时发布评论。

审核UGC对于识别积极贡献和限制消极贡献（例如垃圾邮件和辱骂语言）很有用。 UGC可以从多个环境中审核：

* [社区内容存储](working-with-srp.md)

* [批量审核控制台](moderation.md)

  公共环境中的管理员和[社区审查方](/help/communities/users.md)以及创作环境中的管理员可以访问审查控制台。 当社区内容存储在[公用存储](/help/communities/working-with-srp.md)中时，这是可能的。

* [上下文审核](in-context.md)

  Publish环境中的审核可由管理员和社区审查方直接在发布内容的页面上执行。

## 审核操作 {#moderation-actions}

可以对发布内容(UGC)执行的操作因用户身份和环境而异。 下表使用以下术语根据用户身份描述各种角色：

* `Admin`

  是[community-administrators](users.md)组成员的用户。

* `Moderator`

  [社区审查方](users.md#publishenvironmentusersandgroups)组的成员（具有[审查方权限](in-context.md#moderatorpermissions)）。

* `Creator`

  发布内容的用户。

* `Member`

  没有特殊权限的登录用户。

* `Visitor`

  匿名用户。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>管理员</strong></td>
   <td><strong>审查方</strong></td>
   <td><strong>创建者</strong></td>
   <td><strong>会员</strong></td>
   <td><strong>访客</strong></td>
   <td><strong>事件<br />已触发</strong></td>
   <td><strong>已预审</strong></td>
  </tr>
  <tr>
   <td><strong>编辑/<br />删除</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>剪切</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>拒绝</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>关闭/<br />重新打开</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>标记/<br />取消标记</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>允许</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### 编辑/删除 {#edit-delete}

发布帖子后，创建者、管理员或社区审查方可以编辑或删除帖子。

删除UGC时，它会从存储库中删除，并且可能无法恢复。

### 剪切 {#cut}

管理员或社区审查方可以将一个或多个论坛主题或QnA问题从一个位置移动到另一个位置。 这包括从一个社区站点到另一个社区站点，前提是同一成员在两个站点上具有审核权限。

通过选择“剪切”操作，内容将被复制到剪贴板。 可以将多个帖子作为一个组复制并移动到新位置。

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

在其他位置，当内容显示在剪贴板中时，新Post旁边会显示一个“粘贴”按钮，其中包含一个数字，用于标识将要粘贴的帖子数量。 “粘贴”按钮包括一个用于清除剪贴板而不是粘贴的选项。

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### 拒绝 {#deny}

审查方可能不允许在发布的网站上显示UGC。 对于管理员和社区审查方，该帖子仍可用，并标记为垃圾邮件。

### 关闭/重新打开 {#close-reopen}

“关闭”操作在整个对话会话（论坛主题或初始评论）中运行，并包括所有后续帖子或回复。

关闭后，不仅无法进一步回复，还不允许执行审核操作。

要执行任何操作，必须重新打开主题或注释。

管理员或社区审查方可能会执行关闭/重新打开操作。

### 标记/取消标记 {#flag-unflag}

标记是任何登录成员（内容创建者除外）用于指示帖子内容存在问题的一种方式。 标记后，会显示取消标记图标，允许同一成员取消标记内容。

可以将上下文审核配置为允许成员在标记帖子时选择原因。 可选择的标志原因列表是可配置的，包括是否可以输入自定义原因。 标记原因会与UGC一起保存，但不会触发任何特定操作。 只有标记的数量会触发通知。 已标记的内容将进行相应的批注，以便审查方可以对其进行处理。

系统将跟踪所有已标记的标记以及标记原因，并在达到阈值时发送事件。 如果社区审查方允许UGC，则会存档这些标记。 在允许并存档之后，如果存在后续标记，则会将其存档，就像之前没有标记一样。

### 允许 {#allow}

对于已标记、已拒绝或未在预审核系统中审批的UGC，允许操作是一个选项。 允许操作会清除任何存在的已标记或已拒绝/垃圾邮件状态，并存档任何已标记的数据。

## 常见的审核概念 {#common-moderation-concepts}

### 预审 {#premoderation}

预审UGC时，帖子只有在获得审核操作批准之后才会显示在已发布的网站上。 在创建[社区站点](/help/communities/sites-console.md)期间，选中[内容已预审](sites-console.md#moderation)框将启用整个站点的预审。 将组件放在页面上时，可以使用其“编辑”对话框中的设置将支持审核的组件配置为预审：

* [评论](comments.md)和[评论](reviews.md)
在**[!UICONTROL 用户审核]** > **[!UICONTROL 预审核]**&#x200B;中。

* [论坛](/help/communities/forum.md)、[构思](/help/communities/ideation-feature.md)、[问题与解答](/help/communities/working-with-qna.md)和[日历](/help/communities/calendar.md)
在**[!UICONTROL 设置]** > **[!UICONTROL 已审核]**&#x200B;中。

### 垃圾邮件检测 {#spam-detection}

垃圾邮件检测是一种自动审核功能，它通过将用户生成的提交内容标记为垃圾邮件来过滤掉这些不想要的内容。 一旦启用，它就根据预先配置的垃圾邮件词语集合来识别用户生成的内容是否为垃圾邮件。 默认垃圾邮件词位于

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`。

但是，若要自定义或扩展默认垃圾邮件，请在/apps目录中创建一组包含[叠加](/help/communities/overlay-comments.md)的默认垃圾邮件的单词。

用户生成的包含垃圾邮件词的帖子（涵盖所有内容类型，例如，博客、论坛和评论）在帖子上方标有“此帖子被分类为垃圾邮件”文本。

审查方可以查看此类帖子并标记它们，以允许或拒绝在网站上显示。 可以在上下文中或通过批量审核UI对这些帖子执行审核操作。

![垃圾邮件检测](assets/spamdetection.png)

要启用垃圾邮件检测引擎，请执行以下步骤：

1. 转到`/system/console/configMgr`打开[Web控制台](https://localhost:4502/system/console/configMgr)。

1. 找到&#x200B;**AEM Communities自动审核**&#x200B;配置并对其进行编辑。
1. 添加&#x200B;**[!UICONTROL SpamProcess]**&#x200B;条目。

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>垃圾邮件检测仅针对英语区域设置实施。

### 情绪 {#sentiment}

情绪是根据帖子(UGC)中存在的正关键字和负关键字（[关注词](#configuringwatchwords)）的数量计算的。

情感分析使用一组预先配置的规则并计算UGC的情感。 默认规则位于`/libs/cq/workflow/components/workflow/social/sentiments/rules`。

规则生成的值介于1（所有负值，无正字）到10（所有正值，无负字）之间。 情绪值为5表示中性情绪，此值是默认值。

/libs组件中定义的规则包括：

* 规则1：如果没有正词和至少一个负词，则将值设置为1。
* 规则2：如果没有负词和至少一个正词，则将值设置为10。
* 规则3：如果负面字多于负面字数，则将值设置为3。
* 规则4：如果正词多于负词，则将值设置为8。

要覆盖或添加规则，请在/apps目录中按照默认规则的结构创建一组规则。 编辑情绪配置，以便识别规则的位置。

分析完毕后，该情绪将与UGC一起存储。

在[批量审核控制台](/help/communities/moderation.md)中，可以根据情绪是负面、中性还是正面筛选和查看UGC。

#### 标语 {#watchwords}

AEM Communities提供&#x200B;*关注字分析器*&#x200B;作为评估[情绪](#sentiment)的过程中的步骤。 关注字词对情绪值的贡献是由于对发布内容中使用的负面和正面关注字词与禁止字词的比较。

#### 配置情绪和标语 {#configure-sentiment-and-watchwords}

正面和负面标语列表可以自定义，就像情绪规则一样。

可以将默认标语列表作为存储库中节点的属性输入，这与默认列表类似，也可以通过用标语列表配置OSGi服务`sentimentprocess.name`来覆盖默认列表。

还可以修改&#x200B;**sentimentprocess.name**&#x200B;以引用自定义情绪规则集的位置。

要配置情绪和标语，请执行以下操作：

* 以管理员身份登录到您的创作实例。
* 打开[Web控制台](https://localhost:4502/system/console/configMgr)。
* 找到`sentimentprocess.name`。
* 选择配置，以便您可以在编辑模式下打开它。

![sentimentprocess](assets/sentimentprocess.png)

* **正面标语**

  以逗号分隔的单词列表，这些单词有助于形成覆盖默认值的积极情绪。 默认列表为空。

* **负面标语**

  以逗号分隔的单词列表，这些单词会导致覆盖默认值的负面情绪。 默认列表为空。

* **Watchwords节点的显式路径**

  包含指定默认关注字的默认`positive`和`negative`属性的节点的存储库位置。 默认值为`/libs/settings/community/watchwords/default`。

* **情绪规则**

  用于基于正面和负面关注词计算情绪的规则的存储库位置。 默认值为`/libs/cq/workflow/components/workflow/social/sentiments/rules`（但是，不再涉及任何工作流）。

以下是将`Explicit Path to Watchwords Node`设置为`/libs/settings/community/watchwords/default`时默认标语自定义条目的示例。

![crxde](assets/crxde.png)

### 审查方权限 {#moderator-permissions}

当为同一资源分配以下权限时，这些权限统称为`moderator permissions`：

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
