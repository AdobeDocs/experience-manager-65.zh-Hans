---
title: 如何在AEM自适应表单6.5中使用Turnstile？
description: 使用Turnstile服务轻松增强表单安全性。 里面有分步指南！
feature: Adaptive Forms, Foundation Components
role: User, Developer
exl-id: bed93ce3-89db-477a-8316-7598275e4bca
source-git-commit: 94a9f4087e36bfe5701ad9aafd4e8446ca643ddf
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 11%

---

# 将AEM Forms环境与Turnstile连接 {#connect-your-forms-environment-with-turnstile-service}

<!--
<span class="preview">This feature is based on Feature Toggle id `FT_FORMS-12407`. To enable the feature, follow the steps given in the [Enable Feature Toggle](/help/forms/using/enable-feature-toggle.md) article. </span>
-->

<span class="preview">默认情况下不启用此功能。 您可以从官方地址写信到aem-forms-ea@adobe.com请求访问该功能。</span>

CAPTCHA（区分计算机和人类的完全自动化公共图灵测试）是一种在线交易中常用的程序，用于区分人类和自动化程序或机器人。它提出了一个挑战，并评估用户响应以确定是人还是机器人与网站交互。如果测试失败，它会阻止用户继续操作，并通过阻止机器人发布垃圾邮件或恶意目的来帮助确保在线交易的安全。

AEM Forms 6.5支持以下CAPTCHA解决方案：

* [Turnstile 验证码](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [验证码](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## 将AEM Forms环境与Turnstile验证码集成

Cloudflare的Turnstile Captcha是一项安全措施，旨在保护表单和站点免受自动机器人、恶意攻击、垃圾邮件和不需要的自动流量的侵害。 在允许提交表单之前，它会在表单提交时显示一个复选框，以验证他们是人类。

>[!VIDEO](https://video.tv.adobe.com/v/3440940/)

### 将AEM Forms环境与Turnstile验证码集成的先决条件 {#prerequisite}

要为AEM Forms配置Turnstile，您需要从Turnstile网站获取[Turnstile站点密钥和密钥](https://developers.cloudflare.com/turnstile/get-started/)。

### 配置Turnstile {#steps-to-configure-hcaptcha}

要将AEM Forms与Turnstile服务集成，请执行以下步骤：

1. 在您的AEM Forms环境中创建配置容器。 配置容器包含用于将AEM Forms连接到外部服务的云配置。 要创建配置容器，请执行以下操作：
   1. 打开您的AEM Forms环境。
   1. 转到&#x200B;**[!UICONTROL 工具>常规>配置浏览器]**。
   1. 在配置浏览器中，选择现有文件夹或创建新文件夹：
      * 要创建&#x200B;**新文件夹**&#x200B;并启用云配置，请执行以下操作：
         1. 在配置浏览器中，单击&#x200B;**[!UICONTROL 创建]**。
         1. 在创建配置对话框中，指定名称、标题，并检查&#x200B;**[!UICONTROL 云配置]**。
         1. 单击&#x200B;**[!UICONTROL 创建]**。
      * 要为&#x200B;**现有文件夹**&#x200B;启用云配置：
         1. 在配置浏览器中，选择文件夹，然后单击&#x200B;**[!UICONTROL 属性]**。
         1. 在配置属性对话框中，启用&#x200B;**[!UICONTROL 云配置]**。
         1. 单击&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存配置。

1. 配置Cloud Service：
   1. 在您的AEM创作实例上，转到![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Service]**，然后单击&#x200B;**[!UICONTROL Turnstile]**。

      ![Cloud Service中的旋转门](assets/turnstile-in-ui.png)
   1. 选择已创建或已更新的配置容器，如上一节所述。 单击&#x200B;**[!UICONTROL 创建]**。

      ![配置旋转门](assets/config-hcaptcha.png)
   1. 将&#x200B;**[!UICONTROL 小组件类型]**&#x200B;指定为托管、非交互或不可见。
   1. 提供其他详细信息，如&#x200B;**[!UICONTROL Title]**、**[!UICONTROL Name]**。
   1. 为必备项[&#128279;](#prerequisite)中获取的Turnstile服务指定&#x200B;**[!UICONTROL 站点密钥]**&#x200B;和&#x200B;**[!UICONTROL 密钥]**。
   1. 单击&#x200B;**[!UICONTROL 创建]**。

      ![配置Cloud Service以将AEM Forms环境与Turnstile连接](assets/config-turntstile.png)

   >[!NOTE]
   > 用户无需修改客户端JavaScript验证URL和服务器端验证URL，因为它们已为Turnstile验证预先填充。

   配置Turnstile Captcha服务后，即可在自适应表单中使用。

## 在自适应表单中使用Turnstile{#using-turnstile-aem-6.5}

1. 打开您的AEM Forms环境。
1. 转到&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 选择自适应表单，然后单击&#x200B;**[!UICONTROL 属性]**。 在&#x200B;**[!UICONTROL 配置容器]**&#x200B;中，选择包含将AEM Forms与Turnstile连接的云配置的配置容器。
1. 单击“**[!UICONTROL 保存并关闭]**”。

   如果您没有用于配置Captcha服务的配置容器，请参阅[配置Turnstile](#configure-turnstile-steps-to-configure-hcaptcha)部分以了解如何创建配置容器。

   ![选择配置容器](assets/captcha-properties.png)

1. 选择一个自适应表单，然后单击&#x200B;**[!UICONTROL 编辑]**&#x200B;以在编辑器中打开您的自适应表单。
1. 从组件浏览器中，将&#x200B;**[!UICONTROL Captcha]**&#x200B;组件拖放到自适应表单上。
1. 选择&#x200B;**[!UICONTROL Captcha]**&#x200B;组件并单击“属性”![“属性”图标](assets/configure-icon.svg)图标。 此时将打开“属性”对话框。 指定以下属性：

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Cloudfare Turnstile v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL 标题]：**&#x200B;指定验证码组件的标题。 在表单和规则编辑器中，您可以使用表单组件的唯一标题轻松识别表单组件。
   * **[!UICONTROL 配置设置]：**&#x200B;选择为Turnstile配置的云配置。
   * **[!UICONTROL 验证消息]：**&#x200B;提供验证消息，以便在表单提交或用户操作时验证验证码。
   * **[!UICONTROL Captcha服务]：**&#x200B;为您的表单提交选择CAPTCHA服务，此处选择Turnstile®。
   * **[!UICONTROL 配置设置]：**&#x200B;选择为Turnstile®配置的云配置。

     >[!NOTE]
     >出于类似目的，您的环境中可以有多个云配置。 所以，请仔细选择服务。 如果未列出任何服务，请参阅[将您的AEM Forms环境与Turnstile连接](#connect-your-forms-environment-with-turnstile-service)，了解如何创建将AEM Forms环境与Turnstile服务连接的Cloud Service。

   * **[!UICONTROL 错误消息]：**&#x200B;提供验证码提交失败时向用户显示的错误消息。
   * **验证码大小：**&#x200B;您可以选择hCaptcha®质询对话框的显示大小。 使用&#x200B;**[!UICONTROL Compact]**&#x200B;选项显示小尺寸的，使用&#x200B;**[!UICONTROL Normal]**&#x200B;显示相对大尺寸的hCaptcha®质询对话框。

1. 选择&#x200B;**[!UICONTROL 完成]**。


现在，只有合法的表单，表单填写者才能成功清除Turnstile服务带来的挑战，才能提交表单。

![Turnstile挑战](assets/turnstile-challenge.png)


## 常见问题解答

* **问：能否在自适应表单中使用多个Captcha组件？**
* 不支持在自适应表单中使用多个Captcha组件的&#x200B;**Ans：**。 此外，不建议在标记为延迟加载的片段或面板中使用验证码组件。

## 另请参阅 {#see-also}

* [在自适应表单中使用CAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [在自适应表单中使用Captcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
