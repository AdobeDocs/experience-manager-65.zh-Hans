---
title: 审核控制台
seo-title: 审核控制台
description: 如何访问审核控制台
seo-description: 如何访问审核控制台
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# 审核控制台{#moderation-console}

在AEM Communities中，管理员和社 [区版主](/help/communities/moderate-ugc.md) （分配为版主的受信任社区成员）可以在创作和发布环境中批量审核社区内容。

管理员和社区版主还可以在 [发布环境中执行上下文](/help/communities/in-context.md) 、上下文审核。

所有社区站点的 [一个功能](/help/communities/sites-console.md) , `Administration`是一个菜单项，可供具有管理权限登录的用户使用。 该链 `Administration`接提供对审核控制台的访问。

从“审核”控制台中，管理员和社区审核者将有权访问其有权审核的所有用户生成的内容(UGC)。 如果允许审核多个站点，则可以查看所有站点中的帖子或按选定的社区站点进行筛选。

有关更多详细信息，请 [访问管理用户和用户组](/help/communities/users.md)。

审核控制台支持：

* 批量执行协调任务
* 搜索UGC
* 查看UGC详细信息
* 查看UGC作者详细信息

只有以管理员或具有成员身份登录时，才可 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`以执行审核任务。

## 发布环境访问 {#publish-environment-access}

从已发布的社区站点访问审核控制台是通过管理链接，当社区审查方登录时，会显示该链接。

![publishweretail](assets/publishweretail.png)

通过选择“管理”链接，将显示“审核”控制台：

![版本控制台发布](assets/moderationconsole-publish.png)

## 创作环境访问 {#author-environment-access}

在创作环境中，要访问“审核”控制台

* 从全局导航：导 **航、社区、协调**

仅当以管理员或成员身份登录时，才可 ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`以执行审核任务。 显示的唯一社区内容是允许登录成员审核的社区内容。

>[!NOTE]
>
>只有在所选SRP实现公共存储时，发布环境中的UGC才在作者身上可见。 例如，默认情况下，存储是JSRP，它不是创作和发布的常用存储。 请参阅 [社区内容存储](/help/communities/working-with-srp.md)。

![版本控制台作者](assets/moderationconsoleauthor.png)

## 审核控制台UI {#moderation-console-ui}

除左侧导航边栏（在作者上显示，但在发布上不显示）之外，协调UI具有以下主要区域：

* **[顶部导航栏](#top-navigation-bar)**
* **[工具栏](#toolbar)**
* **[内容区域](#content-area)**

### Top Navigation Bar {#top-navigation-bar}

顶部导航栏对所有控制台都是常数。 有关详细信息，请参阅 [基本处理](/help/sites-authoring/basic-handling.md)。

### 工具栏 {#toolbar}

位于顶部导航栏下方的工具栏在左侧提供了以下切换开关：

* [筛选边栏](/help/communities/moderation.md#filterrail)会打开一个边栏，该边栏允许选择要筛选内容的属性。

位于顶部导航栏下方的工具栏在左侧提供了以下切换开关：

![雪巫](assets/toggleswitch.png)

[筛选边栏](/help/communities/moderation.md#filterrail)在选择“搜索”时打开边栏，该边栏允许选择筛选内容的属性。

![filterrail](assets/filterrail.png)

### 内容区域 {#content-area}

内容区域包含已发布UGC的信息：

* UGC发布
* 成员名称
* 会员头像
* 帖子的位置
* 发布时间
* 帖子的回复数
* [与帖子关联的情绪](/help/communities/moderate-ugc.md#sentiment) ,
* 如果批准，则显示复选标记
* 如果有附件，则显示回形针

>[!NOTE]
>
>内容区域具有 *无限滚动*，这意味着它允许您继续滚动直到内容结束。 即使在滚动时，工具栏仍保留在内容区域上方的固定可见位置。

### 滤镜边栏 {#ootbfilters}

![chlimage_1-212](assets/chlimage_1-212.png)

侧面板图标可打开滤镜边栏。 显示在内容区域左侧的过滤器边栏提供不同的过滤器，每个过滤器对内容区域中显示的引用的UGC具有即时效果。

每个类别中的过滤器 ****&#x200B;或者一起使用，不同类别中的过滤器 ****&#x200B;则一起使用。

例如，选中“问题”和“答案 **”后** ，您会看到内容是“**问题”**或“答案”( **如果********&#x200B;选中)。

但是，如果选 **中“问题** ”和“待定 **”**，您将只看到属于**问题**并且处于“待定” **内容**。

>[!NOTE]
>
>社区审核者可以在审核控制台UI上为预定义的过滤器加书签。 当这些过滤器附加到URL的末尾（作为查询字符串参数）时，版主可以稍后返回到已添加书签的过滤器，并共享这些链接。

![searchicon](assets/searchicon.png)

当过滤器边栏打开时，“搜索”图标可切换侧面板关闭。 但是，要关闭筛选器边栏并仅查看用户生成的内容，请单击“搜索”图标，然后选择“仅内容”选项。

#### 内容路径 {#content-path}

内容路径将显示给放置在指定内容存储库中的帖子的引用UGC限制为限制。

![内容路径](assets/content-path.png)

#### 文本搜索 {#text-search}

文本搜索将引用的UGC限制为包含输入文本的帖子显示。

![chlimage_1-213](assets/chlimage_1-213.png)

#### 站点 {#site}

站点将所引用的UGC限制为显示到选定社区站点的帖子。 如果未选中任何站点，则显示对UGC的所有引用。

![chlimage_1-214](assets/chlimage_1-214.png)

>[!NOTE]
>
>当管理员访问批量审核控制台时，将显示对UGC的所有引用，包括未通过站点创建向导创建的站点 [](/help/communities/sites-console.md)，如Geometrixx示例。
>
>当受信任的社区成员在发布时访问批量审核控制台时，只会显示对为授权其审核的社区站点创建的UGC的引用，并且可以使用站点过滤器进行过滤。

#### 内容类型 {#content-type}

“内容类型”将引用的UGC限制为显示给选定资源类型的帖子。 可以选择以下一种或多种类型。 如果未选择任何类型，则显示所有类型。

* **注释**
* **论坛 - 主题**
* **论坛回复**
* **问题与解答 - 问题**
* **问题与解答 - 回答**
* **博客文章**
* **博客评论**
* **日历事件**
* **日历注释**
* **文件库文件夹**
* **文件库文档**
* **构思**
* **构思评论**

![内容类型](assets/content-types.png)

#### 其他内容类型 {#additional-content-types}

要添加要筛选的其他资源，请执行以下操作：

* 在创作实例上
* 以管理员身份登录
* 打开 [Web控制台](https://localhost:4502/system/console/configMgr)
* 定位 `AEM Communities Moderation Dashboard Filters`
* 选择要在编辑模式下打开的配置
* 输入要筛选的组件的ResourceType

   * 例如，要筛选包含的投票组件，请输入：
      `Voting=social/tally/components/hbs/voting`

![chlimage_1-215](assets/chlimage_1-215.png)

* 选择保存
* 刷新社区——审核控制台

结果是过滤器组下的新的可 `Voting`选过滤 `Content Type` 器。

选择该过滤器后，功能板的内容将显示与输入的任何ResourceTypes匹配的UGC。

#### 状态 {#status}

状态将引用的UGC限制为显示到选定状态的帖子，这些帖子可能是“待定”、“已批准”、“已拒绝”或“已关闭”中的一个或多个，以及“为博客文章草稿”或“已计划”中的一个或多个，以及“已回答或未回答问题”。 如果未选择任何内容，则显示所有内容。

>[!NOTE]
>
>如果仅选择“未回答”状态，则审查方将看到除已回答问题之外的所有内容（适用于所有内容类型）。 这是因为，在未回答的问题和其他内容（如论坛主题、博客文章或评论）的情况下，不存在对已回答问题负责的属性。

![状态](assets/statuses.png)

#### 标记 {#flagging}

标记将所引用的UGC限制为显示给已标记或隐藏的帖子。

标记某个内容后，它会一直保持标记状态，直到您再次选择“标记”**“标记”**按钮取消标记该内容为止。 请注意，不存在标记级别，如重要或后续操作。

![chlimage_1-216](assets/chlimage_1-216.png)

#### 成员 {#members}

成员将引用的UGC限制为由输入的成员名称发布的UGC。

![chlimage_1-217](assets/chlimage_1-217.png)

#### 发布于前一 {#posted-in-the-last}

在“最后一个”中发布时，将引用的UGC显示到在最后一小时、一天、一周、月或年发布的帖子中。

![chlimage_1-218](assets/chlimage_1-218.png)

#### 情绪 {#sentiment}

[情绪](/help/communities/moderate-ugc.md#sentiment) 将引用的UGC限制为显示给具有正面、负面或中性情绪值的帖子。

![chlimage_1-219](assets/chlimage_1-219.png)

## Custom Filters {#custom-filters}

除了过滤器边栏中的现成过滤器 [外](/help/communities/moderation.md#ootbfilters)，还可以将元数据的其他自定义过滤器添加到协调UI。 开发人员可以使用Github中的示例代码扩展现有的协调UI筛选器。

![custom-tag-filter](assets/custom-tag-filter.png)

Github上 [的示例项目](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) (Tag filter)实现了标记过滤器，以根据特定标记是否应用于用户生成的内容来过滤UGC列表。 您可以按照示例代码，为其他类似的UGC元数据字段构建类似的过滤器。

要安装“标记”过滤器的示例，请执行以下操作：

1. 在AEM作者([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))实例和AEM发布([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))实例上打开包管理器。
1. 从Github代码 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` 构建包，并安装和启用它。
1. 在AEM作者()实例和AEM发布( `https://[aem-author]:4502/system/console/bundles`)实例上打开捆绑 `https://[aem-publish]:4503/system/console/bundles`套件控制台。
1. 从Github构建 ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` 包，并安装并启用它。
1. 转到AEM作者上的 **/apps/social/仲裁/facets** 节点([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/仲裁/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))和AEM发布([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/仲裁/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))实例。
1. 添加具有权限 **的技术用户社区——实用程序** -阅 `jcr:read` 读器。

要在现有社区站点上显示自定义过滤器，请执行以下操作：

1. 编辑 `Clientlibs` 现有审核页面 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 添加新类别 `cq.social.hbs.moderation.v2.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * 设置为新组件 `sling:resourceType = social/moderation/v2/filters.`

1. 转到 `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * 设置为新组件 `sling:resourceType = social/moderation/v2/modcontainer`。

## 审核操作 {#moderation-actions}

[可以对](/help/communities/moderate-ugc.md#moderation-actions) “内容”区域中或查看内容详细信息时所做的一个或多个选择执行审核操作。

要批量审核帖子，请在内容区域中单击帖子上的“选择”( ![selecticon](assets/selecticon.png))图标，将鼠标悬停在帖子上方时（桌面）或按住手指在帖子上（移动）会显示该图标。 通过执行此操作，您可以进入多选模式，现在只需单击这些帖子即可选择要批量审核的后续帖子。 使用工具栏上显示的按钮对选定的帖子执行审核操作。 所有操作都将提示进行确认。

要审核内容区域中的单个帖子，请用鼠标（桌面）将鼠标悬停在该帖子上，或按住帖子（移动）上的手指，使帖子上显示按钮。 在单个内容详细信息上操作时，只有删除操作会提示您确认。

### 审核多个帖子 {#moderating-multiple-posts}

单击帖子上的图标，进入批 `Select` 量选择模式：

![select-icon](assets/select-icon.png)

要退出批量选择模式，请选择工具栏中的取消(x)图标：

可对多个帖子执行的审核操作包括：

* 拒绝
* 删除
* 关闭／重新打开帖子

仅当选择多个帖子时，允许这些操作的图标才会显示在工具栏上。

![bulkmeater](assets/bulkmoderate.png)

### 审核单个帖子 {#moderating-a-single-post}

在单选模式下，可以

* 通过选择用户名查看用户详细信息
* 通过选择指向帖子的链接，查看帖子的上下文
* [回复](#reply)
* [允许](#allow)
* [拒绝](#deny)
* [删除](#delete)
* [关闭](#close)
* 查看 [审核历史](#moderation-history)
* [查看详细信息](#viewdetails)

审核操作图标上方的卡片视图中显示帖子文本，下方显示指示

* 如果有回复，则在回复数前面加上
* 如果已标记
* 如果已批准
* UGC发布时

![单电模式](assets/singleselectmode.png)

#### 回复 {#reply}

![chlimage_1-220](assets/chlimage_1-220.png)

处理单个帖子时，如果UGC类型支持回复并配置为允许回复，则将显示回复图标。

#### 允许 {#allow}

![chlimage_1-221](assets/chlimage_1-221.png)

处理单个帖子时，当帖子已被标记或拒绝时，将显示“允许”图标。 如果标记了，选择“允许”将清除所有标记。

#### 拒绝 {#deny}

![chlimage_1-222](assets/chlimage_1-222.png)

**拒绝**仲裁操作仅适用于已审核的内容，除非在多选模式下，否则不会显示在未审核的内容上。

未审核的内容始终会得到批准。

已审核的内容最初进入“待定”状态，之后可修改为批准或拒绝。

离开暂挂状态的内容永远不能返回到暂挂状态。 标记为已批准或已拒绝的内容可随时更改为其他状态。

#### 删除 {#delete}

![chlimage_1-223](assets/chlimage_1-223.png)

在单个选择或批量模式下，您可以选择项目并删除它们。 删除操作会生成确认对话框。 删除后，这些项目会立即从内容区域中消失。 **删除UGC后，它将从存储库中永久删除，以后将无法检索。**

#### 关闭 {#close}

![chlimage_1-224](assets/chlimage_1-224.png)

处理单个帖子时，如果UGC类型支持阻止该资源的其他帖子的功能，则将显示“关闭”图标。

#### 审核历史记录 {#moderation-history}

![chlimage_1-225](assets/chlimage_1-225.png)

处理单个帖子时，将鼠标悬停在帖子上方时将显示“审核历史记录”图标。 选择该图标将显示一个窗格，其中包含对UGC帖子执行的操作的历史记录。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![chlimage_1-226](assets/chlimage_1-226.png)

#### 查看详细信息 {#view-detail}

![chlimage_1-227](assets/chlimage_1-227.png)

使用单个帖子时，可以通过在详细信息模式下打开UGC来查看更多详细信息。

为此，请将鼠标悬停在帖子上以显示图 `View Detail` 标，然后选择它以显示包含帖子更多详细信息的面板。

要返回到显示多个UGC帖子的内容区域，请选择视图详细信息窗格右上角的X。

例如：

![chlimage_1-228](assets/chlimage_1-228.png)

