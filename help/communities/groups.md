---
title: 社区组控制台
description: 了解社区组控制台，该控制台允许您在社区站点的模板结构包括组功能时创建社区组。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
pagetitle: Community Groups Console
role: Admin
exl-id: ef371ff8-6b4f-4e5a-98fb-d7c274927c46
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# 社区组控制台 {#community-groups-console}

当社区站点的[模板结构](/help/communities/sites-console.md#step1)包含[组功能](/help/communities/functions.md#groups-function)时，“组”控制台提供创建社区组的权限。

* AEM Communities支持在其他组内嵌套组。 如果新组](/help/communities/tools-groups.md)的[结构包含组函数，则可能进行组嵌套。
* 仅对于创作环境，有一个与站点创建向导类似的组创建向导。
* 成员是否可以在发布环境中创建组，可以在将组功能添加到社区站点结构或社区组结构时对其进行配置。

在所包含的三个组模板中，只有`Reference Group`模板在其结构中包含组函数。

社区组的不同方面包括：

* **创建**：可以在作者实例上创建新组，也可以在发布实例上创建新组（可选）。
* **控件**：组可以是打开或加密的。
* **嵌套**：组可以包含零个或多个组。

<!-- This is a 404 on helpx. Update or remove.
>[!NOTE]
>
>Community groups, created in the publish environment before the [existence of the Community Groups console](/help/communities/version-history.md#featurepack1fp1), is not listed in the Community Groups console, and thus, are not modifiable using the console.
-->

>[!NOTE]
>
>只能从“社区站点”控制台访问的此“组”控制台不应与管理成员组的成员[组控制台](/help/communities/members.md)混淆。
>
>成员组是在发布环境中注册的用户组，并使用[通道服务](/help/communities/deploy-communities.md#tunnel-service-on-author)从创作环境访问。

## 组创建 {#group-creation}

要访问“组”控制台，请执行以下操作：

* 在“作者”上，使用管理员权限登录。
* 从全局导航： **[!UICONTROL 社区]** > **[!UICONTROL 站点]**。
* 选择现有的社区站点文件夹，以便您可以将其打开。
* 在文件夹中选择社区站点的实例。

   * 社区站点的结构必须包括分组功能。
   * 这些屏幕截图来自[在发布](/help/communities/published-site.md)上创建组后的“快速入门”教程。

  ![创建组](assets/create-group.png)

* 选择&#x200B;**组文件夹**&#x200B;以将其打开。

  打开时，将显示所有现有组(无论是在Author还是Publish中创建)。

  在此“组”控制台中，可以创作新组。

  ![create-new-group](assets/create-new-group.png)

* 选择&#x200B;**创建群组**&#x200B;按钮。

### 步骤1：社区组模板 {#step-community-group-template}

![多语言社区组](assets/multi-lingual-group.png)

* **社区组标题**

  组的显示标题。
标题将显示在组的已发布站点上。

* **社区组说明**

  组的描述。

* **社区组根**

  组的根路径。
默认根是父站点，但根可以移动到网站内的任何位置。 不建议更改此设置。

* **其他可用的社区组语言**&#x200B;菜单

  使用下拉菜单选择可用的社区组语言。 该菜单显示创建父社区站点时采用的所有语言。 用户可以在这些语言中进行选择，以便通过此单一步骤在多个区域设置中创建组。 在相应社区站点的“组”控制台中，使用多种指定语言创建同一组。

* **社区组名称**

  显示在URL中的组根页面的名称。 避免在组名称中使用下划线字符(_)和关键字（如资源和配置）。

   * 请仔细检查名称，因为创建组后更改名称并不容易。
   * 基础URL显示在`Community Group Name`的下方。
   * 对于有效的URL，请附加“.html”
     *例如*，`https://localhost:4502/content/sites/mysight/en/mygroup.html`。

* **社区组模板**&#x200B;菜单

  使用下拉菜单选择可用的[社区组模板](/help/communities/tools.md)。

### 第2步：设计 {#step-design}

### 社区组主题 {#community-group-theme}

![communitygrouptheme](assets/communitygrouptheme.png)

框架使用`Twitter Bootstrap`为站点提供响应式灵活设计。 可以选择多个预加载的Bootstrap主题之一来设置所选社区组模板的样式，或者可以上传Bootstrap主题。

选中后，主题上覆盖有不透明的蓝色复选标记。

可以选择与父站点主题不同的主题。

发布社区站点后，可以[编辑属性](#modifyinggroupproperties)并选择其他主题。

### 社区组品牌 {#community-group-branding}

![社区组品牌](assets/community-group-branding.png)

社区站点品牌化是作为标题显示在每个页面顶部的图像。 可能会显示组与其他网站页面不同的横幅。

图像应设置为与浏览器中页面的预期显示一样宽，且高度为120像素。

创建或选择图像时，请记住：

* 图像高度将裁剪为从图像的上边缘开始测量的120像素
* 图像已固定到浏览器窗口的左边缘
* 不会调整图像大小，因此当图像宽度为：

   * 如果宽度小于浏览器的宽度，则图像将水平重复。
   * 大于浏览器的宽度，图像似乎被裁剪。

### 步骤3：设置 {#step-settings}

**审核**

![选择社区组成员角色](assets/group-admin.png)

**社区组审查方**

默认情况下，父社区站点的审查方列表会被继承。

可以将审查方专门添加到组。 搜索成员（从发布环境）以将它们添加为审查方

**组管理员**

默认情况下，父社区站点管理员也是组的管理员。

但是，可以分配独立的组管理员。 组管理员可以管理其组（例如，G1），并创建嵌套在G1下的子组。 他们还可以为子组分配不同的管理员。

因此，用户U1可以是组G1的管理员，也可以是其嵌套组G2的常规用户。

**成员资格**

成员资格设置允许从三种方式中选择一种来保护社区组。

![社区组成员资格](assets/community-group-membership.png)

* **可选成员资格**

  如果选中，则社区组为公共组。 站点成员可以参与组并发帖，而无需明确加入组。 默认处于选中状态。

* **必需成员资格**

  如果选中，则社区组为开放组。 社区站点成员可以查看组的内容，但必须加入组才能发布内容。 成员通过在发布环境中选择`Join`按钮进行连接。 未选择默认值。

* **受限成员资格**

  如果选中，则社区组是一个机密组。 必须明确邀请社区成员。 在搜索框中输入受邀成员。 稍后可以使用[成员和组控制台](/help/communities/members.md)创作环境添加成员。 未选择默认值。

**缩略图**

![community-group-thumbnail](assets/community-group-thumbnail.png)

缩略图是要在创作和发布时为组显示的图像。

对于受支持的图像格式(如JPG或PNG)，组图像的最佳大小为170 x 90像素。

如果未添加图像，则显示默认图像。

![缩略图图像](assets/thumbnail-image.png)

### 第4步：创建组 {#step-create-group}

![community-create-group](assets/community-create-group.png)

如果需要任何调整，请使用&#x200B;**返回**&#x200B;按钮进行调整。

选择并启动&#x200B;**创建**&#x200B;后，创建组的过程将无法中断。

流程完成后，新子社区站点（组）的卡片将显示在社区站点组控制台中，作者可以在其中添加页面内容，管理员可以修改站点的属性。

![创建社区组](assets/create-community-groups.png)

>[!NOTE]
>
>将按照在其他可用社区组语言中的[步骤1：社区组模板](/help/communities/groups.md#step-community-group-template)中指定的方式，在相应社区站点的社区组控制台中以所有语言创建组。

## 作者组内容 {#author-group-content}

![开放站点](assets/open-site.png)

可以使用与任何其他AEM页面相同的工具创作组的页面内容。 要打开组进行创作，请选择将鼠标悬停在组信息卡上时显示的“打开站点”图标。

## 修改组属性 {#modify-group-properties}

在社区组创建过程中指定的现有子社区站点的属性，可以通过选择将鼠标悬停在组信息卡上时显示的“编辑站点”图标来修改：

![编辑站点](assets/edit-site.png)

以下属性的详细信息与[组创建](#group-creation)部分中提供的描述相匹配。 可以修改任何嵌套组，无论是在发布环境还是创作环境中创建。

![community-group-basic](assets/community-group-basic.png)

### 修改基本 {#modify-basic}

BASIC面板允许修改

* 社区组标题
* 社区组描述

不能修改社区组名称。

选择其他社区组模板对现有社区组站点没有影响，因为模板和站点之间没有连接。

相反，可以修改子社区的[STRUCTURE](#modify-structure)。

### 修改结构 {#modify-structure}

“结构”面板允许修改最初从作者或发布环境创建子社区站点时选择的社区组模板创建的结构。 在面板中，可以：

* 将其他[社区功能](/help/communities/functions.md)拖放到站点结构中。
* 在站点结构中社区功能的实例上：

   * **`Gear icon`**
编辑设置，包括显示标题、URL和[拥有权限的成员组](/help/communities/users.md#privilegedmembersgroups)。

   * **`Trashcan icon`**
从站点结构中移除（删除）函数。

   * **`Grid icon`**
修改在站点顶级导航栏中显示的函数顺序。

>[!CAUTION]
>
>虽然可以更改显示标题而不会产生副作用，但建议不要编辑属于社区站点的社区函数的URL名称。
>
>例如，重命名URL不会移动现有UGC，因此会导致“丢失”UGC。

>[!CAUTION]
>
>组函数必须&#x200B;*不是*&#x200B;是网站结构中的&#x200B;*第一个或唯一的*&#x200B;函数。
>
>任何其他函数（如[page函数](/help/communities/functions.md#page-function)）都必须包含并首先列出。

**示例：将日历函数添加到子社区（组）结构**

![community-group-add-calendar](assets/community-group-add-calendar.png)

### 修改设计 {#modify-design}

“设计”面板允许修改主题：

* [社区组主题](#community-group-theme)
* [社区组品牌](#community-group-branding)

   * 滚动到面板底部，以便更改品牌图像。

### 修改设置 {#modify-settings}

通过“设置”面板，可以添加社区[审查方](#moderation)。

### 修改成员资格 {#modify-membership}

[MEMBERSHIP](#membership)面板仅供参考。 无法更改已建立的组成员资格类型，无论是可选的、必需的还是受限的。

### 修改缩略图 {#modify-thumbnail}

通过[THUMBNAIL](#thumbnail)面板，可以上传图像以在Publish环境中和创作环境中的社区站点的组控制台中向站点访客表示社区组。

## Publish集团 {#publish-the-group}

![发布站点](assets/publish-site.png)

新建或修改社区组后，可以通过选择`Publish Site`图标来发布（激活）该组。

成功发布组后，将显示以下消息：

![组已发布](assets/group-published.png)

>[!CAUTION]
>
>父社区站点和父组应该已经发布。
>
>社区站点和嵌套组应以自上而下的方式发布。

## 删除组 {#delete-the-group}

![删除图标](assets/deleteicon.png)

从社区“组”控制台中删除组，方法是选择将鼠标悬停在该组上时显示的“删除组”图标。

这将删除与组关联的所有项目，例如，将永久删除组的所有内容并从系统中删除用户成员资格。
