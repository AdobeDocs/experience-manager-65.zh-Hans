---
title: 在一台服务器上托管两个AEM Forms工作区实例
description: LC管理员如何自定义HTMLWS，以便在可以通过不同URL访问的单个服务器上托管两个实例。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 32a546fc-e33f-46f9-ac3b-45eca0e12239
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# 在一台服务器上托管两个AEM Forms工作区实例 {#hosting-two-aem-forms-workspace-instances-on-one-server}

AEM Forms的默认安装和设置只允许服务器上有一个AEM Forms工作区。 但是，您可能需要在一台AEM Forms服务器上托管两个不同的AEM Forms工作区实例。 这两个实例可以通过不同的URL进行访问。

AEM Forms管理员自定义工作区，以创建两个不同的URL，并使两个工作区在同一服务器上可用。 在该自定义文章中，您可以假设两个工作区在`https://'[server]:[port]'/lc/ws`和`https://'[server]:[port]':/lc/ws2`处均可访问。

按照以下步骤配置AEM Forms工作区。

1. 在服务器上安装AEM Forms工作区的开发包。 请参阅[开发包](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p)，获取创建该开发包的说明。
1. 通过访问`https://'[server]:[port]'/lc/crx/de/index.jsp`，以管理员身份登录CRXDE Lite。
1. 在/content处复制节点ws，并在/content处粘贴。 将节点重命名为ws2。 单击&#x200B;**[!UICONTROL 全部保存]**。 在此节点的属性中，将`sling:resourceType`的值更改为ws2。 单击&#x200B;**[!UICONTROL 全部保存]**。

1. 从/libs复制文件夹ws并将其粘贴到/apps。 将文件夹重命名为ws2。 单击&#x200B;**[!UICONTROL 全部保存]**。
1. 在`/apps/ws2`的`GET.jsp`中，进行以下代码更改。 替换以下内容

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   ，代码为

   ```html
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. 在`/apps/ws2/js`的`registry.js`中，更改模板路径以引用`/apps/ws2/js/runtime/templates`中的模板。 替换以下代码

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   ，代码为

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. 在`userinfo.js`的`/apps/ws2/js/runtime/models`和`/apps/ws2/js/runtime/views`中，将字符串`/lc/content/ws`更改为`lc/content/ws2`。

1. 在`/apps/ws2/js/runtime/services/service.js`中，将`getLocalizationData`函数中的路径更改为指向`/lc/apps/ws2/Locale.html`。

1. 要引用新Workspace的`pdf.html`，请在`/apps/ws2/js/runtime/views/forms/pdftaskform.js`中更改`pdf.html`的路径。

1. 要引用新Workspace的`pdf.html`，请在`/apps/ws2/js/runtime/templates`处更改`startprocess.html`、`taskdetails.html`和`processinstancehistory.html`中的`pdf.html`和`WsNextAdapter.swf`的路径。

1. 复制`/etc/map/ws`文件夹并粘贴到`/etc/map`。 将新文件夹重命名为ws2。 单击“全部保存”。

1. 在`ws2`的属性中，将`sling:redirect`的值更改为`content/ws2`。

1. 将`sling:match`的值更改为`^[^/\||]/[^/\||]/ws2$`。
