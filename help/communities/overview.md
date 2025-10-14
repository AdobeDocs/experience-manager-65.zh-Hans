---
title: AEM Communities概述
description: 了解Adobe Experience Manager Communities功能和设置的基础知识。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# AEM Communities概述 {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities允许您快速创建本地社区站点，该站点提高了性能、改进了站点管理，并鼓励将站点访客转化为有价值的社区成员。

## Communities功能 {#communities-features}

AEM Communities支持与网站访客建立关系，这些网站访客：

* **通过博客、问答和事件日历通知**，
* 同时&#x200B;**通过论坛、评论和其他社区内容获得见解**，通常称为用户生成内容(UGC)。
* 它允许Publish环境中受信任的成员进行&#x200B;**审核**，
* 使用Twitter和Facebook的&#x200B;**社交登录**，
* 社区内容的&#x200B;**内联翻译**，
* 从已发布的社区站点创建&#x200B;**社区组**，
* **得分**&#x200B;奖励徽章，
* **文件共享**，
* **通知**&#x200B;和&#x200B;**活动流**，
* 允许用户生成内容中的&#x200B;**标记** (@mention)其他注册成员以引起他们的注意。

社区功能可以使用GitHub.com上公开提供的[AEM演示计算机](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)或新的`We.Retail`参考实现进行演示。

## 社区站点 {#community-sites}

社区站点是使用简单向导创建的AEM站点，该向导会导致网站具有许多预连接到站点的常见功能。

[站点创建向导](/help/communities/sites-console.md)：

* 基于所选的[社区站点模板](/help/communities/sites.md)组合站点的功能，该模板为：

   * 通过[社区功能](#community-functions)生成
   * 可选的[社区组](#communitygroups)功能

* 使用设置配置：

   * 审核
   * 登录
   * 转换

* 提供以下基本功能：

   * 响应式设计：使用[TwitterBootstrap主题](https://getbootstrap.com)

   * 登录：自助注册，[社交登录](/help/communities/social-login.md)，用户配置文件

      * 通知：
成员会看到与其相关的事件，以及用户生成的内容，其中他们是[@mentioned](/help/communities/overview.md#mentionssupport)。

      * 消息：成员可以在社区站点中发送或接收消息。
      * 搜索：可在社区站点内搜索。
      * 语言切换：能够为[多语言站点](/help/sites-administering/translation.md)选择语言。

      * 管理：授权成员在社区站点中审核和管理用户的权限。

* 无需执行许多页面级创作步骤：

   * 品牌策略：可选择性上传横幅图像以在社区站点的所有页面上显示
   * 导航菜单：为社区站点模板中包含的功能提供了导航链接。

要体验快速创建社区站点的简便性，请访问[AEM Communities快速入门](/help/communities/getting-started.md)。

## 社区内容持久性 {#community-content-persistence}

为了改进社区内容的性能和同步，AEM Communities要求专门针对在所有AEM（创作和发布）实例之间共享的用户生成内容(UGC)的公共存储。

通过存储资源提供程序(SRP)可轻松访问社区内容，SRP提供了一个将访问与底层拓扑分离开的层，并支持UGC的公共存储。

要了解有关社区内容持久性和建议部署的更多信息，请参阅：

* [社区内容存储](/help/communities/working-with-srp.md) — 讨论可用于UGC的SRP存储选项。
* [推荐的拓扑](/help/communities/topologies.md) — 根据用例和SRP选择讨论拓扑。
* [升级到AEM 6.5 Communities](/help/communities/upgrade.md) — 在迁移到AEM 6.5时提供有关UGC的有用信息。

## 社区控制台 {#communities-consoles}

在创作环境中，全局导航控制台提供对[社区控制台](/help/communities/consoles.md)的访问权限，该控制台包含：

* [Sites &#x200B;](/help/communities/sites-console.md)控制台

   * 站点创建
   * 站点编辑
   * 站点管理
   * [社区组](/help/communities/groups.md)控制台

* [审核](/help/communities/moderation.md)控制台

   * 适用于“创作”和“Publish”环境的通用批量审核UI。
   * 新建筛选条件。

* [成员和组](/help/communities/members.md)管理控制台

   * 允许您从创作环境创建和管理发布端用户（成员）。
   * 允许您禁止成员。
   * 允许您从创作环境创建和管理发布端用户组（成员组）。

* [报告](/help/communities/reports.md)控制台

   * 允许您生成有关工作、帖子及视图的报告。

全局工具控制台提供对以下Communities工具的访问：

* [站点模板](/help/communities/tools.md#sitetemplatesconsole)控制台

   * 创建和管理社区站点模板。

* [组模板](/help/communities/tools.md#grouptemplatesconsole)控制台

   * 创建和管理社区组模板。

* [社区功能](/help/communities/tools.md#communityfunctionsconsole)控制台

   * 创建和管理社区功能。

* [存储配置](/help/communities/tools.md#storageconfiguratonconsole)控制台

   * 选择并配置站点的[公用存储](/help/communities/working-with-srp.md)。

* [组件指南](/help/communities/components-guide.md)

   * 示例站点[社区组件](https://localhost:4502/editor.html/content/community-components/en.html)提供了所有Communities组件的示例及其默认配置和试验这些组件的能力。

## 社区站点模板 {#community-site-templates}

社区站点创建基于选择的社区站点模板，可快速设置独立于任何示例站点的社区站点。

由社区功能和社区组模板组成的社区站点模板提供了社区站点的结构。 其中包括登录、用户配置文件、消息、网站菜单、搜索、主题设定和品牌推广功能。

查看[站点模板控制台](/help/communities/sites.md)。

## 社区功能 {#community-functions}

社区体验的预期功能是众所周知的。 在AEM Communities中，这些功能可用作构建块，称为社区功能。

社区功能是一般的AEM页面，这些页面包含相互连接的组件，这些组件构成了一项功能，该功能可轻松合并到社区站点模板中。

查看[社区功能控制台](/help/communities/functions.md)。

## 社区组和组模板 {#community-groups-and-group-templates}

社区组功能允许作者和发布环境中的授权用户和社区成员在社区站点中动态创建子社区。

在创作环境中，如果模板的结构包含[组功能](/help/communities/functions.md#groups-function)，则可以在现有社区站点内创建社区组（子社区），也可以嵌套在现有组内。

创建社区组需要选择提供社区组页面设计的社区组模板。 将组功能添加到模板结构时，会将其配置为指定一个组模板，或在创建新社区组时提供模板选择。

另请参阅：

* 用于在创作环境中创建子社区的[站点组控制台](/help/communities/groups.md)。
* [组模板控制台](/help/communities/tools-groups.md)，用于创建组的站点结构。
* [AEM Communities快速入门](/help/communities/getting-started.md)教程介绍如何快速创建包含嵌套组的社区站点。

## 社区组件 {#community-components}

从中生成社区站点的[社区组件](/help/communities/author-communities.md)可用于向任何AEM站点添加社区功能。

[社区组件指南](/help/communities/components-guide.md)可用于以交互方式浏览组件。

## 参与社区 {#engagement-community}

参与社区是一个社区站点，它专注于吸引客户以通知、征求反馈并允许客户作为社区成员进行互动。

参与社区的功能可能包括：

* 登录
* 消息
* 论坛
* 评论
* 审核
* 评级
* 投票
* 博客
* 组
* 日历
* 翻译
* 审核
* 通知
* 评分和徽章
* Analytics报表

要体验快速创建参与社区的简便性，请访问[AEM Communities快速入门](/help/communities/getting-started.md)。

## AEM演示计算机 {#aem-demo-machine}

[AEM演示计算机](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)管理和运行AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)和[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)的演示，这些演示通常需要比启动QuickStart实例更多的设置。 AEM Demo Machine设置其他[基础架构](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)，如MongoDB、Solr、MySQL、FFmpeg和电子邮件服务器。

AEM演示计算机包括：

* [图形用户界面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置的[属性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)和[目标](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)的Apache ANT脚本。

* 要安装的包。

已在Windows、macOS和Linux®上成功使用CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4测试AEM演示计算机。

AEM演示计算机需要有效的AEM许可证。

>[!NOTE]
>
>查看AEM演示计算机的[视频简介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) (13:26)。

## AEM Communities文档 {#aem-communities-documentation}

* 访问[部署社区](deploy-communities.md)，了解建议的部署。
* 访问[管理社区站点](administer-landing.md)，您可以在其中了解有关创建社区站点、添加社区组、配置社区站点模板、审核社区内容、管理成员、标记、通知、评分和徽章的信息。
* 访问[开发社区](communities.md)，您可以在其中了解社交组件框架(SCF)和自定义社区组件和功能。
* 访问[创作社区组件](author-communities.md)，您可以在其中了解如何使用及配置社区组件。
