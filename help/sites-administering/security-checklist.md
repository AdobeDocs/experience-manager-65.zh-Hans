---
title: 安全检查列表
seo-title: Security Checklist
description: 了解配置和部署AEM时的各种安全注意事项。
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: f23adcf200b625e2ab2a766460c41fd7e38fae83
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 1%

---

# 安全检查列表 {#security-checklist}

本节介绍您应采取的各种步骤，以确保AEM安装在部署时是安全的。 核对清单应自上而下应用。

>[!NOTE]
>
>此外，还提供了有关发布的最危险安全威胁的更多信息 [Open Web Application Security Project(OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>还有一些其他 [安全注意事项](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) 于开发阶段适用。

## 主要安全措施 {#main-security-measures}

### 在生产就绪模式下运行AEM {#run-aem-in-production-ready-mode}

有关更多信息，请参阅 [在生产就绪模式下运行AEM](/help/sites-administering/production-ready.md).

### 为传输层安全性启用 HTTPS {#enable-https-for-transport-layer-security}

对于具有安全实例，必须在创作实例和发布实例上启用HTTPS传输层。

>[!NOTE]
>
>请参阅 [启用HTTP Over SSL](/help/sites-administering/ssl-by-default.md) 的子菜单。

### 安装安全修补程序 {#install-security-hotfixes}

确保您已安装最新的 [由Adobe提供的安全修补程序](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans).

### 更改AEM和OSGi Console管理帐户的默认密码 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe建议在安装后更改特权用户的密码 [**AEM** `admin` 帐户](#changing-the-aem-admin-password) （在所有情况下）。

这些帐户包括：

* AEM `admin` 帐户

   更改AEM管理员帐户的密码后，在访问CRX时使用新密码。

* 的 `admin` OSGi Web控制台的密码

   此更改也会应用于用于访问Web控制台的管理员帐户，因此在访问该控制台时请使用相同的密码。

这两个帐户使用不同的凭据，并且每个帐户具有不同的强密码对于安全部署至关重要。

#### 更改AEM管理员密码 {#changing-the-aem-admin-password}

AEM管理员帐户的密码可以通过 [Granite操作 — 用户](/help/sites-administering/granite-user-group-admin.md) 控制台。

在此，您可以编辑 `admin` 帐户和 [更改密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>更改管理员帐户也会更改OSGi Web控制台帐户。 更改管理员帐户后，您应将OSGi帐户更改为其他内容。

#### 更改OSGi Web控制台密码的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了AEM `admin` 帐户，如果无法更改OSGi Web控制台密码的默认密码，则可能会导致：

* 在启动和关闭期间使用默认密码暴露服务器（对于大型服务器，这可能需要几分钟）；
* 当存储库关闭/重新启动包且OSGI正在运行时，服务器的暴露。

有关更改Web控制台密码的详细信息，请参阅 [更改OSGi Web控制台管理员密码](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下。

#### 更改OSGi Web控制台管理员密码 {#changing-the-osgi-web-console-admin-password}

更改用于访问Web控制台的密码。 使用 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 要更新 **Apache Felix OSGi管理控制台**:

* **用户名** 和 **密码**，用于访问Apache Felix Web Management Console本身的凭据。
密码必须更改 *after* 初始安装，以确保实例的安全性。

>[!NOTE]
>
>请参阅 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 有关配置OSGi设置的完整详细信息。

**更改OSGi Web控制台管理员密码**:

1. 使用 **工具**, **操作** 菜单，打开 **Web控制台** 并导航到 **配置** 中。
例如，在 `<server>:<port>/system/console/configMgr`.
1. 导航到并打开 **Apache Felix OSGi管理控制台**.
1. 更改 **用户名** 和 **密码**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 选择&#x200B;**保存**。

### 实施自定义错误处理程序 {#implement-custom-error-handler}

Adobe建议定义自定义错误处理程序页面，尤其是404和500 HTTP响应代码的页面，以防止信息泄露。

>[!NOTE]
>
>请参阅 [如何创建自定义脚本或错误处理程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) 以了解更多详细信息。

### 完整的Dispatcher安全检查列表 {#complete-dispatcher-security-checklist}

AEM Dispatcher是您基础架构的关键部分。 Adobe建议您完成 [调度程序安全检查列表](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>使用调度程序，您必须禁用“.form”选择器。

## 验证步骤 {#verification-steps}

### 配置复制和传输用户 {#configure-replication-and-transport-users}

AEM的标准安装指定 `admin` 用作默认内传输凭据的用户 [复制代理](/help/sites-deploying/replication.md). 此外，管理员用户还用于在创作系统上源复制。

出于安全考虑，应当对这两点进行更改，以反映手头的特定用例，同时考虑到以下两个方面：

* 的 **运输用户** 不得是管理员用户。 而是在发布系统上设置一个用户，该用户仅对发布系统的相关部分具有访问权限，并使用该用户的凭据进行传输。

   您可以从捆绑的复制接收器用户开始，并配置此用户的访问权限以匹配您的情况

* 的 **复制用户** 或 **代理用户Id** 也不得是管理员用户，而是只能查看已复制内容的用户。 复制用户用于在将内容发送到发布者之前收集要在创作系统上复制的内容。

### 检查操作仪表板安全运行状况检查 {#check-the-operations-dashboard-security-health-checks}

AEM 6引入了新的操作仪表板，旨在帮助系统操作员解决问题并监视实例的运行状况。

仪表板还附带一组安全运行状况检查。 建议您在生产实例上线之前检查所有安全运行状况检查的状态。 有关更多信息，请参阅 [操作功能板文档](/help/sites-administering/operations-dashboard.md).

### 检查示例内容是否存在 {#check-if-example-content-is-present}

所有示例内容和用户(例如，Geometrixx项目及其组件)都应在生产系统上完全卸载和删除，然后才能公开访问。

>[!NOTE]
>
>示例 `We.Retail` 如果此实例在中运行，则应用程序会被删除 [生产就绪模式](/help/sites-administering/production-ready.md). 如果此方案不适用，您可以卸载示例内容，方法是转到包管理器，然后搜索并卸载所有 `We.Retail` 包。

请参阅 [使用包](package-manager.md).

### 检查CRX开发包是否存在 {#check-if-the-crx-development-bundles-are-present}

应先在创作和发布生产系统上卸载这些开发OSGi包，然后再使其可以访问。

* AdobeCRXDE支持(com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer(com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### 检查Sling开发包是否存在 {#check-if-the-sling-development-bundle-is-present}

的 [AEM Developer Tools](/help/sites-developing/aem-eclipse.md) 部署Apache Sling工具支持安装(org.apache.sling.tooling.support.install)。

应在创作和发布生产系统上卸载此OSGi包，然后才能使其可访问。

### Protect防止跨站点请求伪造 {#protect-against-cross-site-request-forgery}

#### CSRF保护框架 {#the-csrf-protection-framework}

AEM 6.1附带一种有助于防止跨站点请求伪造攻击的机制，称为 **CSRF保护框架**. 有关如何使用该插件的更多信息，请参阅 [文档](/help/sites-developing/csrf-protection.md).

#### Sling反向链接过滤器 {#the-sling-referrer-filter}

要解决CRX WebDAV和Apache Sling中的跨站点请求伪造(CSRF)存在的已知安全问题，请为反向链接过滤器添加配置以使用该过滤器。

反向链接过滤器服务是一种OSGi服务，可让您配置以下内容：

* 应筛选哪些http方法
* 是否允许空反向链接标头
* 以及除服务器主机外允许的服务器列表。

   默认情况下，服务器绑定的所有本地主机和当前主机名变体都在列表中。

要配置反向链接过滤器服务，请执行以下操作：

1. 打开Apache Felix控制台(**配置**):

   `https://<server>:<port_number>/system/console/configMgr`

1. 登录方式 `admin`.
1. 在 **配置** 菜单，选择

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 字段中，输入允许作为反向链接的所有主机。 每个条目必须是格式

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允许来自此服务器的所有具有给定端口的请求。
   * 如果您还希望允许https请求，则必须输入第二行。
   * 如果允许来自该服务器的所有端口，则可以使用 `0` 作为端口号。

1. 检查 `Allow Empty` 字段中，以检查反向链接标题是否为空/缺少。

   >[!CAUTION]
   >
   >Adobe建议您在使用命令行工具(如 `cURL` 而不是允许空值，因为它可能会使您的系统遭受CSRF攻击。

1. 编辑此过滤器用于检查的方法 `Filter Methods` 字段。

1. 单击 **保存** 以保存更改。

### OSGI设置 {#osgi-settings}

默认情况下，会设置一些OSGi设置，以便更轻松地调试应用程序。 更改发布和创作生产实例中的此类设置，以避免内部信息泄露给公众。

>[!NOTE]
>
>以下所有设置( **Day CQ WCM Debug Filter（日CQ WCM调试过滤器）**，将被自动覆盖 [生产就绪模式](/help/sites-administering/production-ready.md). 因此，Adobe建议您在生产环境中部署实例之前先查看所有设置。

对于以下每项服务，必须更改指定的设置：

* [AdobeGraniteHTML库管理器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 启用 **缩小** （删除CRLF和空格字符）。
   * 启用 **Gzip** （允许使用一个请求对文件进行压缩和访问）。
   * 禁用 **调试**
   * 禁用 **计时**

* [Day CQ WCM调试过滤器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * 取消选中 **启用**

* [Day CQ WCM过滤器](/help/sites-deploying/osgi-configuration-settings.md):

   * 仅在发布时设置 **WCM模式** &quot;disabled&quot;

* [Apache Sling JavaScript处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 禁用 **生成调试信息**

* [Apache Sling JSP脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * 禁用 **生成调试信息**
   * 禁用 **映射的内容**

请参阅 [OSGi配置设置](/help/sites-deploying/osgi-configuration-settings.md).

使用AEM时，可通过多种方法来管理此类服务的配置设置；请参阅 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以了解更多详细信息和建议的实践。

## 进一步读数 {#further-readings}

### 缓解拒绝服务(DoS)攻击 {#mitigate-denial-of-service-dos-attacks}

拒绝服务 (DoS) 攻击是一种试图让计算机资源对其目标用户不可用的攻击。这种攻击通常是通过超载资源来完成的；例如：

* 来自外部源的大量请求。
* 请求的信息比系统成功交付的信息要多。

   例如，整个存储库的JSON表示形式。

* 通过请求URL数量不限的内容页面，URL可以包含句柄、一些选择器、扩展和后缀 — 其中的任意一个都可以修改。

   例如， `.../en.html` 也可以请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   所有有效的变量(例如，返回 `200` 响应和配置为缓存)，最终会导致完整文件系统，并且不提供用于进一步请求的服务。

有许多配置点可用于防止此类攻击，但此处只讨论与AEM相关的点。

**配置Sling以阻止DoS**

Sling是 *以内容为中心*. 当每个(HTTP)请求以JCR资源（存储库节点）的形式映射到内容时，处理会集中在内容上：

* 第一个目标是保存内容的资源（JCR节点）。
* 其次，渲染器或脚本位于具有请求某些部分（例如，选择器和/或扩展）的资源属性中。

请参阅 [Sling请求处理](/help/sites-developing/the-basics.md#sling-request-processing) 以了解更多信息。

这种方法使Sling功能强大且灵活，但与往常一样，必须谨慎管理灵活性。

为帮助防止DoS误用，您可以执行以下操作：

1. 在应用程序级别合并控件。 由于可能的变量数，默认配置不可行。

   在您的应用程序中，您应该：

   * 控制应用程序中的选择器，以便您 *仅* 提供所需的显式选择器并返回 `404` 为其他人。
   * 阻止输出无限数量的内容节点。

1. 检查默认渲染器的配置，这可能是一个问题区域。

   * 特别是，JSON渲染器在多个级别上转换树结构。

      例如，请求：

      `http://localhost:4502/.json`

      可以将整个存储库转储为JSON表示形式，这可能会导致严重的服务器问题。 因此，Sling会设置最大结果数的限制。 要限制JSON渲染的深度，请设置以下值：

      **JSON最大结果** ( `json.maximumresults`)

      的配置 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). 超过此限制时，呈现将折叠。 AEM中Sling的默认值为 `1000`.

   * 作为预防措施，您应禁用其他默认渲染器(HTML、纯文本、XML)。 同样，通过配置 [Apache SlingGETServlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >请勿禁用JSON渲染器，因为正常操作AEM时需要此JSON渲染器。

1. 使用防火墙过滤对实例的访问。

   * 在过滤对实例中可能导致拒绝服务攻击（如果保留不受保护）的点的访问时，必须使用操作系统级别防火墙。

**缓解使用表单选择器导致的DoS问题**

>[!NOTE]
>
>此缓解措施应仅在未使用Forms的AEM环境中执行。

因为AEM不为 `FormChooserServlet`，在查询中使用表单选择器可能会触发代价高昂的存储库遍历，通常会使AEM实例停止运行。 表单选择器可通过 **&amp;ast;.form。&amp;ast;** 字符串。

要缓解此问题，您可以执行以下步骤：

1. 通过将浏览器指向 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. 搜索 **Day CQ WCM表单选择器Servlet**
1. 单击条目后，禁用 **高级搜索要求** 在以下窗口中。

1. 单击“**保存**”。

**缓解由资产下载Servlet导致的DoS问题**

默认的资产下载Servlet允许经过身份验证的用户发出任意大的并发下载请求，以创建资产的ZIP文件。 创建大型ZIP存档可能会使服务器和网络过载。 要降低由此行为导致的潜在拒绝服务(DoS)风险， `AssetDownloadServlet` 默认情况下，OSGi组件在 [!DNL Experience Manager] 发布实例。 已启用 [!DNL Experience Manager] 默认情况下，创作实例。

如果您不需要下载功能，请在创作和发布部署中禁用Servlet。 如果您的设置要求启用资产下载功能，请参阅 [本文](/help/assets/download-assets-from-aem.md) 以了解更多信息。 此外，您还可以定义部署可支持的最大下载限制。

### 禁用WebDAV {#disable-webdav}

通过停止相应的OSGi包，在创作和发布环境中禁用WebDAV。

1. 连接到 **Felix管理控制台** 运行于：

   `https://<*host*>:<*port*>/system/console`

   例如：`http://localhost:4503/system/console/bundles`。

1. 在包列表中，找到名为的包：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 要停止此包，请在“操作”(Actions)列中单击“停止”(Stop)按钮。

1. 同样，在包列表中，找到名为的包：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 要停止此包，请单击停止按钮。

   >[!NOTE]
   >
   >无需重新启动AEM。

### 确认您未在用户主页路径中披露个人身份信息 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

务必通过确保不泄露存储库用户主页路径中的任何个人身份信息来保护您的用户。

自AEM 6.1起，用户（也称为可授权）ID节点名称的存储方式将通过 `AuthorizableNodeName` 界面。 新界面不再在节点名称中显示用户ID，而是生成一个随机名称。

不必执行任何配置即可启用它，因为现在它是在AEM中生成可授权ID的默认方式。

虽然不建议这样做，但您可以在需要旧实施以与现有应用程序进行向后兼容性时将其禁用。 要执行此操作，您必须执行以下操作：

1. 转到Web控制台，并从属性中删除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**条目 **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   您还可以通过查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** OSGi配置中的PID。

1. 删除 **Apache Jackrabbit Oak可随机授权的节点名称** 从Web控制台进行OSGi配置。

   为便于查找，此配置的PID为 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>有关更多信息，请参阅Oak文档(位于 [可授权的节点名称生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 匿名权限强化包 {#anonymous-permission-hardening-package}

默认情况下，AEM会存储系统元数据，例如 `jcr:createdBy` 或 `jcr:lastModifiedBy` 作为存储库中常规内容旁边的节点属性。 根据配置和访问控制设置，在某些情况下，这可能会导致泄露个人身份信息(PII)，例如，当此类节点呈现为原始JSON或XML时。

与所有存储库数据一样，这些属性也通过Oak授权堆栈进行中介。 应根据最少特权原则限制对他们的访问。

为支持此功能，Adobe提供了权限强化包，作为客户构建基础。 它的工作方式是在存储库根目录上安装“拒绝”访问控制条目，以限制对常用系统属性的匿名访问。 包可供下载 [此处](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) 和可以安装在所有受支持的AEM版本上。 有关详细信息，请参阅发行说明。

### 防御点击劫持攻击 {#prevent-clickjacking}

为防止Clickjacking，Adobe建议您将Web服务器配置为提供 `X-FRAME-OPTIONS` HTTP标头设置为 `SAMEORIGIN`.

有关Clickjacking的更多信息，请参阅 [OWASP站点](https://www.owasp.org/index.php/Clickjacking).

### 确保在需要时正确复制加密密钥 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些AEM功能和身份验证方案要求您在所有AEM实例中复制加密密钥。

在执行此操作之前，密钥复制在不同版本之间的操作方式不同，因为6.3和更低版本的密钥存储方式不同。

有关更多信息，请参阅下文。

#### 复制AEM 6.3的密钥 {#replicating-keys-for-aem}

而在较旧版本中，复制密钥存储在存储库中，从AEM 6.3开始，它们存储在文件系统中。

因此，要在实例之间复制密钥，请将它们从源实例复制到文件系统上目标实例的位置。

更具体地说，您必须执行以下操作：

1. 访问包含要复制的关键材料的AEM实例（通常为创作实例）；
1. 在本地文件系统中找到com.adobe.granite.crypto.file包。 例如，在以下路径下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   的 `bundle.info` 每个文件夹内的文件标识包名称。

1. 导航到数据文件夹。 例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制HMAC和主控文件。
1. 然后，转到要将HMAC密钥复制到的目标实例，然后导航到数据文件夹。 例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴您之前复制的两个文件。
1. [刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) 目标实例已在运行时。
1. 对要将密钥复制到的所有实例重复上述步骤。

>[!NOTE]
>
>您可以在首次安装AEM时通过添加以下参数，还原到6.3之前存储密钥的方法：
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### 复制AEM 6.2及更低版本的密钥 {#replicating-keys-for-aem-and-older-versions}

在AEM 6.2及更低版本中，键存储在 `/etc/key` 节点。

在实例中安全复制密钥的推荐方法是仅复制此节点。 您可以通过CRXDE Lite有选择地复制节点：

1. 打开CRXDE Lite，方法是：转到 *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. 选择 `/etc/key` 节点。
1. 转到 **复制** 选项卡。
1. 按 **复制** 按钮。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe建议您在开始生产之前对AEM基础架构进行渗透测试。

### 开发最佳实践 {#development-best-practices}

新发展必须遵循 [安全最佳实践](/help/sites-developing/security.md) 以确保AEM环境安全。
