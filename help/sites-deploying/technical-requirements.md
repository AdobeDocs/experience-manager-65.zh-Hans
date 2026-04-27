---
title: 技术要求
description: Adobe Experience Manager支持的客户端和服务器平台列表。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: f2c92b990a5c09cbcf532e0800e264620d98af77
workflow-type: tm+mt
source-wordcount: '3736'
ht-degree: 6%

---

# 技术要求{#technical-requirements}

Adobe支持平台上的(AEM) Adobe Experience Manager，如本文档中的以下信息所述。

有关与平台相关的任何问题，请联系平台供应商。

>[!NOTE]
>
>根据安装AEM的平台，可能会为用户管理提出不同的要求。

## 先决条件 {#prerequisites}

安装Adobe Experience Manager的最低要求：

* 已安装Java™ Platform、Standard Edition JDK或其他支持的[Java™虚拟机](#java-virtual-machines)
* Experience Manager快速入门文件（独立JAR或Web应用程序部署WAR）

### 最低大小要求 {#minimum-sizing-requirements}

运行Adobe Experience Manager的最低要求：

* 安装目录中的5 GB可用磁盘空间
* 2 GB内存

>[!NOTE]
>
>* 数字资产用例需要更多基本内存。 有关详细信息，请参阅[部署和维护](/help/sites-deploying/deploy.md#default-local-install)。
>* [AEM Forms附加组件包](/help/forms/using/installing-configuring-aem-forms-osgi.md)需要15 GB的临时空间。
>

有关详细信息，请参阅[硬件大小调整指南](/help/managing/hardware-sizing-guidelines.md)。

### 支持级别 {#support-levels}

本文档列出了Adobe Experience Manager支持的客户端和服务器平台。 Adobe为推荐配置和其他配置提供了多个级别的支持。

### 支持的配置 {#supported-configurations}

Adobe建议进行这些配置，并在标准软件维护协议中提供全面支持。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>A：受到支持</strong></td>
   <td>Adobe 为此配置提供全面的支持和维护。 此配置包含在 Adobe 质量保证流程中。</td>
  </tr>
  <tr>
   <td><strong>R：有限的支持</strong></td>
   <td>为了确保客户项目成功，Adobe在受限制的支持计划内提供了全面支持，该计划要求满足特定条件。 r级支持需要正式的客户请求和Adobe的确认。 有关详细信息，请联系 Adobe 客户关怀团队。</td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z：不支持** | 此配置不受支持。 Adobe 未做出此配置是否有效的声明，也不支持此配置。 |

## 支持的平台 {#supported-platforms}

### Java™虚拟机 {#java-virtual-machines}

应用程序需要由Java™开发工具包(JDK)分发提供的Java™虚拟机才能运行。

Adobe Experience Manager与以下版本的Java™虚拟机一起运行：

>[!CAUTION]
>
>跟踪Java™供应商的安全公告。 这样做确保了生产环境的安全与保障。 此外，请始终安装最新的Java™更新。

| **平台** | **支持级别** | **链接** |
|---|---|---|
| Oracle Java™ SE 21 JDK | Z：不支持`[1]` |  |
| Oracle Java™ SE 17 JDK | Z：不支持`[1]` |  |
| Oracle Java™ SE 11 JDK - 64位 | A：支持的`[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=24<td>) |
| Oracle Java™ SE 10 JDK | Z：不支持`[1]` |  |
| Oracle Java™ SE 9 JDK | Z：不支持`[1]` |  |
| Oracle Java™ SE 8 JDK - 64位 | A：支持的`[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=10) |
| ® J9虚拟机 — 内部版本2.9，JRE 1.8.0 | A：支持的`[2]` |  |
| ® J9虚拟机 — 内部版本2.8、JRE 1.8.0 | A：支持的`[2]` |  |
| Azul Zulu OpenJDK 11 - 64位 | A：支持的`[3]` | |
| Azul Zulu OpenJDK 8 - 64位 | A：支持的`[3]` | |

1. Oracle已针对Oracle Java™ SE产品改用“长期支持”(LTS)模型。 Java™ 9、Java™ 10和Java™ 12是Oracle的非LTS版本（请参阅[Oracle Java™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html)）。 要在生产环境中部署AEM，Adobe仅对Java™的LTS版本提供支持。 Adobe直接为所有使用Oracle Java™ SE技术的AEM客户支持和分发Oracle Java™ SE JDK，包括LTS版本的所有维护更新。 请参阅适用于Adobe Experience Manager[&#128279;](assets/Java_Policy_for_Adobe_Experience_Manager.pdf)的Java™支持策略。
   **重要信息： [Oracle 6.5 LTS](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-65-lts/content/implementing/deploying/introduction/technical-requirements)支持AEM Java™ 17和21。**

1. ® JRE仅与WebSphere®应用程序服务器一起受支持。

1. 从版本6.5 SP9开始，本地AEM部署支持Azul Zulu OpenJDK LTS版本。 Azul Zulu JDK LTS版本的支持和分发必须由Adobe客户直接从Azul授予许可。


### 存储和持久性 {#storage-persistence}

可以使用各种选项来部署Adobe Experience Manager存储库。 请参阅下面的列表，以了解受支持的技术和存储选项。

| **平台** | **描述** | **支持级别** |
|---|---|---|
| **带有TAR文件的文件系统** `[1]` | 存储库 | A：受到支持 |
| **具有数据存储的文件系统** `[1]` | 二进制文件 | A：受到支持 |
| 在文件系统`[1]`的TAR文件中存储二进制文件 | 二进制文件 | Z：不支持生产 |
| Amazon S3 | 二进制文件 | A：受到支持 |
| ® Azure Blob Storage | 二进制文件 | A：受到支持 |
| MongoDB 企业版 8.0 | 存储库 | A：支持的`[3, 4]` |
| MongoDB 企业版 7.0 | 存储库 | A：支持的`[3, 4]` |
| MongoDB 企业版 6.0 | 存储库 | A：支持的`[3, 4]` |
| MongoDB 企业版 5.0 | 存储库 | A：支持的`[3, 4]` |
| MongoDB 企业版 4.4 | 存储库 | A：支持的`[2, 3, 4, 7]` |
| MongoDB 企业版 4.2 | 存储库 | A：支持的`[2, 3, 4, 7]` |
| MongoDB 企业版 4.0 | 存储库 | Z：不支持 |
| MongoDB 企业版 3.6 | 存储库 | Z：不支持 |
| MongoDB 企业版 3.4 | 存储库 | Z：不支持 |
| ® DB2® 10.5 | 存储库和Forms数据库 | R: Restricted Support `[5]` |
| Oracle Database 12c (12.1.x) | 存储库和Forms数据库 | R：有限的支持 |
| Oracle Database 19c | 存储库和Forms数据库 | R：有限的支持 |
| Microsoft® SQL 服务器 2016 | Forms Database | A：受到支持 |
| Microsoft® SQL Server 2019 (Deprecated) | Forms Database | A：受到支持 |
| Microsoft® SQL 服务器 2022 | Forms Database | A：受到支持 |
| **Apache Lucene (Quickstart built-in)** | Search Service | A：受到支持 |
| Apache Solr | Search Service | A：受到支持 |

1. &#39;File System&#39; includes block storage that is POSIX-compliant. Includes network storage technology. Mind that file system performance might vary and influences the overall performance. Load test AEM with the network/remote file system.
2. MongoDB Enterprise versions 4.2 and 4.4 require AEM 6.5 SP9 as a minimum.
3. MongoDB Sharding is not supported in AEM.
4. MongoDB Storage Engine WiredTiger is supported only.
5. Supported for AEM Forms upgrade customers. Not supported for new installations.
6. Applicable to AEM Forms only:
   * Removed support for Oracle Database 12c and added support for Oracle Database 19c.
   * Removed support for Microsoft® SQL Server 2016 and added support for Microsoft® SQL Server 2019 and Microsoft® SQL Server 2022.

>[!NOTE]
>
>有关AEM Communities功能的详细信息，请参阅[部署社区](/help/communities/deploy-communities.md)。

>[!NOTE]
>
>MongoDB是第三方软件程序，未包含在AEM许可包中。 有关详细信息，请参阅[MongoDB许可策略](https://www.mongodb.com/licensing/server-side-public-license/faq)页。
>
>为了利用MongoDB充分利用AEM部署，Adobe建议许可MongoDB企业版以受益于专业支持。 有关详细信息，请参阅[建议的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)。
>
>该许可证包括一个标准副本集，该副本集由一个主实例和两个辅助实例组成，可用于创作或发布部署。
>
>如果要在MongoDB上同时运行author和publish，则必须购买两个单独的许可证。
>
>Adobe客户关怀团队协助处理与将MongoDB用于AEM相关的资格确认问题。
>
>有关详细信息，请参阅[Adobe Experience Manager的MongoDB页面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。

<!--
>[!NOTE]
>
>Supported relational databases as listed above are third-party software and are not included in the AEM licensing package.
>
>To run AEM 6.5 with a supported relational database, a separate support contract with a database vendor is required. Adobe Customer Care assists qualifying issues related to the usage of relational databases with AEM 6.5.
>
>**Most relational databases are currently supported within Level-R on AEM 6.5, which comes with support criteria and a support program as stated in the Level-R description above.**
-->

### Servlet引擎/应用程序服务器 {#servlet-engines-application-servers}

Adobe Experience Manager可以作为独立服务器（快速入门JAR文件）运行，也可以作为第三方应用程序服务器中的Web应用程序（WAR文件）运行。

需要的最低Servlet API版本是Servlet 3.1

| 平台 | 支持级别 |
|---|---|
| **快速入门内置Servlet引擎(Jetty 9.4)** | A：受到支持 |
| Oracle WebLogic Server 12.2 (12cR2) | Z：不支持 |
| ® WebSphere® Application Server Continuous Delivery (LibertyProfile) with Web Profile 7.0和IBM® JRE 1.8 | R：对新合同的支持受限`[2]` |
| ® WebSphere® Application Server 9.0和IBM® JRE 1.8 | R：对新合同的支持受限`[1]` `[2]` |
| ® WebSphere®应用程序服务器9.0.0.10 | R：对新合同的支持受限`[1]` `[2]` |
| Apache Tomcat 8.5.x | R：对新合同的支持受限`[2]` |
| JBoss® EAP 7.2.x带JBoss®应用程序服务器 | Z：不支持 |
| JBoss® EAP 7.1.4带JBoss®应用程序服务器 | R：对新合同的支持受限`[1]` `[2]` |
| JBoss® EAP 7.0.x带JBoss®应用程序服务器 | Z：不支持 |
| JBoss® EAP 7.4与JBoss®应用程序服务器<sup>[2] [3] [7] | A：受到支持 |

1. 建议使用AEM Forms进行部署。
2. 在应用程序服务器中启动AEM 6.5部署后，将转为有限支持。 现有客户可以升级到AEM 6.5并继续使用应用程序服务器。 对于新客户，它附带支持标准和支持计划，如上面的R级描述中所述。
3. 仅适用于AEM Forms：
   * 移除了对JBoss® EAP 7.1.4的支持，并添加了对JBoss® EAP 7.4.10的支持。

### 服务器操作系统 {#server-operating-systems}

Adobe Experience Manager可与以下服务器平台配合使用以用于生产环境：

| **平台** | **支持级别** |
|---|---|
| **Linux®，基于Red Hat®分发** | A：支持的`[1]` `[3]` |
| Linux®，基于Debian分布，包括 乌班图 | A：支持的`[1]` `[2]` |
| Linux®，基于SUSE®分发 | A：支持的`[1]` |
| Microsoft® Windows Server 2022 | R：有限的支持 |
| ® Windows Server 2019 `[4]`（已弃用） | R：对新合同的支持受限`[5]` |
| ® Windows Server 2016 `[4]` | R：对新合同的支持受限`[5]` |
| ® Windows Server 2012 R2 | Z：不支持 |
| Oracle Solaris™ 11 | Z：不支持 |
| ® AIX® 7.2 | Z：不支持 |

1. Linux®内核2.6、3。 x， 4. x， 5。 x， 6. x和9。 x包括来自Red Hat® Distribution的派生程序，包括Red Hat® Enterprise Linux®、Oracle Linux®和Amazon Linux®。 只有Red Hat® Enterprise Linux® 8和Red Hat® Enterprise Linux® 9支持AEM Forms附加功能。
2. AEM Forms在Ubuntu 20.04和SUSE® Linux® Enterprise Server 15 SP6（64位）上受支持。
3. Adobe Managed Services支持的Linux®分发。

   >[!NOTE]
   >
   >对于基于Linux的服务器（OSGI和JEE栈栈），AEM Forms加载项需要运行时依赖关系，例如：
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 (1.6.7-4)
   >* zlib.x86-64 (1.2.7-17)
   >* libxcb.x86_64 (1.13-1.el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64（2.17或更高版本）
   >* OpenSSL 3（操作系统上的默认位置需要）。

   *对于OpenSSL 3安装：库libcrypto.so.3和libssl.so.3必须在LD_LIBRARY_PATH环境变量表示的默认库路径中可用。 如果它们安装在非标准位置，请确保在启动服务器之前将此路径添加到LD_LIBRARY_PATH。*

4. ® Windows生产部署支持升级到6.5的客户和非生产使用。 AEM Sites和Assets会应请求进行新部署。
5. ® Window Server上支持AEM Forms，但没有支持级别R限制。
6. AEM Forms移除了对Microsoft® Windows Server 2016的支持。

>[!NOTE]
>
>如果要安装AEM Forms 6.5，请确保已安装了以下32位Microsoft® Visual C++可再发行版本。
>
>* ® Visual C++ 2008可再分发
>* ® Visual C++ 2010可再分发
>* ® Visual C++ 2012可再分发
>* ® Visual C++ 2013可再分发
>* ® Visual C++ 2019（VC14.28或更高版本）可再分发

### 虚拟和云计算环境 {#virtual-cloud-computing-environments}

支持在云计算环境中的虚拟机中运行Adobe Experience Manager。 这些环境包括®Azure和Amazon Web Services (AWS)，其运行符合本页列出的技术要求并符合Adobe的标准支持条款。

对于云原生环境，请查看AEM产品线中的最新产品：Adobe Experience Manager as a Cloud Service 。 有关详细信息，请参阅[Adobe Experience Manager as a Cloud Service文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=zh-Hans)。

Adobe还提供Adobe Managed Services功能，以便在Azure或AWS上部署AEM。 Adobe Managed Services为专家提供了在这些云计算环境中部署和操作AEM的经验和技能。 请参阅[有关Adobe Managed Services的其他文档](https://business.adobe.com/cn/products/experience-manager/managed-services.html?aemClk=t)。

在Azure、AWS或任何其他云计算环境中部署AEM的所有其他情况下，虚拟计算环境会包含来自Adobe的支持。 该虚拟环境必须按照本页中列出的技术规范运行。 任何与在任何这些云环境中运行的AEM相关的已报告问题，都必须可独立于任何特定于云计算环境的云服务进行重现。 也就是说，除非本页面上列出的技术要求（例如Azure Blob Storage或AWS S3）支持Cloud Service。

有关如何在Adobe Managed Services之外的Azure或AWS上部署AEM的建议，Adobe建议直接与云提供商合作。 或者，与Adobe合作伙伴合作，为您选择的云环境中部署AEM提供支持。 The selected cloud provider or partner is responsible for the sizing specifications, design, and implementation of the architecture, to meet your specific performance, load, scalability, and security requirements.

### Dispatcher Platforms (Web Servers) {#dispatcher-platforms-web-servers}

The Dispatcher is the caching and load-balancing component. [Download the latest Dispatcher version](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=zh-Hans). Experience Manager 6.5 requires Dispatcher version 4.3.2 or higher.

The following web servers are supported for use with Dispatcher version 4.3.2:

| 平台 | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A：受到支持 |
| Microsoft® IIS 10 (Internet Information Server) | A：受到支持 |
| Microsoft® IIS 8.5 (Internet Information Server) | Z：不支持 |

1. Web servers built based on the Apache httpd source code have as much support as the version of httpd on which it is based. If in doubt, ask Adobe for confirmation of the support level related to the respective server product. The following cases:

   1. The HTTP server was built using only official Apache source distributions, or
   1. The HTTP server was delivered as part of the operating system on which it is running. Examples: IBM® HTTP Server, Oracle HTTP Server

1. Dispatcher is not available for Apache 2.4.x for Windows operating systems.

## 支持的客户端平台 {#supported-client-platforms}

### Supported Browsers for Authoring User Interface {#supported-browsers-for-authoring-user-interface}

The Adobe Experience Manager user interface works with the following client platforms. 所有浏览器都用默认的插件和附加功能进行了测试。

The AEM user interface is optimized for larger screens (typically notebooks and desktop computers) and tablet form factor (such as Apple iPad or Microsoft® Surface). The phone form factor is not supported.

>[!NOTE]
>
>**支持发布周期较快的浏览器：**
>
>Mozilla Firefox, Google Chrome, and Microsoft® Edge release updates every few months. Adobe is committed to provide updates for Adobe Experience Manager to maintain the support level as stated below with upcoming versions of these browsers.

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>Support for UI<br /> </strong></td>
   <td><strong>Support for Classic UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A：受到支持</td>
   <td>A：受到支持</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A：受到支持</td>
   <td>A：受到支持</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A：受到支持</td>
   <td>A：受到支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox last ESR [1]</td>
   <td>A：受到支持</td>
   <td>A：受到支持</td>
  </tr>
  <tr>
   <td>Apple Safari on macOS (Evergreen)</td>
   <td>A：受到支持</td>
   <td>A：受到支持</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x on macOS</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>Apple Safari on iOS 12.x</td>
   <td>A: Supported [2]</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>Apple Safari on iOS 11.x</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
 </tbody>
</table>

1. Extended Support Release of Firefox [Learn more on mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. support for Apple iPad

### 可用于网站的受支持的浏览器 {#supported-browsers-for-websites}

Generally, browser support for websites rendered by AEM Sites depends on the implementation of AEM page templates, design and component output, and is therefore in the control of the party implementing these parts.

### WebDAV Clients {#webdav-clients}

**Microsoft® Windows 7+**

When connecting with Microsoft® Windows 7+ to an AEM instance that is not secured with SSL, basic authentication over an unsecured network must be enabled in Windows. It requires a change in the Windows Registry of the WebClient:

1. Locate the registry subkey:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Add the BasicAuthLevel registry entry to this subkey using a value of 2 or more.

## Additional Platform Notes {#additional-platform-notes}

This section provides special notes and more detailed information about running Adobe Experience Manager and its add-ons.

### IPv4和IPv6 {#ipv-and-ipv}

All elements of Adobe Experience Manager (Instance, Dispatcher) can be installed in both IPv4 and IPv6 networks.

Operation is seamless as no special configuration is required. You specify an IP address using the format that is appropriate to your network type, if necessary.

When an IP address must be specified, you can select (as required) from the following:

* An IPv6 address. 例如，`https://[ab12::34c5:6d7:8e90:1234]:4502`

* An IPv4 address. 例如，`https://123.1.1.4:4502`

* A server name. 例如，`https://www.yourserver.com:4502`

* The default case of `localhost` is interpreted for both IPv4 and IPv6 network installations. 例如，`https://localhost:4502`

### Requirements for AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media is disabled by default. See here to [enable Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

With Dynamic Media enabled, the following additional technical requirements apply.

>[!NOTE]
>
>These system requirements **only** apply if you use Dynamic Media - Hybrid mode; Dynamic Media - Hybrid mode has an embedded image server, which is only certified on certain operating systems.
>
>For Dynamic Media customers who run Dynamic Media - Scene7 mode (that is, **dynamicmedia_scene7** run mode), there are no additional system requirements; only the same system requirements as AEM. Dynamic Media - Scene7 mode architecture uses the cloud-based image service and not the service embedded in AEM.

#### Hardware {#hardware}

The following hardware requirements are applicable for both Linux® and Windows:

* Intel Xeon® or AMD® Opteron CPU with at least four cores
* At least 16 GB of RAM

#### Linux® {#linux}

If you are using Dynamic Media on Linux®, the following prerequisites must be met:

* Red Hat® Enterprise 8及更高版本，带有最新的修复修补程序
* 64位操作系统
* 已禁用交换（推荐）
* 已禁用SELinux（请参阅以下注释）

>[!NOTE]
>
>如果区域设置设置设置得使LC_CTYPE不等于`en_US.UTF-8`，则会导致Dynamic Media无法工作。 要查看其值，请在命令提示符下键入“locale”。 如果未正确设置，请在运行AEM之前键入“export LC_CTYPE=”，以将LC_CTYPE环境变量设置为空字符串。

>[!NOTE]
>
>**禁用SELinux：**&#x200B;图像服务在SELinux打开的情况下不起作用。 此选项默认处于启用状态。 要解决此问题，请编辑&#x200B;**/etc/selinux/config**&#x200B;文件，并将SELinux值从以下位置更改：
>
>`SELINUX=enforcing` **到** `SELINUX=disabled`

>[!NOTE]
>
>**NUMA架构：**&#x200B;处理器采用AMD64和英特尔® EM64T的系统通常配置为非统一内存架构(NUMA)平台。 也就是说，内核在启动时构建多个内存节点，而不是构建单个内存节点。
>
>该多节点结构可导致一个或多个节点上的存储器耗尽，而其它节点则被耗尽。 当内存耗尽时，即使存在可用内存，内核也可以决定终止进程（例如，图像服务器或平台服务器）。
>
>因此，Adobe建议，如果运行的系统导致使用&#x200B;**numa=off**&#x200B;引导选项关闭NUMA，以避免内核终止这些进程。

>[!NOTE]
>
>**服务器主机名必须解析：**&#x200B;请确保服务器的主机名可解析为IP地址。 如果不可能，请将完全限定的主机名和IP地址添加到&#x200B;**/etc/hosts**：
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 交换空间至少相当于物理内存(RAM)容量的两倍

要在Windows上使用Dynamic Media，请安装适用于x64和x86的®Visual Studio 2010、2013和2015可再发行版本。

对于Windows x64：

* 在[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)上获取Microsoft® Visual Studio 2010可再发行组件
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)上获取Microsoft® Visual Studio 2013可再发行版本
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)上获取Microsoft® Visual Studio 2015可再发行组件

对于Windows x86：

* 在[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)上获取Microsoft® Visual Studio 2010可再发行组件
* 在[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)上获取Microsoft® Visual Studio 2013可再发行版本
* 在[https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)上获取Microsoft® Visual Studio 2015可再发行组件

#### macOS {#macos}

* 10.9.x及更高版本
* 仅支持试用和演示

### PDF Generator的注意事项 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>转换到PDF时支持的格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/cn/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a>最新版本</td>
   <td>XPS、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML和HTM</td>
  </tr>

<tr>
   <td>® Office 2021 Professional Plus、零售和批量许可证</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF和TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* PDF Generator仅支持所支持的操作系统和应用程序的英语、法语、德语和日语版本。
>* PDF Generator需要Adobe Acrobat Pro DC（32位）来执行转换。
>* PDF Generator仅支持32位版本的Microsoft® Office Professional Plus以及转换所需的其他软件。
>* 如果® Office安装由于任何原因（例如，批量许可安装无法在指定时间段内找到KMS主机）而停用或取消许可，则在重新许可并重新激活安装之前，转换可能会失败。
>* PDF Generator不支持Microsoft® Office 365。
>* Windows和Linux®均支持OpenOffice的PDF Generator转换。
>* 仅在Windows上支持OCR PDF、优化PDF和Export PDF功能。
>* PDF Generator服务不支持Microsoft® Windows 11。

### AEM Forms Designer的要求 {#requirements-for-aem-forms-designer}

* ® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10或Windows® 11
* 1 GHz或更快的处理器，支持PAE、NX和SSE2。
* 32位RAM为1 GB，64位操作系统为2 GB
* 16 GB的磁盘空间，用于32位或20 GB的磁盘空间，用于64位操作系统
* 图形内存 — 128 MB的GPU（建议使用256 MB）
* 2.35 GB可用硬盘空间
* 1024 X 768像素或更高的显示器分辨率
* 视频硬件加速（可选）
* Acrobat Pro DC、Acrobat Standard DC或Adobe Acrobat Reader DC
* 安装Designer的管理权限
* Microsoft Visual C++ 2019（VC 14.28或更高版本）32位运行时，适用于32位AEM Forms Designer
* Microsoft Visual C++ 2019（VC 14.28或更高版本）适用于64位AEM Forms Designer的64位运行时（适用于OSGI和JEE栈栈）

[安装和配置AEM Forms designer](/help/forms/using/installing-configuring-designer.md)

### AEM Assets XMP元数据回写要求 {#requirements-for-aem-assets-xmp-metadata-write-back}

以下平台和文件格式支持并启用了XMP回写：

* **操作系统：**

   * Linux®（在64位系统上支持32位和32位应用程序）。

   * Windows Server
   * macOS X（64位）

* **文件格式**：JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux®上处理大量元数据的资产的要求 {#assetsonlinux}

XMPFilesProcessor进程需要库GLIBC_2.14才能工作。 使用包含GLIBC_2.14的Linux®内核，例如Linux®内核版本3.1.x。 它提高了处理包含大量元数据的资源（如PSD文件）的性能。 使用以前版本的GLIBC会导致以`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`开头的日志中出现错误。

有关与支持的格式或平台版本相关的任何查询，请联系[AEM Forms支持](https://business.adobe.com/in/support/main.html)
