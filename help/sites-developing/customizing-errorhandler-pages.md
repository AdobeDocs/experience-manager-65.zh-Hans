---
title: 自定义错误处理程序显示的页面
description: Adobe Experience Manager提供了用于处理HTTP错误的标准错误处理程序。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: d6745baa-44da-45dd-b5d5-a9b218e7e8cf
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# 自定义错误处理程序显示的页面{#customizing-pages-shown-by-the-error-handler}

Adobe Experience Manager (AEM)附带用于处理HTTP错误的标准错误处理程序；例如，通过显示：

![chlimage_1-67](assets/chlimage_1-67a.png)

系统提供的脚本存在（位于`/libs/sling/servlet/errorhandler`下）以响应错误代码，默认情况下，标准CQ实例中提供了以下内容：

* 403.jsp
* 404.jsp

>[!NOTE]
>
>AEM基于Apache Sling。 因此，有关Sling错误处理的详细信息，请参阅[错误处理](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)。

>[!NOTE]
>
>在创作实例上，默认启用[CQ WCM调试筛选器](/help/sites-deploying/osgi-configuration-settings.md)。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪来响应。
>
>在发布实例上，CQ WCM调试筛选器为&#x200B;*始终*&#x200B;已禁用（即使配置为已启用）。

## 如何自定义错误处理程序显示的页面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以开发自己的脚本，以自定义遇到错误时错误处理程序显示的页面。 您的自定义页面在`/apps`下创建，并覆盖默认页面（在`/libs`下）。

>[!NOTE]
>
>有关更多详细信息，请参阅[使用叠加图](/help/sites-developing/overlays.md)。

1. 在存储库中，复制默认脚本：

   * 从 `/libs/sling/servlet/errorhandler/`
   * 至`/apps/sling/servlet/errorhandler/`

   默认情况下，由于目标路径不存在，因此，在首次执行该操作时必须创建该路径。

1. 导航到`/apps/sling/servlet/errorhandler`并执行以下任一操作：

   * 编辑相应的现有脚本，以便提供所需的信息。
   * 为所需代码创建和编辑新脚本。

1. 保存更改并进行测试。

>[!CAUTION]
>
>404.jsp和403.jsp处理程序旨在满足CQ5身份验证的要求；特别是允许在出现这些错误时进行系统登录。
>
>因此，这两个处理程序的替换应该非常小心。

### 自定义对HTTP 500错误的响应 {#customizing-the-response-to-http-errors}

HTTP 500错误是由服务器端异常引起的。

* **[500内部服务器错误](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)**
服务器遇到意外情况，无法完成请求。

当请求处理导致出现异常时，Apache Sling框架(AEM构建于之上)：

* 记录异常
* 返回：

   * HTTP响应代码500
   * 异常栈栈跟踪

  在响应的正文中。

通过[自定义错误处理程序](#how-to-customize-pages-shown-by-the-error-handler)显示的页面，可以创建`500.jsp`脚本。 但是，仅当显式执行`HttpServletResponse.sendError(500)`时（即，从异常捕获器）才使用它。

否则，响应代码设置为500，但不执行`500.jsp`脚本。

要处理500个错误，错误处理程序脚本的文件名必须与异常类（或超类）相同。 若要处理所有此类例外，您可以创建脚本`/apps/sling/servlet/errorhandler/Throwable.js`p或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在创作实例上，默认启用[CQ WCM调试筛选器](/help/sites-deploying/osgi-configuration-settings.md)。 这始终导致响应代码200。 默认错误处理程序通过向响应写入完整栈栈跟踪来响应。
>
>对于自定义错误处理程序，需要代码为500的响应，因此必须禁用[CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md)。 这可确保返回响应代码500，这反过来会触发正确的Sling错误处理程序。
>
>在发布实例上，CQ WCM调试筛选器为&#x200B;*始终*&#x200B;已禁用（即使配置为已启用）。
