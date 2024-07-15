---
title: 部署社区
description: 如何部署AEM Communities
content-type: reference
topic-tags: deploying
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1705'
ht-degree: 0%

---


# 部署社区{#deploying-communities}

## 先决条件 {#prerequisites}

* [AEM 6.5平台](/help/sites-deploying/deploy.md)

* AEM Communities许可证

* 可选许可证：

   * [Adobe Analytics for Communities功能](/help/communities/analytics.md)
   * [MongoDB for MSRP](/help/communities/msrp.md)
   * [ASRP的Adobe云](/help/communities/asrp.md)

## 安装核对清单 {#installation-checklist}

**对于[AEM平台](/help/sites-deploying/deploy.md#what-is-aem)**：

* 安装最新的[AEM 6.5更新](#aem64updates)。

* 如果不使用默认端口(4502、4503)，则[配置复制代理](#replication-agents-on-author)。
* [复制加密密钥](#replicate-the-crypto-key)
* 如果支持全球化，请[设置自动翻译](/help/sites-administering/translation.md)
（为开发提供了示例设置）。

**对于[Communities功能](/help/communities/overview.md)**：

* 如果部署[发布场](/help/sites-deploying/recommended-deploys.md#tarmk-farm)，则[标识主发布者](#primary-publisher)

* [启用通道服务](#tunnel-service-on-author)
* [启用社交登录](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [配置Adobe Analytics](/help/communities/analytics.md)
* 设置[默认电子邮件服务](/help/communities/email.md)
* 识别[共享UGC存储](/help/communities/working-with-srp.md) (**SRP**)的选择

   * 如果MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [安装和配置MongoDB](/help/communities/msrp.md#mongodb-configuration)
      * [配置Solr](/help/communities/solr.md)
      * [选择MSRP](/help/communities/srp-config.md)

   * 如果关系数据库SRP [(DSRP)](/help/communities/dsrp.md)

      * [安装用于MySQL的JDBC驱动程序](#jdbc-driver-for-mysql)
      * [安装和配置MySQL for DSRP](/help/communities/dsrp-mysql.md)
      * [配置Solr](/help/communities/solr.md)
      * [选择DSRP](/help/communities/srp-config.md)

   * 如果AdobeSRP [(ASRP)](/help/communities/asrp.md)

      * 与您的客户代表合作进行配置。
      * [选择ASRP](/help/communities/srp-config.md)

   * 如果JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 不是共享的UGC（用户生成的内容）存储：

         * 从不复制UGC。
         * UGC仅在输入它的AEM实例或群集中可见。

      * 默认值为JSRP


## 最新版本 {#latest-releases}

AEM 6.5 Communities GA包含Communities包。 要了解有关AEM 6.5 [社区](/help/release-notes/release-notes.md#experiencemanagercommunities)更新的更多信息，请参阅[AEM 6.5发行说明](/help/release-notes/release-notes.md#communities-release-notes.html)。

### AEM 6.5更新 {#aem-updates}

从AEM 6.4开始，对Communities的更新作为AEM累积修补程序包和Service Pack的一部分提供。

有关AEM 6.5的最新更新，请参阅[Adobe Experience Manager 6.4累积修补程序包和Service Pack](https://helpx.adobe.com/cn/experience-manager/aem-releases-updates.html)。

### 版本历史记录 {#version-history}

与AEM 6.4及更高版本一样，AEM Communities功能和修补程序是AEM Communities累积修补程序包和Service Pack的一部分。 因此，没有单独的功能包。

### 用于MySQL的JDBC驱动程序 {#jdbc-driver-for-mysql}

一个Communities功能使用MySQL数据库：

* 对于[DSRP](/help/communities/dsrp.md)：存储UGC

必须单独获取和安装MySQL连接器。

必需的步骤包括：

1. 从[https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)下载ZIP存档

   * 版本必须>= 5.1.38

1. 提取`mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. 使用Web控制台安装和启动捆绑包：

   * 例如， https://localhost:4502/system/console/bundles
   * 选择&#x200B;**`Install/Update`**
   * 浏览……以选择从下载的ZIP存档提取的包
   * 检查&#x200B;*Oracle公司用于MySQLcom.mysql.jdbc*&#x200B;的JDBC驱动程序是否处于活动状态，如果未处于活动状态，则启动它（或检查日志）

1. 如果在配置JDBC后在现有部署上进行安装，则通过从Web控制台重新保存JDBC配置将JDBC重新绑定到新连接器：

   * 例如， https://localhost:4502/system/console/configMgr
   * 找到`Day Commons JDBC Connections Pool`配置并选择以打开该配置。
   * 选择`Save`。

1. 对所有创作和发布实例重复步骤3和4。

有关安装捆绑包的更多信息，请访问[Web控制台](/help/sites-deploying/web-console.md#bundles)页面。

#### 示例：已安装MySQL连接器捆绑包 {#example-installed-mysql-connector-bundle}

![Adobe Experience Manager Web控制台MySQL连接器包](../assets/mysql-connector.png)

### AEM高级MLS {#aem-advanced-mls}

对于SRP集合（MSRP或DSRP）而言，为了支持高级多语言搜索(MLS)，除了自定义架构和Solr配置之外，还需要新的Solr插件。 所有必需的项目都打包到一个可下载的zip文件中。

高级MLS下载（也称为“phasetwo”）可从Adobe存储库中获取：

* [AEM-SOLR-MLS-phasetwo](https://repo1.maven.org/maven2/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * 版本1.2.40,2016年4月6日
   * 下载AEM-SOLR-MLS-phasetwo-1.2.40.zip

有关详细信息和安装信息，请访问SRP的[Solr配置](/help/communities/solr.md)。

### 关于指向包共享的链接 {#about-links-to-package-share}

在AdobeAEM Cloud中可见的&#x200B;**包**

指向此页上的包的链接不需要正在运行的AEM实例，因为它们将指向`adobeaemcloud.com`上的包共享。 当包可见时，`Install`按钮用于将包安装到Adobe托管的站点中。 如果要在本地AEM实例上安装，请选择`Install`会导致错误。

**如何在本地AEM实例上安装**

若要在本地AEM实例上安装`adobeaemcloud.com`中显示的包，必须首先将该包下载到本地磁盘：

* 选择&#x200B;**Assets**&#x200B;选项卡
* 选择&#x200B;**下载到磁盘**

在本地AEM实例上，使用包管理器(例如，[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))上载到本地AEM包存储库。

或者，使用包共享从本地AEM实例(例如，[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))访问包，`Download`按钮将下载到本地AEM实例的包存储库。

进入本地AEM实例的包存储库后，使用包管理器安装包。

有关详细信息，请访问[如何使用包](/help/sites-administering/package-manager.md#package-share)。

## 建议的部署 {#recommended-deployments}

在AEM Communities中，公用存储用于存储UGC，通常称为[存储资源提供程序(SRP)](/help/communities/working-with-srp.md)。 建议的部署重点是为公用存储选择SRP选项。

公用存储支持在发布环境中对UGC进行审核和分析，同时消除了UGC的[复制](/help/communities/sync.md)的需要。

* [社区内容存储](/help/communities/working-with-srp.md) ：讨论AEM Communities的SRP存储选项

* [推荐的拓扑](/help/communities/topologies.md) ：根据用例和SRP选择讨论要使用的拓扑

## 升级 {#upgrading}

从以前版本的AEM升级到AEM 6.5平台时，请务必阅读[升级到AEM 6.5](/help/sites-deploying/upgrade.md)。

除升级平台外，请阅读[升级到AEM Communities 6.5](/help/communities/upgrade.md)以了解社区更改。

## 配置 {#configurations}

### 主要发布者 {#primary-publisher}

如果选择的部署是[发布场](/help/communities/topologies.md#tarmk-publish-farm)，则必须将一个AEM发布实例标识为&#x200B;**`primary publisher`**，以便执行不应在所有实例上发生的活动。 例如，依赖于&#x200B;**通知**&#x200B;或&#x200B;**Adobe Analytics**&#x200B;的功能。

默认情况下，`AEM Communities Publisher Configuration` OSGi配置配置为选中&#x200B;**`Primary Publisher`**&#x200B;复选框，这样发布场中的所有发布实例都将自我标识为主实例。

因此，必须&#x200B;**编辑所有辅助发布实例上的配置**&#x200B;以取消选中&#x200B;**`Primary Publisher`**&#x200B;复选框。

![AEM Communities发布者配置对话框显示“主发布者”复选框](../assets/primary-publisher.png)

对于发布场中的所有其他（辅助）发布实例：

* 使用管理员权限登录
* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 找到`AEM Communities Publisher Configuration`
* 选择编辑图标
* 取消选中&#x200B;**主发布者**&#x200B;复选框
* 选择&#x200B;**保存**

### 创作实例上的复制代理 {#replication-agents-on-author}

复制用于发布环境中创建的站点内容，如社区组，并使用[通道服务](#tunnel-service-on-author)从创作环境中管理成员和成员组。

对于主发布者，请确保[复制代理配置](/help/sites-deploying/replication.md)正确标识发布服务器和授权用户。 默认授权用户`admin`已具有相应的权限（是`Communities Administrators`的成员）。

对于其他某个用户而言，要拥有相应的权限，必须将其添加为`administrators`用户组（也是`Communities Administrators`的成员）的成员。

创作环境中有两个复制代理需要正确配置传输配置。

* 访问作者的“复制”控制台

   * 从全局导航： **工具、部署、复制、作者代理**

* 对两个代理均遵循相同的过程：

   * **默认代理（发布）**
   * **反向复制代理（发布反向）**

      1. 选择代理。
      1. 选择&#x200B;**编辑**。
      1. 选择&#x200B;**传输**&#x200B;选项卡
      1. 如果它不是端口`4503`，请编辑&#x200B;**URI**&#x200B;以指定正确的端口。

      1. 如果不是用户`admin`，请编辑&#x200B;**用户**&#x200B;和&#x200B;**密码**&#x200B;以指定`administrators`用户组的成员。

下图显示了将端口从4503更改为6103的结果：

#### 默认代理（发布） {#default-agent-publish}

![配置限制](../assets/default-agent-publish.png)

#### 反向复制代理（反向发布） {#reverse-replication-agent-publish-reverse}

![反向复制代理（发布恢复）显示它已打开或已启用。](../assets/reverse-replication-agent.png)

### 作者上的通道服务 {#tunnel-service-on-author}

使用作者环境[创建站点](/help/communities/sites-console.md)、[修改站点属性](/help/communities/sites-console.md#modifying-site-properties)或[管理社区成员](/help/communities/members.md)时，必须访问在发布环境中注册的成员（用户），而不是在作者中注册的用户。

通道服务使用创作实例上的复制代理提供此访问权限。

要启用通道服务，请执行以下操作：

* 在&#x200B;**作者**&#x200B;上，使用管理权限登录。
* 如果发布者不是localhost：4503或传输用户不是`admin`，
然后[配置复制代理](#replication-agents-on-author)。

* 访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 找到`AEM Communities Publish Tunnel Service`
* 选择编辑图标
* 选中&#x200B;**启用**&#x200B;复选框
* 选择&#x200B;**保存**

![AEM Communities Publish Tunnel Service显示“启用”复选框，已选中或已选中。](../assets/tunnel-service.png)

### 复制加密密钥 {#replicate-the-crypto-key}

AEM Communities有两项功能要求所有AEM服务器实例都使用相同的加密密钥。 它们是[Analytics](/help/communities/analytics.md)和[ASRP](/help/communities/asrp.md)。

从AEM 6.3开始，关键资料存储在文件系统中，不再存储在存储库中。

要将关键资料从作者复制到所有其他实例，您需要：

* 访问AEM实例（通常为创作实例），其中包含要复制的关键资料

   * 在本地文件系统中找到`com.adobe.granite.crypto.file`包

     例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`文件标识该捆绑包

   * 导航到数据文件夹
例如，

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 复制hmac和主节点文件。

* 对于每个目标AEM实例

   * 导航到数据文件夹
例如，

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 粘贴之前复制的两个文件
   * 如果目标AEM实例正在运行，则必须[刷新Granite加密包](#refresh-the-granite-crypto-bundle)。

>[!CAUTION]
>
>如果已配置基于加密密钥的其他安全功能，则复制加密密钥可能会损坏配置。 如需帮助，[请联系客户关怀](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)。

#### 存储库复制 {#repository-replication}

将关键资料存储在存储库中(如AEM 6.2及更早版本)可以保留。 在每个AEM实例首次启动时（这将创建初始存储库）指定以下系统属性：

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>验证作者](#replication-agents-on-author)上的[复制代理是否正确配置很重要。

将密钥资料存储在存储库中，将加密密钥从创作实例复制到其他实例的方式如下：

使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) ：

* 浏览至[https://&lt;服务器>：&lt;端口>/crx/de](https://localhost:4502/crx/de)
* 选择`/etc/key`
* 打开`Replication`选项卡
* 选择`Replicate`

* [刷新Granite加密包](#refresh-the-granite-crypto-bundle)

![CRXDE Lite在左面板上显示/etc/key路径并在右下面板中显示“复制”选项卡。](../assets/replicare-repository.png)

#### 刷新Granite加密包 {#refresh-the-granite-crypto-bundle}

* 在每个发布实例上，访问[Web控制台](/help/sites-deploying/configuring-osgi.md)

   * 例如，[https://&lt;服务器>：&lt;端口>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 找到`Adobe Granite Crypto Support`包(com.adobe.granite.crypto)
* 选择&#x200B;**刷新**

![正在刷新AdobeGranite加密支持包。](../assets/refresh-granite-bundle.png)

* 片刻后，应该会显示&#x200B;**成功**对话框：
  `Operation completed successfully.`

### Apache HTTP Server {#apache-http-server}

如果使用Apache HTTP Server，请确保对所有相关条目使用正确的服务器名称。

特别是，在`RedirectMatch`中使用正确的服务器名称，而不是`localhost`。

#### httpd.conf示例 {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

如果使用Dispatcher，请参阅：

* AEM[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html)文档
* [安装 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html)
* [为社区配置Dispatcher](/help/communities/dispatcher.md)
* [已知问题](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 相关社区文档 {#related-communities-documentation}

* 访问[管理社区站点](/help/communities/administer-landing.md)，了解有关创建社区站点、配置社区站点模板、审核社区内容、管理成员和配置消息传送的信息。

* 访问[开发社区](/help/communities/communities.md)，您可以在其中了解社交组件框架(SCF)和自定义社区组件和功能。

* 访问[创作社区组件](/help/communities/author-communities.md)，您可以在其中了解如何使用及配置社区组件。

