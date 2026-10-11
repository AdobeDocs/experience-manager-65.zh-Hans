---
title: 更新文档链接
description: 如何更新AEM Forms工作区中Workspace帮助链接的目标以指向您的自定义文档链接。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 11%
---
# 更新文档链接 {#updating-the-link-to-the-documentation}

您可以通过选择&#x200B;**帮助> AEM Forms帮助**&#x200B;来访问Workspace工作区的默认帮助内容。 它指向Adobe网站上的在线文档。 但是，您可以将其更新为指向任何其他URL。

在您需要更改默认帮助URL时，请考虑以下用例：

* 以您选择的语言提供本地化帮助。
* 用于为您的自定义工作区提供自定义帮助内容。

要更新联机文档的URL，请按照[自定义的一般步骤](/help/forms/using/generic-steps-html-workspace-customization.md)操作，然后执行以下步骤。

1. 将`userinfo.html`文件从`/libs/ws/js/runtime/templates`复制到`/apps/ws/js/runtime/templates`。
1. 更改：

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
   1. 搜索并将`text!/lc/libs/ws/js/runtime/templates/userinfo.html`替换为`text!/lc/apps/ws/js/runtime/templates/userinfo.html`。
