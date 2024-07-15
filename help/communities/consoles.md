---
title: 社区控制台
description: 从全局导航面板了解“创作”环境中可用的Adobe Experience Manager社区控制台。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 36f2e3d2-46c7-48a8-a1e9-213f581bd9f3
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 社区控制台 {#communities-consoles}

AEM Communities的控制台可在全局导航面板的创作环境中使用，用于访问管理任务，例如：

* [创建社区站点](sites-console.md)
* 正在添加嵌套在网站中的[组](groups.md)
* 管理[社区站点模板](sites.md)
* 管理[社区成员](members.md)
* [正在审核](moderate-ugc.md)用户生成的内容(UGC)
* 创建[自定义徽章](badges.md)
* 正在为UGC](srp-config.md)配置[默认存储

当[UGC存储](working-with-srp.md)配置为由Author和Publish环境共享的公用存储时，可在Author和Publish环境中使用的[审核控制台](moderation.md)在UGC的单独实例上运行。

在创作环境中，以管理员权限登录后，`Communities`控制台可以从导航和工具控制台中使用。

>[!NOTE]
>
>在Publish环境中，当登录成员具有相应的权限时，[社区站点](sites-console.md)会显示`Administration`菜单项。

## 全局导航面板 {#global-navigation-panel}

选择左上角的`Adobe Experience Manager`图标，以便您可以打开全局导航面板并访问两个图标：

* [导航控制台](#navigation-console)
* [工具控制台](tools.md)

## 导航控制台 {#navigation-console}

要访问各个Communities控制台，请从全局导航中选择&#x200B;**导航， Communities**。

![社区](assets/communities.png)

* [Sites](sites-console.md)

  可在创作环境中访问站点控制台，用于创建和管理社区站点及其[组](groups.md)。

* [审核](moderation.md)

  “审阅”控制台用于批量审阅UGC和创作环境。 在Publish环境中，对于一个或多个社区站点，分配了[社区审查方](users.md#publishenvironmentusersandgroups)角色的社区成员可以访问类似的批量审查控制台。

* [成员、组](members.md)

  “成员”和“组”控制台用于从创作环境管理Publish环境中存在的社区成员和成员组。

* [报告](reports.md)

  当社区站点启用了[Adobe Analytics](sites-console.md#analytics)时，“报表”控制台可生成有关工作总揽、页面查看和已发布内容(UGC)的报表。 该控制台仅在创作环境中可用。

## 工具控制台 {#tools-console}

若要访问[Communities工具](tools.md)（以前为管理控制台），请从全局导航中访问： **[!UICONTROL 工具]** > **[!UICONTROL Communities]**
