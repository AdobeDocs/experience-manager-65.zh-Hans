---
title: 更改界面上的字体
description: 如何有选择地更改用户界面上的字体。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# 更改界面上的字体{#changing-the-font-on-the-interface}

您可以更改AEM Forms工作区中显示的字体。 在用户界面的特定部分中使用的字体在样式表的相应部分中定义。 您可以选择性地更改用户界面上的字体。

请遵循 [AEM Forms工作区自定义的常规步骤](../../forms/using/generic-steps-html-workspace-customization.md) 根据您的要求，执行自定义CSS和/或HTML的步骤。

1. 在现有样式中更改或添加字体系列。
1. 更改或添加HTML元素的font-family inline。
1. 添加样式并将其用于HTML元素。

例如，要将顶部导航栏锚点文本的字体更改为“Courier New”，请执行以下步骤：

1. 通过访问登录到CRXDE Lite `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. 执行下列操作之一：

   1. 要更改现有样式中的字体系列，请在/apps/ws/css的newStyle.css文件中添加以下内容。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. 要为HTML元素添加font-family inline，请复制 `/libs/ws/js/runtime/templates/appnavigation.html` 文件到 `/apps/ws/js/runtime/templates/appnavigation.html`.

      按如下方式更新/apps/ws/js/runtime/templates/appnavigation.html文件：

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      打开/apps/ws/js/registry.js文件进行编辑和替换 `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` 替换为 `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. 要添加定义字体系列的样式，请在/apps/ws/css的newStyle.css文件中添加以下内容。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      要为HTML元素添加font-family内联，请在/apps/ws/js/runtime/templates的appnavigation.html文件中添加以下内容。

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. 重新启动工作区并清除浏览器缓存，以使更改可见。

![change_font_before](assets/change_font_before.png)

字体自定义前的顶部导航栏

![change_font_after](assets/change_font_after.png)

第一个选项卡的字体自定义后的顶部导航栏
