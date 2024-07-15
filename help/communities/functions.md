---
title: 社区功能
description: 了解如何访问社区功能控制台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# 社区功能{#community-functions}

社区体验中预期的功能类型是众所周知的。 社区功能作为社区功能提供。 本质上，它们是预连接的一个或多个页面，用于实施社区功能，该功能不仅需要在创作模式下将组件添加到页面。 它们是用于定义[社区站点模板](/help/communities/sites.md)结构的构建块，社区站点是从该模板[创建的](/help/communities/sites-console.md)。

创建社区站点后，可以使用标准[AEM创作模式](/help/sites-authoring/editing-content.md)将内容添加到生成的页面。 可以在社区功能控制台中看到各种社区功能。

>[!NOTE]
>
>用于创建[社区站点](/help/communities/sites-console.md)、[社区站点模板](/help/communities/sites.md)、[社区组模板](/help/communities/tools-groups.md)和[社区功能](/help/communities/functions.md)的控制台仅在创作环境中使用。

## 社区功能控制台 {#community-functions-console}

要在创作环境中访问社区功能控制台，请执行以下操作：

* 导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 社区功能]**。

![社区功能](assets/community-functions.png)

## 预建函数 {#pre-built-functions}

以下简要介绍了AEM Communities提供的功能。 每个函数都包括一个或多个AEM页面，其中包含相互连接在一起的社区组件，这些组件可轻松合并到[社区站点模板](/help/communities/sites.md)中的功能。

社区站点模板提供了社区站点的结构，包括登录、用户配置文件、通知、消息、站点菜单、搜索、主题设定和品牌推广功能。

### 标题和URL设置 {#title-and-url-settings}

**标题**&#x200B;和&#x200B;**URL**&#x200B;是所有社区功能通用的属性。

在将社区函数添加到社区站点模板或在[修改](/help/communities/sites-console.md#modifying-site-properties)社区站点的结构时添加该函数时，将打开该函数的对话框，以便可以配置标题和URL。

#### 配置功能详细信息 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **标题**

  （*必需*）网站功能菜单中显示的文本

* **URL**

  （*必需*）用于生成URI的名称。 名称必须符合AEM和JCR实施的[命名约定](/help/sites-developing/naming-conventions.md)。

例如，使用按照[快速入门](/help/communities/getting-started.md)教程创建的站点，如果

* 标题=网页
* URL =页面

然后，指向该页面的URL为https://localhost:4503/content/sites/engage/en/page.html

该页面的菜单链接显示为：

![engage-page](assets/engage-page.png)

### 活动流功能 {#activity-stream-function}

活动流函数是一个具有[活动流组件](/help/communities/activities.md)的页面，其中选定了所有视图（所有活动、用户活动及其他）。 另请参阅开发人员的[Activity Stream Essentials](/help/communities/essentials-activities.md)。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-1}

![函数详细信息](assets/function-details.png)

* [标题和URL设置](#title-and-url-settings)

* **显示“我的活动”视图**

  如果选择，则“活动”页面包括一个选项卡，该选项卡根据当前成员在社区内生成的活动进行筛选。 默认处于选中状态。

* **显示“所有活动”视图**

  如果选择，则“活动”页面包括一个选项卡，其中包含当前成员有权访问的社区内生成的所有活动。 默认处于选中状态。

* **显示“新闻信息源”视图**

  如果选择，活动页面将包含一个选项卡，该选项卡会根据当前成员所关注的活动进行筛选。 默认处于选中状态。

### 博客功能 {#blog-function}

博客功能是带有[博客组件](/help/communities/blog-feature.md)的页面，该组件配置为标记、文件上传、关注、成员自我编辑、投票和审核。 另请参阅开发人员的[博客要点](/help/communities/blog-developer-basics.md)。

添加到模板后，将打开以下对话框：

![博客组件](assets/blog-component.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

  如果选中，则博客仅允许拥有权限的成员通过允许选择[拥有权限的成员组](/help/communities/users.md#privileged-members-group)来创建文章。 如果未选择，则允许创建所有社区成员。 默认值为取消选中。

* **允许文件上传**

  如果选定此选项，则博客将允许成员上传文件。 默认处于选中状态。

* **允许线程回复**

  如果未选中，则博客允许对文章进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许精选内容**

  如果选定该博客，则将其标识为[特色内容](/help/communities/featured.md)。 默认处于选中状态。

### 日历功能 {#calendar-function}

日历函数是一个页面，其中的[日历组件](/help/communities/calendar.md)配置为允许标记。 另请参阅面向开发人员的[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)

添加到模板后，将打开以下对话框：

![日历详细信息](assets/calendar-details.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，则博客仅允许拥有权限的成员通过允许选择[拥有权限的成员组](/help/communities/users.md#privileged-members-group)来创建文章。 如果未选择，则允许创建所有社区成员。 默认值为取消选中。

* **允许文件上传**

  如果选定此选项，则博客将允许成员上传文件。 默认处于选中状态。

* **允许线程回复**

  如果未选中，则博客允许对文章进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许精选内容**

  如果选定，则将其内容标识为[精选内容](/help/communities/featured.md)。 默认处于选中状态。

### 专题内容功能 {#featured-content-function}

特色内容功能是一个页面，该页面具有配置为允许添加和删除评论的[特色内容组件](/help/communities/featured.md)。

每个组件可能允许或不允许使用具有内容功能的功能（请参阅[博客功能](#blog-function)、[日历功能](#calendar-function)、[论坛功能](#forum-function)、[构思功能](#ideation-function)和[QnA功能](#qna-function)）。

添加到模板时，[标题和URL设置](#title-and-url-settings)的唯一配置是。

### 文件库功能 {#file-library-function}

文件库函数是一个页面，其中的[文件库组件](/help/communities/file-library.md)配置为允许添加和删除注释。

添加到模板时，[标题和URL设置](#title-and-url-settings)的唯一配置是。

### 论坛功能 {#forum-function}

论坛功能是一个页面，其中的[论坛组件](/help/communities/forum.md)配置为标记、文件上传、关注、成员自我编辑、投票和审核。

添加到模板后，将打开以下对话框：

#### 配置功能详细信息 {#configuration-function-details-2}

![论坛 — 组件1](assets/forum-component1.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，则论坛仅允许拥有权限的成员通过选择[拥有权限的成员组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，论坛将允许成员上传文件。 默认处于选中状态。

* **允许线程回复**

  如果未选择此选项，则论坛允许对主题进行评论，但不允许对这些评论进行回复。 默认处于选中状态。

* **允许精选内容**

  如果选定该属性，则组件的内容被标识为[特色内容](/help/communities/featured.md)。 默认处于选中状态。

### 组功能 {#groups-function}

>[!CAUTION]
>
>组函数必须&#x200B;*不是*&#x200B;是站点结构或社区站点模板中的&#x200B;*第一个或唯一的*&#x200B;函数。
>
>任何其他函数（如[page函数](#page-function)）都必须包含并首先列出。

“组”功能使社区成员能够在发布环境中的社区站点中创建子社区。

根据[设置](/help/communities/sites-console.md#groupmanagement)（当[社区站点模板](/help/communities/sites.md)中包含组功能时），这些组可以是公共的或私有的，并且可以将一个或多个社区组模板配置为在实际创建社区组时提供模板选择（例如从发布环境）。 [社区组模板](/help/communities/tools-groups.md)指定为组页面（如论坛和日历）创建的社区功能。

创建社区组时，会为新组动态创建成员组，成员可以分配给新组或加入新组。 有关详细信息，请参阅[管理用户和用户组](/help/communities/users.md)。

截至Communities [功能包1](/help/communities/deploy-communities.md#latestfeaturepack)，社区组是使用[Communities Sites的组控制台](/help/communities/groups.md)在创作环境中创建的，在启用时可以在发布环境中创建。

添加到模板后，将打开以下对话框：

![group-template-config](assets/group-template-config.png)

* [标题和URL设置](#title-and-url-settings)

* **选择组模板**

  一个下拉列表，允许选择一个或多个已启用的组模板，新社区组的未来创建者（在发布环境中）可以从中进行选择。

* **允许拥有权限的成员**

  如果选中，则论坛仅允许特权成员通过选择[特权成员安全组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许Publish创建**

  如果选择，则授权社区成员可以在发布环境中创建组。 如果取消选择，则只能从社区站点的“组”控制台在创作环境中创建新组（子社区）。
默认处于选中状态。

### 构思功能 {#ideation-function}

构思函数是一个包含一个[构思组件](/help/communities/ideation-feature.md)的页面。

添加到模板后，将打开以下对话框，其中指定了模板的默认“标题”和URL名称以及默认显示设置：

![构思函数](assets/ideation-function.png)

* [标题和URL设置](#title-and-url-settings)

* **允许拥有权限的成员**

  如果选中，则论坛仅允许特权成员通过选择[特权成员安全组](/help/communities/users.md#privileged-members-group)来发布主题。 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，该想法包括成员上传文件的功能。 默认处于选中状态。

* **允许线程回复**

  如果未选择此构思，则允许对主题进行回复（评论），但不允许对评论进行回复。 默认处于选中状态。

* **允许精选内容**

  如果选定，则将其内容标识为[精选内容](/help/communities/featured.md)。 默认处于选中状态。

### 排行榜功能 {#leaderboard-function}

排行榜功能是具有一个[排行榜组件](/help/communities/enabling-leaderboard.md)的页面。

**注意**：排行榜组件在&#x200B;*之后需要进一步配置*&#x200B;从包含排行榜功能的社区模板创建社区站点。 指定排行榜组件的[规则](/help/communities/enabling-leaderboard.md#rules-tab)，这些规则依赖于社区站点[评分和徽章](/help/communities/implementing-scoring.md)的配置。

添加到模板后，将打开以下对话框，其中指定了模板的默认“标题”和URL名称以及默认显示设置：

![排行榜对话框](assets/leaderboard-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **显示徽章**

  如果选择，则排行榜中将包含徽章图标列。
默认值为取消选中。

* **显示徽章名称**

  如果选择，则徽章名称的列将包含在排行榜中。
默认值为取消选中。

* **显示头像**

  如果选择该选项，则成员的头像图像将包含在排行榜中，位于其名称链接旁边，指向其成员配置文件。
默认值为取消选中。

### 页面功能 {#page-function}

页面功能会向社区站点添加一个空白页面，该页面与社区站点的功能（登录、菜单、通知、消息、主题设置和品牌推广）相链接。 使用[标准AEM创作模式](/help/sites-authoring/editing-content.md)将内容添加到页面。

添加到模板时，[标题和URL设置](#title-and-url-settings)的唯一配置是。

### 问题与解答功能 {#qna-function}

QnA函数是一个页面，其中的[QnA组件](/help/communities/working-with-qna.md)配置为标记、文件上传、关注、自我编辑、投票和审核的成员。

添加到模板后，该配置允许对拥有权限的成员进行限制：

![qna-dialog](assets/qna-dialog.png)

* [标题和URL设置](#title-and-url-settings)

* **允许固定**

  如果选定，论坛允许将主题回复固定到评论列表的开头。 默认处于选中状态。

* **允许拥有权限的成员**

  如果选中，则QnA论坛仅允许特权成员通过选择[特权成员组](/help/communities/users.md#privileged-members-group)来张贴问题。 如果未选择，则允许所有社区成员发帖。 默认值为取消选中。

* **允许文件上传**

  如果选中，问题与解答论坛包括成员上传文件的功能。 默认处于选中状态。

* **允许线程回复**

  如果未选择，问题与解答论坛允许对已发布的问题进行评论（回答），但不允许对答案进行回复。 默认处于选中状态。

* **允许精选内容**

  如果选定，则将其内容标识为[精选内容](/help/communities/featured.md)。 默认处于选中状态。

## 创建社区功能 {#create-community-function}

通过选择位于社区功能控制台顶部的`Create Community Function`图标，可以获得创建社区功能的功能。 可以创建基于同一AEM Blueprint的多个函数，然后通过以创作编辑模式打开来进行唯一自定义。

![create-community-function](assets/create-community-function.png)

### 社区功能名称 {#community-function-name}

![function-name](assets/function-name.png)

在“社区功能名称”面板上，配置了名称、描述以及功能是启用还是禁用：

* **社区功能名称**

  用于显示和存储的函数名称。

* **社区功能描述**

  显示的函数描述。

* **已禁用/已启用**

  用于控制函数是否可引用的切换开关。

### AEM Blueprint {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

在`AEM Blueprint`面板上，可以选择Blueprint，它是社区功能的基础实现。

社区功能是一个微型站点，它包含一个或多个页面，预先布线以包含到社区站点中，包括登录、用户配置文件、通知、消息、站点菜单、搜索、主题设定和品牌推广功能。 创建函数后，就可以[在作者编辑模式下打开函数](#open-community-function)并自定义页面或组件设置。

由于社区功能是作为[Blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)的[Live Copy](/help/sites-administering/msm.md#live-copies)实施的，因此可以转出对功能所做的更改，该功能会影响从[社区站点模板](/help/communities/sites.md)或包含该功能的[社区组模板](/help/communities/tools-groups.md)创建的所有社区站点页面。 也可以取消页面与其父Blueprint的关联，以进行页面级别的修改。

另请参阅[多站点管理器](/help/sites-administering/msm.md)。

### 缩略图 {#thumbnail}

![功能缩略图](assets/funtion-thumbnail.png)

在“缩略图”面板上，可以上传图像以在[社区功能控制台](#community-functions-console)中显示。

## 打开社区功能 {#open-community-function}

![打开函数](assets/open-function.png)

选择`Open Community Function`图标以进入创作页面内容和修改功能组件配置的作者编辑模式。

### 配置组件 {#configuring-components}

社区功能是作为AEM Blueprint的Live Copy实现的，其详细信息记录在[多站点管理器](/help/sites-administering/msm.md)下。

您不仅可以创作页面内容，还可以配置组件。

如果在已创建的社区站点的页面上配置组件，则可能需要取消[继承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)才能配置该组件。 配置完成后，应重新建立继承。

有关配置详细信息，请访问作者的[社区组件](/help/communities/author-communities.md)。

## 编辑社区功能 {#edit-community-function}

![edit-function](assets/edit-function.png)

选择`Edit Community Function`图标可使用与[创建社区函数](#create-community-function)相同的面板编辑该函数的属性，包括启用或禁用该函数。
