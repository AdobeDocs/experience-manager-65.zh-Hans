---
title: 在JEE环境中强化AEM表单
seo-title: 在JEE环境中强化AEM表单
description: 了解各种安全强化设置，以增强在企业内部网中运行的JEE上AEM Forms的安全性。
seo-description: 了解各种安全强化设置，以增强在企业内部网中运行的JEE上AEM Forms的安全性。
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 在JEE环境中强化AEM表单 {#hardening-your-aem-forms-on-jee-environment}

了解各种安全强化设置，以增强在企业内部网中运行的JEE上AEM Forms的安全性。

本文介绍了有关保护在JEE上运行AEM Forms的服务器的建议和最佳实践。 这不是针对操作系统和应用程序服务器的全面的主机强化文档。 相反，本文描述了各种安全强化设置，您应该实施这些设置以增强在公司内部网中运行的JEE上AEM Forms的安全性。 但是，为确保JEE应用程序服务器上的AEM Forms保持安全，您还应实施安全监控、检测和响应过程。

本文描述了在安装和配置生命周期的以下阶段应用的硬化技术：

* **** 预安装：在JEE上安装AEM Forms之前，请使用这些技术。
* **** 安装：在JEE上的AEM Forms安装过程中使用这些技术。
* **** 安装后：在安装后使用这些技术，然后定期使用。

JEE上的AEM Forms可以高度自定义，并可以在许多不同的环境中工作。 其中一些建议可能不符合贵组织的需求。

## 预安装 {#preinstallation}

在JEE上安装AEM Forms之前，您可以将安全解决方案应用到网络层和操作系统。 本节介绍一些问题，并就减少这些领域中的安全漏洞提出建议。

**在UNIX和Linux上安装和配置**

您不应使用根Shell在JEE上安装或配置AEM Forms。 默认情况下，文件安装在/opt目录下，执行安装的用户需要在/opt下安装所有文件权限。 或者，也可以在单个用户的/user目录下执行安装，在该目录下，他们已经拥有所有文件权限。

**在Windows上安装和配置**

如果您使用统包方法在JBoss上的JEE上安装AEM Forms，或者如果您正在安装PDF Generator，则您应以管理员身份在Windows上进行安装。 此外，在具有本机应用程序支持的Windows上安装PDF Generator时，必须以安装Microsoft office的Windows用户的身份运行安装。 有关安装权限的详细信息，请参 **阅在JEE上安装和部署AEM Forms** （在JEE上）文档。

### 网络层安全 {#network-layer-security}

网络安全漏洞是任何面向Internet或面向Intranet的应用程序服务器面临的首要威胁之一。 本节介绍针对这些漏洞强化网络上的主机的过程。 它解决了网络分割、传输控制协议／因特网协议(TCP/IP)栈加固以及使用防火墙保护主机的问题。

下表描述了减少网络安全漏洞的常见进程。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>非军事区(DMZ)</p> </td> 
   <td><p>在非军事区(DMZ)内部署表单服务器。 分段至少应存在于两个级别中，应用程序服务器用于在位于内部防火墙后的JEE上运行AEM Forms。 将外部网络与包含Web服务器的DMZ分离，而Web服务器又必须与内部网络分离。 使用防火墙实现分层。 对通过每个网络层的流量进行分类和控制，以确保仅允许所需数据的绝对最小值。</p> </td> 
  </tr> 
  <tr> 
   <td><p>专用IP地址</p> </td> 
   <td><p>将网络地址转换(NAT)与AEM Forms应用程序服务器上的RFC 1918专用IP地址结合使用。 指定专用IP地址(10.0.0.0/8、172.16.0.0/12和192.168.0.0/16)，使攻击者更难通过Internet将通信路由到NAT内部主机和从内部主机发送的通信。</p> </td> 
  </tr> 
  <tr> 
   <td><p>防火墙</p> </td> 
   <td><p>使用以下条件选择防火墙解决方案：</p> 
    <ul> 
     <li><p>实施防火墙，它们支持代理服务器和／或状态 <em>检查</em> ，而不是简单的包过滤解决方案。</p> </li> 
     <li><p>使用防火墙，它支持拒绝除 <em>明确允许的安全范例外的所</em> 有服务。</p> </li> 
     <li><p>实现双宿主或多宿主防火墙解决方案。 此体系架构提供最高级别的安全性，并有助于防止未经授权的用户绕过防火墙安全性。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>数据库端口</p> </td> 
   <td><p>请勿对数据库使用默认监听端口(MySQL - 3306、Oracle - 1521、MS SQL - 1433)。 有关更改数据库端口的信息，请参阅数据库文档。</p> <p>使用其他数据库端口会影响JEE配置上的整个AEM Forms。 如果更改默认端口，则必须在其他配置区域（如JEE上的AEM Forms数据源）中进行相应的修改。</p> <p>有关在JEE上的AEM Forms中配置数据源的信息，请参阅《 <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">AEM Forms用户指南》中的“在JEE上安装和升级AEM Forms”或“在JEE上升级到AEM Forms”（在JEE上升级到AEM Forms）</a>。</p> </td> 
  </tr> 
 </tbody> 
</table>

### 操作系统安全性 {#operating-system-security}

下表介绍了一些使操作系统中发现的安全漏洞最小化的潜在方法。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p></th> 
   <th><p>描述</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>安全修补程序</p></td> 
   <td><p>如果供应商安全补丁和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问的风险增加。 在将安全修补程序应用到生产服务器之前，先测试这些安全修补程序。</p><p>此外，还可以创建定期检查和安装修补程序的策略和过程。</p></td> 
  </tr> 
  <tr> 
   <td><p>病毒防护软件</p></td> 
   <td><p>病毒扫描器可以通过扫描签名或监视异常行为来识别感染病毒的文件。 扫描仪将其病毒签名保留在文件中，该文件通常存储在本地硬盘上。 由于经常发现新病毒，因此您应该经常为病毒扫描程序更新此文件以识别所有当前病毒。</p></td> 
  </tr> 
  <tr> 
   <td><p>网络时间协议(NTP)</p></td> 
   <td><p>要进行取证分析，请在表单服务器上保持准确的时间。 使用NTP同步直接连接到Internet的所有系统上的时间。</p></td> 
  </tr> 
 </tbody> 
</table>

有关操作系统的其他安全信息，请参 [阅“操作系统安全信息”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information)。

## 安装 {#installation}

本节介绍在AEM Forms安装过程中可用于减少安全漏洞的技术。 在某些情况下，这些技术会使用作为安装过程一部分的选项。 下表介绍了这些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>权限</p> </td> 
   <td><p>使用安装软件所需的最少权限数。 使用“管理员”组中不存在的帐户登录到计算机。 在Windows上，您可以使用“运行为”命令以管理用户身份在JEE安装程序上运行AEM Forms。 在UNIX和Linux系统上，使用诸如安 <code>sudo</code> 装软件的命令。</p> </td> 
  </tr> 
  <tr> 
   <td><p>软件源</p> </td> 
   <td><p>请勿从不受信任的源在JEE上下载或运行AEM Forms。</p> <p>恶意程序可能包含若干种违反安全性的代码，包括数据盗窃、修改和删除以及拒绝服务。 从Adobe DVD或仅从受信任的源在JEE上安装AEM Forms。</p> </td> 
  </tr> 
  <tr> 
   <td><p>磁盘分区</p> </td> 
   <td><p>将AEM Forms放在专用磁盘分区上的JEE上。 磁盘分段是一个过程，它将服务器上的特定数据保存在单独的物理磁盘上，以增加安全性。 这样安排数据可以降低目录遍历攻击的风险。 计划创建一个与系统分区分开的分区，您可以在该分区上的JEE内容目录上安装AEM Forms。 （在Windows上，系统分区包含system32目录或引导分区。）</p> </td> 
  </tr> 
  <tr> 
   <td><p>组件</p> </td> 
   <td><p>评估现有服务并禁用或卸载任何不需要的服务。 请勿安装不必要的组件和服务。</p> <p>应用程序服务器的默认安装可能包含您使用时不需要的服务。 在部署之前，您应禁用所有不必要的服务，以最大限度地减少攻击的入口点。 例如，在JBoss上，可以在META-INF/jboss-service.xml描述符文件中注释掉不必要的服务。</p> </td> 
  </tr> 
  <tr> 
   <td><p>跨域策略文件</p> </td> 
   <td><p>服务器上存 <code>crossdomain.xml</code> 在文件可能会立即削弱该服务器。 建议您尽可能限制域列表。 使用参考线( <code>crossdomain.xml</code> 已弃用)时，请勿将开发过程中使用的文件放 <em>入生产中</em>。 对于使用Web服务的指南，如果服务位于提供该指南的同一台服务器上，则根 <code>crossdomain.xml</code> 本不需要文件。 但是，如果服务位于另一台服务器上，或者如果涉及群集，则需要存 <code>crossdomain.xml</code> 在一个文件。 有关 <a href="https://kb2.adobe.com/cps/142/tn_14213.html">crossdomain</a>.xml文件的详细信息，请参阅https://kb2.adobe.com/cps/142/tn_14213.html。</p> </td> 
  </tr> 
  <tr> 
   <td><p>操作系统安全性设置</p> </td> 
   <td><p>如果需要在Solaris平台上使用192位或256位XML加密，请确保安装而 <code>pkcs11_softtoken_extra.so</code> 非安装 <code>pkcs11_softtoken.so</code>。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 安装后步骤 {#post-installation-steps}

在JEE上成功安装AEM Forms后，从安全角度定期维护环境非常重要。

下节详细介绍了为保护已部署的表单服务器而建议执行的不同任务。

### AEM Forms安全性 {#aem-forms-security}

以下推荐设置适用于管理Web应用程序外的JEE服务器上的AEM Forms。 要降低服务器的安全风险，请在JEE上安装AEM Forms后立即应用这些设置。

**安全修补程序**

如果供应商安全修补程序和升级不能及时应用，则未授权用户可能获得对应用程序服务器的访问权限的风险增加。 在将安全修补程序应用到生产服务器之前先测试这些修补程序，以确保应用程序的兼容性和可用性。 此外，还可以创建定期检查和安装修补程序的策略和过程。 JEE上的AEM Forms更新位于企业产品下载站点上。

**服务帐户（仅限Windows上的JBoss统包）**

JEE上的AEM Forms默认情况下使用LocalSystem帐户安装服务。 内置的LocalSystem用户帐户具有高级的可访问性；它是管理员组的一部分。 如果worker进程标识作为LocalSystem用户帐户运行，则该Worker进程可以完全访问整个系统。

要使用特定的非管理帐户运行部署JEE上的AEM Forms的应用程序服务器，请按照以下说明操作：

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建一个本地用户以登录：

   * 选择“ **用户无法更改密码**”。
   * 在“ **成员** ”选项卡上 **，确保列** 出“用户”组。
   >[!NOTE]
   >
   >您无法更改PDF生成器的此设置。

1. 选择 **“开始** ” > “设 **置** ” > “管 **理工具”** > ****“服务”。
1. 双击JEE上的JBoss for AEM Forms并停止服务。
1. 在“登 **录** ”选项卡上，选择“ **此帐户**”，浏览您创建的用户帐户，然后输入帐户的口令。
1. 在MMC中，打开“本地安 **全设置”** ，然后选择“ **本地策略** ” **>“用户**&#x200B;权限分配”。
1. 将以下权限分配给表单服务器在下运行的用户帐户：

   * 通过终端服务拒绝登录
   * 拒绝本地登录
   * 以服务身份登录（应已设置）

1. 为新用户帐户授予JEE web内容目录项上AEM Forms的“读取并执行”、“列出文件夹内容”和“读取”权限。
1. 启动应用程序服务器。

**禁用配置管理器引导servlet**

配置管理器使用部署在应用程序服务器上的servlet在JEE数据库上执行AEM Forms的引导。 由于配置管理器在配置完成之前访问此servlet，因此授权用户对它的访问尚未受到保护，并且在您成功使用配置管理器在JEE上配置AEM Forms后，应禁用它。

1. 解压缩adobe-livecycle-[appserver].ear文件。
1. 打开META-INF/application.xml文件。
1. 搜索adobe-bootstrapper.war部分：

   ```as3
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. 停止AEM Forms服务器。
1. 注释掉adobe-bootstrapper.war和adobe-lcm-bootstrapper-redirectory。 战争模块如下：

   ```as3
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. 保存并关闭META-INF/application.xml文件。
1. 压缩EAR文件，并将其重新部署到应用程序服务器。
1. 启动AEM Forms服务器。
1. 在浏览器中键入以下URL以测试更改并确保其不再有效。

   https://&lt;localhost>:&lt;port>/adobe bootstrapper/bootstrap

**锁定对信任商店的远程访问**

通过Configuration Manager，您可以将Acrobat Reader DC扩展凭据上传到JEE信任存储上的AEM Forms。 这意味着默认情况下，通过远程协议（SOAP和EJB）访问信任存储凭据服务已启用。 在您使用配置管理器上传权限凭据后，或者如果您决定稍后使用管理控制台来管理凭据，则不再需要此访问。

您可以按照禁用对服务的非基本远程访问部分中的步骤，禁用对所 [有信任存储服务的远程访问](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services)。

**禁用所有非必要的匿名访问**

某些表单服务器服务具有可由匿名调用者调用的操作。 如果不需要匿名访问这些服务，请按照禁用对服务的非必要匿名访 [问中的步骤禁用此功能](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services)。

#### 更改默认管理员密码 {#change-the-default-administrator-password}

安装JEE上的AEM Forms时，将为用户Super Administrator/login-id Administrator配置一个默认用户帐户，其默认密码为 *密码*。 您应使用配置管理器立即更改此密码。

1. 在Web浏览器中键入以下URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

   默认端口号为以下任一端口号：

   **** JBoss:八〇八〇年

   **** WebLogic Server:7001

   **** WebSphere:9080。

1. 在“用 **户名** ”字段中，键 `administrator` 入并在“密码 **”字段中键入**`password`。
1. 单击 **设置** >用 **户管理** > **用户和用户组**。
1. 在“查 `administrator` 找”字 **段中键入** ，然后单击“ **查找**”。
1. 从用 **户列表中单击** “超级管理员”。
1. 单击 **“编辑用户** ”页面上的“更改密码”。
1. 指定新密码，然后单击“ **保存**”。

此外，建议通过执行以下步骤来更改CRX Administrator的默认密码：

1. 使用默 `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` 认用户名／密码登录。
1. 在搜索字段中键入Administrator，然后单击“ **开始**”。
1. 从搜 **索结果中** ，选择Administrator（管理员），然后单击 **用户界面右下角的Edit** （编辑）图标。
1. 在“新密码”字 **段中指定新密码** ，在“密码”字段中指 **定旧密码** 。
1. 单击用户界面右下角的保存图标。

#### 禁用WSDL生成 {#disable-wsdl-generation}

Web服务定义语言(WSDL)生成应该只针对开发环境启用，开发人员在开发环境中使用WSDL生成来构建他们的客户端应用程序。 您可以选择在生产环境中禁用WSDL生成，以避免暴露服务的内部详细信息。

1. 在Web浏览器中键入以下URL:

   ```as3
   https://[host name]:[port]/adminui
   ```

1. 单击 **设置>核心系统设置>配置**。
1. 取消选 **择“启用WSDL** ”，然后单 **击“确定”**。

### 应用程序服务器安全性 {#application-server-security}

下表介绍了在JEE应用程序上安装AEM表单后保护应用程序服务器的一些技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>应用程序服务器管理控制台</p> </td> 
   <td><p>在应用程序服务器上的JEE上安装、配置和部署AEM表单后，您应禁用对应用程序服务器管理控制台的访问。 有关详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>应用程序服务器Cookie设置</p> </td> 
   <td><p>应用程序Cookie由应用程序服务器控制。 部署应用程序时，应用程序服务器管理员可以指定服务器范围或特定于应用程序的cookie首选项。 默认情况下，服务器设置为首选项。</p> <p>由应用程序服务器生成的所有会话Cookie都应包含该 <code>HttpOnly</code> 属性。 例如，使用JBoss Application server时，可将SessionCookie元素修改为 <code>httpOnly="true"</code> 文件 <code>WEB-INF/web.xml</code> 中。</p> <p>您可以限制使用仅HTTPS发送Cookie。 因此，不会通过HTTP发送这些文件。 应用程序服务器管理员应全局为服务器启用安全Cookie。 例如，使用JBoss Application server时，可将连接器元素修改为文 <code>secure=true</code> 件中的 <code>server.xml</code> 元素。</p> <p>有关Cookie设置的更多详细信息，请参阅应用程序服务器文档。</p> </td> 
  </tr> 
  <tr> 
   <td><p>目录浏览</p> </td> 
   <td><p>当有人请求不存在的页面或请求控制器的名称(请求字符串以正斜杠(/)结尾)时，应用程序服务器不应返回该目录的内容。 要防止这种情况发生，您可以禁用应用程序服务器上的目录浏览。 您应该为管理控制台应用程序和服务器上运行的其他应用程序执行此操作。</p> <p>对于JBoss，将属性的列表初始化参数的值设 <code>DefaultServlet</code> 置为 <code>false</code> web.xml文件中的值，如下例所示：</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listings&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>对于WebSphere，将ibm-web-ext.xmi <code>directoryBrowsingEnabled</code> 文件中的属性设置为 <code>false</code>。</p> <p>对于WebLogic，将weblogic.xml文件中的index-directories属性设置为 <code>false</code>，如下例所示：</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 数据库安全性 {#database-security}

在保护数据库时，您应实施数据库供应商描述的度量。 您应分配具有授予JEE上的AEM Forms使用的最低数据库权限的数据库用户。 例如，请勿使用具有数据库管理员权限的帐户。

在Oracle上，您使用的数据库帐户只需要CONNECT、RESOURCE和CREATE VIEW权限。 有关其他数据库的类似要求，请参 [阅准备在JEE（单台服务器）上安装AEM表单](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64)。

#### 在Windows上为JBoss配置SQL server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. 修改 [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} `integratedSecurity=true` 以添加到连接URL，如下例所示：

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 将“从本地系统登录为”的JBoss windows服务(JBoss for AEM Forms on JEE)属性修改为具有AEM Forms数据库和最少权限集的登录帐户。 如果您是从命令行而不是作为Windows服务运行JBoss，则无需执行此步骤。
1. 将“SQL server安全性”从“混 **合** ”模式设 **置为“Windows身份验证”**。

#### 在Windows上为WebLogic配置SQL server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. 通过在Web浏览器的URL行中键入以下URL，启动WebLogic服务器管理控制台：

   ```as3
   https://[host name]:7001/console
   ```

1. 在“更改中心”下，单击“ **锁定并编辑”**。
1. 在“域”下，单 *[击“基域]* ” > **Domain** > “Services **” > “** JDBC ********” > “Sources Sources”（数据源）和“Click The Data Right Pane”（单击右侧IDP）窗格中的DS Idp。
1. 在下一个屏幕的“配 **置** ”选项卡上，单击“连接池 **”选项卡，然后在“属** 性 **”框中键入**`integratedSecurity=true`。
1. 在“域”下，单 **[击“基域]** ” > **Domain** > **Services** > **JDBC******> Sources SourcesSources（数据源）” ，并在右侧窗格中单击DS Right。
1. 在下一个屏幕的“配 **置** ”选项卡上，单击“连接池 **”选项卡，然后在“属** 性 **”框中键入**`integratedSecurity=true`。
1. 将sqljdbc_auth.dll文件添加到运行应用程序服务器的计算机上的Windows系统路径。 sqljdbc_auth.dll文件位于Microsoft SQL JDBC 6.2.1.0驱动程序安装中。
1. 将“SQL server安全性”从“混 **合** ”模式设 **置为“Windows身份验证”**。

#### 在Windows上为WebSphere配置SQL server的集成安全性 {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

在WebSphere上，只有在使用外部SQL Server JDBC驱动程序时，才能配置集成安全性，而不是使用嵌入在WebSphere中的SQL Server JDBC驱动程序。

1. 登录到WebSphere管理控制台。
1. 在导航树中，单 **击“资源** ” > **JDBC** > **Data Sources** ”，在右侧窗格中，单击 **** IDP_DSA。
1. 在右侧窗格的“其他属性”下，单击“自定 **义属性**”，然后单击“ **新建”**。
1. 在“名 **称** ”(Name `integratedSecurity` )框中，键 **入并在“值** ”(Value)框中键入 `true`。
1. 在导航树中，单 **击“资源** ” > **JDBC** > **Data Sources** ”，在右侧窗格中，单击 **** RM_DS。
1. 在右侧窗格的“其他属性”下，单击“自定 **义属性**”，然后单击“ **新建”**。
1. 在“名 **称** ”(Name `integratedSecurity` )框中，键 **入并在“值** ”(Value)框中键入 `true`。
1. 在安装WebSphere的计算机上，将sqljdbc_auth.dll文件添加到Windows系统路径(C:\Windows)。 sqljdbc_auth.dll文件与Microsoft SQL JDBC 1.2驱动程序安装位置相同(默认为 *[InstallDir]*/sqljdbc_1.2/enu/auth/x86)。
1. 选择 **“开始** ” > **“控制面板”** > **“服务”**，右键单击WebSphere的Windows服务(IBM webSphere Application Server &lt;version> - &lt;node>)，然后选择 **** PropertiesAdjusting。
1. 在“属性”对话框中，单击“登 **录”选项卡** 。
1. 选 **择此帐户** ，并提供设置要使用的登录帐户所需的信息。
1. 将SQL server上的“安全性”从“混 **合** ”模式设置 **为“仅Windows身份验证”**。

### 保护对数据库中敏感内容的访问 {#protecting-access-to-sensitive-content-in-the-database}

AEM Forms数据库架构包含有关系统配置和业务流程的敏感信息，应隐藏在防火墙后。 应将数据库考虑在与表单服务器相同的信任边界内。 要防止信息泄露和业务数据被盗用，数据库管理员(DBA)必须配置数据库才允许授权管理员访问。

作为新增的预防措施，您应考虑使用数据库供应商特定工具加密包含以下数据的表中的列：

* Rights Management文档密钥
* 信任存储HSM PIN加密密钥
* 本地用户密码哈希

有关供应商特定工具的信息，请参 [阅“数据库安全信息”](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information)。

### LDAP安全性 {#ldap-security}

轻量级目录访问协议(LDAP)目录通常由JEE上的AEM Forms用作企业用户和用户组信息的源，以及执行密码身份验证的方法。 您应确保将LDAP目录配置为使用安全套接字层(SSL)，并将JEE上的AEM表单配置为使用其SSL端口访问LDAP目录。

#### LDAP拒绝服务 {#ldap-denial-of-service}

使用LDAP的常见攻击涉及攻击者故意多次无法进行身份验证。 这会强制LDAP目录服务器将用户从所有依赖LDAP的服务中锁定出来。

您可以设置当用户多次无法验证AEM表单时AEM表单实施的失败尝试次数和随后的锁定时间。 在管理控制台中，选择低值。 在选择失败尝试次数时，请务必了解，在进行所有尝试后，AEM Forms会在LDAP目录服务器之前锁定用户。

#### 设置自动帐户锁定 {#set-automatic-account-locking}

1. 登录到管理控制台。
1. 单击 **设置** >用 **户管理** > **域管理**。
1. 在“自动帐户锁定设置”下， **将“最大连续身份验证失败数** ”设置为低数，如3。
1. 单击&#x200B;**保存**。

### 审核和记录 {#auditing-and-logging}

正确、安全地使用应用程序审计和记录有助于确保尽可能快地跟踪和检测安全和其他异常事件。 有效使用应用程序中的审计和日志记录包括跟踪成功登录和失败登录等项目以及关键应用程序事件（如创建或删除关键记录）。

您可以使用审核来检测多种类型的攻击，包括：

* 蛮力密码攻击
* 拒绝服务攻击
* 注入恶意输入和相关类别的脚本攻击

此表介绍了可用于减少服务器漏洞的审计和日志记录技术。

<table> 
 <thead> 
  <tr> 
   <th><p>问题</p> </th> 
   <th><p>描述</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>日志文件ACL</p> </td> 
   <td><p>在JEE日志文件访问控制列表(ACL)上设置相应的AEM Forms。</p> <p>设置适当的凭据有助于防止攻击者删除文件。</p> <p>日志文件目录上的安全权限应为管理员和系统组的完全控制权限。 AEM Forms用户帐户应仅具有读取和写入权限。</p> </td> 
  </tr> 
  <tr> 
   <td><p>日志文件冗余</p> </td> 
   <td><p>如果资源允许，则通过使用Syslog、Tivoli、Microsoft Operations Manager(MOM)Server或其他机制将日志实时发送到攻击者无法访问的另一台服务器（仅写入）。</p> <p>这样保护日志有助于防止篡改。 此外，将日志存储在中央存储库有助于进行关联和监控（例如，如果使用多个表单服务器，并且跨多台计算机进行密码猜测攻击，其中每台计算机都被查询密码）。</p> </td> 
  </tr> 
 </tbody> 
</table>

## 在JEE上配置AEM Forms，以便在企业之外进行访问 {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

在JEE上成功安装AEM Forms后，请务必定期维护环境的安全性。 本节介绍为维护JEE生产服务器上AEM Forms的安全性而建议执行的任务。

### 为Web访问设置反向代理 {#setting-up-a-reverse-proxy-for-web-access}

可 *以使用反向代理* ，以确保外部和内部用户均可使用JEE web应用程序上AEM Forms的一组URL。 此配置比允许用户直接连接到JEE上运行AEM Forms的应用程序服务器更安全。 反向代理为在JEE上运行AEM Forms的应用程序服务器执行所有HTTP请求。 用户只能通过网络访问反向代理，并且只能尝试反向代理支持的URL连接。

**JEE根URL上的AEM Forms，与反向代理服务器一起使用**

JEE web应用程序上每个AEM Forms的以下应用程序根URL。 您应仅配置反向代理，以公开要向最终用户提供的Web应用程序功能的URL。

某些URL会高亮显示为面向最终用户的Web应用程序。 您应避免暴露配置管理器的其他URL，以便通过反向代理访问外部用户。

<table> 
 <thead> 
  <tr> 
   <th><p>根URL</p> </th> 
   <th><p>用途和／或关联的Web应用程序</p> </th> 
   <th><p>基于Web的界面</p> </th> 
   <th><p>最终用户访问</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Acrobat Reader DC扩展最终用户Web应用程序，用于将使用权限应用于PDF文档</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Rights Management最终用户Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>Web服务URL，用于权限管理</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>PDF Generator管理Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>工作区最终用户Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>工作区客户端应用程序需要的工作区Servlet和数据服务</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>用于在JEE存储库上引导AEM表单的Servlet</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>表单服务器Web服务的信息页</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>所有表单服务器服务的Web服务URL</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Rights Management管理Web应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>管理控制台主页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>有抵押/*</p> </td> 
   <td><p>“信任商店管理”页</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>用于测试和调试表单渲染的Forms IVS应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>用于测试和调试输出服务的输出IVS应用程序</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>REST URL for Rights Management</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>输出管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>表单Web应用程序文件</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>用于在HTML转换过程中获取JavaScript</p> </td> 
   <td><p>否</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>表单管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>WebDAV（调试）访问的URL</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>应用程序和服务用户界面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>工作区管理页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>其余支持页面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>“JEE核心配置设置”页上的AEM Forms</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>用户管理身份验证</p> </td> 
   <td><p>否</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>用户管理管理界面</p> </td> 
   <td><p>是</p> </td> 
   <td><p>否</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>在启用HTTP文档的情况下，通过SOAP传输或EJB传输，上传和下载在访问远程端点、SOAP WSDL端点和Java SDK时要处理的文档。</p> </td> 
   <td><p>是</p> </td> 
   <td><p>是</p> </td> 
  </tr> 
 </tbody> 
</table>

## 防止跨站点请求伪造攻击 {#protecting-from-cross-site-request-forgery-attacks}

跨站点请求伪造(CSRF)攻击利用网站对用户的信任来传输用户未授权和无意的命令。 通过在网页中包括链接或脚本或电子邮件中的URL来设置攻击，以访问用户已通过身份验证的其他站点。

例如，您可能在同时浏览其他网站时登录到管理控制台。 网页之一可以包括HTML图像标签，该HTML图像标签具有 `src` 以受害者网站上的服务器端脚本为目标的属性。 通过利用Web浏览器提供的基于cookie的会话身份验证机制，攻击网站可以向此受害服务器端脚本发送恶意请求，伪装成合法用户。 有关更多示例，请参 [阅https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples)。

CSRF共有以下特点：

* 涉及依赖用户身份的站点。
* 利用站点对该身份的信任。
* 诱骗用户的浏览器将HTTP请求发送到目标站点。
* 涉及具有副作用的HTTP请求。

JEE上的AEM Forms使用“引用过滤器”功能来阻止CSRF攻击。 本节中使用以下术语来描述引用过滤机制：

* **** 允许的参照：引用是向服务器发送请求的源页面的地址。 对于JSP页或表单，引用通常是浏览历史记录中的上一页。 图像的参照通常是显示图像的页面。 您可以通过将允许访问服务器资源的引用添加到允许的引用列表来标识允许访问的引用。
* **** 允许的参照例外：您可能希望限制“允许的引用”列表中特定引用的访问范围。 要实施此限制，您可以将该引用的单个路径添加到允许的引用例外列表。 阻止从允许的引用例外列表中的路径产生的请求调用表单服务器上的任何资源。 您可以为特定应用程序定义允许的参照例外，还可以使用适用于所有应用程序的例外的全局列表。
* **** 允许的URI:这是一个资源列表，无需检查引用标题即可提供。 例如，帮助页面在服务器上不会导致状态更改的资源可以添加到此列表中。 “允许的URI”列表中的资源不会被“引用过滤器”阻止，而不管引用者是谁。
* **** 空引用：未与父网页关联或未源自父网页的服务器请求被视为来自空引用的请求。 例如，当您打开新的浏览器窗口，键入地址并按Enter时，发送到服务器的引用为null。 向Web服务器发出HTTP请求的桌面应用程序（.NET或SWING）也向服务器发送空引用。

### 引用筛选 {#referer-filtering}

引用过滤过程可描述如下：

1. 表单服务器检查用于调用的HTTP方法：

   1. 如果是POST，表单服务器将执行“引用”标题检查。
   1. 如果表单是GET，则表单服务器会绕过“引用”检查，除非 *CSRF_CHECK_GETS* 设置为true，在这种情况下，它将执行“引用”标题检查。 *CSRF_CHECK_GETS* 是在应用程 *序的web.xml文件中指定的* 。

1. 表单服务器检查所请求的URI是否列入白名单：

   1. 如果URI已列入白名单，则服务器接受该请求。
   1. 如果请求的URI未列入白名单，则服务器将检索请求的引用。

1. 如果请求中有引用，服务器将检查它是否为允许的引用。 如果允许，服务器将检查引用异常：

   1. 如果该请求为例外，则会阻止该请求。
   1. 如果该请求不是例外，则会通过该请求。

1. 如果请求中没有引用，服务器将检查是否允许空引用：

   1. 如果允许空引用，则会传递请求。
   1. 如果不允许空引用，服务器将检查所请求的URI是否为空引用的例外，并相应地处理请求。

### 管理引用过滤 {#managing-referer-filtering}

JEE上的AEM Forms提供了一个引用过滤器，用于指定允许访问您的服务器资源的引用。 默认情况下，“引用”过滤器不过滤使用安全HTTP方法（例如GET）的请求，除非 *CSRF_CHECK_GETS* 设置为true。 如果“允许的引用”条目的端口号设置为0，则JEE上的AEM Forms将允许来自该主机的所有具有引用的请求，而不管端口号如何。 如果未指定端口号，则仅允许来自默认端口80(HTTP)或端口443(HTTPS)的请求。 如果“允许的引用”列表中的所有条目都被删除，则“引用过滤”将被禁用。

首次安装Document services时，“允许的引用”列表将更新为安装了Document services的服务器的地址。 服务器的条目包括服务器名、IPv4地址、启用IPv6时的IPv6地址、环回地址和localhost条目。 添加到“允许的引用”列表的名称由主机操作系统返回。 例如，IP地址为10.40.54.187的服务器将包括以下条目： `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. 对于由主机操作系统重新调整的任何非限定名称（没有IPv4地址、IPv6地址或限定域名的名称），不更新白名单。 修改“允许的引用”列表以适合您的业务环境。 请勿使用默认的允许引用列表在生产环境中部署表单服务器。 修改任何允许的引用、引用例外或URI后，请确保重新启动服务器以使更改生效。

**管理允许的引用列表**

您可以从管理控制台的用户管理界面管理允许的引用列表。 用户管理界面为您提供了创建、编辑或删除列表的功能。 有关使用“允 *[许的引用](/help/forms/using/admin-help/preventing-csrf-attacks.md)*”列表的&#x200B;*更多信息，请参阅管理帮助中的*“防止CSRF攻击”一节。

**管理允许的引用异常和允许的URI列表**

JEE上的AEM Forms提供API来管理允许的引用异常列表和允许的URI列表。 您可以使用这些API检索、创建、编辑或删除列表。 以下是可用API列表：

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

有关API的更 *多信息，请参阅JEE API上的AEM Forms* 。

使用全局级 ***的“允许参照例外”的LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** （即定义适用于所有应用程序的例外）列表。 此列表仅包含具有绝对路径(例如， `/index.html`)或相对路径(例如 `/sample/`)。 您还可以在相对URI的末尾附加正则表达式，例如， `/sample/(.)*`.

LC_GLOBAL_ALLOWED_REFERER_EXCEPTION ****** list ID在命名空间的类中定义为常数 `UMConstants` , `com.adobe.idp.um.api` 位于 `adobe-usermanager-client.jar`。 您可以使用AEM Forms API创建、修改或编辑此列表。 例如，要创建“全局允许的引用例外”列表，请使用：

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

对于特 ***定于应用程序的异常，请使用CSRF_ALLOWED_REFERER_EXCEPTIONS*** 列表。

**禁用引用过滤器**

如果引用过滤器完全阻止对表单服务器的访问，并且您无法编辑允许的引用列表，则可以更新服务器启动脚本并禁用引用过滤。

在启动脚 `-Dlc.um.csrffilter.disabled=true` 本中包含JAVA参数并重新启动服务器。 确保在正确重新配置“允许的引用”列表后删除JAVA参数。

**自定义WAR文件的引用过滤**

您可能已创建自定义WAR文件以在JEE上与AEM Forms一起使用，以满足您的业务要求。 要为自定义WAR文件启用引用过滤，请在WAR的类路径中包含 ***adobe-usermanager-client.jar*** ，并在 ** web.xml文件中包含一个包含以下参数的过滤器条目：

**CSRF_CHECK_GETS控制GET请求的** “参照”检查。 如果未定义此参数，则将默认值设置为false。 仅在要过滤GET请求时，才包含此参数。

**CSRF_ALLOWED_REFERER_EXCEPTIONS** 是“允许的参照例外”列表的ID。 引用过滤器可阻止来自由列表ID标识的列表中引用者的请求调用表单服务器上的任何资源。

**CSRF_ALLOWED_URIS_LIST_NAME** 是“允许的URI”列表的ID。 引用过滤器不会阻止对列表ID所标识的列表中任何资源的请求，而不管请求中引用标题的值如何。

**CSRF_ALLOW_NULL_REFERER** 在引用为null或不存在时控制引用过滤器行为。 如果未定义此参数，则将默认值设置为false。 仅当您希望允许空引用时，才包含此参数。 允许空引用可能会允许某些类型的跨站点请求伪造攻击。

**CSRF_NULL_REFERER_EXCEPTIONS** 是一个URI列表，当引用为null时，不会对其执行引用检查。 仅当 *CSRF_ALLOW_NULL_REFERER设置为false时* ，才启用此参数。 在列表中用逗号分隔多个URI。

以下是 *SAMPLE******* WAR文件web.xml文件中的过滤器条目示例：

```as3
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**疑难解答**

如果CSRF过滤器阻止了合法的服务器请求，请尝试以下任一方法：

* 如果拒绝的请求包含“引用”标题，请仔细考虑将其添加到“允许的引用”列表。 仅添加您信任的引用。
* 如果拒绝的请求没有引用头，请修改您的客户端应用程序以包含引用头。
* 如果客户端可以在浏览器中工作，请尝试该部署模型。
* 作为最后的选择，您可以将资源添加到“允许的URI”列表。 这不是建议的设置。

## 安全网络配置 {#secure-network-configuration}

本节介绍JEE上的AEM Forms所需的协议和端口，并提供在JEE上部署AEM Forms的建议，使其能够安全地配置网络。

### JEE上的AEM Forms使用的网络协议 {#network-protocols-used-by-aem-forms-on-jee}

如上节所述，当您配置安全网络架构时，JEE上的AEM Forms与企业网络中的其他系统之间的交互需要以下网络协议。

<table> 
 <thead> 
  <tr> 
   <th><p>协议</p> </th> 
   <th><p>用法</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>浏览器显示配置管理器和最终用户Web应用程序</p> </li> 
     <li><p>所有SOAP连接</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Web服务客户端应用程序，如。NET应用程序</p> </li> 
     <li><p>Adobe Reader®将SOAP用于JEE服务器Web服务上的AEM Forms</p> </li> 
     <li><p>Adobe Flash®应用程序使用SOAP提供表单服务器Web服务</p> </li> 
     <li><p>在SOAP模式中使用时，JEE SDK上的AEM Forms调用</p> </li> 
     <li><p>工作台设计环境</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>在Enterprise javaBeans(EJB)模式中使用时，JEE SDK上的AEM Forms调用</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>基于电子邮件的服务输入（电子邮件端点）</p> </li> 
     <li><p>通过电子邮件发送用户任务通知</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>UNC文件IO</p> </td> 
   <td><p>JEE上的AEM Forms监视已监视文件夹以输入到服务（已监视文件夹端点）</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>同步目录中的组织用户和组信息</p> </li> 
     <li><p>交互式用户的LDAP身份验证</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>在使用JDBC服务执行进程期间对外部数据库进行的查询和过程调用</p> </li> 
     <li><p>对JEE存储库上的AEM Forms进行内部访问</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>支持通过任何WebDAV客户端在JEE设计时存储库（表单、片段等）上远程浏览AEM Forms</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Adobe Flash应用程序，其中JEE服务器服务上的AEM Forms配置了远程处理端点</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>JEE上的AEM Forms公开了使用JMX进行监视的MBean</p> </td> 
  </tr> 
 </tbody> 
</table>

### 应用程序服务器的端口 {#ports-for-application-servers}

本节介绍支持的每种类型应用程序服务器的默认端口（和备用配置范围）。 必须在内部防火墙上启用或禁用这些端口，具体取决于您希望允许连接到在JEE上运行AEM Forms的应用程序服务器的客户端的网络功能。

>[!NOTE]
>
>默认情况下，服务器在adobe.com命名空间下显示多个JMX MBean。 仅公开对服务器运行状况监控有用的信息。 但是，为了防止信息泄露，您应防止不受信任的网络中的调用者查找JMX MBean并访问健康指标。

**JBoss端口**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>端口</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>访问Web应用程序</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1连接器端口8080</p> <p>AJP 1.3连接器端口8009</p> <p>SSL/TLS连接器端口8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>CORBA支持</p> </td> 
   <td><p>[JBoss根目录]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**WebLogic端口**

<table> 
 <thead> 
  <tr> 
   <th><p>用途</p> </th> 
   <th><p>端口</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>访问Web应用程序</p> </td> 
   <td> 
    <ul> 
     <li><p>Admin server监听端口：默认为7001</p> </li> 
     <li><p>Admin Server SSL监听端口：默认为7002</p> </li> 
     <li><p>为Managed server配置的端口，例如8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>在JEE上访问AEM Forms不需要WebLogic管理端口</p> </td> 
   <td> 
    <ul> 
     <li><p>Managed server监听端口：可配置从1到65534</p> </li> 
     <li><p>Managed Server SSL监听端口：可配置从1到65534</p> </li> 
     <li><p>Node Manager监听端口：默认为5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**WebSphere端口**

有关AEM Forms on JEE需要的WebSphere端口的信息，请转到WebSphere应用程序服务器UI中的端口号设置。

### 配置SSL {#configuring-ssl}

有关JEE物理架构上的 [AEM Forms部分中介绍的物理架构](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)，您应为计划使用的所有连接配置SSL。 具体而言，所有SOAP连接都必须通过SSL进行，以防止用户凭据在网络上暴露。

有关如何在JBoss、WebLogic和WebSphere上配置SSL的说明，请参阅管理帮助中的“配置SSL” [部分](https://www.adobe.com/go/learn_aemforms_admin_64)。

### 配置SSL重定向 {#configuring-ssl-redirect}

在将应用程序服务器配置为支持SSL后，必须确保应用程序和服务的所有HTTP通信都强制使用SSL端口。

要为WebSphere或WebLogic配置SSL重定向，请参阅应用程序服务器文档。

1. 打开命令提示符，导航到/JBOSS_HOME/standalone/configuration目录，然后执行以下命令：

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. 打开JBOSS_HOME/standalone/configuration/standalone.xml文件进行编辑。

   在&lt;subsystem xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>元素之后，添加以下详细信息：

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. 在https连接器元素中添加以下代码：

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   保存并关闭standalone.xml文件。

## 特定于Windows的安全建议 {#windows-specific-security-recommendations}

此部分包含特定于Windows的安全建议，当用于在JEE上运行AEM Forms时。

### JBoss服务帐户 {#jboss-service-accounts}

默认情况下，JEE统包安装上的AEM Forms使用本地系统帐户设置服务帐户。 内置的本地系统用户帐户具有高度的可访问性；它是管理员组的一部分。 如果某个Worker进程标识作为本地系统用户帐户运行，则该Worker进程对整个系统具有完全访问权限。

#### 使用非管理帐户运行应用程序服务器 {#run-the-application-server-using-a-non-administrative-account}

1. 在Microsoft管理控制台(MMC)中，为表单服务器服务创建一个本地用户以登录：

   * 选择“ **用户无法更改密码**”。
   * 在“ **成员** ”选项卡上，确保列出用户组。

1. 选择 **设置** > **管理工具** > **服务**。
1. 双击应用程序服务器服务并停止该服务。
1. 在“登 **录** ”选项卡上，选择“ **此帐户**”，浏览您创建的用户帐户，然后输入帐户的口令。
1. 在“本地安全设置”窗口的“用户权限分配”下，为表单服务器在下运行的用户帐户授予以下权限：

   * 通过终端服务拒绝登录
   * 拒绝本地登录
   * 以服务身份登录（应已设置）

1. 为JEE web内容目录上的AEM Forms赋予新的用户帐户“读取和执行”、“列出文件夹内容”和“读取”权限。
1. 启动应用程序服务器服务。

### 文件系统安全性 {#file-system-security}

JEE上的AEM Forms通过以下方式使用文件系统：

* 存储处理文档输入和输出时使用的临时文件
* 将文件存储在全局存档存储中，这些文件用于支持已安装的解决方案组件
* 监视文件夹存储已丢弃的文件，这些文件用作文件系统文件夹位置中服务的输入

使用监视文件夹作为通过表单服务器服务发送和接收文档的方式时，请注意文件系统安全性。 当用户将内容放置到监视的文件夹中时，该内容会通过监视的文件夹公开。 在这种情况下，服务不会验证实际的最终用户。 相反，它依赖于在文件夹级别设置的ACL和共享级别安全性，以确定谁可以有效调用服务。

## 特定于JBoss的安全建议 {#jboss-specific-security-recommendations}

本节包含特定于JBoss 7.0.6（当用于在JEE上运行AEM Forms时）的应用程序服务器配置建议。

### 禁用JBoss管理控制台和JMX控制台 {#disable-jboss-management-console-and-jmx-console}

在JBoss上的JEE上使用统包安装方法安装AEM Forms时，已配置对JBoss管理控制台和JMX控制台的访问权限（JMX监视功能被禁用）。 如果您使用自己的JBoss Application Server，请确保对JBoss管理控制台和JMX监视控制台的访问是安全的。 在名为jmx-invoker-service.xml的JBoss配置文件中设置对JMX监视控制台的访问权限。

### 禁用目录浏览 {#disable-directory-browsing}

登录到管理控制台后，可以通过修改URL浏览控制台的目录列表。 例如，如果将URL更改为以下URL之一，则可能会显示目录列表：

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## 特定于WebLogic的安全建议 {#weblogic-specific-security-recommendations}

本节包含在JEE上运行AEM Forms时保护WebLogic 9.1的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-1}

将weblogic.xml文件中的index-directories属性设置为 `false`，如下例所示：

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### 启用WebLogic SSL端口 {#enable-weblogic-ssl-port}

默认情况下，WebLogic不启用默认的SSL监听端口7002。 在配置SSL之前，在WebLogic服务器管理控制台中启用此端口。

## WebSphere特定的安全建议 {#websphere-specific-security-recommendations}

本节包含用于保护在JEE上运行AEM Forms的WebSphere的应用程序服务器配置建议。

### 禁用目录浏览 {#disable_directory_browsing-2}

将ibm- `directoryBrowsingEnabled` web-ext.xml文件中的属性设置为 `false`。

### 启用WebSphere管理安全性 {#enable-websphere-administrative-security}

1. 登录到WebSphere管理控制台。
1. 在导航树中，转到“安全 **性** ”>“全 **局安全性”**
1. 选择“ **启用管理安全性**”。
1. 取消选择“ **启用应用程序安全** ”和“ **使用Java 2安全性”**。
1. 单击“ **确定** ”或“ **应用**”。
1. 在“消 **息** ”框中，单 **击“直接保存到主配置”**。

