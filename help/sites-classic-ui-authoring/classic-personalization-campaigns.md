---
title: Campaign Management
description: Campaign管理为数字营销人员提供了交付个性化内容并为访客创建专用体验的机会。 它可让您跨Web、电子邮件和移动服务编排营销活动，从而吸引访客。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: d1741525-a475-4a76-bd16-55318023495e
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Campaign Management{#campaign-management}

Campaign管理为数字营销人员提供了交付个性化内容并为访客创建专用体验的机会。

它可让您跨Web、电子邮件和移动服务编排营销活动，从而吸引访客。 您可以为特定用户配置文件创建内容、细分访客、推送和提升目标内容并跨多个渠道管理营销活动。

本文档介绍了构成营销活动的各种元素。 更多详细信息见以下文档：

* [Teaser和策略](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [电子邮件营销](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [登陆页面](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Target优惠](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [使用营销活动经理](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [了解分段](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [设置活动](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

营销活动管理由各种元素组成：

* **品牌**
在Adobe Experience Manager (AEM)中，品牌是顶层单位，构成了**促销活动**&#x200B;的集合。

* **营销活动**
营销活动是单个**体验**&#x200B;的集合。

* **体验**
重点内容形成了各种体验，在**接触点**&#x200B;提供给访客。 有多种类型的体验可用：

   * **预告**
     [Teaser页面/段落](#teasers)用于引导特定访客&#x200B;**区段**&#x200B;访问关注其兴趣的内容。

     Teaser页面可以：

      * 提供一系列选项供访客选择
      * 仅显示一个基于特定访客区段的Teaser段落。 例如，显示的Teaser段落可能取决于访客的年龄。

     通常，Teaser页面是一种临时操作，在特定时间段内持续存在，直到它被下一个Teaser页面替换为止。

   * **新闻稿**

     [电子邮件通信](#emailmarketing)用于吸引用户并鼓励他们访问您的网站。 这些通常采用新闻稿的形式，发送给您的&#x200B;**潜在客户**（这些潜在客户已分组到&#x200B;**列表**）。 **注意：** Adobe不打算进一步增强此功能。 建议您[使用Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

   * **Adobe Target**

     这允许与Adobe Target（以前称为Test&amp;Target）集成，后者为营销人员提供了一个转化网站优化工具，让他们拥有必要的功能，以便始终提供与其客户更密切相关的在线内容和选件，从而产生更高的转化。 Adobe Target提供了一个直观的界面，可用于从单个应用程序设计和执行测试、创建受众区段和定位内容。

* **接触点**

  这些是访客与您的营销活动之间的联系点。 接触点会连接到您创建的体验。

  例如，对于Teaser，它是Teaser段落所在的内容页面；对于新闻稿，它是邮寄列表。

* **潜在客户**

  您收集到的有关访客的信息以及如何联系这些访客的信息构成了潜在客户的基础。 **注意：** Adobe不打算进一步增强此功能。

  建议您[使用Adobe Campaign以及与AEM](/help/sites-administering/campaign.md)的集成。

* **列表**

  潜在客户将分组到列表中，以便您能够对其执行集体操作。 注意： **注意：** Adobe不打算进一步增强此功能。

  建议使用[使用Adobe Campaign以及与AEM的集成。](/help/sites-administering/campaign.md)

* **区段**

  网站访客在访问网站时具有不同的兴趣和目标。 根据网站上的活动、注册的用户档案信息和其他网站上的活动等因素对此进行分析可帮助您定义区段。 然后，可以根据访客匹配的区段，将内容定位到访客的需求和兴趣上。

* **MCM**

  营销活动管理器(MCM)是一个控制台，可让您访问创建和控制营销活动、品牌、体验、接触点、潜在客户、列表、区段和报表所需的所有功能。

  可以从各种位置（标记为&#x200B;**促销活动**）访问，例如，使用URL访问：

  `http://localhost:4502/libs/mcm/content/admin.html`
