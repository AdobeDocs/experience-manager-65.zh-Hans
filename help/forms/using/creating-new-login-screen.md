---
title: 创建登录界面
description: 如何修改LiveCycle模块的登录页面，例如AEM Forms工作区或Forms Manager。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 5%

---

# 创建登录界面{#creating-a-new-login-screen}

您可以修改所有使用AEM Forms登录屏幕的AEM Forms模块的登录屏幕。 例如，修改会同时影响Forms Manager和AEM Forms工作区的登录屏幕。

## 先决条件 {#prerequisite}

1. 使用管理员权限在`/lc/crx/de`登录。
1. 执行以下操作：

   1. 在`/libs/livecycle/core/content`处复制`/apps/livecycle/core/content`的分层结构。

      维护相同的（节点/文件夹）属性和访问控制。

   1. 复制内容文件夹：

      发件人： `/libs/livecycle/core`

      收件人：`/apps/livecycle/core`。

   1. 删除`/apps/livecycle/core`文件夹的内容。

1. 执行以下操作：

   1. 在`/libs/livecycle/core/components/login`处复制`/apps/livecycle/core/components/login`的分层结构。 维护相同的（节点/文件夹）属性和访问控制。

   1. 将组件文件夹：从`/libs/livecycle/core`复制到`/apps/livecycle/core`。

   1. 删除文件夹的内容： `/apps/livecycle/core/components/login`。

### 添加新区域设置 {#adding-a-new-locale}

1. 复制`i18n`文件夹：

   * 从 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 删除`i18n`中的所有文件夹（除一个文件夹外），例如`en`。

1. 在文件夹`en`上，执行以下操作：

   1. 将文件夹重命名为要支持的区域设置名称。 例如 `ar`。

   1. 将`jcr:language`文件夹的属性`ar`值更改为`ar`。

   >[!NOTE]
   >
   >如果区域设置是语言 — 国家/地区代码组合，例如`ar-DZ`，则将文件夹名称和属性值更改为`ar-DZ`。

1. 复制`login.jsp`：

   * 从 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 修改`/apps/livecycle/core/components/login/login.jsp`的以下代码片段：

   ***区域设置是语言代码***

   ```jsp
   String browserLocale = "en";
   
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   收件人

   ```jsp
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ```jsp
   String browserLocale = "en";
   
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   收件人

   ```jsp
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

***更改默认区域设置***

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### 添加新文本或修改现有文本 {#adding-new-text-or-modifying-existing-text}

1. 复制`i18n`文件夹：

   * 从 `/libs/livecycle/core/components/login`
   * 至`/apps/livecycle/core/components/login`

1. 现在，修改要更改其文本的节点的属性`sling:message`的值（在所需的区域设置代码文件夹下）。 通过节点的`sling:key`属性值中提到的键完成翻译。

1. 要添加新的键值对，请执行以下步骤。 查看以下屏幕快照中的示例。

   1. 在所有区域设置文件夹下创建类型为`sling:MessageEntry`的节点，或复制现有节点并将其重命名。
   1. 复制`login.jsp` ：

      * 从 `/libs/livecycle/core/components/login`

      * 至`/apps/livecycle/core/components/login`

   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合并新添加的文本。

   ![添加新的键值对](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   收件人

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### 添加新样式，或修改现有样式 {#adding-new-style-or-modifying-existing-style}

1. 复制`login`节点：

   * 从 `/libs/livecycle/core/content`
   * 至`/apps/livecycle/core/content`

1. 从节点`login.js`删除文件`jquery-1.8.0.min.js`和`/apps/livecycle/core/content/login.`
1. 修改CSS文件中的样式。
1. 要添加新样式，请执行以下操作：

   1. 向`/apps/livecycle/core/content/login/login.css`添加新样式
   1. 复制`login.jsp`

      * 从 `/libs/livecycle/core/components/login`

      * 至`/apps/livecycle/core/components/login`

   1. 修改`/apps/livecycle/core/components/login/login.jsp`以合并新添加的样式。


例如：

* 将以下内容添加到`/apps/livecycle/core/content/login/login.css`。

  ```
  css.newLoginContentArea {
      width: 700px;
      padding: 100px 0px 0px 100px;
  }
  ```

* 在`/apps/livecycle/core/components/login.jsp`中修改以下内容。


  ```jsp
  <div class="loginContentArea">
  ```

  收件人

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>如果删除`/apps/livecycle/core/content/login`（从`/libs/livecycle/core/content/login`复制）中的现有图像，则删除CSS中的相应引用。

### 添加新图像 {#add-new-images}

1. 按照添加新样式或修改现有样式（如上所述）的步骤操作。
1. 在`/apps/livecycle/core/content/login`中添加新图像。 要添加图像，请执行以下操作：

   1. 安装WebDAV客户端。
   1. 使用webDAV客户端导航到`/apps/livecycle/core/content/login`文件夹。 有关详细信息，请参阅[WebDAV访问](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=zh-Hans)。

   1. 添加新图像。

1. 在`/apps/livecycle/core/content/login/login.css,`中添加与在`/apps/livecycle/core/content/login`中添加的新图像对应的新样式。
1. 在`login.jsp`的`/apps/livecycle/core/components`处使用新样式。

   例如：


   ```css
   .newLoginContainerBkg {
   
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```


   * 在/apps/livecycle/core/components/login.jsp中修改以下内容。

   ```jsp
   <div class="loginContainerBkg">
   ```

   收件人

   ```jsp
   <div class="newLginContainerBkg">
   ```
