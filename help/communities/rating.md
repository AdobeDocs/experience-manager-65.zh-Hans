---
title: 使用评级
description: 了解如何向页面添加评级组件，该页面允许登录社区成员通过评级内容来表达他们的意见。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# 使用评级 {#using-ratings}

`Rating`组件是独立使用的或与其他Communities功能一起使用。 此组件允许登录的社区成员通过评级内容来表达他们的意见。

## 向页面添加评级 {#adding-a-rating-to-a-page}

要将`Rating`组件添加到创作模式下的页面，请找到组件`Communities / Rating`并将其拖动到页面上的适当位置，例如相对于要评级成员的功能的位置。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](rating-basics.md#essentials-for-client-side)时，`Rating`组件的显示方式如下所示。

![评分](assets/rating.png)

## 配置评级 {#configuring-rating}

选择放置的`Rating`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置 — 新](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文本和标签]**&#x200B;选项卡下，指定评级的内部标识符。

![tallyname](assets/tallyname.png)

**[!UICONTROL 记帐名称]**
（*必需*）唯一标识此实例的`Rating`的简单名称。 必须为存储库的有效节点名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

每个成员只允许一个评级。 会员可以随时变更等级。

### 匿名 {#anonymous}

不支持匿名发布评级。 网站访客必须注册（成为会员）并登录才能参与。

## 附加信息 {#additional-information}

可在面向开发人员的[Rating Essentials](rating-basics.md)页面上找到更多信息。
