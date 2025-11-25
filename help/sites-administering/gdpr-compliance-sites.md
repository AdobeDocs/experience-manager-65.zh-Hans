---
title: AEM Sites - GDPR 就绪
description: 了解在 AEM Sites 中处理 GDPR 请求的操作流程，以及如何使用这些流程。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 100%

---

# AEM Sites - GDPR 就绪{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>以下章节以 GDPR 为示例进行说明，但其中涵盖的细节同样适用于所有数据保护和隐私法规，例如 GDPR 和 CCPA 等。

欧盟《通用数据保护条例》关于数据隐私权的规定自 2018 年 5 月起正式生效。

AEM Sites 已经准备好帮助客户履行 GDPR 合规义务。此页面将指导客户完成在 AEM Sites 中处理 GDPR 请求的过程。它描述了私有数据的存储位置，以及如何手动或使用代码移除私有数据。

有关更多信息，请参阅 [Adobe 隐私中心的 GDPR 页面](https://www.adobe.com/privacy/general-data-protection-regulation.html)。

>[!NOTE]
>
>有关更多详细信息，请参阅 [AEM GDPR 就绪](/help/managing/data-protection-and-privacy.md)。

## 作者服务器 {#author-server}

[平台 GDPR 文档](/help/managing/data-protection-and-privacy.md)涵盖了创作服务器上的用户帐户和 UGC 内容。

## 发布服务器 {#publish-server}

[平台 GDPR 文档](/help/managing/data-protection-and-privacy.md)涵盖了发布服务器上用于验证网站访客的用户帐户和 UGC 内容。

默认情况下，AEM Sites 组件不会存储访客在发布服务器上输入的表单数据。建议将数据转发到第三方系统或 Adobe Campaign 以供进一步处理。

## 选择加入/选择退出 {#opt-in-opt-out}

AEM 提供了一个 [Cookie 退出服务](/help/sites-developing/cookie-optout.md)，可用于管理用户的选择加入或选择退出。

## 通过 Analytics 提供的增强型洞察 {#enhanced-insights-by-analytics}

AEM Sites 包括与通过 Analytics 提供的增强型洞察的可选集成，该集成使用 Adobe Analytics 按需服务中的功能。

有关管理与 Adobe Analytics 相关的 GDPR 数据主体请求的更多信息，请参见 [Adobe Analytics 与 GDPR](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=zh-Hans)。

## 通过 Target 提供的增强型个性化 {#enhanced-personalization-by-target}

AEM Sites 包括与通过 Target 提供的增强型个性化的可选集成，该集成使用 Adobe Target 按需服务中的功能。

有关管理与 Adobe Target 相关的 GDPR 数据主体请求的更多信息，请参见 [Adobe Target - 隐私与通用数据保护条例](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en)。

## ContextHub {#contexthub}

AEM 提供了一个可选的数据层 [ContextHub](/help/sites-developing/contexthub.md)。这会将特定于访客的数据保留在浏览器中，以用于基于规则的个性化。

默认情况下，此访客数据不会存储在 AEM 中；AEM 将规则发送到数据层，以在浏览器中做出个性化决策。

>[!NOTE]
>
>在 Adobe AEM（CQ）5.6 之前，ClientContext（ContextHub 的早期版本）会将数据发送至服务器，但不会存储这些数据。
>
>Adobe AEM 6.4 及更早版本现已停止提供支持（EOL），不在本文档涵盖范围内。请参见[旧版本的 Adobe Experience Manager、CQ 和 CRX 文档](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions)。

### 实施选择加入/选择退出 {#implementing-opt-in-opt-out}

网站所有者需要根据以下指南实施选择退出组件。

这些指南将选择加入作为默认设置加以实施。因此，在任何个人数据存储到浏览器（客户端）持久层之前，网站访问者必须明确同意。

* 每次包含 ContextHub 组件时都应包含选择退出组件。
* 网站需向访问者展示与 GDPR 相关的条款和条件，并允许他们：

   * 接受
   * 拒绝
   * 更改其上一个选择

* 如果网站访客接受网站的条款和条件，则应删除 ContextHub 选择退出 Cookie：

  ```java
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  ```

* 如果网站访客不接受网站的条款和条件，则应设置 ContextHub 选择退出 Cookie：

  ```java
  ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
  ```

* 要检查 ContextHub 是否正在选择退出模式下运行，应在浏览器的控制台中进行以下调用：

  ```java
  var isOptedOut = ContextHub.isOptedOut(true) === true;
  // if isOptedOut is true, ContextHub is running in opt-out mode
  ```

### 预览 ContextHub 的持久存储 {#previewing-persistence-of-contexthub}

要预览使用 ContextHub 的持久存储，用户可以：

* 例如，使用浏览器的控制台：

   * Chrome：

      * 打开“开发人员工具”>“应用程序”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”

   * Firefox：

      * 打开“开发人员工具”>“存储”：

         * “本地存储”>“（网站）”>“ContextHubPersistence”
         * “会话存储”>“（网站）”>“ContextHubPersistence”
         * “Cookie”>“（网站）”>“SessionPersistence”

   * Safari：

      * 在菜单栏中打开“偏好设置”>“高级”>“显示开发”菜单
      * 打开“开发”>“显示 JavaScript 控制台”

         * “控制台”>“存储”>“本地存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“会话存储”>“（网站）”>“ContextHubPersistence”
         * “控制台”>“存储”>“Cookie”>“（网站）”>“ContextHubPersistence”

   * Internet Explorer：

      * 打开“开发人员工具”>“控制台”

         * localStorage.getItem（&#39;ContextHubPersistence&#39;）
         * sessionStorage.getItem（&#39;ContextHubPersistence&#39;）
         * document.cookie

* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（default）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 存储会定义使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。

例如，要查看存储在 localStorage 中的数据，请执行以下操作：

要预览使用 ContextHub 的持久存储，用户可以：

* 使用浏览器的控制台：

   * Chrome - 打开“开发人员工具”>“应用程序”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”

   * Firefox - 打开“开发人员工具”>“存储”：

      * “本地存储”>“（网站）”>“ContextHubPersistence”
      * “会话存储”>“（网站）”>“ContextHubPersistence”
      * “Cookie”>“（网站）”>“SessionPersistence”

* 在浏览器的控制台中使用 ContextHub API：

   * ContextHub 提供以下数据持久层：

      * ContextHub.Utils.Persistence.Modes.LOCAL（default）
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

     ContextHub 存储会定义使用哪个持久层，因此，要查看持久存储的当前状态，应检查所有层。

例如，要查看存储在 localStorage 中的数据，请执行以下操作：

```java
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### 清除 ContextHub 的持久存储 {#clearing-persistence-of-contexthub}

要清除 ContextHub 持久存储，请执行以下操作：

* 要清除当前加载的持久存储，请执行以下操作：

  ```java
  // to be able to fully access persistence layer, Opt-Out must be turned off
  ContextHub.Utils.Cookie.removeItem('cq-opt-out');
  
  // following call asks all currently loaded stores to clear their data
  ContextHub.cleanAllStores();
  
  // following call asks all currently loaded stores to set back default values (provided in their configs)
  ContextHub.resetAllStores();
  ```

* 要清除特定的持久层（例如 sessionStorage），请执行以下操作：

  ```java
  var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
  storage.setItem('/store', null);
  storage.setItem('/_', null);
  
  // to confirm that nothing is stored:
  console.log(storage.getTree());
  ```

* 要清除所有 ContextHub 持久层，必须为所有层调用适当的代码：

   * ContextHub.Utils.Persistence.Modes.LOCAL（default）
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
