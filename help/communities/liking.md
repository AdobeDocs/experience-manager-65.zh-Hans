---
title: 使用点赞
description: 了解如何添加和配置Liking组件，以便用户可以就特定内容（如评论）发表意见。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# 使用点赞 {#using-liking}

`Liking`组件是一个有用的工具，它允许用户表达对特定内容的意见，如论坛中的评论。 使用`Liking`组件时，成员会选择心形图标来指示积极意见。

## 向页面添加点赞 {#adding-liking-to-a-page}

要将`Liking`组件添加到创作模式下的页面，请使用组件浏览器来查找

* `Communities / Liking`

并将其拖动到页面上的适当位置，例如用户喜欢的相对于该功能的位置。

有关必要的信息，请访问[社区组件基础知识](basics.md)。

当包含[所需的客户端库](essentials-liking.md#essentials-for-client-side)时，`Liking`组件的显示方式如下所示。

![liking-component](assets/liking-component.png)

## 配置点赞 {#configuring-liking}

选择放置的`Liking`组件，以便您可以访问并选择用于打开“编辑”对话框的`Configure`图标。

![配置 — 新](assets/configure-new.png)

在&#x200B;**[!UICONTROL 文本和标签]**&#x200B;选项卡下，指定用于记录赞的属性。

![配置链接](assets/configure-liking.png)

* **[!UICONTROL 正面响应标签]**

  （*必需*）正响应的属性名称。

* **[!UICONTROL 负响应标签]**

  （*必需*）负响应的属性名称。

* **[!UICONTROL 记帐名称]**

  （*必需*）投票组件的此实例的内部可识别属性名称。

## 网站访客体验 {#site-visitor-experience}

### 成员 {#members}

成员可随时更改“赞”。

### 匿名 {#anonymous}

不支持匿名点赞。 网站访客必须注册（成为会员）并登录才能参与点赞。

## 附加信息 {#additional-information}

更多信息可在[Liking Essentials](essentials-liking.md)页面上找到开发人员。
