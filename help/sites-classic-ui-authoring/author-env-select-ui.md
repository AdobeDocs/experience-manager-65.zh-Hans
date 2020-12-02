---
title: 选择您的 UI
seo-title: 选择您的 UI
description: 为了创作用户方便起见，触屏优化 UI 允许在必要时切换到经典 UI。
seo-description: 为了创作用户方便起见，触屏优化 UI 允许在必要时切换到经典 UI。
uuid: 755e513e-990c-4dba-8316-623f17bf5c33
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: dcac2a3a-3241-47de-96ce-982ab0bc05eb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 60%

---


# 选择您的 UI{#selecting-your-ui}

由于触屏优化UI将取代经典UI,AEM实例的用户或管理员必须主动决定继续使用经典UI。 由于经典UI不再进行维护，因此创作用户无法简单地从经典UI切换到触屏优化UI中的等效UI。

为了创作用户方便起见，触屏优化 UI 允许在必要时切换到经典 UI。有关详细信息，请参阅标准创作文档中的[选择您的 UI](/help/sites-authoring/select-ui.md)。

>[!NOTE]
>
>对于从以前版本升级而来的实例，页面创作将继续使用经典 UI。
>
>升级后，页面创作不会自动切换到触屏优化UI，但您可以使用&#x200B;**WCM创作UI模式服务**（`AuthoringUIMode`服务）的[OSGi配置](/help/sites-deploying/configuring-osgi.md)进行配置。 请参阅[编辑器的 UI 重写](#uioverridesfortheeditor)。

## 配置实例的默认 UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以通过使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)配置启动和登录时显示的 UI。

该设置可能会被用户默认设置或会话设置所重写。
