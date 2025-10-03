---
title: 安全清单
description: 了解配置和部署 AEM 时的各种安全注意事项。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: ht
source-wordcount: '2959'
ht-degree: 100%

---

# 安全清单 {#security-checklist}

本节介绍部署后确保 AEM 安装的安全性所需采取的各项步骤。建议按清单自上而下逐项执行。

>[!NOTE]
>
>您还可参考[开放 Web 应用程序安全项目（OWASP）](https://owasp.org/www-project-top-ten/)发布的最严重安全威胁，以获取更多信息。

>[!NOTE]
>
>在开发阶段，还适用一些其他[安全注意事项](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)。

## 主要安全措施 {#main-security-measures}

### 以生产就绪模式运行 AEM {#run-aem-in-production-ready-mode}

有关更多信息，请参阅[以生产就绪模式运行 AEM](/help/sites-administering/production-ready.md)。

### 为传输层安全性启用 HTTPS {#enable-https-for-transport-layer-security}

必须在创作与发布实例上启用 HTTPS 传输层，方可保障实例的安全性。

>[!NOTE]
>
>请参阅[启用基于 SSL 的 HTTP](/help/sites-administering/ssl-by-default.md) 部分，以了解更多信息。

### 安装安全热修复补丁 {#install-security-hotfixes}

请确认已安装 [Adobe 提供的最新的安全热修复补丁](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=zh-Hans)。

### 更改 AEM 与 OSGi 控制台管理员帐户的默认密码 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobe 建议在安装完成后（适用于所有实例）更改具有特权的 [**AEM** `admin` 帐户](#changing-the-aem-admin-password)的密码。

这些帐户包括：

* AEM 的 `admin` 帐户

  更改 AEM 管理员帐户密码后，访问 CRX 时请使用新密码。

* OSGi 网页控制台的 `admin` 密码

  此更改同样适用于访问网页控制台的管理员帐户，请使用相同的新密码进行访问。

这两个帐户的凭据相互独立。为每个帐户设置不同且强度高的密码，对保障部署安全至关重要。

#### 更改 AEM 管理员密码 {#changing-the-aem-admin-password}

可通过 [Granite 操作——用户](/help/sites-administering/granite-user-group-admin.md)控制台更改 AEM 管理员帐户的密码。

在此可编辑 `admin` 帐户并[更改其密码](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)。

>[!NOTE]
>
>更改该管理员帐户同时会影响 OSGi 网页控制台的帐户。在更改管理员帐户后，建议将 OSGi 帐户的凭据进一步修改为与之不同的密码。

#### 更改 OSGi 网页控制台密码的重要性 {#importance-of-changing-the-osgi-web-console-password}

除了 AEM 的 `admin` 帐户外，如未更改 OSGi 网页控制台的默认密码，可能会导致：

* 服务器在启动与关闭期间（大型服务器可能持续数分钟）因使用了默认密码而暴露。
* 当存储库宕机/重新启动捆绑包而 OSGi 仍在运行时，服务器处于暴露状态。

关于更改网页控制台密码的详细信息，请参见下文[更改 OSGi 网页控制台管理员密码](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)。

#### 更改 OSGi 网页控制台管理员密码 {#changing-the-osgi-web-console-admin-password}

请更改用于访问网页控制台的密码。通过 [OSGi 配置](/help/sites-deploying/configuring-osgi.md)来更新 **Apache Felix OSGi 管理控制台**&#x200B;的以下属性：

* **用户名**&#x200B;和&#x200B;**密码**：用于访问 Apache Felix Web 管理控制台的凭据。为确保实例安全，必须在初始安装&#x200B;*之后*&#x200B;更改该密码。

>[!NOTE]
>
>有关配置 OSGi 设置的完整说明，请参见 [OSGi 配置](/help/sites-deploying/configuring-osgi.md)。

**更改 OSGi 网页控制台管理员密码的步骤**：

1. 在&#x200B;**工具**、**操作**&#x200B;菜单中，打开&#x200B;**网页控制台**，进入&#x200B;**配置**部分。
例如：`<server>:<port>/system/console/configMgr`。
1. 找到并打开 **Apache Felix OSGi 管理控制台**&#x200B;的条目。
1. 更改&#x200B;**用户名**&#x200B;和&#x200B;**密码**。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 选择&#x200B;**保存**。

### 实施自定义错误处理程序 {#implement-custom-error-handler}

Adobe 建议定义自定义错误处理页，特别是针对 404 与 500 等 HTTP 响应码，以防止敏感信息泄露。

>[!NOTE]
>
>请参阅[如何创建自定义脚本或错误处理程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=zh-Hans)，以了解更多详细信息。

### 完成 Dispatcher 安全清单 {#complete-dispatcher-security-checklist}

AEM Dispatcher 是您基础架构中的关键组件。Adobe 建议完成 [Dispatcher 安全清单](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=zh-Hans)。

>[!CAUTION]
>
>使用 Dispatcher 时，必须禁用 “.form” 选择器。

## 验证步骤 {#verification-steps}

### 配置复制与传输用户 {#configure-replication-and-transport-users}

在 AEM 标准安装流程中，默认[复制代理](/help/sites-deploying/replication.md)会将 `admin` 作为传输凭据的用户。此外，创作系统上用于发起复制的用户也通常是 admin。

基于安全考虑，应根据实际使用场景更换上述帐户，并注意以下两点：

* **传输用户**&#x200B;不得为管理员帐户。建议在发布系统上创建仅具备相应区域访问权限的用户，并使用该用户的凭据进行传输。

  您可从随附的 replication-receiver 用户着手，按需配置该用户的访问权限。

* **复制用户**&#x200B;或&#x200B;**代理用户 ID** 同样不能为管理员帐户，而是应为仅能查看复制内容的用户。复制用户用于在创作系统上收集待复制内容，然后再发送至发布者。

### 检查操作仪表板的安全健康检查 {#check-the-operations-dashboard-security-health-checks}

AEM 6 引入了全新的操作仪表板，以帮助运维人员排障并监控实例健康状况。

该仪表板包含一系列安全健康检查。建议在生产实例上线前，检查所有安全健康检查的状态。如需了解更多信息，请参阅[操作仪表板文档](/help/sites-administering/operations-dashboard.md)。

### 检查示例内容是否仍存在 {#check-if-example-content-is-present}

在对外开放前，应在生产系统上彻底卸载并删除所有示例内容与示例用户（如 Geometrixx 项目及其组件）。

>[!NOTE]
>
>若实例以[生产就绪模式](/help/sites-administering/production-ready.md)运行，示例 `We.Retail` 应用程序会移除。如非上述情况，可以在包管理器中搜索并卸载所有 `We.Retail` 包以移除示例内容。

请参阅[使用包](package-manager.md)。

### 检查是否存在 CRX 开发用捆绑包 {#check-if-the-crx-development-bundles-are-present}

在对外开放前，应在创作与发布生产系统上卸载以下开发用 OSGi 捆绑包：

* Adobe CRXDE Support（com.adobe.granite.crxde-support）
* Adobe Granite CRX Explorer（com.adobe.granite.crx-explorer）
* Adobe Granite CRXDE Lite（com.adobe.granite.crxde-lite）

### 检查是否存在 Sling 开发用捆绑包 {#check-if-the-sling-development-bundle-is-present}

[AEM 开发人员工具](/help/sites-developing/aem-eclipse.md)会部署 Apache Sling Tooling Support Install（org.apache.sling.tooling.support.install）。

在对外开放前，应在创作与发布生产系统上卸载该 OSGi 捆绑包。

### 防止出现跨站点请求伪造 {#protect-against-cross-site-request-forgery}

#### CSRF 保护框架 {#the-csrf-protection-framework}

自 AEM 6.1 起，系统内置名为 **CSRF 防护框架**&#x200B;的机制，用于抵御跨站点请求伪造攻击。有关使用方法的更多信息，请参加[相关文档](/help/sites-developing/csrf-protection.md)。

#### Sling 反向链接过滤器 {#the-sling-referrer-filter}

为解决 CRX WebDAV 和 Apache Sling 中已知的跨站点请求伪造（CSRF）安全问题，需要配置以启用反向链接过滤器。

反向链接过滤器服务是一个 OSGi 服务，该服务允许您配置以下内容：

* 需要被过滤的 HTTP 方法
* 是否允许空的反向链接头
* 以及除当前服务器主机外允许的服务器列表。

  默认情况下，所有 localhost 的变体以及服务器绑定的当前主机名均在允许列表中。

要配置反向链接过滤器服务：

1. 在以下地址打开 Apache Felix 控制台（**配置**）：

   `https://<server>:<port_number>/system/console/configMgr`

1. 以 `admin` 身份登录。
1. 在&#x200B;**配置**&#x200B;菜单中选择：

   `Apache Sling Referrer Filter`

1. 在 `Allow Hosts` 字段中输入所有允许作为反向链接的主机。每个条目必须采用以下格式：

   &lt;protocol>://&lt;server>:&lt;port>

   例如：

   * `https://allowed.server:80` 允许来自该服务器指定端口的所有请求。
   * 若还需允许 https 请求，必须另起一行单独输入。
   * 若要允许该服务器的所有端口，可以使用 `0` 作为端口号。

1. 如需允许空的或缺失的反向链接头，请勾选 `Allow Empty` 字段。

   >[!CAUTION]
   >
   >Adobe 建议在使用 `cURL` 等命令行工具时提供反向链接，而非允许空值，否则可能使系统暴露于 CSRF 攻击风险中。

1. 在 `Filter Methods` 字段中编辑过滤器用于检查的方法。

1. 单击&#x200B;**保存**&#x200B;以保存更改。

### OSGI 设置 {#osgi-settings}

某些 OSGi 设置默认启用，以便于对应用程序进行调试。在发布与创作生产实例上应修改这些设置，以避免内部信息泄露。

>[!NOTE]
>
>除 **Day CQ WCM 调试筛选条件**&#x200B;外，下列所有设置均已由[生产就绪模式](/help/sites-administering/production-ready.md)自动覆盖。因此，Adobe 建议在生产环境部署实例之前，检查所有相关设置。

对于以下每项服务，都必须更改指定的设置：

* [Adobe Granite HTML 库管理器](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager)：

   * 启用&#x200B;**缩小**（移除 CRLF 和空白字符）。
   * 启用 **Gzip**（允许文件压缩并通过单个请求访问）。
   * 禁用&#x200B;**调试**
   * 禁用&#x200B;**计时**

* [Day CQ WCM 调试筛选条件](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 取消选中&#x200B;**启用**

* [Day CQ WCM 筛选条件](/help/sites-deploying/osgi-configuration-settings.md)：

   * 在发布实例上，将 **WCM 模式**&#x200B;设置为“已禁用”

* [Apache Sling JavaScript 处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler)：

   * 禁用&#x200B;**生成调试信息**

* [Apache Sling JSP 脚本处理程序](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * 禁用&#x200B;**生成调试信息**
   * 禁用&#x200B;**映射内容**

请参阅 [OSGi 配置设置](/help/sites-deploying/osgi-configuration-settings.md)。

在使用 AEM 时，可通过多种方式管理这些服务的配置设置。有关更多详情与最佳做法，请参阅[配置 OSGi](/help/sites-deploying/configuring-osgi.md)。

## 进一步阅读 {#further-readings}

### 缓解拒绝服务（DoS）攻击 {#mitigate-denial-of-service-dos-attacks}

拒绝服务（DoS）攻击是指试图使计算机资源对预期用户不可用的行为。此类攻击通常通过资源过载来实现，例如：

* 来自外部源的请求洪流。
* 请求超出系统可正常提供的信息量。

  例如，请求整个存储库的 JSON 展现方案。

* 通过请求一个包含无限数量 URL 的内容页面，URL 可以包含一个句柄、一些选择器、一个扩展名和一个后缀，其中任何一项都可以进行修改。

  例如，`.../en.html` 可被请求为：

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  所有有效变体（例如返回 `200` 响应并配置为可缓存）都会被 Dispatcher 缓存，最终可能导致文件系统被填满，从而无法处理进一步请求。

防止此类攻击的配置点很多，这里仅讨论与 AEM 相关的部分。

**配置 Sling 以防止 DoS 攻击**

Sling 采用&#x200B;*以内容为中心*&#x200B;的框架。每个 HTTP 请求都会以 JCR 资源（存储库节点）的形式映射到内容上，因此处理流程会围绕内容展开：

* 首个目标是存放内容的资源（JCR 节点）。
* 其次，系统会根据请求的部分内容（如选择器和/或扩展名）以及资源属性定位渲染器或脚本。

请参阅 [Sling 请求处理](/help/sites-developing/the-basics.md#sling-request-processing)，以了解更多信息。

这种方式使 Sling 功能强大且灵活，但必须谨慎管理这种灵活性。

为防止滥用 DoS，可采取以下措施：

1. 在应用程序层面引入控制。由于可能存在大量变体，默认配置不可行。

   在应用程序中应当：

   * 控制应用程序中的选择器，*仅*&#x200B;提供明确需要的选择器，并对其他选择器一律返回 `404`。
   * 防止输出无限数量的内容节点。

1. 检查默认渲染器的配置，因为它们可能成为问题来源。

   * 尤其是 JSON 渲染器会跨多个层级遍历树结构。

     例如，该请求：

     `http://localhost:4502/.json`

     可能将整个存储库导出为 JSON 展现方案，从而引发严重的服务器问题。因此，Sling 对最大结果数设有限制。要限制 JSON 渲染的深度，请为以下属性设置值：

     **JSON 最大结果数**（`json.maximumresults`）

     位于 [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet) 的配置中。超过该限制时，渲染会被中止。AEM 中 Sling 的默认值为 `1000`。

   * 作为预防措施，应禁用其他默认渲染器（HTML、纯文本、XML）。同样通过配置[Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet) 实现。

   >[!CAUTION]
   >
   >请勿禁用 JSON 渲染器，因为 AEM 的正常运行依赖于它。

1. 使用防火墙来过滤对实例的访问。

   * 必须使用操作系统级别的防火墙来过滤对实例中各点的访问，因为如果不加以保护，这些访问可能会导致拒绝服务攻击。

**缓解因使用表单选择器引发的 DoS 攻击**

>[!NOTE]
>
>仅当 AEM 环境未使用 Forms 时，才应执行此缓解措施。

由于 AEM 并未为 `FormChooserServlet` 提供开箱即用的索引，在查询中使用表单选择器可能会触发代价高昂的存储库遍历，而这通常会导致 AEM 实例停滞。表单选择器可通过查询是否存在 **&amp;ast;.form.&amp;ast;** 字符串来识别。

要缓解此问题，可以执行以下步骤：

1. 通过在浏览器中访问 *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* 来打开网页控制台

1. 搜索 **Day CQ WCM 表单选择器 Servlet**
1. 点击该条目后，在以下窗口中禁用&#x200B;**高级搜索要求**。

1. 单击&#x200B;**保存**。

**缓解因资产下载 Servlet 引发的 DoS 攻击**

默认的资产下载 Servlet 允许已验证的用户发起任意规模的并发下载请求，以创建资产的 ZIP 文件。生成大型 ZIP 压缩包可能会导致服务器与网络过载。为降低此行为带来的潜在的拒绝服务（DoS）风险，[!DNL Experience Manager] 的发布实例默认禁用 `AssetDownloadServlet` OSGi 组件。但在 [!DNL Experience Manager] 作者实例上则默认启用。

若无需下载功能，请在创作与发布部署中均禁用该 Servlet。如果您的环境必须启用资产下载功能，请参见[从 Adobe Experience Manager 下载资产](/help/assets/download-assets-from-aem.md)，以获取更多信息。此外，您还可以为部署定义可承受的最大下载限制。

### 禁用 WebDAV {#disable-webdav}

可在创作与发布环境中停止相关 OSGi 捆绑包来禁用 WebDAV。

1. 连接到正在以下位置运行的 **Felix 管理控制台**：

   `https://<*host*>:<*port*>/system/console`

   例如 `http://localhost:4503/system/console/bundles`。

1. 在捆绑包列表中找到以下名称的捆绑包：

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. 在“操作”列中点击“停止”按钮即可停止该捆绑包。

1. 同样，在捆绑包列表中找到以下名称的捆绑包：

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 点击“停止”按钮停止该捆绑包。

   >[!NOTE]
   >
   >无需重启 AEM。

### 确认您未在用户主路径中泄露个人身份信息 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

确保存储库用户主路径中不会暴露任何个人身份信息，这是保护用户的重要措施。

自 AEM 6.1 起，用户（即可授权）ID 节点名称的存储方式已通过新的 `AuthorizableNodeName` 接口实施。该新接口不再在节点名中暴露用户 ID，而是生成随机名称。

无需额外配置，因为该方式已成为 AEM 生成可授权 ID 的默认方式。

尽管不推荐，但如需与现有应用程序保持向后兼容，可禁用该功能以恢复旧的实施。如需禁用，请执行以下操作：

1. 进入网页控制台，在 **Apache Jackrabbit Oak SecurityProvider** 中的 **requiredServicePids** 属性里移除** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** 条目。

   您也可在 OSGi 配置中查找 **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID 来定位 Oak 安全提供商。

1. 在网页控制台中删除 **Apache Jackrabbit Oak 随机可授权节点名称** OSGi 配置。

   为方便查找，该配置的 PID 为 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**。

>[!NOTE]
>
>若要了解更多信息，请参阅 Oak 文档[生成可授权节点名称](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)。

### 匿名权限强化包 {#anonymous-permission-hardening-package}

默认情况下，AEM 会将系统元数据（如 `jcr:createdBy` 或 `jcr:lastModifiedBy`）作为节点属性与常规内容一并存储在存储库中。根据配置与访问控制设置的不同，在某些情况下这可能会导致个人身份信息（PII）暴露，例如当此类节点以原始 JSON 或 XML 形式渲染时。

与所有存储库数据一样，这些属性由 Oak 授权栈介导。应遵循最小权限原则限制对这些属性的访问。

为此，Adobe 提供了一个权限强化包，供客户在此基础上进一步扩展。该强化包通过在存储库根目录安装一条“拒绝”访问控制项，限制匿名用户访问常用系统属性。此包可在所有受支持的 AEM 版本中[下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip)并安装。

为说明这些变化，以下对比展示了安装该包前后匿名用户可查看的节点属性：

![安装包之前](/help/sites-administering/assets/before_resized.png)

以及安装包后可查看的属性，其中 `jcr:createdBy` 和 `jcr:lastModifiedBy` 已不可见：

![安装包之后](/help/sites-administering/assets/after_resized.png)

有关更多信息，请参阅该包的发行说明。

### 防御点击劫持攻击 {#prevent-clickjacking}

若要防御点击劫持攻击，Adobe 建议您将 Web 服务器配置为将 `X-FRAME-OPTIONS` HTTP 标头集提供给 `SAMEORIGIN`。

有关点击劫持攻击的更多信息，请参阅 [OWASP 网站](https://www.owasp.org/index.php/Clickjacking)。

### 确保在需要时正确复制加密密钥 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

某些 AEM 功能与身份验证机制要求在所有 AEM 实例间复制加密密钥。

在执行之前请注意，不同版本的密钥复制方式不同，因为 6.3 与更早版本存储密钥的方式不同。

有关详细信息，请参阅下文。

#### 在 AEM 6.3 中复制密钥 {#replicating-keys-for-aem}

在早期版本中，复制密钥存储在存储库中；而从 AEM 6.3 起，密钥存储在文件系统中。

因此，要在实例间复制密钥，需要将其从源实例复制到目标实例文件系统中的相应位置。

具体步骤如下：

1. 访问包含要复制的密钥材料的 AEM 实例（通常是作者实例）；
1. 在本地文件系统中找到 com.adobe.granite.crypto.file 捆绑包。例如，路径如下：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   每个文件夹内的 `bundle.info` 文件标识了对应的捆绑包名称。

1. 进入数据文件夹。例如：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 复制 HMAC 与主文件。
1. 随后进入要复制 HMAC 密钥的目标实例，并导航到数据文件夹。例如：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 粘贴先前复制的两个文件。
1. 如果目标实例已在运行，请[刷新加密包](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)。
1. 对所有需要复制密钥的实例重复上述步骤。

#### 在 AEM 6.2 及更早版本中复制密钥 {#replicating-keys-for-aem-and-older-versions}

在 AEM 6.2 及更早版本中，密钥存储于存储库的 `/etc/key` 节点下。

推荐的安全做法是仅复制该节点，以在实例间复制密钥。您可以通过 CRXDE Lite 有选择地复制节点：

1. 通过访问 *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`* 来打开 CRXDE Lite
1. 选择 `/etc/key` 节点。
1. 切换到&#x200B;**复制**&#x200B;选项卡。
1. 点击&#x200B;**复制**&#x200B;按钮。

### 执行渗透测试 {#perform-a-penetration-test}

Adobe 建议在进入生产环境前对您的 AEM 基础架构执行渗透测试。

### 开发最佳做法 {#development-best-practices}

新开发的项目必须遵循[安全性最佳做法](/help/sites-developing/security.md)，以确保 AEM 环境的安全性。
