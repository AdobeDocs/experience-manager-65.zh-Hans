---
title: 配置帐户环境
description: AEM 提供了用于配置帐户和创作环境的某些方面的功能
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 6079431d-7d08-4973-8bb4-a8d10626a795
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 81%

---

# 配置帐户环境{#configuring-your-account-environment}

AEM 提供了用于配置帐户和创作环境的某些方面的功能。

通过使用[标题](/help/sites-authoring/basic-handling.md#the-header)和关联的[我的首选项](#userpreferences)对话框中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项，您可以修改用户选项。

首先，访问标题中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项。

## 用户设置 {#user-settings}

在&#x200B;**用户**&#x200B;设置对话框中，您可以访问：

* 模拟为

   * 通过使用[模拟为](/help/sites-administering/security.md#impersonating-another-user)功能，用户可以代表其他用户工作。

* 配置文件

   * 提供指向您的[用户设置](/help/sites-administering/security.md)的便捷链接

* [我的偏好设置](/help/sites-authoring/user-properties.md#my-preferences)

   * 指定用户特有的各种首选项设置

![screen_shot_2018-03-20at103808](assets/screen_shot_2018-03-20at103808.png)

### 我的偏好设置 {#my-preferences}

**我的首选项**&#x200B;对话框可通过标题中的[用户](/help/sites-authoring/user-properties.md#user-settings)选项进行访问。

每个用户都可以为自己设置某些属性。

![screen-shot_2019-03-05at100322](assets/screen-shot_2019-03-05at100322.png)

* **语言**

  此选项定义要用于创作环境 UI 的语言。从可用列表中选择所需语言。

  此配置还用于经典UI。

* **窗口管理**

  此选项定义打开窗口的行为。选择：

   * **多窗口**（默认）

      * 页面会在新窗口中打开。

   * **单窗口**

      * 页面会在当前窗口中打开。

* **显示适用于资源的桌面操作**

  此选项需要使用AEM桌面应用程序。

* **注释颜色**

  此选项定义创建注释时使用的默认颜色。

   * 单击颜色块，以便可以打开样本选择器并选择颜色。
   * 或者，可在字段中输入所需颜色的十六进制代码。

* **相对日期显示**

  为了提高可读性，AEM 会将过去七天内的日期显示为相对日期（例如三天前），而将更早的日期则显示为确切日期（例如 2017 年 3 月 20 日）。

  此选项定义系统中日期的显示方式。以下选项可供选择：

   * **始终显示确切日期**：将始终显示确切日期（从不显示相对日期）。
   * **1 天**：对于一天内的日期显示相对日期，其他情况则显示确切日期。

   * **7 天（默认）**：对于七天内的日期显示相对日期，其他情况则显示确切日期。

   * **1 个月**：对于一个月内的日期显示相对日期，其他情况则显示确切日期。

   * **1 年**：对于一年内的日期显示相对日期，其他情况则显示确切日期。

   * **始终显示相对日期**：从不显示确切日期，只显示相对日期。

* **启用快捷键**

  AEM支持使用多个键盘快捷键，以便更高效地创作。

   * [用于编辑页面的键盘快捷键](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)
   * [控制台的键盘快捷键](/help/sites-authoring/keyboard-shortcuts.md)

  此选项可启用键盘快捷键。默认情况下启用这些键盘快捷键，但也可禁用，例如，如果用户有特定的辅助功能要求。

* **使用经典创作体验**

  此选项启用基于[经典UI](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md)的页面创作。 默认情况下，使用标准UI。

* **启用资源主页**

  只有系统管理员为整个组织启用了资源主页体验，才有此选项可用。

* **Stock 配置**

  通过此选项，可指定首选的 Adobe Stock 配置，并且只有系统管理员已启用 [Adobe Stock 集成](/help/assets/aem-assets-adobe-stock.md)，才有此选项可用。
