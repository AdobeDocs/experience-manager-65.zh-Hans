---
title: 更改品牌推广的组织徽标
description: 要打造AEM Forms工作区，请通过自定义默认徽标提供您组织的徽标。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# 更改品牌推广的组织徽标 {#changing-the-organization-logo-for-branding}

组织徽标显示在AEM Forms工作区的左上角。 要更新徽标，请按照 [AEM Forms工作区自定义的常规步骤](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) 然后执行以下步骤。

1. 创建徽标并将文件命名为 `NewWorkspace.png`. 使用WebDAV客户端将图像文件放置到/apps/ws/images文件夹中。

   >[!NOTE]
   >
   >徽标图像的推荐大小为218像素×20像素。

   >[!NOTE]
   >
   >有关更多信息，请参阅 [WebDAV访问](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en).

   [WebDAV访问](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=en)

1. 通过添加以下样式，在/apps/ws/css/newStyle.css的样式表中引用新的徽标图像。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
