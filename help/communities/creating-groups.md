---
title: 社区组
description: 了解社区组功能如何让您通过Publish和Author中的授权用户在社区站点中动态创建子社区。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 社区组 {#community-groups}

社区组功能允许子社区由发布和创作环境中的授权用户（社区成员和作者）在社区站点中动态创建。

当[社区站点](/help/communities/sites-console.md)结构中存在[组函数](/help/communities/functions.md#groups-function)时，此功能就会出现。

在动态创建社区组时，[社区组模板](/help/communities/tools-groups.md)提供了社区组页面的设计。

将功能添加到社区站点的结构或社区站点模板时，会为组功能选择一个或多个组模板。 此组模板列表向从社区站点动态创建组的成员或作者显示。

## 创建新组 {#creating-a-new-group}

创建社区组的功能依赖于存在包含组功能的社区站点，例如从[引用站点模板](/help/communities/sites.md)创建的社区站点。

下面的示例使用从`Reference Site Template`创建的社区站点，如[AEM Communities快速入门](/help/communities/getting-started.md)教程中所述。

这是选择&#x200B;**组**&#x200B;菜单项时加载到发布的页面：

![新组](assets/new-group.png)

选择&#x200B;**新建组**&#x200B;图标时，将打开编辑对话框。

在&#x200B;**设置**&#x200B;选项卡下，提供该组的基本功能：

![组设置](assets/group-settings.png)

* **组名称**

  要在社区站点上显示的组的标题。 避免在组名中使用下划线字符(_)和关键字（如资源和配置）。

* **描述**

  要在社区站点上显示的组的描述。

* **邀请**

  邀请加入组的成员列表。 提前输入搜索可提供社区成员邀请的建议。

* **组URL名称**

  成为URL一部分的组页面的名称。

* **打开组**

  选择`Open Group`表示任何匿名网站访客都可以查看该内容，并取消选择`Member Only Group`。

* **仅限成员的组**

  选择`Member Only Group`表示只有组成员可以查看内容，并取消选择`Open Group`。

在&#x200B;**模板**&#x200B;选项卡下，您可以从社区组模板列表中进行选择。 当组功能包含在社区站点的结构或社区站点模板中时，会指定这些模板。

![组模板](assets/group-template.png)

在&#x200B;**图像**&#x200B;选项卡下，您可以上传图像以在社区站点的“组”页面上为组显示。 默认样式表将图像大小调整为170 x 90像素。

![组图像](assets/group-image.png)

通过选择&#x200B;**创建组**，将根据所选模板创建组的页面，并为成员资格创建用户组，并且更新“组”页面以显示新的子社区。

例如，标题为“焦点组”的新子社区（已为其上传图像缩略图）的“组”页面如下所示（仍以社区组管理员身份登录）：

![组页面](assets/group-page.png)

选择`Focus Group`链接将在浏览器中打开“焦点组”页面，该页面的初始外观基于所选模板，并在主社区站点的菜单下包含一个子菜单：

![open-group-page](assets/open-group-page.png)

### 社区组成员列表组件 {#community-group-member-list-component}

`Community Group Member List`组件专供群组模板的开发人员使用。

### 附加信息 {#additional-information}

在开发人员的[社区组Essentials](/help/communities/essentials-groups.md)页面上可找到更多信息。

有关社区组的其他信息，请访问[管理用户和用户组](/help/communities/users.md)。
