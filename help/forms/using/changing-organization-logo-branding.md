---
title: 更改品牌的组织徽标
seo-title: 更改品牌的组织徽标
description: 要品牌化AEM Forms工作区，请通过自定义默认徽标来提供您组织的徽标。
seo-description: 要品牌化AEM Forms工作区，请通过自定义默认徽标来提供您组织的徽标。
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更改品牌的组织徽标 {#changing-the-organization-logo-for-branding}

组织徽标显示在AEM Forms工作区的左上角。 要更新标志，请按照AEM Forms工作 [区自定义的常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) ，然后执行以下步骤。

1. 创建标志并将文件命名为 `NewWorkspace.png`。 使用WebDAV客户端将图像文件放入/apps/ws/images文件夹。

   >[!NOTE]
   >
   >Logo图像的建议大小为218 px × 20 px。

   >[!NOTE]
   >
   >有关WebDAV访问的详细信息，请参 [阅https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html)。

1. 通过添加以下样式，在/apps/ws/css/newStyle.css中引用样式表中的新标志图像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```

[联系支持](https://www.adobe.com/account/sign-in.supportportal.html)
