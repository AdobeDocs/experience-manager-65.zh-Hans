---
title: 在AEM中选择用户界面
description: 配置在Adobe Experience Manager 6.5中使用的界面。
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# 选择您的UI{#selecting-your-ui}

Adobe Experience Manager (AEM)触屏优化UI现在是标准的UI，通过管理和编辑站点，几乎达到了功能对等性。 但是，有时用户可能会想要切换到[经典UI](/help/sites-classic-ui-authoring/classicui.md)。 执行此操作有多种选项。

>[!NOTE]
>
>有关经典UI的功能对等状态的详细信息，请参阅[触控UI功能对等](/help/release-notes/touch-ui-features-status.md)文档。

您可以在多个位置定义要使用的UI：

* [为实例配置默认UI](#configuring-the-default-ui-for-your-instance)
这将设置在用户登录时显示的默认UI。 用户可以覆盖此内容，并为其帐户或当前会话选择其他UI。

* [正在为您的帐户设置经典UI创作](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
这会在编辑页面时将UI设置为默认值，但用户可以覆盖此设置，并为其帐户或当前会话选择其他UI。

* [切换到当前会话的经典UI](#switching-to-classic-ui-for-the-current-session)
切换到当前会话的经典UI。

* 对于[页面创作，系统会对UI](#ui-overrides-for-the-editor)进行某些覆盖。

>[!CAUTION]
>
>用于切换到经典UI的各种选项并非立即可用，必须为实例配置这些选项。
>
>有关详细信息，请参阅[启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md)。

>[!NOTE]
>
>从以前的版本升级的实例会保留用于页面创作的经典UI。
>
>升级后，页面创作不会自动切换到触控式UI，但您可以使用&#x200B;**WCM创作UI模式服务** （`AuthoringUIMode`服务）的[OSGi配置](/help/sites-deploying/configuring-osgi.md)配置此设置。 查看编辑器](#ui-overrides-for-the-editor)的[UI覆盖。

## 为实例配置默认UI {#configuring-the-default-ui-for-your-instance}

系统管理员可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping)来配置启动时看到的UI和登录。

这可以由用户默认设置或会话设置覆盖。

## 为您的帐户设置经典UI创作 {#setting-classic-ui-authoring-for-your-account}

每个用户都可以访问自己的[用户偏好设置](/help/sites-authoring/user-properties.md#userpreferences)来定义他们是否要使用经典UI进行页面创作，而不是默认UI。

会话设置可以覆盖此设置。

## 切换到当前会话的经典UI {#switching-to-classic-ui-for-the-current-session}

使用触屏优化UI时，桌面用户可能希望还原到经典（仅限桌面）UI。 有多种方法可用于切换到当前会话的经典UI：

* **导航链接**

  >[!CAUTION]
  >
  >用于切换到经典UI的此选项并非立即可用，必须针对您的实例对其进行配置。
  >
  >
  >有关详细信息，请参阅[启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md)。

  如果启用此功能，则每当您将鼠标悬停在适用的控制台上时，都会显示一个图标（监视器符号）。 点按/单击此项将在经典UI中打开相应的位置。

  例如，从&#x200B;**站点**&#x200B;到&#x200B;**站点管理员**&#x200B;的链接：

  ![syui-01](assets/syui-01.png)

* **URL**

  可以使用位于`welcome.html`的欢迎屏幕的URL访问经典UI。 例如：

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >触屏优化UI可通过`sites.html`访问。 例如：
  >
  >
  >`https://localhost:4502/sites.html`

### 编辑页面时切换到经典UI {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>用于切换到经典UI的此选项并非立即可用，必须针对您的实例对其进行配置。
>
>有关详细信息，请参阅[启用对经典UI的访问](/help/sites-administering/enable-classic-ui.md)。

如果启用，**打开经典UI**&#x200B;可在&#x200B;**页面信息**&#x200B;对话框中找到：

![syui-02](assets/syui-02.png)

### 编辑器的UI覆盖 {#ui-overrides-for-the-editor}

如果存在页面创作，则系统可能会覆盖用户或系统管理员定义的设置。

* 创作页面时：

   * 在URL中使用`cf#`访问页面时，强制使用经典编辑器。 例如：
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * 在URL中使用`/editor.html`或使用触控设备时，会强制使用已启用触控功能的编辑器。 例如：
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* 任何强制都是临时的，并且仅对浏览器会话有效

   * Cookie集的设置取决于使用的是已启用触屏(`editor.html`)还是经典(`cf#`)。

* 通过`siteadmin`打开页面时，会检查是否存在以下内容：

   * Cookie
   * 用户首选项
   * 如果两者都不存在，则默认为&#x200B;**WCM创作UI模式服务** （`AuthoringUIMode`服务）的[OSGi配置](/help/sites-deploying/configuring-osgi.md)中设置的定义。

>[!NOTE]
>
>如果[用户已为页面创作](#settingthedefaultauthoringuiforyouraccount)定义了首选项，则不会通过更改OSGi属性来覆盖该首选项。

>[!CAUTION]
>
>由于使用了Cookie（如上所述），因此不建议执行以下任一操作：
>
>* 手动编辑URL — 非标准URL可能会导致未知情况和功能缺失。
>* 同时打开两个编辑器 — 例如，在不同窗口中打开。
