---
title: 成员和组管理控制台
description: 如何访问成员和组管理控制台
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: b64e24d2-8407-484c-8216-8d328ef5fa4f
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# 成员和组管理控制台 {#members-groups-management-consoles}

## 概述 {#overview}

AEM Communities功能通常要求网站访客先注册并登录，然后才能在发布环境中加入社区。 其用户注册只需要存在于发布环境中，通常称为&#x200B;*成员*&#x200B;以将其与在创作环境中注册的&#x200B;*用户*&#x200B;区分开来。

### Publish上的成员（用户） {#members-users-on-publish}

使用社区成员和组控制台，可以在&#x200B;*作者*&#x200B;环境中创建和管理在&#x200B;*发布*&#x200B;环境中注册的成员和成员组。 仅当启用了[通道服务](deploy-communities.md#tunnel-service-on-author)时，才可能执行此操作。

### 作者中的用户 {#users-on-author}

要管理在&#x200B;*作者*&#x200B;环境中注册的用户和组，必须使用平台的安全控制台：

* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**。
* 从全局导航中，选择&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 组]**。

>[!NOTE]
>
>部署和启用示例内容后，创作和发布环境中都会存在许多示例用户。 使用[nosamplecontent运行模式](../../help/sites-administering/production-ready.md)运行时，这些用户将不存在。

## 成员控制台 {#members-console}

在创作环境中，要访问成员控制台以管理在发布环境中注册的成员，请执行以下操作：

* 从全局导航中，选择&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 成员]**

>[!CAUTION]
>
>如果未启用[通道服务](deploy-communities.md#tunnel-service-on-author)，则无法使用“成员”控制台。

![成员控制台](assets/member-console1.png)

### 搜索 {#search-features}

选择`Members`标题左侧的侧面板图标以切换打开搜索侧面板。

![搜索侧面板图标。](assets/leftpanel-icon.png)


![成员控制台的筛选器选项](assets/member-console2.png)

选择`Members`标题左侧的搜索图标可关闭搜索侧面板。

### 成员统计信息 {#member-statistics}

显示`Views`、`Posts`、`Follows`和`Likes`的列已更新，如果用户是启用了[Adobe Analytics](sites-console.md#analytics)的一个或多个社区站点的成员。

### 导出 CSV {#export-csv}

选择`Export CSV`链接会导致以逗号分隔值列表的形式下载所有成员，适合导入到电子表格中。

列标题为

`| Screen Name |Last Name |First Name |Status |Views |Posts |Follows |Likes |`

## 创建新成员 {#create-new-member}

选择`Create Member`以在发布环境中创建用户。

![创建新成员窗口](assets/create-member1.png)

### 常规 — 成员详细信息 {#general-member-details}

大多数字段是可选字段，成员以后可在其配置文件中填写。

* **[!UICONTROL ID]**

（*必需*）可授权ID是成员的登录ID。
默认情况下，ID设置为所需电子邮件地址的值。
*创建后，ID可能无法修改*。

* **[!UICONTROL 电子邮件地址]**

（*必需*）成员的电子邮件地址。
成员可以在更新个人资料时更改其电子邮件地址。I
如果ID默认使用电子邮件地址，则在更改电子邮件地址时，该ID将*不会*&#x200B;更改。

* **[!UICONTROL 密码]**

  （*必需*）登录密码。

* **[!UICONTROL Retype密码]**

  （*必需*）重新输入验证密码。

* **[!UICONTROL 将成员添加到站点]**

  （*可选*）从现有社区站点中选择，以将成员添加到社区站点的成员组。

* **[!UICONTROL 将成员添加到组]**

  （*可选*）从现有成员组中选择以将该成员添加到该组。

* 选择&#x200B;**[!UICONTROL 保存]**

### 常规 — 帐户设置 {#general-account-settings}

在“帐户设置”下，社区管理员可以：

* **[!UICONTROL 状态]**
   * 已禁止
成员无法登录，导致他们无法查看页面或参与需要登录的活动。 他们仍可匿名访问开放的社区站点。

   * 未禁止
成员具有对社区站点的完全访问权限。

  默认值为`Not Banned`。

* **[!UICONTROL 贡献限制]**

  如果选中，则成员发布内容的能力有限。
默认值取决于贡献限制的配置。
请参阅[成员贡献限制](limits.md)。

* **[!UICONTROL 更改密码]**

  修改现有成员时显示的链接。 使社区管理员能够重置成员的密码。

### 常规 — 照片 {#general-photo}

要为该成员提供头像，请选择&#x200B;**[!UICONTROL 上传图像]**，然后选择.jpg、.png、.tif或.gif类型的图像。 图像的首选大小为240 x 240像素(72 dpi)。

### 常规 — 将成员添加到站点 {#general-add-member-to-sites}

可以将成员添加到一个或多个社区站点的成员组。 首先在文本框中输入文本。

### 常规 — 将成员添加到组 {#general-add-member-to-groups}

可以将成员添加到一个或多个成员组。 首先在文本框中输入文本。

### 徽章选项卡 {#badges-tab}

`BADGES`面板提供手动分配徽章和撤销徽章的功能。 该徽章可用于通常获得的指定角色和徽章。

另请参阅[评分和徽章](implementing-scoring.md)。

![编辑成员资格设置窗口](assets/create-member2.png)

* **[!UICONTROL 添加徽章]**
   * 开始键入以从[可用徽章](badges.md)中选择。 选择徽章后，选择每个站点或所有站点，徽章应随成员的头像一起显示在这些站点上。
   * 可以选择多个徽章和站点。
* **[!UICONTROL 移除徽章]**
   * 选择徽章旁边的垃圾桶图标以将其删除。

## 组控制台 {#groups-console}

通过可在创作环境中使用的组控制台，可创建和管理在发布环境中注册的成员组。 它对[拥有权限的成员组](users.md#privilegedmembersgroups)特别有用。

要访问“组”控制台，请执行以下操作：
* 从全局导航中，选择&#x200B;**[!UICONTROL 导航]** > **[!UICONTROL 社区]** > **[!UICONTROL 组]**。

>[!CAUTION]
>
>如果未启用[通道服务](deploy-communities.md#tunnel-service-on-author)，则无法使用组控制台。

### 创建新组 {#create-new-group}

选择`Add Group`以在发布环境中创建组。

![新建组窗口](assets/group-console1.png)

创建发布端成员组的必填字段包括：

* **[!UICONTROL ID]**

  （*必需*）组的唯一ID。

  *ID创建后可能无法修改。*

* **[!UICONTROL 名称]**

  （*可选*）组的显示名称。

  默认值为ID。

* **[!UICONTROL 描述]**

  （*可选*）组的用途和权限的说明。

* **[!UICONTROL 将成员添加到组]**

  （*可选*）选择要作为组的初始成员包括的发布端成员。

* 选择&#x200B;**[!UICONTROL 保存]**

## 授权管理员 {#authorized-administrators}

使用Communities成员控制台中的成员时，需要以具有适当权限的用户身份登录，并且要正确配置[通道服务](deploy-communities.md#tunnel-service-on-author)使用的复制代理。

如果未以`admin`身份登录，则登录用户必须是`administrators`用户组的成员。

另请参阅作者[&#128279;](deploy-communities.md#replication-agents-on-author)上的复制代理。
