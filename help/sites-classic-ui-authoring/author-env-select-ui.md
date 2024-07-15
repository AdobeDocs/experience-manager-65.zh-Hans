---
title: 选择您的UI
description: 为了方便创作用户，启用了触屏的UI允许在必要时切换到经典UI。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 57d45b06-e76e-420c-8cd0-389bd9f811af
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# 选择您的UI{#selecting-your-ui}

由于触屏优化UI取代了经典UI，因此AEM实例的用户或管理员必须做出积极决定，才能继续使用经典UI。 由于经典UI不再进行维护，因此创作用户不可能简单地从经典UI切换到触屏UI中的等效项。

为了方便创作用户，启用了触屏的UI允许在必要时切换到经典UI。 有关详细信息，请参阅标准创作文档中的[选择您的UI](/help/sites-authoring/select-ui.md)。

>[!NOTE]
>
>从以前的版本升级的实例将保留用于页面创作的经典UI。
>
>升级后，页面创作将不会自动切换到触控式UI，但您可以使用&#x200B;**WCM创作UI模式服务** （`AuthoringUIMode`服务）的[OSGi配置](/help/sites-deploying/configuring-osgi.md)配置此设置。 查看编辑器](#uioverridesfortheeditor)的[UI覆盖。

## 为实例配置默认UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)来配置启动时看到的UI和登录。

这可以由用户默认设置或会话设置覆盖。
