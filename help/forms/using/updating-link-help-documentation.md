---
title: 更新指向文档的链接
seo-title: Updating the link to the documentation
description: 如何更新AEM Forms工作区中“工作区帮助”链接的目标，以指向您的自定义文档链接。
seo-description: How-to update the destination of Workspace Help link in AEM Forms workspace to point to your custom documentation link.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 3%

---

# 更新指向文档的链接 {#updating-the-link-to-the-documentation}

您可以通过选择 **帮助>工作区帮助**. 它指向Adobe网站上的在线文档。 但是，您可以更新它以指向任何其他URL。

请考虑以下用例，您可能希望更改默认帮助URL:

* 提供所选语言的本地化帮助。
* 用于为自定义工作区提供自定义帮助内容。

要更新在线文档的URL，请在 [自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md) 然后执行以下步骤。

1. 复制 `userinfo.html` 文件来源 `/libs/ws/js/runtime/templates` to `/apps/ws/js/runtime/templates`.
1. 更改:

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   到

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 执行以下操作：

   1. 打开/apps/ws/js/registry.js进行编辑。
   1. 搜索和替换 `text!/lc/libs/ws/js/runtime/templates/userinfo.html` with `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
