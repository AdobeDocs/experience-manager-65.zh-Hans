---
title: 社区站点控制台
description: 了解如何访问社区站点控制台以进行站点创建、编辑和管理。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 426e3adf-3723-4d17-a988-6eb050939e68
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3084'
ht-degree: 0%

---

# 社区站点控制台 {#communities-sites-console}

社区站点控制台提供对以下内容的访问：

* 站点创建
* 站点编辑
* 站点管理
* [创建和编辑嵌套组](/help/communities/groups.md) （子社区）

请参阅[AEM Communities快速入门](/help/communities/getting-started.md)，从中可了解在创作环境中创建社区站点的速度以及如何从创作和发布环境创建社区组。

>[!NOTE]
>
>用于创建[社区站点](/help/communities/sites-console.md)、[社区站点模板](/help/communities/sites.md)、[社区组模板](/help/communities/tools-groups.md)和[社区功能](/help/communities/functions.md)的主社区菜单仅在创作环境中使用。

## 先决条件 {#prerequisites}

在创建社区站点之前，*需要*&#x200B;执行以下操作：

* 确保有一个或多个Publish实例正在运行。
* 启用[通道服务](/help/communities/deploy-communities.md#tunnel-service-on-author)以管理成员和成员组。
* 识别[主发布者](/help/communities/deploy-communities.md#primary-publisher)。
* [当主发布者端口不是默认端口时，配置复制](/help/communities/deploy-communities.md#replication-agents-on-author) (4503)。

为确保站点能够支持多种功能，最佳做法是执行以下步骤：

* 安装[最新功能包](/help/communities/deploy-communities.md#latestfeaturepack)。
* 为AEM Communities启用[Adobe Analytics](/help/communities/analytics.md)。
* 配置[电子邮件](/help/communities/email.md)
* 识别[社区管理员](/help/communities/users.md#creating-community-members)。
* [为社交登录启用OAuth处理程序](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)。

## 访问社区站点控制台 {#accessing-communities-sites-console}

在创作环境中，要访问社区站点控制台，请执行以下操作：

* 从全局导航： **[!UICONTROL 社区]** > **[!UICONTROL 站点]**

“社区站点”控制台显示任何现有的社区站点。 从此控制台中，可以创建、编辑、管理和删除社区站点。

要创建社区站点，请选择&#x200B;**创建**&#x200B;图标。

要访问现有的社区站点以创作、修改、发布、导出或添加嵌套组，请选择站点的文件夹图标。

## 站点创建 {#site-creation}

站点创建控制台提供了一种分步方法，用于根据选定的[社区站点模板](/help/communities/sites.md)和设置来组装站点的功能。

创建的每个网站都包含登录功能，因为网站访客在发布内容、发送消息或参与群组之前都需要登录。 包括的其他功能包括用户配置文件、消息传送、通知、网站菜单、搜索、主题设定和品牌推广。

通过选择社区站点控制台顶部的`Create`按钮来启动进程。

创建过程是作为面板显示的一系列步骤，其中包含要配置的一组功能（作为子面板显示）。 可以前进到&#x200B;**下一步**&#x200B;步骤或&#x200B;**上一步**，然后在最后一个步骤中提交站点。

### 第1步：站点模板 {#step-site-template}

![newsitetemplate](assets/newsitetemplate.png)

在“站点模板”面板上，指定标题、描述、站点根、基本语言、名称和站点模板：

* **社区站点标题**

  站点的显示标题。

  标题会显示在已发布的站点和站点管理员UI中。

* **社区站点描述**

  站点的描述。

  该描述未出现在已发布的网站上。

* **社区站点根目录**

  站点的根路径。

  默认根目录为`/content/sites`，但该根目录可以移动到网站内的任何位置。

* **社区站点基本语言**

  （保持原样为单语言：英语）使用下拉菜单从可用语言中选择一种&#x200B;*或更多*&#x200B;种基本语言 — 德语、意大利语、法语、日语、西班牙语、葡萄牙语（巴西）、繁体中文、简体中文。 为添加的每个语言创建一个社区站点，该社区站点按照[翻译多语言站点的内容](/help/sites-administering/translation.md)中所述的最佳实践存在于同一站点文件夹中。 每个站点的根页面都包含一个由所选语言之一的语言代码命名的子页面，例如“en”表示英语，“fr”表示法语。

* **社区站点名称**：

  显示在URL中的站点根页面的名称。

   * 双击名称，因为创建站点后不易更改名称。
   * 基础URL ( `https://server:port/site root/site name)`显示在`Community Site Name`的下方。

   * 对于有效的URL，请附加基本语言代码+“.html”

     *例如*，`https://localhost:4502/content/sites/mysight/en.html`

* **社区站点模板**&#x200B;菜单

  使用下拉菜单选择可用的[社区站点模板](/help/communities/tools.md)。

* 选择&#x200B;**下一步**。

### 第2步：设计 {#step-design}

“设计”面板包含两个用于选择主题和品牌推广横幅的子面板：

#### 社区站点主题 {#community-site-theme}

![站点主题](assets/sitetheme.png)

框架使用`Twitter Bootstrap`为站点提供响应式灵活设计。 可以选择多个预加载的Bootstrap主题之一来造型所选择的社区站点模板，或者可以上传Bootstrap主题。

选中后，主题将叠加一个不透明的蓝色复选标记。

发布社区站点后，可以[编辑属性](#modifying-site-properties)并选择其他主题。

#### 社区站点品牌化 {#community-site-branding}

![网站品牌](assets/site-branding.png)

社区站点品牌化是作为标题显示在每个页面顶部的图像。

图像应设置为与浏览器中页面的预期显示一样宽，且高度为120像素。

创建或选择图像时，请记住：

* 图像高度将裁剪为从图像的上边缘开始测量的120像素。
* 图像将固定到浏览器窗口的左边缘。
* 不会调整图像大小，因此当图像宽度为……

   * 如果宽度小于浏览器的宽度，图像将水平重复。
   * 大于浏览器的宽度，图像似乎会被裁剪。

* 选择&#x200B;**下一步**。

### 步骤3：设置 {#step-settings}

“设置”面板包含多个子面板，这些子面板提供了在移动到创建站点的最后一步之前要配置的功能。

* [USER MANAGEMENT](#user-management)
* [标记](#tagging)
* [角色](#roles)
* [审核](#moderation)
* [ANALYTICS](#analytics)
* [翻译](#translation)

>[!NOTE]
>
>**启用通道服务**
>
>有几个“设置”子面板允许分配受信任成员来审核UGC、管理组或成为发布环境中启用资源的联系人。
>
>该约定用于发布端[用户和用户组](/help/communities/users.md) （成员和成员组）在创作环境中不重复。
>
>因此，在创作环境中创建社区站点并将受信任成员分配给各种角色时，必须从发布环境中检索成员数据。
>
>这是通过为创作环境启用` [AEM Communities Publish Tunnel Service](/help/communities/deploy-communities.md#tunnel-service-on-author)`来实现的。

#### USER MANAGEMENT {#user-management}

![createsitesettings](assets/createsitesettings.png)

* **允许用户注册**

  如果选中，站点访客可以通过自助注册成为社区成员。
如果未选中，则社区站点为*受限的*，并且必须将站点访客分配给社区站点的成员组、发出请求或通过电子邮件向其发送邀请。 如果未选中，则不应允许匿名访问。
取消选中*私有*&#x200B;社区站点。 默认值为选中。

* **允许匿名访问**

  如果选中，社区站点为&#x200B;*打开*，任何站点访客都可以访问该站点。
如果未选中，则只有已登录成员才能访问该站点。
取消选中*私有*&#x200B;社区站点。 默认值为选中。

* **允许发送消息**

  如果选中，成员可以相互发送消息并发送给社区站点中的组。
如果未选中，则不会为社区设置消息。
默认值为未选中。

* **允许社交登录： Facebook**

  如果选中，则允许网站访客使用其Facebook帐户凭据登录。 应将选定的[Facebook云配置](/help/communities/social-login.md#create-a-facebook-connect-cloud-service)配置为在创建社区站点后将用户添加到社区站点的成员组。
如果未选中，则不会显示Facebook登录信息。
取消选中*私有*&#x200B;社区站点。 默认值为未选中。

* **允许社交登录：Twitter**

  如果选中，则允许网站访客使用其Twitter帐户凭据登录。 应将选定的[Twitter云配置](/help/communities/social-login.md#create-a-twitter-connect-cloud-service)配置为在创建社区站点后将用户添加到社区站点的成员组。
如果未选中，则不会显示Twitter登录信息。
取消选中*私有*&#x200B;社区站点。 默认值为未选中。

>[!NOTE]
>
>**允许社交登录**
>
>虽然Facebook和Twitter配置示例可能存在，并且可用于[生产环境](/help/sites-administering/production-ready.md)，但需要创建自定义Facebook和Twitter应用程序。 请参阅[使用Facebook和Twitter进行社交登录](/help/communities/social-login.md)。

#### 标记 {#tagging}

![站点标记](assets/site-tagging.png)

可以通过选择之前通过[标记控制台](/help/sites-administering/tags.md#tagging-console)定义的标记命名空间来控制可应用于社区内容的标记。

此外，为社区站点选择标记命名空间会限制在定义目录和资源时显示的选择。

* 文本搜索框：开始键入以标识允许在网站上使用的标记。

#### 角色 {#roles}

![社区角色](assets/site-admin-2.png)

社区成员[&#128279;](/help/communities/users.md)的角色已分配了这些设置。

使用提前输入搜索可以轻松查找社区成员。

* **社区管理员**

  开始键入以选择一个或多个社区成员或成员组，这些成员或成员组可以管理社区成员和成员组。

* **社区审查方**

  开始键入以选择一个或多个社区成员或成员组，这些成员或成员组将被信任为用户生成内容的审查方。

* **拥有权限的社区成员**

  开始键入以选择一个或多个社区成员或成员组，以便在为[社区功能](/help/communities/functions.md)选择`Allow Privileged Member`时为其提供创建内容的能力。

* **社区管理员**

  开始键入以选择一个或多个站点管理员，这些管理员可以独立于其他站点管理员和默认社区管理员来处理站点结构。 他们可以在层次结构的任何级别创建组，并成为嵌套组的默认管理员（但之后可以从嵌套组的管理员角色中删除他们）。

#### 审核 {#moderation}

![站点审核](assets/site-moderation.png)

用于审核用户生成内容(UGC)的全局设置由这些设置控制。 单个组件具有用于控制审核的其他设置。

* **内容已预审**

  如果选中，则在审查方批准之前，不会显示发布的社区内容。 默认值为未选中。 有关详细信息，请参阅[审核社区内容](/help/communities/moderate-ugc.md#premoderation)。

* **隐藏内容前的标记阈值**

  如果大于0，则在从公开视图隐藏主题或帖子之前，必须对其进行标记的次数。 如果设置为–1，则标记的主题或帖子永远不会从公开视图中隐藏。 默认值为5。

#### ANALYTICS {#analytics}

![站点分析](assets/site-analytics.png)

* **启用Analytics**

  仅在[为Communities功能](/help/communities/analytics.md)配置Adobe Analytics时可用。
默认值为未选中。 选中后，会出现其他选择菜单：

![站点分析 — 启用](assets/site-analytics-enable.png)

* **云配置框架引用**

  从下拉菜单中，选择为此社区站点配置的Analytics Cloud服务框架。
  `Communities`是[Analytics Configuration for Communities Features](/help/communities/analytics.md#aem-analytics-framework-configuration)文档的框架示例。

#### 翻译 {#translation}

![站点翻译](assets/site-translation.png)

* **允许机器翻译**

  选中后（默认取消选中），将为站点中的UGC启用机器翻译。 这不会影响任何其他内容，例如页面内容，即使站点设置为多语言站点也是如此。 有关为AEM Communities配置许可翻译服务的信息，请参阅[翻译用户生成的内容](/help/communities/translate-ugc.md)。 请参阅[翻译多语言站点的内容](/help/sites-administering/translation.md)以了解完整概述。

![允许机器翻译](assets/allow-machine-translation.png)

* **为所选语言启用机器翻译**

  为机器翻译启用的语言默认为[翻译集成配置](/help/communities/translate-ugc.md#translation-integration-configuration)指定的系统设置。 可以通过删除默认设置和/或从下拉菜单中选择其他语言来覆盖此站点的这些默认设置。

* **选择翻译提供商**

  默认情况下，服务提供商是仅使用`microsoft`进行演示的试用服务。 如果没有许可任何翻译服务提供商，则应取消选中&#x200B;**允许机器翻译**。

* **选择全局共享存储**

  对于具有多个语言副本的网站，全局共享存储提供了从每个语言副本中可见的单个会话线程。 这是通过选择作为语言副本包含的语言之一来实现的。 默认值为&#x200B;*没有全局共享存储*。

* **选择翻译提供商配置**

  选择为许可翻译提供商创建的[翻译集成框架](/help/sites-administering/tc-tic.md)。

* **为您的社区站点选择翻译选项**

   * **翻译整个页面**

     如果选定此选项，则页面上的所有UGC都将翻译为该页面的基本语言。

     默认值为&#x200B;*未选择*。

   * **仅翻译选定内容**

     如果选中，则每个帖子旁边都会显示翻译选项，以便可以将单个帖子翻译为页面的基本语言。
默认值为*选定*。

* **选择持久性选项**

   * **根据用户请求翻译贡献内容并在此后保留**
如果选定此项，则在发出请求之前不会翻译内容。 翻译后，翻译将存储在存储库中。

     默认值为&#x200B;*未选择*。

   * **不保留翻译**

     如果选择，则翻译不会存储在存储库中。

     如果未选择，则会保留翻译。

     默认值为&#x200B;*未选择*。

* **智能渲染**

  选择以下选项之一：

   * `Always show contributions in the original language`（默认）
   * `Always show contributions in user preferred language`
   * `Show contributions in user preferred language for only logged-in users`

### 步骤4 ：创建社区站点 {#step-create-communities-site}

如果需要任何调整，请使用&#x200B;**返回**&#x200B;按钮进行调整。

选择并启动&#x200B;**创建**&#x200B;后，将无法中断创建站点的过程。

创建站点后：

* 不支持更改url （节点名称）。
* 对社区站点模板的未来更改不会影响已创建的社区站点。
* 禁用社区站点模板不会影响已创建的社区站点。
* 可以通过修改社区站点的属性来编辑其的[STRUCTURE](#modify-structure)。

![create-site](assets/create-site1.png)

进程完成后，新站点的文件夹会显示在Communities Sites控制台中，作者可以在其中添加页面内容，管理员可以修改站点的属性。

![modify-site-property](assets/modify-site-property.png)

要编辑社区站点，请选择其项目文件夹以将其打开：

![站点项目](assets/site-project.png)

当使用鼠标将鼠标悬停在站点上或触摸站点卡时，会出现允许出现以下内容的图标：

* [在创作模式下编辑站点](#authoring-site-content)
* [打开站点属性以进行修改](#modifying-site-properties)
* [发布站点](#publishing-the-site)
* [导出站点](#exporting-the-site)
* [删除站点](#deleting-the-site)

## 创作站点内容 {#authoring-site-content}

可以使用与任何其他AEM网站相同的工具创作站点的内容。 要打开站点进行创作，请选择鼠标悬停在站点上时显示的`Open Site`图标。 站点将在新选项卡中打开，以便社区站点控制台保持可访问状态。

![站点内容](assets/site-content.png)

>[!NOTE]
>
>如果不熟悉AEM，请查看有关[基本处理](/help/sites-authoring/basic-handling.md)的文档以及[页面创作快速指南](/help/sites-authoring/qg-page-authoring.md)。

## 修改站点属性 {#modifying-site-properties}

![编辑站点](assets/edit-site.png)

在站点创建过程中指定的现有站点的属性，可以通过选择鼠标悬停在站点上时显示的`Edit Site`图标进行修改。

`Details of the following properties match the descriptions provided in the` [站点创建](#site-creation)分区。

![modify-site-basicinfo](assets/modify-site-basicinfo.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改：

* 社区站点标题
* 社区站点描述

不能修改社区站点名称。

选择其他社区站点模板对现有社区站点没有影响，因为模板和站点之间没有连接。

相反，可以修改社区站点的[STRUCTURE](#modify-structure)。

### 修改结构 {#modify-structure}

“结构”面板允许修改最初从所选社区站点模板创建的结构。 在面板中，可以：

* 将其他[社区功能](/help/communities/functions.md)拖放到站点结构中。
* 在站点结构中社区功能的实例上：

   * **`gear icon`**

     编辑设置，包括显示标题和URL名称，以及[拥有权限的成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`trashcan icon`**

     从站点结构中移除（删除）函数。

   * **`grid icon`**

     修改在站点顶级导航栏中显示的函数顺序。

>[!NOTE]
>
>您可以更改“站点结构”中所有函数（顶部的函数除外）的顺序。 因此，无法更改社区站点的主页。

>[!CAUTION]
>
>* 尽管显示标题可能会发生更改并且不会产生副作用，但建议不要编辑属于社区站点的社区函数的URL名称。
>
>例如，重命名URL不会移动现有UGC，因此“丢失”UGC。

>[!CAUTION]
>
>组函数必须&#x200B;*不是*&#x200B;是网站结构中的&#x200B;*第一个或唯一的*&#x200B;函数。
>
>任何其他函数（如[page函数](/help/communities/functions.md#page-function)）都必须包含并首先列出。

#### 示例：将目录函数添加到社区站点结构 {#example-adding-a-catalog-function-to-a-community-site-structure}

![add-catalog-site](assets/add-catalog-site.png)

### 修改设计 {#modify-design}

“设计”面板允许应用新主题：

* [社区站点主题](#community-site-theme)
* [社区站点品牌化](#community-site-branding)

   * 滚动到面板底部，以便更改品牌图像。

### 修改设置 {#modify-settings}

通过“设置”面板，可访问社区站点创建步骤3的子面板下的大多数设置：

* [用户管理](#user-management)
* [标记](#tagging)
* [审核](#moderation)
* [成员角色](#roles)
* [分析](#analytics)
* [翻译](#translation)

### 修改缩略图 {#modify-thumbnail}

利用“缩略图”面板，可上传图像以在“社区站点”控制台中表示站点。

## 发布站点 {#publishing-the-site}

新建或修改社区站点后，通过选择鼠标悬停在站点上时显示的`Publish Site`图标，可以发布（激活）站点。

![发布站点](assets/publish-site.png)

成功发布站点后有指示。

![站点已发布](assets/site-published.png)

### 使用嵌套组发布 {#publishing-with-nested-groups}

发布社区站点后，必须单独发布使用[组控制台](/help/communities/groups.md)创建的每个子社区（嵌套组）。

## 导出站点 {#exporting-the-site}

![export-site](assets/export-site.png)

将鼠标悬停在该站点上时，选择导出图标，以便创建同时存储在[包管理器](/help/sites-administering/package-manager.md)中并下载的社区站点的包。

站点包中未包含UGC。

## 删除站点 {#deleting-the-site}

![deleteicon](assets/deleteicon.png)

要删除社区站点，请选择将鼠标悬停在社区站点控制台中的站点上时显示的删除站点图标。 此操作将删除与站点关联的所有项目，例如UGC、用户组、资源和数据库记录。

## 已创建社区用户组 {#created-community-user-groups}

发布新的社区站点后，将新建成员组（在发布环境中创建用户组），这些成员组具有为各种管理和成员角色设置的相应权限。

为成员组创建的名称包含[步骤1](#step13asitetemplate)中给定的&#x200B;*site-name*（显示在URL中的名称）。 它还包含唯一ID，以避免与具有不同社区站点根目录的社区站点和组具有相同的站点名称发生冲突。

例如，如果标题为“Getting Started Tutorial”的网站的名称为“engage”，则版主的用户组将为：

* title：社区参与审查方
* 名称： community-*engage-uid*-moderators

在创建站点时，任何成员都分配了作为版主或组管理员的角色，这些成员将分配给相应的组并分配给成员组。 发布新站点时，会在发布上创建这些组和成员分配。

有关详细信息，请参阅[管理用户和用户组](/help/communities/users.md)。

>[!NOTE]
>
>如果[允许社交登录： Facebook](#user-management)已启用，则用户组`community-<site-name>-<uid>-members`后
>创建，应用的[Facebook云服务](/help/communities/social-login.md#createafacebookcloudservice)应配置为将用户添加到此组。

## 配置身份验证错误 {#configure-for-authentication-error}

默认情况下，当用户输入错误的凭据且无法登录时，社区站点会重定向到示例登录页面。 此示例登录在[生产服务器](/help/sites-administering/production-ready.md)上不存在。

要正确重定向，请在配置站点并推送到发布后，完成以下步骤以获取身份验证失败以重定向到社区站点：

* 在每个AEM发布实例上。
* 使用管理员权限登录。
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)。

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)。

* 找到`Adobe Granite Login Selector Authentication Handler`。
* 选择`pencil`图标以打开配置进行编辑。
* 按如下方式输入&#x200B;**登录页映射**：

  `/content/sites/<site-name>/path/to/login/page:/content/sites/<site-name>`

  例如：
  `/content/sites/engage/en/signin:/content/sites/engage/en`

* 选择&#x200B;**保存**。

![auth-error](assets/auth-error.png)

### 测试身份验证重定向 {#test-authentication-redirection}

在配置有社区站点的登录页面映射的同一AEM发布实例上：

* 浏览到社区站点主页。

   * 例如，[https://localhost:4503/content/sites/engage/en.html](https://localhost:4503/content/sites/engage/en.html)

* 选择“注销”。
* 选择“登录”。
* 输入不正确的凭据，如用户名“x”和密码“x”。
* 登录页面应显示“无效登录”错误。

![测试身份验证](assets/test-authentication.png)

## 从主站点控制台访问社区站点 {#accessing-community-sites-from-main-sites-console}

从全局导航站点控制台中，社区站点位于`Community Sites`文件夹中。

虽然可以通过此方式访问社区站点，但对于管理任务，应从社区站点控制台访问社区站点。

![访问站点](assets/access-site.png)
