---
title: 在AEM表单中启用单点登录
seo-title: Enabling single sign-on in AEM forms
description: 了解如何使用HTTP标头和SPNEGO启用单点登录(SSO)。
seo-description: Learn how to enable single sign-on (SSO) using HTTP headers and SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# 在AEM表单中启用单点登录{#enabling-single-sign-on-in-aem-forms}

AEM forms提供两种启用单点登录(SSO)的方法 — HTTP标头和SPNEGO。

实施SSO时，AEM Forms用户登录页面不是必需的，并且如果用户已经通过其公司门户进行了身份验证，则不会显示。

如果AEM Forms无法使用上述任一方法验证用户，则会将用户重定向到登录页面。

## 使用HTTP标头启用SSO {#enable-sso-using-http-headers}

您可以使用“门户配置”页面在应用程序和支持通过HTTP标头传送身份的任何应用程序之间启用单点登录(SSO)。 实施SSO时，AEM Forms用户登录页面不是必需的，并且如果用户已经通过其公司门户进行了身份验证，则不会显示。

您还可以使用SPNEGO启用SSO。 (请参阅 [使用SPNEGO启用SSO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. 在管理控制台中，单击设置>用户管理>配置>配置门户属性。
1. 选择“是”以启用SSO。 如果选择“否”，则页面上的其余设置不可用。
1. 根据需要设置页面上的其余选项，然后单击确定：

   * **SSO类型：** （必需）选择HTTP标头以使用HTTP标头启用SSO。
   * **用户标识符的HTTP标头：** （必需）标头的名称，其值包含登录用户的唯一标识符。 “用户管理”使用此值在“用户管理”数据库中查找用户。 从该标头获得的值应与从LDAP目录同步的用户的唯一标识符匹配。 (请参阅 [用户设置](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **标识符值映射到用户的用户ID，而不是用户的唯一标识符：** 将用户的唯一标识符值映射到用户ID。 如果用户的唯一标识符是一个二进制值，无法通过HTTP标头轻松传播，请选择此选项（例如，如果从Active Directory同步用户，则选择objectGUID）。
   * **域的HTTP头：** （非必需）其值包含域名的标头名称。 仅当没有单个HTTP标头唯一标识用户时，才使用此设置。 当存在多个域且唯一标识符仅在域中唯一时，可使用此设置。 在这种情况下，请在此文本框中指定标头名称，并在域映射框中指定多个域的域映射。 (请参阅 [编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **域映射：** （必需）指定格式中多个域的映射 *标头值=域名*.

      例如，考虑以下情况：域的HTTP标头是domainName，并且它可能具有domain1、domain2或domain3值。 在这种情况下，请使用域映射将domainName值映射到“用户管理”域名。 每个映射必须位于不同的行上：

      domain1=UMdomain1

      domain2=UMdomain2

      域3=UM域3

### 配置允许的引用 {#configure-allowed-referers}

有关配置允许的反向链接的步骤，请参阅 [配置允许的引用](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## 使用SPNEGO启用SSO {#enable-sso-using-spnego}

在Windows环境中使用Active Directory作为LDAP服务器时，可以使用简单和受保护的GSSAPI协商机制(SPNEGO)来启用单点登录(SSO)。 启用SSO后，AEM Forms用户登录页面不是必填页面，因此不会显示。

您还可以使用HTTP标头启用SSO。 (请参阅 [使用HTTP标头启用SSO](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>JEE上的AEM Forms不支持在多个子域环境中使用Kerberos/SPNEGO配置SSO。

1. 决定使用哪个域来启用SSO。 AEM Forms服务器和用户必须是同一Windows域或受信任域的一部分。
1. 在Active Directory中，创建一个代表AEM表单服务器的用户。 (请参阅 [创建用户帐户](enabling-single-sign-on-aem.md#create-a-user-account).) 如果要配置多个域以使用SPNEGO，请确保每个用户的密码不同。 如果密码不同，则SPNEGO SSO不起作用。
1. 映射服务主体名称。 (请参阅 [映射服务主体名称(SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. 配置域控制器。 (请参阅 [防止Kerberos完整性检查失败](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. 添加或编辑企业域，如中所述 [添加域](/help/forms/using/admin-help/adding-domains.md#adding-domains) 或 [编辑和转换现有域](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). 创建或编辑企业域时，执行以下任务：

   * 添加或编辑包含Active Directory信息的目录。
   * 将LDAP添加为身份验证提供程序。
   * 将Kerberos添加为身份验证提供程序。 在Kerberos的“新建身份验证”或“编辑身份验证”页面上提供以下信息：

      * **身份验证提供程序：** Kerberos
      * **DNS IP：** 运行AEM表单的服务器的DNS IP地址。 您可以通过运行来确定此IP地址 `ipconfig/all` 在命令行上。
      * **KDC主机：** 用于身份验证的Active Directory服务器的完全限定主机名或IP地址
      * **服务用户：** 传递到KtPass工具的服务主体名称(SPN)。 在前面使用的示例中，服务用户是 `HTTP/lcserver.um.lc.com`.
      * **服务领域：** Active Directory域名。 在前面使用的示例中，域名是 `UM.LC.COM.`
      * **服务密码：** 服务用户的密码。 在前面使用的示例中，服务口令为 `password`.
      * **启用SPNEGO：** 允许将SPNEGO用于单点登录(SSO)。 选择此选项。

1. 配置SPNEGO客户端浏览器设置。 (请参阅 [配置SPNEGO客户端浏览器设置](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### 创建用户帐户 {#create-a-user-account}

1. 在SPNEGO中，将服务注册为域控制器上Active Directory中的用户，以表示AEM表单。 在域控制器上，转到“开始”菜单>管理工具> Active Directory用户和计算机。 如果“Administrative Tools（管理工具）”不在“Start（开始）”菜单中，请使用控制面板。
1. 单击Users文件夹以显示用户列表。
1. 右键单击用户文件夹，然后选择“新建”>“用户”。
1. 键入名字/姓氏和用户登录名，然后单击下一步。 例如，设置以下值：

   * **名字**：umspnego
   * **用户登录名**： spnegodemo

1. 键入密码。 例如，将其设置为 *密码*. 确保选中了“密码永不过期”，并且未选中其他选项。
1. 单击“下一步”，然后单击“完成”。

### 映射服务主体名称(SPN) {#map-a-service-principal-name-spn}

1. 获取KtPass实用程序。 此实用程序用于将SPN映射到REALM。 您可以将KtPass实用程序作为Windows Server工具包或资源工具包的一部分获取。 (请参阅 [Windows Server 2003 Service Pack 1支持工具](https://support.microsoft.com/kb/892777).)
1. 在命令提示符下，运行 `ktpass` 使用以下参数：

   `ktpass -princ HTTP/`*主机* `@`*领域* `-mapuser`*用户*

   例如，键入以下文本：

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   必须提供的值描述如下：

   **主机：** 表单服务器的完全限定名或任何唯一URL。 在此示例中，它被设置为lcserver.um.lc.com。

   **领域：** 域控制器的Active Directory领域。 在此示例中，它被设置为UM.LC.COM。 确保以大写字符输入领域。 要确定Windows 2003的领域，请完成以下步骤：

   * 右键单击“My Computer（我的电脑）”并选择“Properties（属性）”
   * 单击“Computer Name（计算机名称）”选项卡。 域名值是领域名称。

   **用户：** 您在上一个任务中创建的用户帐户的登录名。 在本例中，它被设置为spnegedemo。

如果您遇到此错误：

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

尝试将用户指定为spnegodemo@um.lc.com：

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### 防止Kerberos完整性检查失败 {#prevent-kerberos-integrity-check-failures}

1. 在域控制器上，转到“开始”菜单>管理工具> Active Directory用户和计算机。 如果“Administrative Tools（管理工具）”不在“Start（开始）”菜单中，请使用控制面板。
1. 单击Users文件夹以显示用户列表。
1. 右键单击在上一个任务中创建的用户帐户。 在此示例中，用户帐户为 `spnegodemo`.
1. 单击重置密码。
1. 键入并确认与之前键入的密码相同的密码。 在本例中，它被设置为 `password`.
1. 取消选择“下次登录时更改密码”，然后单击“确定”。

### 配置SPNEGO客户端浏览器设置 {#configuring-spnego-client-browser-settings}

要使基于SPNEGO的身份验证正常工作，客户端计算机必须是创建用户帐户所在的域的一部分。 您还必须将客户端浏览器配置为允许基于SPNEGO的身份验证。 此外，需要基于SPNEGO的身份验证的站点必须是受信任的站点。

如果使用计算机名(如https://lcserver:8080 )访问服务器，则Internet Explorer不需要任何设置。 如果您输入的URL不包含任何点(“。”)，Internet Explorer会将站点视为本地Intranet站点。 如果站点使用完全限定的名称，则必须将该站点添加为受信任的站点。

**配置Internet Explorer 6.x**

1. 转到“工具”>“Internet选项”，然后单击“安全”选项卡。
1. 单击“本地Intranet”图标，然后单击“站点”。
1. 单击高级，然后在将此网站添加到区域框中键入表单服务器的URL。 例如，键入 `https://lcserver.um.lc.com`
1. 单击“确定”，直到关闭所有对话框。
1. 通过访问AEM Forms服务器的URL测试配置。 例如，在浏览器URL框中，键入 `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**配置Mozilla Firefox**

1. 在浏览器URL框中，键入 `about:config`

   出现about：config - Mozilla Firefox对话框。

1. 在“筛选器”框中，键入 `negotiate`
1. 在显示的列表中，单击network.negotiate-auth.trusted-uri ，然后键入以下适合您环境的命令之一：

   `.um.lc.com` — 将Firefox配置为允许SPNEGO访问任何以um.lc.com结尾的URL。 确保包含点(“。”) 开始的时候。

   `lcserver.um.lc.com`  — 将Firefox配置为仅允许特定服务器使用SPNEGO。 此值不能以点(“。”)开头。

1. 通过访问应用程序测试配置。 此时应会显示目标应用程序的欢迎页面。
