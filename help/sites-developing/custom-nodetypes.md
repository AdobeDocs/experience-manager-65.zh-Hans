---
title: 自定义节点类型
description: Adobe Experience Manager (AEM)基于Sling，使用JCR存储库和由两者提供的节点类型，但AEM也提供了一系列自定义节点类型
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: bfd50aa9-579e-47d5-997d-ec764c782497
source-git-commit: 939132e8b461b51e1c49237e481243bcc5de3bf6
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 9%

---

# 自定义节点类型{#custom-node-types}

由于Adobe Experience Manager (AEM)基于Sling并使用JCR存储库，因此这两者提供的节点类型均可供使用：

* [JCR节点类型](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/3_Repository_Model.html#3.1.7-Node-Types)
* [Sling节点类型](https://cwiki.apache.org/confluence/display/SLING/Sling+Node+Types)

除此之外。 AEM提供了一系列自定义节点类型。

## 审核 {#audit}

### cq：AuditEvent {#cq-auditevent}

**描述**

定义审核事件节点的节点类型。

* `@prop cq:time`
* `@prop cq:userid`
* `@prop cq:path`
* `@prop cq:type`
* `@prop cq:category`
* `@prop cq:properties`

**定义**

* `[cq:AuditEvent]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
* `- cq:time (date)`
* `- cq:userid (string)`
* `- cq:path (string)`
* `- cq:type (string)`
* `- cq:category (string)`
* `- cq:properties (binary)`

## 注释 {#comment}

### cq：Comment {#cq-comment}

**描述**

定义注释节点的节点类型。

* `@prop userIdentifier`

**定义**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq：CommentAttachment {#cq-commentattachment}

**描述**

定义节点的类型 `commentattachment` 节点

**定义**

* `[cq:CommentAttachment] > nt:file`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：CommentContent {#cq-commentcontent}

**描述**

定义评论内容节点的节点类型

**定义**

* `[cq:Comment] > mix:title, mix:created, mix:language, nt:unstructured, cq:Taggable`
* `- email (string)`
* `- ip (string)`
* `- referer (string)`
* `- url (string)`
* `- userAgent (string)`
* `- userIdentifier (string)`
* `- authorizableId (string)`

### cq：GeoLocation {#cq-geolocation}

**描述**

定义以小数位数(DD)表示的地理位置的mixin

* `@prop latitude`  — 使用小数位数编码为双精度的latitude
* `@prop longitude`  — 使用小数位数编码为双倍的经度

**定义**

* `[cq:GeoLocation] mixin`
* `- latitude (double)`
* `- longitude (double)`

### cq：Trackback {#cq-trackback}

**描述**

定义引用通告节点的节点类型。

**定义**

* `[cq:Trackback] > mix:title, mix:created, mix:language, nt:unstructured`

## 核心 {#core}

### cq:Page {#cq-page}

**描述**

定义默认CQ页面。

* `@node jcr:content`  — 页面的主要内容。

**定义**

* `[cq:Page] > nt:hierarchyNode orderable`
   * `+ jcr:content (nt:base) = nt:unstructured copy primary`
   * `+ * (nt:base) = nt:base version`

### cq：PseudoPage {#cq-pseudopage}

**描述**

定义将节点标记为伪页面的mixin类型。 这意味着它们可以适应页面和WCM编辑支持。

**定义**

* `[cq:PseudoPage] mixin`

### cq:PageContent {#cq-pagecontent}

**描述**

定义页面内容的默认节点，具有WCM使用的最小属性。

* `@prop jcr:title`  — 页面标题。
* `@prop jcr:description`  — 此页面的描述。
* `@prop cq:template`  — 用于创建页面的模板的路径。
* `@prop cq:allowedTemplates`  — 用于确定允许模板的路径的正则表达式列表。
* `@prop pageTitle`  — 标题通常显示在 `<title>` 标记之前。
* `@prop navTitle`  — 导航中通常使用的标题。
* `@prop hideInNav`  — 指定是否应在导航中隐藏页面。
* `@prop onTime`  — 此页面生效的时间。
* `@prop offTime`  — 此页面失效的时间。
* `@prop cq:lastModified`  — 上次修改页面（或其段落）的日期。
* `@prop cq:lastModifiedBy`  — 最后一个更改页面（或其段落）的用户。
* `@prop jcr:language`  — 页面内容的语言。

>[!NOTE]
>
>页面内容不必使用此类型。

**定义**
* `[cq:PageContent] > nt:unstructured, mix:title, mix:created, cq:OwnerTaggable, sling:VanityPath, cq:ReplicationStatus, sling:Resource orderable`
   * `- cq:template (string)`
   * `- cq:allowedTemplates (string) multiple`
   * `- pageTitle (string)`
   * `- navTitle (string)`
   * `- hideInNav (boolean)`
   * `- onTime (date)`
   * `- offTime (date)`
   * `- cq:lastModified (date)`
   * `- cq:lastModifiedBy (string)`
   * `- cq:designPath (string)`
   * `- jcr:language (string)`

### cq:Template {#cq-template}

**描述**

定义CQ模板。

* `@node jcr:content`  — 新页面的默认内容。
* `@node icon.png`  — 包含特征图标的文件。
* `@node thumbnail.png`  — 包含特征缩略图图像的文件。
* `@node workflows`  — 自动分配工作流配置。 配置将遵循以下结构：
   * `+ workflows`
      * `+ name1`
         * `- cq:path`
            * `- cq:workflowName`
* `@prop allowedParents`  — 用于确定允许作为父模板的模板的路径的正则表达式模式。
* `@prop allowedChildren`  — 用于确定允许作为子模板的模板的路径的正则表达式模式。
* `@prop ranking`  — 在“创建页面”对话框的模板列表中的位置。

**定义**

* `[cq:Template] > nt:hierarchyNode, mix:title`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ jcr:content (nt:base) copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `+ workflows (nt:base) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `- ranking (long)`

### cq:Component {#cq-component}

**描述**

定义CQ组件。

* `@prop jcr:title`  — 组件的标题。
* `@prop jcr:description`  — 组件的描述。
* `@node dialog`  — 主对话框。
* `@prop dialogPath`  — 主对话框路径（对话框的替代方法）。
* `@node design_dialog`  — “设计”对话框。
* `@prop cq:cellName`  — 设计单元格的名称。
* `@prop cq:isContainer`  — 指示这是否为容器组件。 这会强制使用子组件的单元格名称而不是路径名称。 例如， `parsys` 是一个容器组件。 如果未定义此值，则会根据是否存在 `cq:childEditConfig`.
* `@prop cq:noDecoration`  — 如果为true，则无修饰 `div` 标记在包含此组件时绘制。
* `@node cq:editConfig`  — 定义编辑栏参数的配置。
* `@node cq:childEditConfig`  — 由子组件继承的编辑配置。
* `@node cq:htmlTag`  — 定义添加到“周围”的其他标记属性 `div` 标记。
* `@node icon.png` — 包含特征图标的文件。
* `@node thumbnail.png`  — 包含特征缩略图图像的文件。
* `@prop allowedParents`  — 用于确定允许作为父组件的组件的路径的正则表达式模式。
* `@prop allowedChildren`  — 用于确定允许作为子组件的组件的组件的路径的正则表达式模式。
* `@node virtual`  — 包含反映用于组件拖放的虚拟组件的子节点。
* `@prop componentGroup`  — 组件组的名称，用于组件拖放。
* `@node cq:infoProviders`  — 包含子节点，每个子节点都有一个属性 `className` 指的是 `PageInfoProvider`.

**定义**

* `[cq:Component] > nt:folder, mix:title, sling:ResourceSuperType`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ * (nt:base) = nt:base multiple version`
   * `+ dialog (nt:base) = nt:unstructured copy`
   * `- dialogPath (string)`
   * `+ design_dialog (nt:base) = nt:unstructured copy`
   * `- cq:cellName (string)`
   * `- cq:isContainer (boolean)`
   * `- cq:noDecoration (boolean)`
   * `+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:childEditConfig (cq:EditConfig) = cq:EditConfig copy`
   * `+ cq:htmlTag (nt:base) = nt:unstructured copy`
   * `+ icon.png (nt:file) copy`
   * `+ thumbnail.png (nt:file) copy`
   * `- allowedParents (string) multiple`
   * `- allowedChildren (string) multiple`
   * `+ virtual (nt:base) = sling:Folder copy`
   * `- componentGroup (string)`
   * `+ cq:infoProviders (nt:base) = nt:unstructured copy`

### cq：ComponentMixin {#cq-componentmixin}

**描述**

将CQ组件定义为mixin类型。

**定义**

`[cq:ComponentMixin] > cq:Component mixin`

### cq：EditConfig {#cq-editconfig}

**描述**

定义“编辑栏”的配置。

* `@prop cq:dialogMode`  — 对话框模式：
   * `floating`  — 对于普通浮动对话框
   * `inline`  — 内联编辑
   * `auto`  — 自动检测（取决于可用空间）
* `@node cq:inplaceEditing`  — 为此组件替换编辑配置。
* `@prop cq:layout` — 编辑栏布局：
   * `editbar`  — 编辑栏
   * `rollover`  — 将鼠标指针置于框架之上
   * `auto`  — 自动检测
* `@node cq:formParameters` — 要添加到对话框表单的其他参数。
* `@prop cq:actions` — 操作列表（编辑栏按钮或菜单项）。
* `@node cq:actionConfigs`  — 用于编辑栏或菜单项的小组件配置。
* `@prop cq:emptyText`  — 没有可视内容时显示的文本。
* `@node cq:dropTargets`  — 收藏集 `{@link cq:DropTargetConfig}` 节点。

**定义**

* `[cq:EditConfig] > nt:unstructured, nt:hierarchyNode orderable`
   * `- cq:dialogMode (string) < 'auto', 'floating', 'inline'`
   * `- cq:layout (string) < 'editbar', 'rollover', 'auto' + cq:formParameters (nt:base) = nt:unstructured`
   * `- cq:actions (string) multiple`
   * `+ cq:actionConfigs (nt:base) = nt:unstructured`
   * `- cq:emptyText (string)`
   * `+ cq:dropTargets (nt:base) = nt:unstructured`
   * `+ cq:listeners (nt:base) = cq:EditListenersConfig`

### cq：DropTargetConfig {#cq-droptargetconfig}

**描述**

配置组件的一个放置目标。 此节点的名称将用作拖放的ID。

* `@prop accept`  — 此放置目标接受的MIME类型列表；例如 `["image/*"]`
* `@prop groups`  — 接受源的拖放组列表。
* `@prop propertyName`  — 用于存储引用的属性的名称。

**定义**

* `[cq:DropTargetConfig] > nt:unstructured orderable`
   * `- accept (string) multiple`
   * `- groups (string) multiple`
   * `- propertyName (string)`
   * `+ parameters (nt:base) = nt:unstructured`

### cq：VirtualComponent {#cq-virtualcomponent}

**描述**

定义虚拟CQ组件。 它们当前仅用于新组件拖放向导。

* `@prop jcr:title`  — 此组件的标题。
* `@prop jcr:description`  — 此组件的描述。
* `@node cq:editConfig`  — 编辑定义编辑栏参数的配置。
* `@node cq:childEditConfig` — 编辑由子组件继承的配置。
* `@node icon.png`  — 包含特征图标的文件。
* `@node thumbnail.png`  — 包含特征缩略图图像的文件。
* `@prop allowedParents`  — 用于确定允许作为父组件的组件的路径的正则表达式模式。
* `@prop allowedChildren`  — 用于确定允许作为子组件的组件的组件的路径的正则表达式模式。
* `@prop componentGroup`  — 用于组件拖放的组件组的名称。

**定义**

`[cq:VirtualComponent] > nt:folder, mix:title`
`- * (undefined)`
`- * (undefined) multiple`
`+ * (nt:base) = nt:base multiple version`
`+ cq:editConfig (cq:EditConfig) = cq:EditConfig copy`
`+ icon.png (nt:file) copy`
`+ thumbnail.png (nt:file) copy`
`- allowedParents (string) multiple`
`- allowedChildren (string) multiple`
`- componentGroup (string)`

### cq：EditListenersConfig {#cq-editlistenersconfig}

**描述**

定义要在编辑事件上执行的（客户端）侦听器。 这些值必须引用有效的客户端侦听器函数或包含预定义的快捷方式：

* `REFRESH_PAGE`
* `REFRESH_SELF`
* `REFRESH_PARENT`

* `@prop aftercreate`  — 在创建组件后触发。
* `@prop afteredit`  — 在编辑（修改）组件后触发。
* `@prop afterdelete`  — 删除组件后触发。
* `@prop afterinsert`  — 将组件添加到此容器后触发。
* `@prop afterremove`  — 从容器中删除组件后触发。
* `@prop aftermove`  — 在此容器中移动组件后触发。

**定义**

* `[cq:EditListenersConfig]`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `+ &ast; (nt:base) = nt:base multiple version`
   * `- aftercreate (string)`
   * `- afteredit (string)`
   * `- afterdelete (string)`
   * `- afterinsert (string)`
   * `- afterremove (string)`
   * `- aftermove (string)`

## DAM {#dam}

### dam:AssetContent {#dam-assetcontent}

**描述**

DAM资源的内容。

**定义**

* `[dam:AssetContent] > nt:unstructured`
   * `+ metadata (nt:unstructured)`
   * `+ renditions (nt:folder)`

### dam:Asset {#dam-asset}

**描述**

DAM资产。

**定义**

`[dam:Asset] > nt:hierarchyNode`
`+ jcr:content (dam:AssetContent) = dam:AssetContent copy primary`
`+ * (nt:base) = nt:base version`

### dam：Thumbnail {#dam-thumbnail}

**描述**

表示DAM资源的缩略图。

**定义**

* `[dam:Thumbnails]`
   * `mixin`
   * `+ dam:thumbnails (nt:folder)`

## 交货容器列表 {#delivery-container-list}

### cq：containerList {#cq-containerlist}

**描述**

容器列表。

**定义**

* `[cq:containerList]`
   * `mixin`

## 投放页面 {#delivery-page}

### cq：Cq4PageAttributes {#cq-cq-pageattributes}

**描述**

`cq:attributes` 是ContentBus版本标记的节点类型。 此节点只有一系列属性；其中三个属性是预定义的“created”、“csd”和“timestampe”。

* `@prop created (long) mandatory copy`  — 创建版本信息的时间戳，通常是以前版本的签入时间或页面创建时间。
* `@prop csd (string) mandatory copy` - csd标准属性，页面节点的cq：csd属性的副本
* `@prop timestamp (long) mandatory copy`  — 上次版本修改的时间戳，通常为签入时间。
* `@prop * (string) copy`  — 其他属性，使用父节点进行版本控制。

**定义**

* `[cq:Cq4PageAttributes] > nt:base`
   * `- created (long) mandatory copy`
   * `- csd (string) mandatory copy`
   * `- timestamp (long) mandatory copy`
   * `- &ast; (string) copy`

### cq：Cq4ContentPage {#cq-cq-contentpage}

**描述**

节点类型 `cq:contentPage` 包含ContentBus内容页的属性和子节点定义。 仅当将此mixin类型添加到类型的节点时 `cq:page`，节点将变为ContentBus内容页。

中的项目 `cq:Cq4ContentPage` 为：

* `@prop cq:csd`  — 页面的ContentBusCSD。
* `@node cq:content`  — 页面的内容。 如果页面节点处于“Existing without content”或“Deleted”状态，则此子节点不存在。
* `@node cq:attributes`  — 页面属性的列表，以前称为版本标记。 对于cq：contentPage类型，此节点是必需的。 当页面为节点进行版本控制时，将对“属性”节点进行版本控制。

**定义**

* `[cq:Cq4ContentPage]`
   * `- cq:csd (string) mandatory copy`
   * `+ cq:attributes (cq:Cq4PageAttributes)`

## 导入程序 {#importer}

### cq:PollConfig {#cq-pollconfig}

**描述**

轮询配置。

* `@prop source (String) mandatory`  — 数据源URI，这是必需项，不得为空
* `@prop target (String)`  — 存储从数据源检索的数据的目标位置。 这是可选的，默认为cq：PollConfig节点。
* `@prop interval (Long)`  — 轮询数据源中新数据或更新数据的时间间隔（以秒为单位）。 这是可选设置，默认为30分钟（1800秒）。
* [为Adobe Experience Manager创建自定义数据导入器服务](https://helpx.adobe.com/experience-manager/using/polling.html)

**定义**

* `[cq:PollConfig]`
   * `mixin`
   * `- source (String) mandatory`
   * `- target (String)`
   * `- interval (Long)`

### cq:PollConfigFolder {#cq-pollconfigfolder}

**描述**

方便创建轮询配置节点的主节点类型。

**定义**

`[cq:PollConfigFolder] > sling:Folder, cq:PollConfig`

## 位置 {#location}

### cq：GeoLocation {#cq-geolocation-1}

**描述**

定义以小数度(DD)为单位的地理位置的mixin。

* `@prop latitude`  — 使用小数位数编码为双精度的Latitude。
* `@prop longitude`  — 使用小数位数编码为双倍的经度。

**定义**

* `[cq:GeoLocation]`
   * `mixin`
   * `- latitude (double)`
   * `- longitude (double)`

## 邮件程序 {#mailer}

### cq：mailerMessage {#cq-mailermessage}

**描述**

MailerService节点类型 邮件程序使用具有此mixin的节点作为消息定义的根节点。

**定义**

* `[cq:mailerMessage]`
   * `mixin`
   * `- messageStatus (string)`
   * `= 'new'`
   * `mandatory autocreated`

## MSM {#msm}

### cq：LiveRelationship {#cq-liverelationship}

**描述**

定义LiveRelationship mixin。 可通过LiveRelationship虚拟链接主源（控制）节点和Live Copy（控制）节点。

**定义**

* `[cq:LiveRelationship] mixin`
   * `- cq:lastRolledout (date)`
   * `- cq:lastRolledoutBy (string)`
   * `- cq:sourceUUID (string)`

### cq：LiveSync {#cq-livesync}

**描述**

定义LiveSync Mixin。 如果某个节点与主源（控制）节点和Live Copy（控制）节点的LiveRelationship有关，则该节点将标记为LiveSync。

* `@prop cq:master` - LiveRelationship的主源（控制）的路径。
* `@prop cq:isDeep`  — 定义关系是否可用于子项。
* `@prop cq:syncTrigger`  — 定义同步何时触发。
* `@node * LiveSyncAction`  — 要在同步时执行的操作

**定义**

`[cq:LiveSync] > cq:LiveRelationship mixin orderable`
`+ * (cq:LiveSyncAction) = cq:LiveSyncAction`
`+ cq:LiveSyncConfig (nt:base) = cq:LiveSyncConfig`

### cq：LiveSyncCanceled {#cq-livesynccancelled}

**描述**

定义LiveSyncCanceled mixin。 取消LiveCopy（受控）节点的LiveSync行为，该节点可能因其父节点之一而包含在LiveRelationship中。

* `@prop cq:isCancelledForChildren`  — 定义是否取消了LiveSync；也适用于子项。

**定义**

* `[cq:LiveSyncCancelled] > cq:LiveRelationship mixin`
   * `- cq:isCancelledForChildren (boolean)`

### cq：LiveSyncAction {#cq-livesyncaction}

**描述**

定义附加到LiveSync的LiveSyncAction。

* `@prop name`  — 操作名称
* `@prop value`  — 操作值

**定义**

* `[cq:LiveSyncAction] > nt:unstructured`

### cq：LiveSyncConfig {#cq-livesyncconfig}

**描述**

实时同步配置。

**定义**

* `[cq:LiveSyncConfig]`
   * `- cq:master (string) mandatory`
   * `- cq:isDeep (boolean)`
   * `- cq:trigger (string) /** deprecated **/`

对于AEM 5.4，在列表末尾添加：

* `- cq:rolloutConfigs (string) multiple /** deprecated **/`

### cq：BlueprintAction {#cq-blueprintaction}

**描述**

Blueprint操作

**定义**

* `[cq:BlueprintAction] > nt:unstructured`

## Platform {#platform}

### cq：Console {#cq-console}

**描述**

定义控制台节点的节点类型。

**定义**

* `[cq:Console] > sling:VanityPath, mix:title`
   * `mixin`

## 复制 {#replication}

### cq：ReplicationStatus {#cq-replicationstatus}

**描述**

定义复制状态信息mixin。

* `@prop cq:lastPublished` — 上次发布页面（不再使用）的日期。
* `@prop cq:lastPublishedBy` — 最后发布页面的用户（不再使用）。
* `@prop cq:lastReplicated`  — 上次复制页面的日期。
* `@prop cq:lastReplicatedBy`  — 最后复制页面的用户。
* `@prop cq:lastReplicationAction`  — 复制操作：激活或停用。
* `@prop cq:lastReplicationStatus`  — 复制状态（不再使用）。

**定义**

* `[cq:ReplicationStatus]`
   * `mixin`
   * `- cq:lastPublished (date) ignore`
   * `- cq:lastPublishedBy (string) ignore`
   * `- cq:lastReplicated (date) ignore`
   * `- cq:lastReplicatedBy (string) ignore`
   * `- cq:lastReplicationAction (string) ignore`
   * `- cq:lastReplicationStatus (string) ignore`

## 安全性 {#security}

### cq：ApplicationPrivilege {#cq-applicationprivilege}

**描述**

定义应用程序权限。

**定义**

* `[cq:ApplicationPrivilege] mixin`

### cq：PrivilegeAcl {#cq-privilegeacl}

**描述**

定义应用程序权限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定义**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：PrivilegeAce {#cq-privilegeace}

**描述**

定义应用程序权限ACE。

* `@prop path`
* `@prop deny`

**定义**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

### cq：ApplicationPrivilege {#cq-applicationprivilege-1}

**描述**

定义应用程序权限。

**定义**

* `[cq:ApplicationPrivilege] mixin`

### cq：PrivilegeAcl {#cq-privilegeacl-1}

**描述**

定义应用程序权限ACL。

* `@prop cq:isPathDependent`
* `@node * ACEs`

**定义**

* `[cq:PrivilegeAcl] > cq:ApplicationPrivilege mixin orderable`
   * `- cq:isPathDependent (boolean)`
   * `+ * (cq:PrivilegeAce) = cq:PrivilegeAce`

### cq：PrivilegeAce {#cq-privilegeace-1}

**描述**

定义应用程序权限ACE。

* `@prop path`
* `@prop deny`

**定义**

* `[cq:PrivilegeAce]`
   * `- path mandatory`
   * `- deny (boolean)`

## 站点导入程序 {#site-importer}

### cq：ComponentExtractorSource {#cq-componentextractorsource}

**描述**

定义一个mixin类型，用于标记可使用组件提取器打开的文件。

**定义**

`[cq:ComponentExtractorSource] mixin`

## 标记 {#tagging}

### cq：Tag {#cq-tag}

**描述**

定义单个标记，但也可以包含标记，从而创建分类

**定义**

* `[cq:Tag] > nt:base, mix:title`
   * `- sling:resourceType (String)`
   * `- * (undefined) multiple`
   * `- * (undefined)`
   * `+ * (nt:base) = cq:Tag version`

### cq:Taggable {#cq-taggable}

**描述**

可标记内容的抽象基本mixin。

* `@node cq:tags`

**定义**

* `[cq:Taggable]`
   * `- cq:tags (string) multiple`

### cq：OwnerTaggable {#cq-ownertaggable}

**描述**

仅允许作者/所有者标记内容（审核/管理标记）。

**定义**

* `[cq:OwnerTaggable] > cq:Taggable`

### cq：UserTaggable {#cq-usertaggable}

**描述**

任何用户/公共网站都可以标记内容（Web2.0样式），该内容在cq：userContent中使用。

**定义**

* `[cq:UserTaggable] > cq:Taggable`
   * `mixin`

### cq：AllowsUserContent {#cq-allowsusercontent}

**描述**

添加 `cq:userContent` 可由用户修改的子节点。 每个用户都有自己的 `cq:userContent/<userid>` 子节点，通常具有mixin `cq:UserTaggable`.

**定义**

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (nt:unstructured)`

扩展变体，更明确地定义 `cq:userContent` 树

* `[cq:AllowsUserContent]`
   * `mixin`
   * `+ cq:userContent (cq:UserContent)`

### cq：UserContent {#cq-usercontent}

**描述**

可由用户修改。

**定义**

* `[cq:UserContent] > nt:unstructured`
   * `// userids`
   * `+ * (cq:UserData)`
   * `// other content`
   * `+ * (nt:base)`

### cq：UserData {#cq-userdata}

**描述**

用户数据

**定义**

* `[cq:UserData] > nt:unstructured, cq:UserTaggable`

## 小组件 {#widgets}

### cq：ClientLibraryFolder {#cq-clientlibraryfolder}

**描述**

客户端库文件夹

**定义**

* `[cq:ClientLibraryFolder] > sling:Folder`
   * `- categories (string) multiple`
   * `- dependencies (string) multiple`

### cq：Widget {#cq-widget}

**描述**

小组件

**定义**

* `[cq:Widget] > nt:unstructured orderable`
   * `- xtype (string)`
   * `- name (string)`
   * `- title (string)`
   * `+ items (nt:base) = cq:WidgetCollection copy`

### cq：WidgetCollection {#cq-widgetcollection}

**描述**

构件集合

**定义**

* `[cq:WidgetCollection] > nt:unstructured`
   * `orderable`
   * `+ * (cq:Widget) = cq:Widget copy`

### cq：Dialog {#cq-dialog}

**描述**

对话框

**定义**

* `[cq:Dialog] > cq:Widget orderable`

### cq：Panel {#cq-panel}

**描述**

面板

**定义**

`[cq:Panel] > cq:Widget orderable`

### cq：TabPanel {#cq-tabpanel}

**描述**

选项卡面板

**定义**

* `[cq:TabPanel]` > `cq:Panel orderable`
   * `- activeTab (long)`

### cq：Field {#cq-field}

**描述**

字段

**定义**

* `[cq:Field] > cq:Widget orderable`
   * `- fieldLabel (string)`
   * `- value (string)`
   * `- ignoreData (boolean)`

## 维客 {#wiki}

### wiki：主题 {#wiki-topic}

**描述**

Wiki主题

**定义**

* `[wiki:Topic] > nt:unstructured, nt:hierarchyNode, mix:versionable, mix:lockable`
   * `+ * (wiki:Topic) version`
   * `+ wiki:attachments (nt:folder) = nt:folder version`
   * `+ wiki:properties (wiki:Properties) = wiki:Properties copy`
   * `- wiki:text (string) mandatory primary`
   * `- wiki:lastModified (date) mandatory`
   * `- wiki:lastModifiedBy (string) mandatory`
   * `- wiki:topicName`
   * `- wiki:topicTitle`
   * `- wiki:lockedBy`
   * `- wiki:logMessage (string)`
   * `- wiki:quietSave (boolean)`

### wiki：用户 {#wiki-user}

**描述**

Wiki用户

**定义**

* `[wiki:User] mixin`
   * `- wiki:subscriptions (string) multiple`

### wiki：属性 {#wiki-properties}

**描述**

Wiki属性

**定义**

* `[wiki:Properties]`
   * `- wiki:isGlobal (boolean)`
   * `- * (undefined)`

## 工作流 {#workflow}

### cq：Workflow {#cq-workflow}

**描述**

表示工作流实例。

**定义**

* `[cq:Workflow] > nt:base, mix:referenceable`
   * `- modelId (String)`
   * `- modelVersion (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- initiator (String)`
   * `- &ast; (undefined)`
   * `- &ast; (undefined) multiple`
   * `- sling:resourceType (String) = "cq/workflow/components/instance" mandatory autocreated`
   * `+ workflowStack (nt:unstructured)`
   * `+ wait (nt:unstructured)`
   * `+ orTab (nt:unstructured)`
   * `+ data (cq:WorkflowData)`
   * `+ history (nt:unstructured)`
   * `+ metaData (nt:unstructured)`
   * `+ workItems (nt:unstructured)`

### cq：WorkItem {#cq-workitem}

**描述**

工作项。

**定义**

* `[cq:WorkItem]`
   * `- assignee (String)`
   * `- workflowId (String)`
   * `- nodeId (String)`
   * `- startTime (Date)`
   * `- endTime (Date)`
   * `- dueTime (Date)`
   * `- sling:resourceType (String) = "cq/workflow/components/workitem" mandatory autocreated`
   * `+ metaData (nt:unstructured)`

### cq：Payload {#cq-payload}

**描述**

有效负荷

**定义**

* `[cq:Payload]`
   * `- path (Path)`
   * `- uuid (String)`
   * `- jcr:url (String)`
   * `- binary (Binary)`
   * `- javaObject (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`

### cq：WorkflowData {#cq-workflowdata}

**描述**

工作流数据

**定义**

* `[cq:WorkflowData]`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ payload (cq:Payload)`
   * `+ metaData (nt:unstructured) copy`

### cq：WorkflowModel {#cq-workflowmodel}

**描述**

自动分配工作流配置。 配置将遵循以下结构：
* `workflows`
   * `+ name1`
      * `- cq:path`
      * `- cq:workflowName`
   * `+ workflows (nt:base)`

**定义**

* `[cq:WorkflowModel] > nt:base, mix:versionable`
   * `orderable`
   * `- title (String)`
   * `- description (String)`
   * `- sling:resourceType (String) = "cq/workflow/components/model" mandatory autocreated`
   * `+ nodes (nt:unstructured)`
      * `copy`
   * `+ transitions (nt:unstructured)`
      * `copy`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq：WorkflowNode {#cq-workflownode}

**描述**

工作流节点

**定义**

* `[cq:WorkflowNode] orderable`
   * `- title (String)`
   * `- description (String)`
   * `- maxIdleTime (long)`
   * `- type (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
   * `+ metaData (nt:unstructured)`
      * `copy`
   * `+ timeoutConfiguration (nt:unstructured)`
      * `copy`

### cq：WorkflowTransition {#cq-workflowtransition}

**描述**

工作流过渡

**定义**

* `[cq:WorkflowTransition] orderable`
   * `- from (String)`
   * `- to (String)`
   * `- rule (String)`
   * `+ metaData (nt:unstructured)`
      * `copy`

### cq：OrTab {#cq-ortab}

**描述**

或选项卡

**定义**

* `[cq:OrTab]`
   * `- workflowId (String) // not compulsory as this node will already be attached to the workflow node`
   * `- nodeId (String)`

### cq：Wait {#cq-wait}

**描述**

等待

**定义**

* `[cq:Wait]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- destNodeId (String)`
   * `- fromNodeId (String)`

### cq：WorkflowStack {#cq-workflowstack}

**描述**

工作流栈栈

**定义**

* `[cq:WorkflowStack]`
   * `- containeeInstanceId (String)`
   * `- parentInstanceId (String)`
   * `- nodeId (String)`

### cq：ProcessStack {#cq-processstack}

**描述**

进程栈栈

**定义**

* `[cq:ProcessStack]`
   * `- workflowId (String) // not compulsory as this node will be already attached to the workflow node`
   * `- containerWorkflowModelId (String)`
   * `- containerWorkflowNodeId`
   * `- containerWorkflowEndNodeId // still needed (if name already defines that id)`

### cq：WorkflowLauncher {#cq-workflowlauncher}

**描述**

工作流启动器

**定义**

* `[cq:WorkflowLauncher]`
   * `- nodetype (String)`
   * `- glob (String)`
   * `- eventType (Long)`
   * `- description (String)`
   * `- condition (String)`
   * `- workflow (String)`
   * `- * (undefined)`
   * `- * (undefined) multiple`
