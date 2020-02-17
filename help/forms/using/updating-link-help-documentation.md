---
title: 更新指向文档的链接
seo-title: 更新指向文档的链接
description: 如何更新AEM Forms工作区中“工作区帮助”链接的目标位置，以指向您的自定义文档链接。
seo-description: 如何更新AEM Forms工作区中“工作区帮助”链接的目标位置，以指向您的自定义文档链接。
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更新指向文档的链接 {#updating-the-link-to-the-documentation}

通过选择“帮助”>“工作区帮助”，可以访问AEM Forms工作区的 **默认帮助内容**。 它指向Adobe网站上的在线文档。 但是，您可以更新它以指向任何其他URL。

请考虑以下用例，您可能希望更改默认帮助URL:

* 以您选择的语言提供本地化帮助。
* 为自定义工作区提供自定义帮助内容。

要更新联机文档的URL，请按照自定义的 [常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md) ，然后执行以下步骤。

1. 将文 `userinfo.html` 件从复 `/libs/ws/js/runtime/templates` 制到 `/apps/ws/js/runtime/templates`。
1. 更改：

   ```
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   到

   ```
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索并替换 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` 为 `text!/lc/apps/ws/js/runtime/templates/userinfo.html`。

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
