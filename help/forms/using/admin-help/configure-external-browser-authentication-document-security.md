---
title: 为文档安全配置来自外部浏览器的扩展身份验证
description: 了解如何配置外部浏览器身份验证，以便用户可以使用系统默认Web浏览器在Acrobat或Reader中对受策略保护的PDF文档进行身份验证。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 89a07256cd5bb850aac19565ad86273322fa1f31
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# 为文档安全配置来自外部浏览器的扩展身份验证 {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> 确保您具有访问AEM Forms管理控制台的管理员权限。

通过来自外部浏览器的扩展身份验证，用户可以使用系统的默认Web浏览器（如Microsoft Edge或Google Chrome）而不是Acrobat或Reader中的嵌入式浏览器控件来验证受策略保护的PDF文档。 这可以启用现代身份验证方法，例如PassKey、生物特征身份验证和其他需要现代浏览器的身份提供程序(IDP)功能。

启用后，在Acrobat或Reader中打开受策略保护的文档将在用户的默认浏览器中启动IDP登录页面。 身份验证后，用户会自动重定向回Acrobat或Reader，并且文档会被解锁。

## 先决条件 {#prerequisites}

在配置外部浏览器身份验证之前，请确保满足以下要求：

* 已部署Service Pack 6.5.25.0的JEE上的AEM Forms 6.5，或已部署Service Pack 6.5.24.0，并在支持的应用程序服务器（JBoss、WebLogic或WebSphere）上安装适用的JEE修补程序修补程序。 查看AEM Forms JEE修补程序2的[软件分发链接6.5.24.0](#software-distribution-links)。
* 扩展身份验证（第三方身份验证）已经在IDP中启用和正常工作。 请参阅[服务器配置设置](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)和[添加扩展身份验证提供程序](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider)。
* 使用最新更新安装在客户端Windows PC上的Adobe Acrobat Pro或Adobe Acrobat Reader（64位）。

>[!NOTE]
>
> 外部浏览器身份验证需要客户端上的Adobe Acrobat或Adobe Acrobat Reader的支持版本。 有关版本详细信息和更新，请参阅[Acrobat发行说明（2026年3月连续跟踪）](https://www.adobe.com/devnet-docs/acrobatetk/tools/ReleaseNotesDC/continuous/dccontinuousmarch2026.html#dccontinuousmarchtwentytwentysix)。

### AEM Forms JEE修补程序2的软件分发链接6.5.24.0 {#software-distribution-links}

JEE Service Pack 6.5.25.0及更高版本上的AEM Forms中提供了外部浏览器身份验证。

如果您在JEE Service Pack 6.5.24.0或更早版本上的AEM Forms上，请执行以下操作之一：

* 升级到JEE Service Pack 6.5.25.0[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)上的AEM Forms。
* 使用以下链接为您的应用程序服务器和平台安装AEM Forms JEE修补程序6.5.24.0修补程序。

从[AEM Forms Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)下载并安装适用于您平台的Adobe JEE修补程序6.5.24.0修补程序：

**JBoss**

* Windows：适用于JBoss JEE服务器的Windows上的AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)
* Linux：适用于JBoss JEE服务器的Linux上AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows：适用于WebSphere JEE服务器的Windows上的AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)
* Linux：适用于WebSphere JEE服务器的Linux上AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows：适用于WebLogic JEE服务器的Windows上的AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)
* Linux：适用于WebLogic JEE服务器的Linux上AEM Service Pack 6.5.24.0的[修补程序](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

有关安装说明，请参阅[安装JEE修补程序](/help/release-notes/jee-patch-installer-65.md)。

## 启用外部浏览器身份验证 {#enable-external-browser-authentication}

本视频说明如何在AEM Forms Document Security服务器上启用外部浏览器身份验证。

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. 在管理控制台中，单击&#x200B;**服务** > **Document Security** > **配置** > **服务器配置**。
1. 找到&#x200B;**允许从外部浏览器对Adobe客户端应用程序进行扩展身份验证**&#x200B;部分。
1. 选中要启用的每个Adobe客户端平台的复选框：
   * **Adobe Acrobat和Reader（64位） — 桌面**
   * **Adobe Acrobat Reader（32位） — 桌面**
1. 单击&#x200B;**确定**。

有关服务器设置说明，请参阅[服务器配置设置](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)。

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## 验证 {#verification}

本视频说明如何验证外部浏览器身份验证：在Acrobat中打开受策略保护的PDF，通过默认浏览器登录，并确认文档在身份验证后解锁。

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. 使用Document Security服务器创建受策略保护的PDF文档。
1. 在Windows客户端计算机上，在Acrobat Pro或Acrobat Reader中打开受保护的PDF。
1. Acrobat中将显示同意对话框。 单击&#x200B;**登录**。
1. 验证系统默认浏览器是否打开，并显示IDP登录页面。
1. 完成身份验证。
1. 验证受保护文档是否成功打开。

## 疑难解答 {#troubleshooting}

### 此时将打开嵌入式浏览器，而不是系统浏览器 {#embedded-browser-opens-instead-of-system-browser}

* 验证服务器是否启用了外部浏览器身份验证。 请参阅[启用外部浏览器身份验证](#enable-external-browser-authentication)。
* 确认Acrobat或Reader版本支持此功能。 请参阅[Acrobat](#acrobat)。

### 在浏览器中验证成功，但文档未解锁 {#authentication-succeeds-but-document-does-not-unlock}

* 确保Acrobat或Reader正在运行且未被防火墙或安全软件阻止。
* 如果问题仍然存在，请重新安装或修复Acrobat或Reader安装以恢复协议处理程序注册。

### Acrobat中显示“您无法登录”消息 {#we-couldnt-sign-you-in-message}

* 用户完成身份验证可能花费了太长时间。 请重试。
* 检查浏览器和AEM Forms服务器之间的网络连接。

### 登录页面上未显示身份验证选项 {#authentication-option-does-not-appear}

* 身份验证方法和选项由IDP配置，而不由AEM Forms或Acrobat配置。 确保IDP支持您要使用的身份验证方法。
* 验证登录页面是否在系统浏览器（而非嵌入式浏览器）中加载。
