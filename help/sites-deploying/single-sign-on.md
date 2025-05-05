---
title: 单点登录
description: 了解如何为Adobe Experience Manager (AEM)实例配置单点登录(SSO)。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
exl-id: 7d2e4620-c3a5-4f5a-9eb6-42a706479d41
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# 单点登录 {#single-sign-on}

单点登录(SSO)允许用户在提供一次身份验证凭据（如用户名和密码）后访问多个系统。 独立的系统（称为可信验证器）执行验证并向Experience Manager提供用户凭据。 Experience Manager会检查并强制实施用户的访问权限（即确定允许用户访问的资源）。

SSO身份验证处理程序服务(`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`)处理受信任的身份验证程序提供的身份验证结果。 SSO身份验证处理程序按以下顺序在下列位置搜索SSO标识符(SSID)作为特殊属性的值：

1. 请求标头
1. Cookies
1. 请求参数

找到某个值后，即完成搜索，并将使用此值。

配置以下两个服务以识别存储SSID的属性的名称：

* 登录模块。
* SSO身份验证服务。

为两个服务指定相同的属性名称。 该属性包含在提供给`Repository.login`的`SimpleCredentials`中。 属性的值是无关的和被忽略的，仅仅它的存在是很重要和可以验证的。

## 配置SSO {#configuring-sso}

要为AEM实例配置SSO，请配置[SSO身份验证处理程序](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)：

1. 使用AEM时，可通过多种方法管理此类服务的配置设置；请参阅[配置OSGi](/help/sites-deploying/configuring-osgi.md)以了解更多详细信息和建议的做法。

   例如，对于NTLM set：

   * **路径：**&#x200B;为必填项；例如，`/`
   * **标头名称**： `LOGON_USER`
   * **ID格式**： `^<DOMAIN>\\(.+)$`

     其中`<*DOMAIN*>`被替换为您自己的域名。

   对于CoSign：

   * **路径：**&#x200B;为必填项；例如，`/`
   * **标头名称**： remote_user
   * **ID格式：**&#x200B;原样

   对于SiteMinder：

   * **路径：**&#x200B;为必填项；例如，`/`
   * **标头名称：** SM_USER
   * **ID格式**： AsIs

1. 确认单点登录是否按要求工作；包括授权。

>[!CAUTION]
>
>确保如果配置了SSO，则用户无法直接访问AEM。
>
>通过要求用户通过运行SSO系统代理的Web服务器，可以确保任何用户都不能直接发送标头、Cookie或参数，从而使其受到AEM的信任，因为如果从外部发送，代理将过滤此类信息。
>
>任何无需通过Web服务器即可直接访问您的AEM实例的用户都可以通过发送标头、Cookie或参数（如果名称已知）来作为任何用户。
>
>另外，请确保在标头、Cookie和请求参数名称中，您仅配置SSO设置所需的名称。
>

>[!NOTE]
>
>单点登录通常用于[LDAP](/help/sites-administering/ldap-config.md)。

>[!NOTE]
>
>如果您还将[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hans)与Microsoft® Internet Information Server (IIS)一起使用，则需要在中进行其他配置：
>
>* `disp_iis.ini`
>* IIS
>
>在`disp_iis.ini`集合中：
>(有关完整详细信息，请参阅[将Dispatcher与Microsoft® Internet Information Server一起安装](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=zh-Hans#microsoft-internet-information-server))
>
>* `servervariables=1` （将IIS服务器变量作为请求标头转发到远程实例）
>* `replaceauthorization=1` （将除“Basic”以外的任何名为“Authorization”的标头替换为其“Basic”等效标头）
>
>在IIS中：
>
>* 禁用&#x200B;**匿名访问**
>
>* 启用&#x200B;**集成Windows身份验证**
>

您可以使用Felix控制台的&#x200B;**Authenticator**&#x200B;选项查看正在将哪个身份验证处理程序应用于内容树的任何部分；例如：

`http://localhost:4502/system/console/slingauth`

首先查询与路径最匹配的处理程序。 例如，如果您为路径`/`配置处理程序A，为路径`/content`配置处理程序B，则对`/content/mypage.html`的请求将首先查询处理程序B。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 示例 {#example}

对于Cookie请求（使用URL `http://localhost:4502/libs/wcm/content/siteadmin.html`）：

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

使用以下配置：

* **路径**： `/`

* **标头名称**： `TestHeader`

* **Cookie名称**： `TestCookie`

* **参数名称**： `TestParameter`

* **ID格式**： `AsIs`

答案是：

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

如果您请求，这也适用：
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

或者，您可以使用以下curl命令将`TestHeader`标头发送到`admin:`
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>在浏览器中使用请求参数时，您只会看到部分HTML（不带CSS）。 这是因为来自HTML的所有请求都是在不使用request参数的情况下进行的。

## 删除AEM注销链接 {#removing-aem-sign-out-links}

使用SSO时，登录和注销在外部进行处理，因此AEM自己的注销链接不再适用，应将其删除。

可以使用以下步骤删除欢迎屏幕上的注销链接。

1. 覆盖`/libs/cq/core/components/welcome/welcome.jsp`到`/apps/cq/core/components/welcome/welcome.jsp`
1. 从jsp中删除以下部分。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

要删除用户右上角个人菜单中的注销链接，请执行以下步骤：

1. 覆盖`/libs/cq/ui/widgets/source/widgets/UserInfo.js`到`/apps/cq/ui/widgets/source/widgets/UserInfo.js`

1. 从文件中删除以下部分：

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
