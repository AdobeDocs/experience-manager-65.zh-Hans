---
title: 更改接口的颜色方案
description: 如何有选择地修改AEM Forms Workspace用户界面部分的配色方案。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: e0a261a2-518b-4984-a5b5-24f0b9222e24
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# 更改接口的颜色方案 {#changing-the-color-scheme-of-the-interface}

您可以修改AEM Forms工作区用户界面部分的配色方案以满足您的要求。 以下是一些具有代表性的颜色方案自定义示例。 除了本文中讨论的步骤之外，请参阅[AEM Forms工作区自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md)。

## 顶部导航栏 {#top-navigation-bar}

### 使用背景图像 {#using-background-image}

更新AEM Forms工作区顶部的导航栏。

1. 创建背景图像以更新颜色。 将文件命名为newBackground.jpg。
1. 使用WebDAV客户端上传/apps/ws/images文件夹中的背景图像文件。

   >[!NOTE]
   >
   >有关详细信息，请参阅[WebDAV访问](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en)。

1. 添加以下样式以引用/apps/ws/css/newStyle.css中的新背景图像。

   ```css
   #header {
       background:#292929 url(../images/newBackground.jpg) repeat-x;
   }
   ```

### 在CSS中使用color属性 {#using-color-property-in-css}

1. 在/apps/ws/css的newStyle.css中添加以下样式

   ```css
   #header {
   background : none;
   background-color: gray;
   }
   ```

## 类别组件 {#category-component}

类别组件在左侧面板中显示任务的各种类别。 要更改其颜色，请在CSS文件的`.category`元素中定义背景颜色。

## 任务组件 {#task-component}

任务显示在称为TaskList组件的中间面板中。 要更改其颜色，请修改样式表中与.task选择器关联的样式。
