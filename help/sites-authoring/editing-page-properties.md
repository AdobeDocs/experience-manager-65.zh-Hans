---
title: 编辑页面属性
description: 在Adobe Experience Manager中为页面定义所需的属性。
exl-id: 3cd9374f-6f16-40fb-97cf-5f9a750b8dd2
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
mini-toc-levels: 2
source-git-commit: d0515a6a3d08e181eada4a22e0d128305148e6ea
workflow-type: tm+mt
source-wordcount: '2477'
ht-degree: 38%

---


# 编辑页面属性{#editing-page-properties}

您可以为页面定义所需的属性。这些属性会因页面性质而异。例如，某些页面可能已连接到Live Copy，而其他页面未连接到，因此Live Copy信息会根据需要变得可用。

## 页面属性 {#page-properties}

属性分布于多个选项卡中。

### 基本 {#basic}

#### 标题和标记 {#tile}

* **标题** — 页面的标题显示在各种位置
   * 例如，**网站**&#x200B;选项卡列表和&#x200B;**站点**&#x200B;卡片/列表视图。
   * 这是必填字段。
* **标记** — 在此，可以通过更新选择框中的列表在页面中添加或删除标记。
   * 选择某个标记后，该标记会列在选择框的下方。 您可以使用“x”从此列表中移除标记。
   * 通过在空的选择框中键入名称可输入新标记。
      * 当您按Enter键时，将创建新标记。
      * 新标记将在右侧显示一个小星号，指示它是新标记。
   * 通过下拉列表，您可以从现有标记中进行选择。
   * 当您将鼠标悬停在选择框中的标记条目上时，会显示 x，用于为此页面删除该标记。
   * 有关标记的详细信息，请参阅[使用标记。](/help/sites-authoring/tags.md)
* **在导航中隐藏** — 指示在生成的站点的页面导航中是显示还是隐藏页面

#### 品牌化 {#branding}

通过将品牌概要附加到每个页面标题，跨页面应用一致的品牌识别。此功能需要使用 2.14.0 版或更高版本的[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans)中的页面组件。

* **覆盖** – 选中可在此页面上定义品牌概要。
   * 该值会由任何子页面继承，除非它们也设置了&#x200B;**覆盖**&#x200B;值。
* **覆盖值** — 要附加到页面标题的品牌概要的文本
   * 该值附加到页面标题后的竖线字符（如`Cycling Tuscany | Always ready for the WKND`）

#### 更多标题和描述 {#more}

* **页面标题** — 要在页面上使用的标题
   * 通常由标题组件使用
   * 如果留空，则会使用&#x200B;**标题**。
* **导航标题** — 您可以指定单独的标题以在导航中使用（例如，如果您希望某些内容能更加简洁）。
   * 如果留空，则会使用&#x200B;**标题**。
* **子标题** — 要在页面上使用的子标题
* **描述** — 页面的描述、用途或要添加的任何其他详细信息

#### 开启/结束时间 {#on-time}

页面的打开/关闭时间是一种临时隐藏已发布内容的便捷方法。 关闭发布实例后，内容仍会保留在该实例上。 关闭页面不会取消发布内容。

* **开启时间** – 使已发布页面在发布环境中可见（呈现）的日期和时间。该页面必须手动发布或通过预配置的自动复制进行发布。

   * 如果已经[发布，](/help/sites-authoring/publishing-pages.md)此页面在发布实例上可用，但在指定时间呈现之前保持隐匿（隐藏）状态。
   * 如果未发布并[配置为自动复制，](/help/sites-deploying/replication.md)则页面将在指定的时间自动发布，然后呈现。
   * 如果未发布且未配置为自动复制，则该页面不会自动发布，因此在尝试访问该页面时将会显示404。

* **结束时间** – 与&#x200B;**开启时间**&#x200B;类似并且经常与其结合使用，可定义已发布页面在发布环境中隐藏的时间。

对于要发布的页面，请将这些字段（**开启时间**&#x200B;和&#x200B;**关闭时间**）留空，这些字段可立即在发布环境中使用并可用，直到它们被停用（一般场景）。

>[!NOTE]
>如果&#x200B;**开启时间**&#x200B;或&#x200B;**结束时间**&#x200B;是过去的时间，并且已配置自动复制，则会立即触发相关操作。

>[!TIP]
>
>开启/关闭时间严格处理已发布的内容（手动或通过自动复制）。 因此，发布工作流（例如批准内容的工作流）不会由触发为开启/关闭时间，并且开启/关闭时间不会影响页面的发布状态。 因此，打开/关闭时间最适合临时显示/隐藏已批准和发布的内容。
>
>如果要发布包含所有关联工作流的新内容，或从站点中完全删除（取消发布内容），请考虑[管理您的发布。](/help/sites-authoring/publishing-pages.md#manage-publication)

#### 虚 URL {#vanity-url}

输入此页面的虚URL，这样可让您的URL长度更短和/或更具有表现性。

例如，如果将网站`http://example.com,`的虚URL设置为由路径`/v1.0/startpage`标识的页面`welcome`，则`http://example.com/welcome`将是`http://example.com/content/v1.0/startpage`的虚URL

>[!CAUTION]
>
>虚 URL：
>
>* 必须是唯一的。
>* 不支持正则表达式模式。
>* 不应设置为现有页面。

配置Dispatcher以启用对虚名URL的访问。 有关详细信息，请参阅[启用对虚名URL的访问](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hans#enabling-access-to-vanity-urls-vanity-urls)。

* **添加** — 点击或单击可添加虚URL。
* **删除** — 点击或单击可删除虚URL。
  **重定向虚URL** — 指示您希望页面使用虚URL还是重定向到页面的实际URL

### 高级 {#advanced}

#### 设置 {#settings}

* **语言** – 页面语言
* **语言根** – 如果页面是语言副本的根，则必须选中
* **重定向** – 指示此页面应自动重定向到的页面
* **设计** — 指示用于此页面的[设计](/help/sites-developing/designer.md)。
* **别名** – 指定要用于此页面的别名
   * 例如，如果您为页面 `/content/wknd/us/en/magazine/members-only` 定义别名 `private`，则也可以通过 `/content/wknd/us/en/magazine/private` 访问此页面
   * 创建别名将设置页面节点上的 `sling:alias` 属性，这只会影响资源，而不会影响存储库路径。
   * 无法发布编辑器中按别名处理的页面。编辑器中的[发布选项](/help/sites-authoring/publishing-pages.md)仅适用于通过其实际路径访问的页面。
   * 有关详细信息，请参阅SEO和URL管理最佳实践下的[本地化的页面名称](/help/managing/seo-and-url-management.md#localized-page-names)。

#### 配置 {#configuration}

* **继承自&lt;*路径*>** — 启用/禁用页面&#x200B;**云配置**&#x200B;的继承
* **云配置** – 配置的路径

#### 模板设置 {#templates}

* **允许的模板** – [定义在此子分支内可用的模板的列表](/help/sites-authoring/templates.md#allowingatemplate)

#### 身份验证要求 {#authentication}

* **启用** — 启用（或禁用）身份验证的使用，以便您可以访问该页面
* **登录页面** – 要用于登录的页面

>[!NOTE]
>
>页面的已关闭的用户组在&#x200B;**[权限](/help/sites-authoring/editing-page-properties.md#permissions)**&#x200B;选项卡上定义。

>[!CAUTION]
>
>**[权限](#permissions)**&#x200B;选项卡允许根据`granite:AuthenticationRequired` mixin的存在来编辑CUG配置。 如果使用已弃用的CUG配置配置配置页面权限，则根据是否存在`cq:cugEnabled`属性，将在&#x200B;**身份验证要求**&#x200B;下显示一条警告消息，并且该选项不可编辑，[权限](/help/sites-authoring/editing-page-properties.md#permissions)也不可编辑。
>
>
>在这种情况下，必须在[经典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中编辑CUG权限。

#### 导出 {#export}

* **配置** — 指定导出配置

#### SEO {#seo}

* **规范URL** — 用于覆盖页面的规范URL
   * 如果留空，则页面的URL是它的规范URL。
* **Robots标记** — 使用下拉菜单选择Robots标记以控制搜索引擎爬网程序的行为
   * 有些选项会相互冲突，在这种情况下，以更宽松的选项为准。
* **生成站点地图** — 在选中时，将为此页面及其后代生成`sitemap.xml`。

### 图像 {#images}

#### 特色图像 {#featured-image}

此部分用于选择和配置要显示的图像。 这用于引用页面的组件；例如，Teaser、页面列表等。

* **图像** — 您可以&#x200B;**挑选**&#x200B;资源，或浏览要上传的文件，然后&#x200B;**编辑**&#x200B;或&#x200B;**清除**&#x200B;选定的图像。
* **替换文本** — 用于表示图像的含义和/或功能的文本，通常由屏幕阅读器使用
* **继承 — 取自DAM资源的值** — 选中后，将使用DAM中`dc:description`元数据的值填充替换文本。

#### 缩略图 {#thumbnail}

此部分用于选择和配置页面的图像缩略图。 这用于引用页面的组件；例如，Teaser、页面列表等。

* **生成预览** — 生成要用作缩略图的页面预览
* **上传图像** — 上传要用作缩略图的图像
* **选择图像** — 选择要用作缩略图的现有资源
* **还原** — 在您更改缩略图后，此选项将变得可用。 如果不想保留您的更改，可以在保存前还原更改。

### Cloud Service {#cloud-services}

* **Cloud Service配置** — 定义用于页面的云服务的配置
* **继承自** — 对于活动副本和语言副本，默认从Blueprint继承云配置。
   * 取消选中以覆盖继承

### 个性化 {#personalization}

#### ContextHub 配置 {#contexthub}

* **继承自** — 默认情况下，ContextHub配置继承自父页面。
   * 取消选中以覆盖继承。
* **ContextHub路径** — 选择[ContextHub配置](/help/sites-developing/ch-configuring.md)
* **段路径** — 选择[段路径](/help/sites-administering/segmentation.md)。

#### 定位配置 {#targeting}

选择一个[品牌以指定定位范围。](/help/sites-authoring/target-adobe-campaign.md)

>[!NOTE]
>此选项要求用户帐户属于 `Target Adminstrators` 组。

### 权限 {#permissions}

使用&#x200B;**权限**&#x200B;选项卡定义哪些用户、组或[封闭用户组(CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=zh-Hans)可以访问和/或修改页面。

* [添加权限](/help/sites-administering/user-group-ac-admin.md)
* [编辑已关闭的用户组](/help/sites-administering/cug.md#applying-your-closed-user-group-to-content-pages)
* 查看[有效权限](/help/sites-administering/user-group-ac-admin.md)

>[!CAUTION]
>
>**权限**&#x200B;选项卡允许根据`granite:AuthenticationRequired` mixin的存在来编辑CUG配置。 如果使用已弃用的CUG配置配置配置页面权限，则根据是否存在`cq:cugEnabled`属性，将显示一条警告消息，并且CUG权限不可编辑，[高级](/help/sites-authoring/editing-page-properties.md#advanced)选项卡上的身份验证要求也不可编辑。
>
>
>在这种情况下，必须在[经典UI](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)中编辑CUG权限。

>[!NOTE]
>
>“权限”选项卡不允许创建空的CUG组，通过这种简单的方式可以拒绝每个用户访问。 为此，必须使用CRX Explorer。 有关详细信息，请参阅文档[用户、组和访问权限管理](/help/sites-administering/user-group-ac-admin.md)。

### Blueprint {#blueprint}

此选项卡仅对用作 Blueprint 的页面可见。Blueprint 用作 Live Copy 的基础，并且是[多站点管理](/help/sites-administering/msm.md)的一部分。

* **转出** — 启动Blueprint内容到活动副本的转出
* **Live Copy概述** — 打开一个窗口以浏览Live Copy页面结构
* **当前活动副本** — 基于所选Blueprint页面的页面列表（即活动副本）
* **转出配置** — 定义页面的转出配置

### Live Copy {#live-copy}

此选项卡仅对配置为 Live Copy 的页面可见。与[Blueprint一样，](#blueprint)活动副本是[多站点管理的一部分。](/help/sites-administering/msm.md)

* **同步** — 将Live Copy与Blueprint同步，并保留本地修改
* **重置** — 将Live Copy重置为Blueprint的状态，并删除本地修改
* **暂停** — 暂停Live Copy以防止进一步的转出修改
* **分离** — 从Blueprint分离Live Copy

#### 源 {#source}

* 显示此 Live Copy 的 Blueprint 的路径

#### 状态 {#status}

* 列出页面的当前 Live Copy 状态

#### 配置 {#live-copy-config}

* **Live Copy继承** — 如果选中，Live Copy配置将在所有子项上都有效。
* **从父项继承转出配置** — 如果选中，则从页面的父项继承转出配置。
* **选择转出配置** – 定义从 Blueprint 传播修改的情况，并且仅在未选择&#x200B;**从父项继承转出配置**&#x200B;时可用
* **排除的路径列表**

## 编辑页面属性 {#editing-page-properties-1}

您可以定义页面属性：

* 从&#x200B;**Sites**&#x200B;控制台中：

   * [创建页面](/help/sites-authoring/managing-pages.md#creating-a-new-page)（属性的子集）

   * 单击或点按&#x200B;**属性**

      * 单页面
      * 多个页面（只有一部分属性可用于整体编辑）

* 从页面编辑器中：

   * 使用&#x200B;**页面信息**（然后&#x200B;**打开属性**）

### 从 Sites 控制台中 – 单个页面 {#from-the-sites-console-single-page}

单击或点按&#x200B;**属性**&#x200B;以定义页面属性：

1. 使用&#x200B;**Sites**&#x200B;控制台，导航到要查看和编辑属性的页面位置。

1. 使用以下任一方式为所需的页面选择&#x200B;**属性**&#x200B;选项：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [选择模式](/help/sites-authoring/basic-handling.md#selectionmode)

   此时会使用相应的选项卡显示页面属性。

1. 查看或编辑所需的属性。

1. 然后，使用&#x200B;**保存**&#x200B;保存您的更新，接着使用&#x200B;**关闭**，以便返回控制台。

### 编辑页面时 {#when-editing-a-page}

编辑页面时，您可以使用&#x200B;**页面信息**&#x200B;来定义页面属性：

1. 打开要编辑属性的页面。

1. 选择&#x200B;**页面信息**&#x200B;图标以打开选择菜单：

   ![screen_shot_2018-03-22at095740](assets/screen_shot_2018-03-22at095740.png)

1. 选择&#x200B;**打开属性**，此时将打开一个对话框，允许您编辑按相应选项卡排序的属性。 工具栏右侧还提供以下按钮：

   * **取消**
   * **保存并关闭**

1. 使用&#x200B;**保存并关闭**&#x200B;按钮以保存更改。

### 从 Sites 控制台中 – 多个页面 {#from-the-sites-console-multiple-pages}

从&#x200B;**站点**&#x200B;控制台中，您可以选择多个页面，然后使用&#x200B;**查看属性**&#x200B;查看和/或编辑页面属性。 这称为批量编辑页面属性。

>[!NOTE]
>
>也可以对资源使用批量编辑属性功能。两者相似，但在几个方面有所不同。 有关详细信息，请参阅[编辑多个Assets的属性](/help/assets/metadata.md)。
>
>还有[批量编辑器](/help/sites-administering/bulk-editor.md)。 通过此编辑器，您可以使用GQL(Google查询语言)从多个页面搜索内容，然后直接使用批量编辑器编辑内容，再将更改保存到原始页面。

可以通过多种方法选择要批量编辑的多个页面，这些方法包括：

* 在浏览 **Sites** 控制台时
* 在使用&#x200B;**搜索**&#x200B;找到一组页面后

![epp-01](assets/epp-01.png)

选择页面后，单击或点按&#x200B;**属性选项**，此时会显示批量属性：

![epp-02](assets/epp-02.png)

只有符合以下条件的页面才能进行批量编辑：

* 属于同一资源类型
* 不是 Live Copy 的一部分

   * 如果有任何页面在 Live Copy 中，则会在属性打开时显示一条消息。

进入“批量编辑”后，可以执行以下操作：

* **查看**

  查看多个页面的页面属性时，您可以看到以下内容：

   * 受影响的页面列表

      * 您可以根据需要进行选择/取消选择

   * 选项卡

      * 与查看单页面的属性时一样，这些属性按选项卡进行排序。

   * 一部分属性

      * 将显示所有选定页面的可用属性，这些属性已明确定义为可批量编辑。
      * 如果将选择的页面减少到一页，则会显示所有属性。

   * 具有相同值的通用属性

      * 在“查看”模式中，只显示具有相同值的属性。
      * 当字段为多值（例如，标记）时，仅当&#x200B;*所有*&#x200B;为公共值时才会显示值。 如果只有一些是通用的，则仅在编辑时才显示它们。

  如果不存在具有相同值的属性，则会显示一条消息。

* **编辑**

  编辑多个页面的页面属性时：

   * 您可以更新可用字段中的值。

      * 当您选择&#x200B;**完成**&#x200B;时，新值会应用于所有选定页面。
      * 当字段有多个值时（例如，“标记”），您可以附加新值或删除公共值。

   * 如果不同页面具有相同的字段，但这些字段的值不同，则会用一个特殊的值表示它们，例如文本`<Mixed Entries>`。

>[!NOTE]
>
>可以对页面组件进行配置，以指定可批量编辑的字段。请参阅[配置页面以批量编辑页面属性](/help/sites-developing/bulk-editing.md)。
