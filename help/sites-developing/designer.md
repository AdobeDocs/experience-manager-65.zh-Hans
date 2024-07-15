---
title: 设计和Designer
description: 了解如何使用Designer为您的网站和AEM创建设计。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 设计和Designer{#designs-and-the-designer}

>[!CAUTION]
>
>本文介绍了如何基于经典UI创建网站。 Adobe建议为您的网站使用最新的AEM技术，如文章[开发AEM Sites快速入门](/help/sites-developing/getting-started.md)中所述。

Designer用于在AEM中使用[Classic UI](/help/release-notes/touch-ui-features-status.md)为您的网站创建设计。

>[!NOTE]
>
>有关Web辅助功能的详细信息，请参阅[AEM和Web辅助功能准则](/help/managing/web-accessibility.md)。

## 使用Designer {#using-the-designer}

您的设计可在&#x200B;**工具**&#x200B;选项卡的&#x200B;**设计**&#x200B;部分中定义：

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

您可以在此处创建存储设计所需的结构，然后上载所需的层叠样式表和图像。

设计存储在`/apps/<your-project>`下。 使用`jcr:content`节点的`cq:designPath`属性指定了网站要使用的设计路径。

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>在设计模式下对页面所做的所有更改将保留在网站的设计节点下，并自动应用于具有相同设计的所有页面。

## 您将需要什么 {#what-you-will-need}

要实现您的设计，您需要：

**CSS** — 层叠样式表定义页面上特定区域的格式。
**图像** — 用于背景、按钮等功能的任何图像。

### 设计网站时的注意事项 {#considerations-when-designing-your-website}

在开发网站时，强烈建议在`/apps/<your-project>`下存储图像和CSS文件，以便您可以根据当前设计引用资源，如以下代码片段所述。

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

上述示例提供了多种好处：

* 组件可以使用不同的设计路径根据每个站点具有不同的外观。
* 只需将设计路径指向站点根目录下从`design/v1`到`design/v2.`的其他节点，即可重新设计网站

* `/etc/designs`和`/content`是浏览器看到的唯一外部URL，用于保护您免受外部用户对`/apps`树下内容的好奇。 上述URL好处还可帮助系统管理员设置更好的安全性，因为您将资产暴露限制在几个不同的位置。
