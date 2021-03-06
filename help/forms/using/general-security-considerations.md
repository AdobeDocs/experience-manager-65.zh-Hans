---
title: JEE上AEM Forms的一般安全注意事项
seo-title: JEE上AEM Forms的一般安全注意事项
description: 了解如何准备在JEE环境中强化AEM Forms。
seo-description: 了解如何准备在JEE环境中强化AEM Forms。
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---

# JEE上AEM Forms的一般安全注意事项{#general-security-considerations-for-aem-forms-on-jee}

本文提供了一些介绍性信息，可帮助您为强化AEM Forms环境做好准备。 它包括有关JEE上的AEM Forms、操作系统、应用程序服务器和数据库安全性的先决条件信息。 在继续锁定环境之前，请查看此信息。

## 特定于供应商的安全信息 {#vendor-specific-security-information}

本部分包含有关操作系统、应用程序服务器和数据库的安全相关信息，这些信息已纳入到您的AEM Forms on JEE解决方案中。

使用此部分中的链接可查找特定于供应商的操作系统、数据库和应用程序服务器的安全信息。

### 操作系统安全信息 {#operating-system-security-information}

在保护操作系统时，请仔细考虑实施操作系统供应商描述的措施，包括：

* 定义和控制用户、角色和权限
* 监控日志和审计跟踪
* 删除不必要的服务和应用程序
* 备份文件

有关JEE上的AEM Forms支持的操作系统的安全信息，请参阅表中的资源：

<table>
 <thead>
  <tr>
   <th><p>操作系统</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">IBM AIX安全优势</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Windows Server 2016安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP或ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat Enterprise Linux安全指南</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">安全性和强化准则</a></p> </td>
  </tr>
  <tr>
   <td>OracleLinux® 7更新3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">版本7的安全指南</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">保护文档</a></td>
  </tr>
 </tbody>
</table>

### 应用程序服务器安全信息 {#application-server-security-information}

在保护应用程序服务器时，请仔细考虑实施服务器供应商描述的措施，包括：

* 使用非明显的管理员用户名
* 禁用不必要的服务
* 保护控制台管理器
* 启用安全Cookie
* 关闭不需要的端口
* 按IP地址或域限制客户端
* 使用Java™ Security Manager以编程方式限制权限

有关JEE上的AEM Forms支持的应用程序服务器的安全信息，请参阅此表中的资源。

<table>
 <thead>
  <tr>
   <th><p>应用程序服务器</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>OracleWebLogic®</p> </td>
   <td><p>在<a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>中搜索“了解WebLogic安全”。</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">保护应用程序及其环境</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">安全子系统配置</a></p> </td>
  </tr>
 </tbody>
</table>

### 数据库安全信息 {#database-security-information}

在保护数据库时，请考虑实施数据库供应商描述的措施，包括：

* 使用访问控制列表(ACL)限制操作
* 使用非标准端口
* 在防火墙后隐藏数据库
* 在将敏感数据写入数据库之前对其进行加密（请参阅数据库制造商的文档）

有关JEE上的AEM Forms支持的数据库的安全信息，请参阅此表中的资源。

<table>
 <thead>
  <tr>
   <th><p>数据库</p> </th>
   <th><p>安全资源</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">DB2产品系列库</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>在Web上搜索“SQL Server 2016:安全性”</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">MySQL 5.0一般安全问题</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">MySQL 5.1一般安全问题</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>请参阅<a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Oracle12g文档</a>中的“安全”一章</p> </td>
  </tr>
 </tbody>
</table>

此表介绍了在JEE配置过程中AEM Forms所需打开的默认端口。 如果您通过https连接，请相应地调整端口信息和IP地址。 有关配置端口的更多信息，请参阅应用程序服务器的&#x200B;*在JEE*&#x200B;上安装和部署AEM Forms文档。

<table>
 <thead>
  <tr>
   <th><p>产品或服务</p> </th>
   <th><p>端口号</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebLogic Managed Server</p> </td>
   <td><p>配置期间由管理员设置</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060，如果启用了“全局安全”，则默认的SSL端口值为9043。</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>BAM服务器</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>运行LDAP服务器的端口。 默认端口通常为389。 但是，如果选择SSL选项，则默认端口通常为636。 向LDAP管理员确认要指定的端口。</p> </td>
  </tr>
 </tbody>
</table>

### 将JBoss配置为使用非默认HTTP端口 {#configuring-jboss-to-use-a-non-default-http-port}

JBoss Application Server使用8080作为默认HTTP端口。 JBoss还具有预配置的端口8180、8280和8380，这些端口在jboss-service.xml文件中注释掉。 如果您的计算机上有已使用此端口的应用程序，请按照以下步骤更改JEE上的AEM Forms使用的端口：

1. 打开以下文件进行编辑：

   单个服务器安装：[JBoss根]/standalone/configuration/standalone.xml

   群集安装：[JBoss根]/domain/configuration/domain.xml

1. 将&#x200B;**&lt;socket-binding>**&#x200B;标记中&#x200B;**port**&#x200B;属性的值更改为自定义端口号。 例如，以下代码使用端口8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot; />

1. 保存并关闭文件。
1. 重新启动JBoss应用程序服务器。

## AEM Forms on JEE安全注意事项 {#aem-forms-on-jee-security-considerations}

本节介绍一些您应该了解的与JEE相关的AEM Forms安全问题。

### 未在数据库中加密电子邮件凭据 {#email-credentials-not-encrypted-in-database}

应用程序存储的电子邮件凭据在存储到JEE数据库上的AEM Forms中之前不会进行加密。 将服务端点配置为使用电子邮件时，作为该端点配置的一部分使用的任何密码信息在存储到数据库中时都不会加密。

### Rights Management数据库中的敏感内容 {#sensitive-content-for-rights-management-in-the-database}

AEM Forms on JEE使用AEM Forms on JEE数据库来存储敏感文档密钥信息和用于策略文档的其他加密材料。 保护数据库免受入侵有助于保护此敏感信息。

### 以明文形式显示密码 {#password-in-clear-text-format-in-adobe-ds-xml}

用于在JEE上运行AEM Forms的应用程序服务器需要其自己的配置，以便通过应用程序服务器上配置的数据源访问数据库。 确保应用程序服务器在其数据源配置文件中不以明文形式公开数据库密码。

lc_[database].xml文件不应包含明文格式的密码。 请咨询应用程序服务器供应商，了解如何为应用程序服务器加密这些密码。

>[!NOTE]
>
>JEE JBoss统包安装程序上的AEM Forms加密数据库密码。

默认情况下，IBM WebSphere Application Server和OracleWebLogic Server可能会加密数据源密码。 但是，请通过应用程序服务器文档进行确认，以确保出现这种情况。

### 保护存储在信任存储中的私钥 {#protecting-the-private-key-stored-in-trust-store}

在信任存储中导入的私钥或凭据存储在JEE数据库的AEM Forms中。 采取适当的预防措施保护数据库并限制仅对指定管理员的访问。
