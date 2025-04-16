---
title: 技术要求
description: Adobe Experience Manager支持的客户端和服务器平台列表。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 5dbdce2d8e558e6bf26c6713fd44d58038d38152
workflow-type: tm+mt
source-wordcount: '3593'
ht-degree: 1%

---

# 技术要求{#technical-requirements}

Adobe支持平台上的(AEM) Adobe Experience Manager，本文档中的以下信息中有详细说明。

如有任何与平台相关的问题，请联系平台供应商。

>[!NOTE]
>
>根据安装AEM的平台，用户管理可能会有不同的要求集。

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

本文档列出了Adobe Experience Manager支持的客户端和服务器平台。 Adobe提供了多个级别的支持，包括推荐的配置和其他配置。

### 支持的配置 {#supported-configurations}

Adobe建议进行这些配置，并在标准软件维护协议中提供全面支持。

<table>
 <tbody>
  <tr>
   <td>支持级别</td>
   <td>描述<br /> </td>
  </tr>
  <tr>
   <td><strong>答：支持</strong></td>
   <td>Adobe为此配置提供全面支持和维护。 Adobe的质量保证流程涵盖此配置。</td>
  </tr>
  <tr>
   <td><strong>R：有限的支持</strong></td>
   <td>为了确保客户项目成功，Adobe在受限制的支持计划内提供了全面支持，该计划要求满足特定条件。 r级支持需要正式的客户请求和Adobe的确认。 有关更多信息，请联系Adobe客户关怀部门。</td>
  </tr>
 </tbody>
</table>

### 不支持的配置 {#unsupported-configurations}

| 支持级别 | 描述 |
|---|---|
| **Z：不支持** | 不支持该配置。 Adobe不声明配置是否有效，也不支持该配置。 |

## 支持的平台 {#supported-platforms}

### Java™ 虚拟机 {#java-virtual-machines}

该应用程序需要 Java™ 虚拟机才能运行，该虚拟机由 Java™ 开发工具包 （JDK） 分发版提供。

Adobe Experience Manager 可与以下版本的 Java™ 虚拟机配合使用：

>[!CAUTION]
>
>跟踪 Java™ 供应商提供的安全公告。 这样做可确保生产环境的安全性。 此外，请始终安装最新的 Java™ 更新。

| **平台** | **支持级别** | **链接** |
|---|---|---|
| Oracle Java™ SE 17 JDK | Z：不支持`[1]` |
| Oracle Java™ SE 11 JDK - 64位 | A：支持的`[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z：不支持`[1]` |
| Oracle Java™ SE 9 JDK | Z：不支持`[1]` |
| Oracle Java™ SE 8 JDK - 64位 | A：支持的`[1]` | [下载](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9虚拟机 — 内部版本2.9，JRE 1.8.0 | A：支持的`[2]` |
| IBM® J9虚拟机 — 内部版本2.8、JRE 1.8.0 | A：支持的`[2]` |
| Azul Zulu OpenJDK 11 - 64位 | A：支持的`[3]` | |
| Azul Zulu OpenJDK 8 - 64位 | A：支持的`[3]` | |

1. oracle已针对OracleJava™ SE产品转向“长期支持”(LTS)模式。 Java™ 9、Java™ 10和Java™ 12是按Oracle列出的非LTS版本(请参阅[OracleJava™ SE支持路线图](https://www.oracle.com/technetwork/java/eol-135779.html))。 要在生产环境中部署AEM，Adobe仅支持Java™的LTS版本。 所有使用OracleJava™ SE技术的AEM客户均可直接Adobe，从而支持和分发OracleJava™ SE JDK（包括公共更新结束后对LTS版本的所有维护更新）。 请参阅Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf)的[Java™支持政策。
   **重要说明：至少在2026年9月之前支持OracleJava™ 11。 正在准备对OracleJava™ 17的支持。**

1. IBM® JRE仅与WebSphere®应用程序服务器一起受支持。

1. 从版本6.5 SP9开始，本地AEM部署支持Azul Zulu OpenJDK LTS版本。 Azul Zulu JDK LTS版本的支持和分发必须由Adobe客户直接从Azul授予许可。


### 存储和持久性 {#storage-persistence}

可以使用各种选项来部署Adobe Experience Manager存储库。 有关支持的技术和存储选项，请参阅以下列表。

| **平台** | **描述** | **支持级别** |
|---|---|---|
| **带有TAR文件的文件系统** `[1]` | 存储库 | 答：支持 |
| **具有数据存储的文件系统** `[1]` | 二进制文件 | 答：支持 |
| 在文件系统`[1]`的TAR文件中存储二进制文件 | 二进制文件 | Z：不支持生产 |
| Amazon S3 | 二进制文件 | 答：支持 |
| ® Microsoft Azure Blob 存储 | 二进制文件 | 答：支持 |
| MongoDB Enterprise 6.0 | 存储库 | A：支持的`[3, 4]` |
| MongoDB Enterprise 5.0 | 存储库 | 答：支持 `[3, 4]` |
| MongoDB Enterprise 4.4 | 存储库 | 答：支持 `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | 存储库 | A：支持的`[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | 存储库 | Z：不支持 |
| MongoDB Enterprise 3.6 | 存储库 | Z：不支持 |
| MongoDB Enterprise 3.4 | 存储库 | Z：不支持 |
| IBM® DB2® 10.5 | 存储库和Forms数据库 | R：限制的支持`[5]` |
| Oracle数据库12c (12.1.x) | 存储库和Forms数据库 | R：有限的支持 |
| Microsoft® SQL Server 2016 | Forms数据库 | 答：支持 |
| **Apache Lucene（快速入门内置）** | 搜索服务 | A：支持 |
| Apache Solr | 搜索服务 | A：支持 |

1. “文件系统”包括与POSIX兼容的数据块存储。 包括网络存储技术。 请注意，文件系统性能可能会有所不同，并影响整体性能。 使用网络/远程文件系统对AEM进行负载测试。
1. MongoDB Enterprise版本4.2和4.4至少需要AEM 6.5 SP9。
1. AEM中不支持MongoDB分片。
1. 仅支持MongoDB存储引擎WiredTiger。
1. 支持AEM Forms升级客户。 新安装不支持。
1. 仅适用于AEM Forms：
   * 移除了对Oracle Database 12c的支持，并增加了对Oracle Database 19c的支持。
   * 删除了对Microsoft® SQL Server 2016的支持，并添加了对Microsoft® SQL Server 2019的支持。
1. AEM Forms不支持。

>[!NOTE]
>
>有关AEM Communities功能的详细信息，请参阅[部署社区](/help/communities/deploy-communities.md)。

>[!NOTE]
>
>MongoDB是第三方软件程序，未包含在AEM许可包中。 有关更多信息，请参阅 [MongoDB 许可策略](https://www.mongodb.com/licensing/server-side-public-license/faq) 页面。
>
>为了充分利用MongoDB的AEM部署，Adobe建议许可MongoDB Enterprise版本以获得专业支持。 有关详细信息，请参阅[建议的部署](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)。
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
>**Most relational databases are currently supported within Level-R on AEM 6.5, which comes with support criteria and a support program as stated in the Level-R description above.**-->

### Servlet引擎/应用程序服务器 {#servlet-engines-application-servers}

Adobe Experience Manager 既可以作为独立服务器（快速入门 JAR 文件），也可以作为第三方应用程序服务器中的 Web 应用程序（WAR 文件）运行。

所需的最低 Servlet API 版本是 Servlet 3.1

| Platform | 支持级别 |
|---|---|
| **快速入门内置 Servlet 引擎 （Jetty 9.4）** | 答：支持 |
| Oracle WebLogic Server 12.2 (12cR2) | Z：不支持 |
| IBM® WebSphere® Application Server Continuous Delivery (LibertyProfile) with Web Profile 7.0和IBM® JRE 1.8 | R：对新合同的支持受限`[2]` |
| IBM® WebSphere® Application Server 9.0和IBM® JRE 1.8 | R：对新合同`[1]`的支持受限 `[2]` |
| Apache Tomcat 8.5.x | R：对新合同的支持受限 `[2]` |
| JBoss® EAP 7.2.x带JBoss®应用程序服务器 | Z：不支持 |
| JBoss® EAP 7.1.4带JBoss®应用程序服务器 | R：对新合同的支持受限`[1]` `[2]` |
| JBoss® EAP 7.0.x带JBoss®应用程序服务器 | Z：不支持 |

1. 建议使用AEM Forms进行部署。
1. 在应用程序服务器中启动AEM 6.5部署后，将转为有限支持。 现有客户可以升级到AEM 6.5并继续使用应用程序服务器。 对于新客户，它附带支持标准和支持计划，如上面的R级描述中所述。
1. 仅适用于AEM Forms：
   * 移除了对JBoss® EAP 7.1.4的支持，并添加了对JBoss® EAP 7.4.10的支持。

### 服务器操作系统 {#server-operating-systems}

Adobe Experience Manager可与以下服务器平台配合使用以用于生产环境：

| **平台** | **支持级别** |
|---|---|
| **Linux®，基于Red Hat®分发** | A：支持的`[1]` `[3]` |
| Linux®，基于Debian分布，包括 乌班图 | A：支持的`[1]` `[2]` |
| Linux®，基于SUSE®分发 | A：支持的`[1]` |
| Microsoft® Windows Server 2019 `[4]` | R：对新合同的支持受限`[5]` |
| Microsoft® Windows Server 2016 `[4]` | R：对新合同的支持受限`[5]` |
| Microsoft® Windows Server 2012 R2 | Z：不支持 |
| Oracle Solaris™ 11 | Z：不支持 |
| IBM® AIX® 7.2 | Z：不支持 |

1. Linux®内核2.6、3。 x， 4. x， 5。 x和6。 x包括来自Red Hat® Distribution的派生程序，包括Red Hat® Enterprise Linux®、CentOS、Oracle Linux®和Amazon Linux®。 只有CentOS 7、Red Hat® Enterprise Linux® 7、Red Hat® Enterprise Linux® 8和Red Hat® Enterprise Linux® 9支持AEM Forms附加功能。
1. Ubuntu 20.04 LTS支持AEM Forms。
1. Adobe Managed Services支持的Linux®分发。

   >[!NOTE]
   >
   >对于基于Linux的服务器（OSGI和JEE栈栈），AEM Forms加载项需要运行时依赖关系，例如：
   >* glibc.x86_64 (2.17-196)
   >* libX11.x86_64 （1.6.7-4）
   >* zlib.x86-64 （1.2.7-17）
   >* libxcb.x86_64 (1.13-1.el7)
   >* libXau.x86_64 (1.0.8-2.1.el7)
   >* glibc-locale.x86_64（2.17或更高版本）

1. Microsoft® Windows生产部署支持升级到6.5的客户和非生产使用。 AEM Sites和Assets会应请求进行新部署。
1. Microsoft® Window Server上支持AEM Forms，但没有支持级别R限制。
1. AEM Forms删除了对Microsoft® Windows Server 2016的支持。

>[!NOTE]
>
>如果要安装 AEM Forms 6.5，请确保已安装以下 32 位 Microsoft® 可视C++可再发行组件。
>
>* ® Microsoft Visual C++ 2008 可再发行组件
>* ® Microsoft Visual C++ 2010 可再发行组件
>* Microsoft® Visual C++ 2012可再分发
>* Microsoft® Visual C++ 2013可再分发
>* Microsoft® Visual C++ 2019（VC14.28或更高版本）可再分发


### 虚拟和云计算环境 {#virtual-cloud-computing-environments}

支持在云计算环境中的虚拟机中运行Adobe Experience Manager。 这些环境包括Microsoft®Azure和Amazon Web Services (AWS)，其运行符合本页列出的技术要求并符合Adobe的标准支持条款。

对于云原生环境，请查看 AEM 产品线的最新产品：Adobe Experience Manager 即云服务。 有关详细信息，请参阅[Adobe Experience Manager as a Cloud Service文档](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html)。

Adobe 还提供 Adobe 托管服务，用于在 Azure 或 AWS 上部署 AEM。 Adobe Managed Services 为专家提供了在这些云计算环境中部署和作 AEM 的经验和技能。 请参阅 [有关 Adobe 托管服务](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t)的其他文档。

在 Azure 或 AWS 或任何其他云计算环境中部署 AEM 的所有其他情况下，Adobe 的支持包含在虚拟计算环境中。 该虚拟环境的运行必须符合此页面上列出的技术规范。 任何与在任何这些云环境中运行的AEM相关的已报告问题，都必须可独立于任何特定于云计算环境的云服务进行重现。 也就是说，除非本页面上列出的技术要求(例如Azure Blob Storage或AWS S3)支持Cloud Service。

有关如何在Adobe Managed Services之外的Azure或AWS上部署AEM的建议，Adobe建议直接与云提供商合作。 或者，与Adobe合作伙伴合作，为您选择的云环境中部署AEM提供支持。 选定的云提供商或合作伙伴负责体系结构的规模调整、设计和实施，以满足您的特定性能、负载、可扩展性和安全要求。

### Dispatcher平台（Web服务器） {#dispatcher-platforms-web-servers}

Dispatcher是缓存和负载平衡组件。 [下载最新的Dispatcher版本](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html)。 Experience Manager 6.5需要Dispatcher版本4.3.2或更高版本。

以下Web服务器支持与Dispatcher版本4.3.2一起使用：

| Platform | 支持级别 |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | 答：支持 |
| Microsoft® IIS 10 (Internet Information Server) | 答：支持 |
| ® Microsoft IIS 8.5 （Internet Information Server） | Z：不支持 |

1. 基于 Apache httpd 源代码构建的 Web 服务器的支持与其所基于的 httpd 版本一样多。 如有疑问，请向 Adobe 请求确认与相应服务器产品相关的支持级别。 以下情况：

   1. HTTP 服务器仅使用官方 Apache 源代码发行版构建，或者
   1. HTTP服务器是作为运行它的操作系统的一部分提供的。 示例： IBM® HTTP Server、Oracle HTTP Server

1. Dispatcher不适用于适用于Windows操作系统的Apache 2.4.x。

## 支持的客户端平台 {#supported-client-platforms}

### 支持创作用户界面的浏览器 {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager用户界面可与以下客户端平台配合使用。 所有浏览器都使用默认插件和加载项集进行测试。

AEM用户界面已针对大屏幕（通常是笔记本电脑和台式计算机）和平板电脑外形规格(如Apple iPad或Microsoft® Surface)进行了优化。 不支持电话的外形规格。

>[!NOTE]
>
>**对具有快速发布周期的浏览器的支持：**
>
>Mozilla Firefox、Google Chrome和Microsoft® Edge每隔几个月发布一次更新。 Adobe承诺为Adobe Experience Manager提供更新，以在这些浏览器的即将发行版本中保持下述支持级别。

<table>
 <tbody>
  <tr>
   <td><strong>浏览器</strong></td>
   <td><strong>支持UI<br /> </strong></td>
   <td><strong>支持经典UI</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome（常绿市）</strong></td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft®Edge（常青网）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>Mozilla Firefox上一个ESR [1]</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>macOS 上的 Apple Safari （Evergreen）</td>
   <td>答：支持</td>
   <td>答：支持</td>
  </tr>
  <tr>
   <td>macOS 上的 Apple Safari 11.x</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>iOS 12.x上的Apple Safari</td>
   <td>答：支持的[2]</td>
   <td>Z：不支持</td>
  </tr>
  <tr>
   <td>iOS 11.x上的Apple Safari</td>
   <td>Z：不支持</td>
   <td>Z：不支持</td>
  </tr>
 </tbody>
</table>

1. Firefox [的扩展支持版本了解有关mozilla.org的更多信息](https://www.mozilla.org/en-US/firefox/enterprise/)
1. 支持Apple iPad

### 支持的网站浏览器 {#supported-browsers-for-websites}

通常，AEM Sites渲染的网站的浏览器支持取决于AEM页面模板的实施、设计和组件输出，因此受实施这些部分的方的控制。

### WebDAV 客户端 {#webdav-clients}

**Microsoft® Windows 7+**

在与Microsoft® Windows 7+连接到一个不使用SSL保护的AEM实例时，必须在Windows中启用通过不安全网络进行的基础身份验证。 它需要在WebClient的Windows注册表中进行更改：

1. 找到注册表子项：

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. 使用值 2 或更大值向此子项添加 BasicAuthLevel 注册表项。

## 其他平台说明 {#additional-platform-notes}

本节提供了有关运行Adobe Experience Manager及其加载项的特殊说明和更多详细信息。

### IPv4和IPv6 {#ipv-and-ipv}

Adobe Experience Manager(实例、Dispatcher)的所有元素都可以安装在IPv4和IPv6网络中。

作是无缝的，因为不需要特殊配置。 如有必要，您可以使用适合您的网络类型的格式指定 IP 地址。

当必须指定 IP 地址时，可以（根据需要）从以下选项中进行选择：

* IPv6 地址。 例如，`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4 地址。 例如，`https://123.1.1.4:4502`

* 服务器名称。 例如，`https://www.yourserver.com:4502`

* 对于IPv4和IPv6网络安装，都会解释`localhost`的默认情况。 例如，`https://localhost:4502`

### AEM Dynamic Media加载项的要求 {#requirements-for-aem-dynamic-media-add-on}

默认情况下，AEM Dynamic Media处于禁用状态。 请参阅此处[启用Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media)。

启用Dynamic Media后，需要满足以下附加技术要求。

>[!NOTE]
>
>如果您使用Dynamic Media — 混合模式，则这些系统要求&#x200B;**仅**&#x200B;适用；Dynamic Media — 混合模式具有嵌入式图像服务器，该服务器仅在某些操作系统上经过验证。
>
>对于运行Dynamic Media - Scene7模式（即&#x200B;**dynamicmedia_scene7**&#x200B;运行模式）的Dynamic Media客户，没有其他系统要求；只有与AEM相同的系统要求。 Dynamic Media - Scene7模式架构使用基于云的图像服务，而不是嵌入到AEM中的服务。

#### 硬件 {#hardware}

以下硬件要求适用于Linux®和Windows：

* 英特尔至强®或AMD®皓龙CPU，至少具有四个内核
* 至少16 GB RAM

#### Linux® {#linux}

如果您在Linux®上使用Dynamic Media，则必须满足以下先决条件：

* Red Hat® Enterprise 7或CentOS 7及更高版本，带有最新的修复修补程序
* 64位操作系统
* 已禁用交换（推荐）
* 已禁用SELinux（请参阅以下注释）

>[!NOTE]
>
>如果区域设置设置设置得使LC_CTYPE不等于`en_US.UTF-8`，则会导致Dynamic Media无法工作。 要查看其值，请在命令提示符下键入“locale”。 如果未正确设置，请在运行AEM之前键入“export LC_CTYPE=”，以将LC_CTYPE环境变量设置为空字符串。

>[!NOTE]
>
>**禁用 SELinux：** 打开 SELinux 后，图像服务不起作用。 默认情况下，此选项处于启用状态。 要解决此问题，请编辑 **/etc/selinux/config** 文件并将 SELinux 值从：
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
>**服务器主机名必须解析：** 确保服务器的主机名可解析为 IP 地址。 如果无法做到这一点，请将完全限定的主机名和 IP 地址 **添加到 /etc/hosts**：
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 交换空间至少相当于物理内存(RAM)容量的两倍

要在Windows上使用Dynamic Media，请安装适用于x64和x86的Microsoft®Visual Studio 2010、2013和2015可再发行版本。

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
* 仅支持用于试用和演示目的

### AEM Forms PDF Generator的要求 {#requirements-for-aem-forms-pdf-generator}

### PDF Generator的软件支持 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>产品</strong></p> </th>
   <th><p><strong>转换到PDF时支持的格式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 经典曲目</a> 最新版本</td>
   <td>XPS、图像格式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM、DWG、DXF 和 DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a>最新版本（已弃用）</td>
   <td>XPS、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、DWG、DXF和DWF</td>
  </tr>
  <tr>
   <td>® Microsoft Office 2019</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF 和 TXT</td>
  </tr>
  <tr>
   <td>® Microsoft Office 2016（已弃用）</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF 和 TXT</td>
  </tr>
  <tr>
   <td>完美字 2020<br /> </td>
   <td>WP 、 WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016（已弃用）<br /> </td>
   <td>VSD、VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016（已弃用）<br /> </td>
   <td>公共</td>
  </tr>
  <tr>
   <td>Microsoft®项目2016（已弃用）<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2（已弃用）</td>
   <td>ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、图像格式(BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC)、HTML、HTM、RTF、TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator仅支持所支持的操作系统和应用程序的英语、法语、德语和日语版本。
>
>另外，
>
>* PDF Generator需要32位版本的[Acrobat 2020 classic track版本20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html)来执行转换。
>* PDF Generator仅支持32位版本的Microsoft® Office Professional Plus以及转换所需的其他软件。
>* Microsoft® Office Professional Plus安装可以使用零售或基于MAK/KMS/AD的批量许可。
>* 如果Microsoft® Office安装由于任何原因（例如，批量许可安装无法在指定时间段内找到KMS主机）而停用或取消许可，则在重新许可并重新激活安装之前，转换可能会失败。
>* PDF Generator支持Linux®操作系统上的32位版本的OpenOffice。
>* PDF Generator不支持Microsoft® Office 365。
>* 仅在Windows和Linux®上支持OpenOffice的PDF Generator转换。
>* 仅在Windows上支持OCR PDF、优化PDF和Export PDF功能。
>* Acrobat的一个版本与AEM Forms捆绑在一起，用于启用PDF Generator功能。 在AEM Forms许可证有效期内，只能以编程方式访问AEM Forms捆绑的版本，以便与AEM Forms PDF Generator结合使用。 有关详细信息，请参阅根据您的部署([内部部署](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html)或[Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))提供的AEM Forms产品说明
>* PDF Generator服务不支持Microsoft® Windows 10。
>* PDF Generator无法使用Microsoft® Visio 2019转换文件。
>* PDF Generator无法使用Microsoft® Project 2019转换文件。

### AEM Forms Designer的要求 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10或Windows® 11
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

   * Linux®（在64位系统上支持32位和32位应用程序）。 有关安装32位客户端库的步骤，请参阅[如何在64位Red Hat® Linux®](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)上启用XMP提取和回写。

   * Windows Server
   * macOS X（64位）

* **文件格式**：JPEG、PNG、TIFF、PDF、INDD、AI和EPS。

### AEM Assets在Linux®上处理大量元数据的资产的要求 {#assetsonlinux}

XMPFilesProcessor 进程需要库 GLIBC_2.14 才能工作。 使用包含 GLIBC_2.14 的 Linux® 内核，例如 Linux® 内核版本 3.1.x。它提高了处理包含大量元数据的资产（如 PSD 文件）的性能。 使用以前版本的 GLIBC 会导致以 开头 `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`的日志出错。
