---
title: 创作嵌套组
description: 了解如何为Adobe Experience Manager Communities站点创建嵌套组。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 55803b7a-9064-4392-9cc2-9f113fa8dc29
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# 创作嵌套组{#authoring-nested-groups}

## 创建创作组 {#creating-groups-on-author}

在AEM创作实例上，从全局导航：

* 选择&#x200B;**[!UICONTROL 社区]** > **[!UICONTROL 站点]**。
* 选择&#x200B;**[!UICONTROL 参与文件夹]**&#x200B;以将其打开。
* 选择&#x200B;**[!UICONTROL 入门教程]**&#x200B;英语站点的信息卡。

   * 选择卡片图像。
   * 请&#x200B;*不*&#x200B;选择一个图标。

结果访问[组控制台](/help/communities/groups.md)：

![创建组](assets/create-group.png)

“组”功能将显示为文件夹，可在其中创建组的实例。 要打开该文件夹，请选择“组”文件夹。 在Publish上创建的组可见。

![create-new-group](assets/create-new-group.png)

## 创建主艺术组 {#create-main-arts-group}

可以创建此组，因为用于接合的站点结构包括组的功能。 站点`Reference Template`中函数的配置默认为允许选择任何启用的组模板。 因此，为此新组选择的模板是`Reference Group`。

这些控制台与社区站点控制台类似。

* 选择&#x200B;**[!UICONTROL 创建群组]**

* **社区组模板**：

   * **[!UICONTROL 社区组标题]**：艺术
   * **[!UICONTROL 社区组描述]**：各种艺术组的父组
   * **[!UICONTROL 社区组根]**： *保留为默认值*
   * **[!UICONTROL 其他可用的社区组语言]**：使用下拉菜单选择可用的社区组语言。 该菜单显示创建父社区站点时采用的所有语言。 用户可以在这些语言中进行选择，以便通过此单一步骤在多个区域设置中创建组。 在相应社区站点的“组”控制台中，以多种指定语言创建同一组。
   * **[!UICONTROL 社区组名称]**： arts
   * **[!UICONTROL 模板]**：用于选择`Reference Group`的下拉列表
   * 选择&#x200B;**[!UICONTROL 下一步]**

![嵌套社区组](assets/parent-to-nestedgroup.png)

使用这些设置继续浏览其他面板：

* **[!UICONTROL Design]**

   * 更改设计或允许默认父站点的设计。
   * 选择&#x200B;**[!UICONTROL 下一步]**。

* **[!UICONTROL 设置]**

   * **[!UICONTROL 审核]**

      * 留空（继承自父站点）。

   * **[!UICONTROL 成员资格]**

      * 使用默认`Optional Membership.`

      * **[!UICONTROL 缩略图]**
         * `optional.*`

      * **[!UICONTROL 选择“下一步”]**。

* 选择&#x200B;**[!UICONTROL 创建]**。

### 艺术组内的嵌套组 {#nesting-groups-within-arts-group}

`groups`文件夹现在包含两个组（刷新页面）。

![嵌套组](assets/create-community-group.png)

#### Publish集团 {#publish-group}

在创建嵌套在`arts`组中的组之前，将鼠标悬停在`arts`卡片上并选择发布图标以进行发布。

![发布站点](assets/publish-site.png)

等待确认该组已发布。

![组已发布](assets/group-published.png)

`arts`组还应包含一个`groups`文件夹，但该文件夹为空并且可以在其中创建新组。 导航到艺术组文件夹并创建三个嵌套的艺术组，每个艺术组具有不同的成员资格设置：

1. **[!UICONTROL 可视化]**

   * 标题： `Visual Arts`
   * 名称：`visual`
   * 模板： `Reference Group`
   * 成员资格：选择`Optional Membership`，公共组，对所有成员开放。

1. **[!UICONTROL 听觉]**

   * 标题： `Auditory Arts`
   * 名称：`auditory`
   * 模板： `Reference Group`
   * 成员资格：选择开放组`Required Membership`，可供成员加入。

1. **[!UICONTROL 历史记录]**

   * 标题： `Art History`
   * 名称：`history`
   * 模板： `Reference Group`
   * 成员资格：选择`Restricted Membership`，一个仅对受邀成员可见的机密组。 例如，邀请[演示用户](/help/communities/tutorials.md#demo-users) `emily.andrews@mailinator.com`。

刷新页面，以便您能够查看所有三个嵌套的组（子社区）。

要从社区站点控制台导航到嵌套组，请执行以下操作：

* 选择&#x200B;**[!UICONTROL 参与文件夹]**
* 选择&#x200B;**[!UICONTROL 入门教程卡]**
* 选择&#x200B;**[!UICONTROL 组]**&#x200B;文件夹
* 选择&#x200B;**[!UICONTROL 艺术卡]**
* 选择&#x200B;**[!UICONTROL 组]**&#x200B;文件夹

![create-new-group2](assets/create-new-group2.png)

## 发布组 {#publishing-groups}

![发布站点](assets/publish-site.png)

发布主社区站点后：

* Publish各个组：

   * 正在等待确认该组已发布。

* 在发布嵌套于以下位置的任何组之前，先对父组进行Publish：

   * 必须以自上而下的方式发布所有组。

![组已发布](assets/group-published.png)

## Publish体验 {#experience-on-publish}

登录时可能会体验不同的组，例如，使用[演示用户](/help/communities/tutorials.md#demo-users)进行以下操作：

* 艺术/历史组成员： `emily.andrews@mailinator.com/password`
   * 受限（机密）组“艺术/历史”可见：
   * 能够查看可选（公共）组。
   * 能够加入受限（开放）组。

* 组管理器： `aaron.mcdonald@mailinator.com/password`

   * 能够查看可选（公共）组。
   * 能够加入受限（开放）组。
   * 无法查看受限（机密）组。

访问作者上的社区[成员和组控制台](/help/communities/members.md)以将其他用户添加到与社区组对应的各种成员组。
