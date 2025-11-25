---
title: 创作
description: Adobe Experience Manager 6.5中的创作和发布概念。
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 28%

---

# 创作{#authoring}

## 创作（和发布）概念 {#concept-of-authoring-and-publishing}

AEM为您提供两种环境：

* 创作
* 发布

通过这些交互可以将内容放到您的网站上，以便访客能够阅读这些内容。

创作环境提供了用于在实际发布内容前创建、更新和审核该内容的机制：

* 作者创建和审查内容（可以是多种类型；例如，页面、资产、出版物等）
* 这些将在某一时刻发布到您的网站。

![环境概述](assets/chlimage_1-132.png)

在创作环境中，AEM的功能通过两个UI提供。 对于发布环境，可以设计提供给用户使用的界面的整体外观。

### 创作环境 {#author-environment}

作者在称为&#x200B;**创作环境**&#x200B;的环境中工作。这为创建内容提供了易于使用的界面(图形用户界面（GUI或UI）)。 它位于公司防火墙的后面，可提供全面保护，并要求作者使用已分配了相应访问权限的帐户登录。

>[!NOTE]
>
>您的帐户需要适当的访问权限才能创建、编辑或发布内容。

根据您的实例和个人访问权限的配置方式，您可以对内容执行许多任务，其中包括（但不限于）：

* 在页面上生成新内容或编辑现有内容
* 使用预定义模板创建新内容页面
* 创建、编辑和管理您的资源和收藏集
* 创建、编辑和管理您的出版物
* 开发营销活动和相关资源
* 开发和管理社区站点
* 移动、复制或删除内容页面、资源等
* 发布（或取消发布）页面、资源等

此外，还有一些管理任务可帮助管理内容：

* 控制更改的管理方式的工作流；例如，在发布之前实施审核
* 协调各个任务的项目

>[!NOTE]
>
>AEM也是来自创作环境的[受管理](/help/sites-administering/home.md)（对于大多数任务）。

#### 发布环境 {#publish-environment}

准备就绪后，AEM站点的内容将发布到&#x200B;**发布环境**。 在该环境中，根据设计界面的具体观感，目标受众可以使用网站页面。

通常，发布环境位于非军事区内；换句话说，发布环境可用于Internet，但不再受内部网络的完全保护。

当AEM站点是[社区站点](/help/communities/overview.md)或包含[社区组件](/help/communities/author-communities.md)时，登录的站点访客（成员）可能会与社区功能进行交互。 例如，他们可以在论坛中发帖、发表评论或关注其他成员。 可以授予成员执行通常仅限于创作环境的活动的权限，例如创建新页面（社区组）、博客文章和审核其他成员的帖子。

>[!NOTE]
>
>不幸的是，使用的术语有时存在重叠。 这种情况可能会发生在以下位置：
>
>* **发布/取消发布**
>  这些是在发布环境中公开提供（或不公开提供）您的内容的主要操作术语。
>
>* **激活／取消激活**
>  这两个术语与发布/取消发布同义。
>
>* **复制**
>  这些是技术术语，用于指示数据（例如，页面内容、文件、代码、用户注释）从一个环境移动到另一个环境；即在发布或反向复制用户注释时。
>

#### Dispatcher {#dispatcher}

为了优化网站访问性能，**[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)**&#x200B;实施了负载平衡和缓存。
