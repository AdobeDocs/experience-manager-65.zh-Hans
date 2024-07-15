---
title: 徽章控制台
description: 通过“社区徽章”控制台，您可以添加自定义徽章，当成员获得（授予）或在社区中承担特定角色（已分配）时，徽章将会显示
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 50ed9ec4-ff04-4f9d-aefb-0837542a9455
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 4%

---

# 徽章控制台 {#badges-console}

## 关于徽章 {#about-badges}

通过“社区徽章”控制台，可添加自定义徽章，当成员获得（授予）或在社区中承担特定角色（已分配）时，徽章可显示给成员。

### 徽章可见性 {#badge-visibility}

目前，社区成员获得的徽章或分配的徽章与其名称和头像一起显示在以下位置：

* 配置文件
* [论坛](/help/communities/forum.md)
* [问题与解答](/help/communities/working-with-qna.md)
* [排行榜](/help/communities/enabling-leaderboard.md)
* [构思](/help/communities/ideation-feature.md)

在创作环境中，导航到徽章控制台：

* 从全局导航： **[!UICONTROL 工具]** > **[!UICONTROL 社区]** > **[!UICONTROL 徽章]**

此控制台显示当前可用的徽章，并可从中添加新徽章。

![徽章 — 主页](assets/badges-homepage.png)

## 创建徽章 {#create-badge}

通过上载适当小图像（高度为26-32像素的72 dpi）并提供名称来创建徽章。 徽章图像存储在`/libs/settings/community/badging/images`的存储库中，并自动复制到发布环境。

如果发布环境是发布服务器场，则需要配置[用户同步](/help/communities/sync.md)。

![创建徽章](assets/create-badge.png)

* **上传图像**

  （*必需*）徽章图像，建议大小为32 x 32像素，以72 dpi为JPEG或PNG格式。

* **名称**

  （*必需*）徽章名称。 它是默认`Display Name`和存储库节点名称。 如果`Name`不是有效的存储库节点名称，则会修改它。

* **显示名称**

  （*可选*）用户界面中为徽章显示的名称。 默认值是为`Name`输入的未更改文本。

* **描述**

  （*可选*）徽章的说明。

## 附加信息 {#additional-information}

有关设置评分和徽章规则的详细信息，请参阅[评分和徽章](/help/communities/implementing-scoring.md)。

有关管理成员的徽章，请参阅[成员控制台](/help/communities/members.md)。
