---
title: 社区评分和徽章
description: AEM Communities评分和徽章可让您识别并奖励社区成员
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 2%

---

# 社区评分和徽章 {#communities-scoring-and-badges}

## 概述 {#overview}

AEM Communities评分和徽章功能使您能够识别和奖励社区成员。

评分和徽章的主要方面包括：

* [分配徽章](#assign-and-revoke-badges)以标识社区中成员的角色。

* [将徽章的基本奖励](#enable-scoring)给成员，以鼓励其参与（创建的内容数量）。

* [高级奖励徽章](/help/communities/advanced.md)以将成员识别为专家（创建的内容质量）。

**请注意**，默认情况下未启用徽章授予[&#128279;](/help/communities/implementing-scoring.md#main-pars-text-237875536)。

>[!CAUTION]
>
>在CRXDE Lite中可见的实施结构在UI可用时可能会发生更改。

## 徽章 {#badges}

徽章放置在成员的名称下，以指示其在社区中的角色或地位。 徽章可以显示为图像或名称。 显示为图像时，该名称将作为辅助功能的替换文本包含在内。

默认情况下，徽章位于以下存储库中：

* `/libs/settings/community/badging/images`

如果存储在其他位置，则每个人都可以读取这些文件。

在UGC中区分徽章，无论它们是按照规则分配还是按照规则获得的。 目前，分配的徽章显示为文本，已获得的徽章显示为图像。

### 徽章管理UI {#badge-management-ui}

社区[徽章控制台](/help/communities/badges.md)允许您添加自定义徽章，当成员获得（授予）或在社区中承担特定角色（已分配）时，可以显示这些徽章。

### 已分配的徽章 {#assigned-badges}

基于角色的徽章由管理员根据社区成员在社区中的角色分配给社区成员。

已分配（和已授予）的徽章存储在选定的[SRP](/help/communities/srp.md)中，无法直接访问。 在GUI可用之前，分配基于角色的徽章的唯一方法是使用代码或cURL。 有关cURL说明，请参阅标题为[分配和撤销徽章](#assign-and-revoke-badges)的部分。

此版本中包含三个基于角色的徽章：

* **审查方**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **组管理员**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **特权成员**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![已分配的徽章](assets/assigned-badges.png)

### 已授予的徽章 {#awarded-badges}

评分服务会根据适用于社区成员在社区中活动的规则，向社区成员授予基于奖励的徽章。

要让徽章显示为对活动的奖励，必须发生以下两种情况：

* 功能组件的徽章必须为[启用](#enableforcomponent)。
* 评分和徽章规则必须[应用于](#applytopage)组件所在的页面（或祖先）。

此版本中包含三个基于奖励的徽章：

* **金**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **银**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **铜级**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![奖励徽章](assets/awarded-badges.png)

>[!NOTE]
>
>可以将评分规则配置为为标记为不适当并因此影响得分值的帖子分配负分。 但是，获得徽章后，不会由于评分点减少或评分规则更改而自动删除该徽章。
>
>授予的徽章可以与分配的徽章相同的方式被撤销。 请参阅[分配和撤销徽章](#assign-and-revoke-badges)部分。 未来的改进将包括一个UI来管理成员的徽章。

### 自定义徽章 {#custom-badges}

可以使用[徽章控制台](/help/communities/badges.md)安装自定义徽章，并在徽章规则中指定或分配。

从“徽章”控制台安装后，自定义徽章会自动复制到发布环境。

## 启用评分 {#enable-scoring}

默认情况下不启用评分。 设置和启用徽章评分和授予的基本步骤如下：

* 识别学习点数规则（[评分规则](#scoring-rules)）。
* 对于每个评分规则累计的点数，分配[徽章](#badges) （[徽章规则](#badging-rules)）。

* [将评分和徽章规则应用于社区站点](#apply-rules-to-content)。
* [为社区功能启用徽章](#enable-badges-for-component)。

请参阅[快速测试](#quick-test)部分，以使用论坛和评论的默认评分和徽章规则为社区站点启用评分。

### 将规则应用于内容 {#apply-rules-to-content}

要启用评分和徽章，请将属性`scoringRules`和`badgingRules`添加到网站内容树中的任意节点。

如果站点已发布，请在应用所有规则和启用组件后，重新发布站点。

应用于启用了徽章的组件的规则适用于当前节点或其祖先的规则。

如果节点的类型为`cq:Page`（推荐），则使用CRXDE|Lite将属性添加到其`jcr:content`节点。

| **属性** | **类型** | **描述** |
|---|---|---|
| 徽章规则 | 字符串 | [徽章规则](#badging-rules)的数组列表 |
| 评分规则 | 字符串 | [评分规则](#scoring-rules)的数组列表 |

>[!NOTE]
>
>如果评分规则似乎对奖励徽章没有影响，请确保评分规则未受到徽章规则的scoringRules属性的阻止。 请参阅标题为[徽章规则](#badging-rules)的部分。

### 为组件启用徽章 {#enable-badges-for-component}

评分和徽章规则仅对通过在[创作模式](/help/communities/author-communities.md)中编辑组件配置而启用徽章的组件实例有效。

布尔属性`allowBadges`启用/禁用组件实例的徽章显示。 可以通过标记为&#x200B;**显示徽章**&#x200B;的复选框在论坛、QnA和评论组件的[组件“编辑”对话框](/help/communities/author-communities.md)中对其进行配置。

#### 示例：用于论坛组件实例的allowBadges {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>任何组件都可以叠加以使用论坛、问题与解答中的HBS代码作为示例来显示徽章。

## 评分规则 {#scoring-rules}

评分规则是颁发徽章进行评分的基础。

每个评分规则是一个包含一个或多个子规则的列表。 评分规则将应用于社区站点内容，以确定在启用徽章时要应用的规则。

评分规则是继承的，但不是累加的。 例如：

* 如果页面2包含评分规则2，并且其祖先page1包含评分规则1。
* 在page2组件上的操作同时调用rule1和rule2。
* 如果两个规则包含相同`topic/verb`的适用子规则：

   * 只有规则2中的子规则会影响得分。
   * 两个子规则的分数均不添加。

当存在多个评分规则时，将分别为每个规则维护得分。

评分规则是`cq:Page`类型的节点，其`jcr:content`节点上具有属性，这些属性指定定义该规则的子规则列表。

分数存储在SRP中。

>[!NOTE]
>
>最佳实践：唯一地命名每个评分规则。
>
>评分规则名称应具有全局唯一性；它们不应以相同的名称结尾。
>
>*不*&#x200B;执行的操作的示例：
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### 评分子规则 {#scoring-sub-rules}

评分子规则包含详细说明参与社区的值的属性。

每个评分子规则确定：

* 正在跟踪哪些活动？
* 涉及哪些特定的社区功能？
* 会奖励多少分？

默认情况下，积分被授予采取操作的成员，除非子规则将内容的所有者指定为接收积分(`forOwner`)。

每个子规则可以包含在一个或多个评分规则中。

子规则的名称通常遵循使用&#x200B;*主题*、*对象*&#x200B;和&#x200B;*谓词*&#x200B;的模式。 例如：

* member-comment-create
* 会员 — 接收 — 投票

子规则是`cq:Page`类型的节点，其`jcr:content`节点上具有指定[谓词和主题](#topics-and-verbs)的属性。

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>类型</th>
   <th> 值说明</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>长</td>
   <td>
    <ul>
     <li>必需；动词对应于事件操作</li>
     <li>必须至少有一个动词属性</li>
     <li>谓词必须全部大写</li>
     <li>动词属性可以有多个，但不存在重复项</li>
     <li>该值是要应用于此事件的分数</li>
     <li>该值可为正或负</li>
     <li>此版本中支持的动词列表位于<a href="#topics-and-verbs">主题和动词</a>部分</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>字符串</td>
   <td>
    <ul>
     <li>可选；将子规则限制为按事件主题标识的社区组件</li>
     <li>如果已指定：值是事件主题的多值字符串</li>
     <li>此版本中的主题列表位于<a href="#topics-and-verbs">主题和动词</a>部分</li>
     <li>默认设置为应用于与动词相关的所有主题</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>布尔值</td>
   <td>
    <ul>
     <li>可选；在成员根据其拥有的内容进行操作时不可用</li>
     <li>如果为true，则将得分应用于所执行内容的所有者</li>
     <li>如果为false，则对成员执行操作应用分数</li>
     <li>默认为false</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>字符串</td>
   <td>
    <ul>
     <li>可选；标识评分引擎</li>
     <li>如果为“基本”，则根据数量指定评分引擎
      <ul>
       <li>包含在版本中</li>
      </ul> </li>
     <li>如果为“高级”，则根据质量和数量指定评分引擎
      <ul>
       <li>需要<a href="/help/communities/advanced.md">额外的包</a></li>
      </ul> </li>
     <li>默认为“basic”</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 包含评分规则和子规则 {#included-scoring-rules-and-sub-rules}

此版本中包含了[论坛功能](/help/communities/functions.md#forum-function)的两个评分规则（论坛功能的论坛和评论组件各一个）：

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-give-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-give-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**注释：**

* `rules`和`sub-rules`节点的类型为cq：Page。

* `subRules`是规则的`jcr:content`节点上类型为String[]的属性。

* `sub-rules`可以在各种评分规则之间共享。
* `rules`应位于存储库位置，每个人都具有读取权限。

   * 无论位置如何，规则名称都必须是唯一的。

### 激活自定义评分规则 {#activating-custom-scoring-rules}

在创作环境中对评分规则或子规则所做的任何更改或添加必须安装在发布上。

## 徽章规则 {#badging-rules}

徽章规则通过指定以下内容将评分规则链接到徽章：

* 评分规则
* 授予特定徽章所需的分数

徽章规则是`cq:Page`类型的节点，其`jcr:content`节点上具有将评分规则与分数和徽章关联的属性。

徽章规则由必需的`thresholds`属性组成，该属性是映射到徽章的分数排序列表。 必须按递增值对得分进行排序。 例如：

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * 铜牌得一分。

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * 银牌可获得60分。

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * 金牌获得八十分的奖励。

徽章规则与评分规则配对，后者决定积分的积累方式。 请参阅标题为[将规则应用于内容](#apply-rules-to-content)的部分。

徽章规则的`scoringRules`属性仅限制哪些评分规则可以与该特定徽章规则配对。

>[!NOTE]
>
>最佳实践：创建每个AEM站点唯一的徽章图像。

![徽章 — 规则 — 配置](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>属性</th>
   <th>类型</th>
   <th>值说明</th>
  </tr>
  <tr>
   <td>阈值</td>
   <td>字符串</td>
   <td><em>（必需）</em>格式为“number|path”的多值字符串
    <ul>
     <li>数字=得分</li>
     <li>| =垂直线字符(U+007C)</li>
     <li>path =徽章图像资源的完整路径</li>
    </ul> 必须对字符串进行排序，以使数字在值中递增，并且在数字和路径之间不应出现空格。<br />示例条目：<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>徽章类型</td>
   <td>字符串</td>
   <td><em>（可选）</em>将评分引擎标识为“basic”或“advanced”。 如果需要高级评分引擎，请参阅<a href="/help/communities/advanced.md">高级评分和徽章</a>。 默认值为“basic”。</td>
  </tr>
  <tr>
   <td>评分规则</td>
   <td>字符串</td>
   <td>（<em>可选</em>）多值字符串，用于限制标记规则只查看由评分规则标识的评分事件</td>
  </tr>
 </tbody>
</table>

### 包含的徽章规则 {#included-badging-rules}

发行版中包含两个徽章规则，它们对应于[论坛和评论评分规则](#includedscoringrules)。

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**注释：**

* `rules`节点的类型为cq：Page。
* `rules`应位于存储库位置，每个人都具有读取权限。

   * 无论位置如何，规则名称都必须是唯一的。

### 激活自定义徽章规则 {#activating-custom-badging-rules}

在创作环境中对标记规则或图像所做的任何更改或添加都必须安装在发布上。

## 分配和撤销徽章 {#assign-and-revoke-badges}

可以使用[成员控制台](/help/communities/members.md#badges-tab)或以编程方式使用cURL命令为成员分配徽章。

以下cURL命令显示了分配和撤消徽章的HTTP请求所必需的。 基本格式为：

cURL -i -XPOST-H *标头* -u *登录* -F *操作* -F *徽章* *member-profile-url*

*标头* = &quot;Accept：application/json&quot;
要传递到服务器的自定义标头（必需）

*登录* = administrator-id：password
例如，admin：admin

*operation* = &quot;：operation=social：assignBadge&quot; OR &quot;：operation=social：deleteBadge&quot;

*徽章* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* =徽章图像文件在存储库中的位置
例如，/libs/settings/community/badging/images/moderator/jcr：content/moderator.png

*member-profile-url* =发布时成员配置文件的端点
例如，https://&lt;服务器>：&lt;端口>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>*member-profile-url*：
>
>* 如果启用了[通道服务](/help/communities/users.md#tunnel-service)，则可以引用作者实例。
>* 可能是一个模糊的随机名称 — 请参阅关于可授权ID的[安全核对清单](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path)。

### 示例： {#examples}

#### 分配审查方徽章 {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### 撤销分配的银质徽章 {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>使用cURL分配和撤销徽章适用于任何徽章图像，但是，当分配而不是获得徽章时，它们会被标记为已分配的徽章并进行相应处理。

## 自定义组件的评分和徽章 {#scoring-and-badges-for-custom-components}

通过将为组件创建的事件主题与动词相关联，可以为自定义组件创建评分和徽章规则。

## 主题和动词 {#topics-and-verbs}

当成员与社区功能交互时，会发送可触发异步侦听器的事件，例如通知和评分。

组件的SocialEvent实例将事件记录为`topic`发生的`actions`。 SocialEvent包含用于返回与操作关联的`verb`的方法。 `actions`和`verbs`之间存在&#x200B;*n-1*&#x200B;关系。

对于交付的社区组件，下表描述了为[评分子规则](#scoring-sub-rules)中可用的每个`topic`定义的`verbs`。

>[!NOTE]
>
>新的布尔属性`allowBadges`启用/禁用组件实例的徽章显示。 可以在更新的[组件编辑对话框](/help/communities/author-communities.md)中通过标记为&#x200B;**显示徽章**&#x200B;的复选框对其进行配置。

**[日历组件](/help/communities/calendar.md)**
社交活动`topic`= com/adobe/cq/social/calendar

| **动词** | **描述** |
|---|---|
| POST | 成员创建日历事件 |
| 添加 | 成员对日历事件的评论 |
| 更新 | 编辑成员的日历事件或评论 |
| 删除 | 成员的日历事件或评论已删除 |

**[注释组件](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **动词** | **描述** |
|---|---|
| POST | 成员创建注释 |
| 添加 | 成员回复评论 |
| 更新 | 编辑成员的注释 |
| 删除 | 已删除成员的评论 |

**[文件库组件](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **动词** | **描述** |
|---|---|
| POST | 成员创建文件夹 |
| 附加 | 成员上传文件 |
| 更新 | 成员更新文件夹或文件 |
| 删除 | 成员删除文件夹或文件 |

**[论坛组件](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **动词** | **描述** |
|---|---|
| POST | 成员创建论坛主题 |
| 添加 | 成员对论坛主题的回复 |
| 更新 | 编辑成员的论坛主题或回复 |
| 删除 | 已删除成员的论坛主题或回复 |

**[日志组件](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **动词** | **描述** |
|---|---|
| POST | 成员创建博客文章 |
| 添加 | 成员对博客文章的评论 |
| 更新 | 编辑成员的博客文章或评论 |
| 删除 | 已删除成员的博客文章或评论 |

**[QnA组件](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **动词** | **描述** |
|---|---|
| POST | 成员创建问题与解答问题 |
| 添加 | 成员创建QnA答案 |
| 更新 | 编辑成员的问题或答案 |
| 选择 | 已选择成员的答案 |
| 取消选择 | 已取消选择成员的答案 |
| 删除 | 已删除成员的问题或答案 |

**[审阅组件](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **动词** | **描述** |
|---|---|
| POST | 成员创建审核 |
| 更新 | 成员的审核已编辑 |
| 删除 | 已删除成员的审核 |

**[评级组件](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **动词** | **描述** |
|---|---|
| 添加评级 | 成员内容已上标 |
| 删除评级 | 成员内容已降级 |

**[投票组件](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **动词** | **描述** |
|---|---|
| 添加投票 | 成员内容已被投票表决 |
| 删除投票 | 成员内容已被否决 |

**启用审核的组件**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **动词** | **描述** |
|---|---|
| 拒绝 | 成员内容被拒绝 |
| 标记为不适当 | 成员内容已标记 |
| 取消标记为不适当 | 成员内容未标记 |
| ACCEPT | 审阅人已批准成员的内容 |
| 关闭 | 成员关闭评论以进行编辑和回复 |
| 打开 | 成员重新打开注释 |

### 自定义组件事件 {#custom-component-events}

对于自定义组件，SocialEvent被实例化，以将组件的事件记录为`topic`发生的`actions`。

为了支持评分，SocialEvent需要覆盖方法`getVerb()`，以便为每个`action`返回相应的`verb`。 为操作返回的`verb`可以是常用的（如`POST`）或组件专用的（如`ADD RATING`）。 `actions`和`verbs`之间存在&#x200B;*n-1*&#x200B;关系。

## 疑难解答 {#troubleshooting}

### 未显示徽章 {#badges-are-not-appearing}

如果评分和徽章规则已应用于网站的内容，但未授予任何活动的徽章，请确保已为该组件的实例启用徽章。

请参阅[为组件](#enable-badges-for-component)启用徽章。

### 评分规则无效 {#scoring-rule-has-no-effect}

如果评分和徽章规则已应用于网站的内容，并且授予了一些操作的徽章，但其他操作没有这样做，请检查徽章规则是否未限制其适用的评分规则。

查看[徽章规则](#badging-rules)的`scoringRules`属性。

### 区分大小写的拼写错误 {#case-sensitive-typo}

大多数属性和值（尤其是动词）区分大小写。 在评分子规则中使用动词时，必须全部大写。

如果功能无法按预期工作，请确保已正确输入数据。

## 快速测试 {#quick-test}

可以使用[入门教程](/help/communities/getting-started.md) （参与）网站快速尝试评分和徽章：

* 访问有关作者的CRXDE Lite。
* 浏览到基本页：

   * /content/sites/engage/en/jcr：content

* 添加badgingRules属性：

   * **名称**：`badgingRules`
   * **类型**：`String`
   * 选择&#x200B;**多个**
   * 选择&#x200B;**添加**
   * 输入`/libs/settings/community/badging/rules/forums-badging`
   * 选择&#x200B;**+**
   * 输入`/libs/settings/community/badging/rules/comments-badging`
   * 选择&#x200B;**确定**

* 添加scoringRules属性：

   * **名称**：`scoringRules`
   * **类型**：`String`
   * 选择&#x200B;**多个**
   * 选择&#x200B;**添加**
   * 输入`/libs/settings/community/scoring/rules/forums-scoring`
   * 选择&#x200B;**+**
   * 输入`/libs/settings/community/scoring/rules/comments-scoring`
   * 选择&#x200B;**确定**

* 选择&#x200B;**全部保存**。

![测试得分 — 徽章](assets/test-scoring-badging.png)

接下来，确保论坛和评论组件允许显示徽章：

* 再次使用CRXDE Lite。
* 浏览到论坛组件

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* 如有必要，添加allowBadges布尔属性，并确保该属性为true。

   * **名称**：`allowBadges`
   * **类型**：`Boolean`
   * **值**：`true`

![test-forum-component](assets/test-forum-component.png)

接下来，[重新发布](/help/communities/sites-console.md#publishing-the-site)社区站点。

最后，

* 浏览到发布实例上的组件。
* 以社区成员身份登录(例如，weston.mccall@dodgit.com /密码)。
* Post是一个新的论坛主题。
* 必须刷新页面才能显示徽章。

   * 注销并以其他社区成员身份登录(例如：aaron.mcdonald@mailinator.com/password)。

* 选择论坛。

由于第一个论坛徽章规则的第一个阈值为1分，因此这应该会为社区成员获取随论坛帖子可见的铜级徽章。

![bronzebadge](assets/bronzebadge.png)

## 附加信息 {#additional-information}

可在面向开发人员的[评分和徽章要点](/help/communities/configure-scoring.md)页面上找到更多信息。

有关高级评分引擎的信息，请参阅[高级评分和徽章](/help/communities/advanced.md)。

可配置的排行榜[组件](/help/communities/enabling-leaderboard.md)和[功能](/help/communities/functions.md#leaderboard-function)简化了成员及其分数在社区网站上的显示。
