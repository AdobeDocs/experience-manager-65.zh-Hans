---
title: 初始设置
description: 了解如何初始设置Adobe Experience Manager Communities。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 1%

---

# 初始设置 {#initial-setup}

## 启动Author和Publish实例 {#start-author-and-publish-instances}

出于开发和演示目的，需要运行一个作者实例和一个发布实例。

为此，请按照基本的Adobe Experience Manager (AEM) [快速入门](../../help/sites-deploying/deploy.md#getting-started)说明进行操作，从而生成以下内容：

* [localhost：4502](http://localhost:4502/)上的作者环境
* [localhost：4503](http://localhost:4503/)上的Publish环境

对于AEM Communities，

* 创作环境用于：

   * 站点、模板和组件的开发。
   * 管理和配置任务。

* Publish环境用于：

   * 发布和审核内容的社区体验。
   * 创建社区组、成员和成员组。

>[!NOTE]
>
>如果不熟悉AEM，请查看有关[基本处理](../../help/sites-authoring/basic-handling.md)的文档以及[页面创作快速指南](../../help/sites-authoring/qg-page-authoring.md)。

## 安装最新的Communities版本 {#install-latest-communities-release}

本教程基于AEM Communities 6.2 Feature Pack 1.10版创建了一个[参与社区站点](overview.md#engagement-community)。

要确保已安装最新的功能包，请访问：

* [最新版本](deploy-communities.md#latest-releases)

## 配置 Analytics {#configure-analytics}

当为社区站点[&#128279;](analytics.md)配置了Adobe Analytics时，社区活动信息可用，可以增强社区成员的体验并向站点管理员提供反馈。

与Adobe Analytics集成是可选的。

## 配置通知电子邮件 {#configure-email-for-notifications}

通知功能默认适用于使用`Communities Sites`控制台创建的所有站点，它提供了通知的电子邮件渠道。

要为站点正确配置电子邮件，这是必需的。

请参阅[配置电子邮件](email.md)。

## 启用通道服务 {#enable-the-tunnel-service}

在“创作”环境中创建社区站点时，通过通道服务，可以将角色分配给在Publish环境中注册的受信任社区成员。 通道服务还允许从创作环境中的[成员和组控制台](members.md)访问社区成员。

该惯例适用于在Publish环境中创建的成员和成员组，即&#x200B;*不在创作环境中重新创建*。 有关详细信息，请参阅[管理用户和用户组](users.md)。

有关在&#x200B;**作者**&#x200B;实例上启用通道服务的简单说明，请参阅[通道服务](deploy-communities.md#tunnel-service-on-author)。

## 社区管理员角色 {#community-administrator-role}

社区管理员组的成员可以创建社区站点、管理站点、管理成员（他们可以从社区中禁止成员）和审核内容。

### 创建用户 {#create-user}

在&#x200B;*作者*&#x200B;上创建分配了社区管理员角色的用户：

* 在创作实例上

   * 例如，[http://localhost:4502/](http://localhost:4503/)

* 使用管理员权限登录

   * 例如，用户名“管理员”/密码“管理员”

* 从主控制台导航到&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL 安全性]** > **[!UICONTROL 用户]**。
* 从&#x200B;**编辑**&#x200B;菜单中，选择&#x200B;**[!UICONTROL 添加用户]**

* 在`Create New User`对话框中，输入：

   * **[!UICONTROL ID]**： sirius
   * **[!UICONTROL 电子邮件地址]**： sirius.nilson@mailinator.com
   * **[!UICONTROL 密码]**：密码
   * **[!UICONTROL 确认密码&amp;amp；ast；]**：密码
   * **[!UICONTROL 名字]**： Sirius
   * **[!UICONTROL 姓氏]**： Nilson

### 将Sirius分配给社区管理员组 {#assign-sirius-to-community-administrators-group}

向下滚动到`Add User to Groups`：

* 输入“C”进行搜索

   * 选择`Community Administrators`
   * 选择`Community Enablement Managers`

* 选择&#x200B;**[!UICONTROL 保存]**。

![create-user](assets/create-user.png)

## 启用社交登录 {#enable-social-login}

在使用Facebook和Twitter社交登录的演示版本之前，必须

1. 安装修复包或[最新功能包](deploy-communities.md#latestfeaturepack)(有关2017年3月Facebook API的更改)。
1. [在发布环境中启用OAuth提供程序](social-login.md#adobe-granite-oauth-authentication-handler)。

对于生产服务器，必须创建提供社交登录所需的云服务。

请参阅[使用Facebook和Twitter进行社交登录](social-login.md)。

## 创建教程标记 {#create-tutorial-tags}

创建标记，以便您可以使用`Tutorial`的标记命名空间将它们用于engage教程。

使用[标记控制台](../../help/sites-administering/tags.md#tagging-console)创建以下标记：

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

然后按照说明执行以下操作：

1. [设置标记权限](../../help/sites-administering/tags.md#setting-tag-permissions)。
1. [Publish标记](../../help/sites-administering/tags.md#publishing-tags)。

为AEM Communities快速入门Tutorials创建的标记示例包

[获取文件](assets/tutorial_tags-v63.zip)

## 适用于UGC公用存储的MongoDB {#mongodb-for-ugc-common-store}

建议将[MSRP](msrp.md) (MongoDB)设置为[公用存储](working-with-srp.md)以体验从发布和/或创作环境审核所有UGC的灵活性，但这是可选的。

有关说明，请访问[如何为演示设置MongoDB](demo-mongo.md)。

默认情况下，作者实例和发布AEM实例的安装导致用户生成的内容(UGC)存储在[JCR Tar存储](../../help/sites-deploying/platform.md)中，使用[JSRP](jsrp.md)访问该存储。 JSRP不是通用存储，这意味着UGC仅在输入它的实例上可见。 通常，UGC是在发布实例上输入的，在创作环境中不可见，从而导致所有审核任务都需要使用发布实例。
